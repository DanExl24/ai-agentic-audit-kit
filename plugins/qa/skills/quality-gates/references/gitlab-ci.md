# Notas: GitLab CI/CD

## Esqueleto con pipelines de merge request

```yaml
# .gitlab-ci.yml
stages: [test, e2e]

workflow:
  rules:
    - if: $CI_PIPELINE_SOURCE == "merge_request_event"
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH
    - if: $CI_PIPELINE_SOURCE == "schedule"

default:
  image: node:22
  interruptible: true          # un push nuevo cancela el pipeline anterior del mismo MR
  cache:
    key:
      files: [package-lock.json]
    paths: [.npm/]
  before_script:
    - npm ci --cache .npm --prefer-offline

unit:
  stage: test
  timeout: 15m
  script:
    - npm test -- --coverage
  coverage: '/All files[^|]*\|[^|]*\s+([\d\.]+)/'
  artifacts:
    when: always
    reports:
      junit: results/junit.xml
      coverage_report:
        coverage_format: cobertura
        path: coverage/cobertura-coverage.xml

integration:
  stage: test
  timeout: 20m
  services:
    - name: postgres:16
      alias: db
  variables:
    POSTGRES_DB: app_test
    POSTGRES_PASSWORD: test
    DATABASE_URL: postgres://postgres:test@db:5432/app_test
  script:
    - npm run db:migrate
    - npm run test:integration
  artifacts:
    when: always
    reports:
      junit: results/integration-junit.xml
```

- `artifacts:reports:junit` muestra los tests fallidos en el MR; `coverage_report` marca las líneas cubiertas en el diff.
- `artifacts:when: always` para conservar resultados cuando el job falla.

## E2E con paralelismo

```yaml
e2e:
  stage: e2e
  image: mcr.microsoft.com/playwright:<versión-igual-al-paquete>-noble
  parallel: 4
  timeout: 30m
  script:
    - npx playwright test --shard=$CI_NODE_INDEX/$CI_NODE_TOTAL
  artifacts:
    when: always
    expire_in: 7 days
    paths: [blob-report/, test-results/]
    reports:
      junit: results/junit.xml
```

Un job posterior con `needs: [e2e]` y `when: always` puede unir los informes (`npx playwright merge-reports`).

## Selección por cambios y nocturnos

```yaml
backend-tests:
  rules:
    - if: $CI_PIPELINE_SOURCE == "merge_request_event"
      changes: [backend/**/*, shared/**/*]
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH

nightly-full-e2e:
  rules:
    - if: $CI_PIPELINE_SOURCE == "schedule"
```

Los pipelines programados se crean en CI/CD → Schedules; que fallen debe notificar a un canal o crear una issue.

## Reintentos y fallos permitidos

```yaml
retry:
  max: 1
  when: [runner_system_failure, stuck_or_timeout_failure]   # solo fallos de infraestructura
```

- No reintentes `script_failure` de forma automática: esconde tests intermitentes.
- `allow_failure: true` solo para jobs explícitamente informativos (y con nombre que lo diga).

## Protección

- Rama principal protegida, sin push directo.
- En los ajustes del proyecto: "Pipelines must succeed" para fusionar MRs y, si hay mucho tráfico, *merge trains*.
- Variables con secretos marcadas como *protected* y *masked*.
