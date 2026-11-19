# Notas: GitHub Actions

## Esqueleto de PR con jobs en paralelo

```yaml
# .github/workflows/tests.yml
name: tests
on:
  pull_request:
  push:
    branches: [main]
  merge_group:            # necesario si usas la cola de merge

concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true   # cancela ejecuciones obsoletas del mismo PR

permissions:
  contents: read

jobs:
  unit:
    runs-on: ubuntu-latest
    timeout-minutes: 15
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version-file: .nvmrc
          cache: npm
      - run: npm ci
      - run: npm test -- --reporter=default --reporter=junit --outputFile.junit=results/junit.xml
      - uses: actions/upload-artifact@v4
        if: always()                      # sube resultados también si falla
        with:
          name: unit-results
          path: results/

  integration:
    runs-on: ubuntu-latest
    timeout-minutes: 20
    services:
      postgres:
        image: postgres:16
        env:
          POSTGRES_PASSWORD: test
          POSTGRES_DB: app_test
        ports: ['5432:5432']
        options: >-
          --health-cmd pg_isready --health-interval 5s --health-timeout 5s --health-retries 10
    env:
      DATABASE_URL: postgres://postgres:test@localhost:5432/app_test
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with: { node-version-file: .nvmrc, cache: npm }
      - run: npm ci
      - run: npm run db:migrate && npm run test:integration
```

Las credenciales de los servicios de CI son de usar y tirar; las reales van en *secrets* y nunca se imprimen.

## E2E con sharding y un informe unificado (Playwright)

```yaml
  e2e:
    runs-on: ubuntu-latest
    timeout-minutes: 30
    strategy:
      fail-fast: false
      matrix:
        shard: [1, 2, 3, 4]
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with: { node-version-file: .nvmrc, cache: npm }
      - run: npm ci
      - run: npx playwright install --with-deps chromium
      - run: npx playwright test --shard=${{ matrix.shard }}/4
      - uses: actions/upload-artifact@v4
        if: always()
        with:
          name: blob-report-${{ matrix.shard }}
          path: blob-report
          retention-days: 7

  e2e-report:
    if: always()
    needs: [e2e]
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with: { node-version-file: .nvmrc, cache: npm }
      - run: npm ci
      - uses: actions/download-artifact@v4
        with:
          path: all-blob-reports
          pattern: blob-report-*
          merge-multiple: true
      - run: npx playwright merge-reports --reporter html ./all-blob-reports
      - uses: actions/upload-artifact@v4
        with: { name: e2e-html-report, path: playwright-report, retention-days: 14 }
```

## Nocturno

```yaml
on:
  schedule:
    - cron: '0 3 * * *'     # UTC
  workflow_dispatch:
```

Si falla, que abra o actualice una issue (acción de la comunidad o `gh issue create` con el token del workflow) en lugar de depender de que alguien lea el email.

## Filtros por rutas y checks obligatorios

- `on.pull_request.paths` evita ejecuciones innecesarias, **pero** un workflow que no se ejecuta deja su check obligatorio "pendiente" para siempre. Para checks obligatorios, ejecuta siempre el workflow y decide dentro con un paso de detección de cambios (p. ej. una acción de filtros por rutas) que salte los jobs caros, o marca como obligatorio un job final que siempre corre.
- Protección de la rama principal con *rulesets* o *branch protection*: checks obligatorios por nombre de job estable, rama actualizada o cola de merge, sin push directo.

## Seguridad del pipeline

- `permissions:` mínimos por workflow; `pull_request_target` solo si entiendes el riesgo (ejecuta con secretos sobre código ajeno).
- Acciones de terceros fijadas por SHA de commit, no por etiqueta móvil.
- Nada de `set -x` o `echo` de variables con secretos.
