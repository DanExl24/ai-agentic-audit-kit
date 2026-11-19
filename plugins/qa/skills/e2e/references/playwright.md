# Notas: Playwright (@playwright/test)

## Configuración base

```ts
// playwright.config.ts
import { defineConfig, devices } from '@playwright/test';

export default defineConfig({
  testDir: './e2e',
  fullyParallel: true,
  forbidOnly: !!process.env.CI,           // un test.only olvidado rompe CI
  retries: process.env.CI ? 1 : 0,        // los reintentos se ven como "flaky" en el informe
  reporter: process.env.CI ? [['blob'], ['junit', { outputFile: 'results/junit.xml' }]] : 'html',
  use: {
    baseURL: process.env.BASE_URL ?? 'http://localhost:5173',
    trace: 'on-first-retry',
    screenshot: 'only-on-failure',
    video: 'retain-on-failure',
  },
  projects: [
    { name: 'setup', testMatch: /.*\.setup\.ts/ },
    {
      name: 'chromium',
      use: { ...devices['Desktop Chrome'], storageState: 'playwright/.auth/user.json' },
      dependencies: ['setup'],
    },
  ],
  webServer: {
    command: 'npm run dev',
    url: 'http://localhost:5173',
    reuseExistingServer: !process.env.CI,
  },
});
```

Añade `playwright/.auth/` al `.gitignore`: contiene sesiones.

## Autenticación reutilizada

```ts
// e2e/setup/auth.setup.ts
import { test as setup, expect } from '@playwright/test';

setup('autenticar usuario', async ({ request }) => {
  const res = await request.post('/api/auth/login', {
    data: { email: process.env.E2E_USER!, password: process.env.E2E_PASSWORD! },
  });
  expect(res.ok()).toBeTruthy();
  await request.storageState({ path: 'playwright/.auth/user.json' });
});
```

Para varios roles, un archivo de estado por rol y un proyecto (o `test.use({ storageState })`) por rol. Las credenciales de prueba vienen de variables de entorno o secretos de CI, nunca del código.

## Fixtures con datos propios

```ts
// e2e/fixtures/index.ts
import { test as base, expect } from '@playwright/test';

type Order = { id: string };

export const test = base.extend<{ order: Order }>({
  order: async ({ request }, use) => {
    const res = await request.post('/api/test/orders', { data: { items: 1 } });
    const order = (await res.json()) as Order;
    await use(order);
    await request.delete(`/api/test/orders/${order.id}`);   // limpieza
  },
});
export { expect };
```

## Localizadores y aserciones

```ts
await page.getByRole('button', { name: 'Pagar' }).click();
await page.getByLabel('Correo electrónico').fill('ana@example.com');
await expect(page.getByRole('alert')).toHaveText('Pago confirmado');   // reintenta hasta cumplirse
await expect(page.getByRole('row')).toHaveCount(3);
```

- `expect(locator)` reintenta; `expect(await locator.textContent())` no: evítalo.
- Esperar una respuesta concreta: `const resp = page.waitForResponse('**/api/orders'); await click; await resp;`.
- `page.waitForTimeout()` solo para depurar.

## Red

```ts
await page.route('**/api.stripe.com/**', (route) =>
  route.fulfill({ status: 200, json: { status: 'succeeded' } }));
```

Simula terceros, no tu backend.

## Etiquetas, smoke y selección

```ts
test('checkout hasta el pago', { tag: '@smoke' }, async ({ page }) => { /* … */ });
```

- `npx playwright test --grep @smoke` para el smoke tras desplegar.
- `--repeat-each=10` para medir intermitencia; `--last-failed` para reejecutar fallos en local; `--only-changed` para los tests afectados por el diff.

## Paralelismo e informes en CI

- `--shard=1/4` … `4/4` en jobs paralelos; con el reporter `blob`, une los informes al final con `npx playwright merge-reports --reporter html ./all-blob-reports`.
- Sube el informe HTML y las trazas como artefactos; `npx playwright show-trace trace.zip` reproduce el fallo paso a paso.

## Accesibilidad y visual

- `@axe-core/playwright`: `const results = await new AxeBuilder({ page }).analyze(); expect(results.violations).toEqual([]);` en los estados clave.
- `await expect(page).toHaveScreenshot()` con `mask: [locatorDeFechas]`; genera y compara las capturas en el mismo contenedor (imagen oficial de Playwright) para evitar diferencias de fuentes.
