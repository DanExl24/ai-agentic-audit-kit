# Notas: Cypress

## Configuración base

```ts
// cypress.config.ts
import { defineConfig } from 'cypress';

export default defineConfig({
  e2e: {
    baseUrl: process.env.BASE_URL ?? 'http://localhost:5173',
    specPattern: 'cypress/e2e/**/*.cy.ts',
    testIsolation: true,                       // estado limpio entre tests (por defecto desde v12)
    retries: { runMode: 1, openMode: 0 },      // los reintentos se registran; investiga los intermitentes
    video: false,                              // actívalo si lo necesitas; las capturas de fallo van por defecto
  },
});
```

Diferencias de modelo que importan:
- Los comandos de Cypress se **encolan** y reintentan; no se usan con `async/await`. Para valores, `.then()` o alias (`.as()`).
- Corre dentro del navegador, una pestaña y un origen por test (`cy.origin()` para otros dominios).

## Autenticación reutilizada

```ts
// cypress/support/commands.ts
Cypress.Commands.add('loginAs', (role: 'admin' | 'reader') => {
  cy.session(role, () => {
    cy.request('POST', '/api/auth/login', {
      email: Cypress.env(`${role}_email`),
      password: Cypress.env(`${role}_password`),
    });
  }, {
    validate: () => { cy.request('/api/auth/me').its('status').should('eq', 200); },
  });
});
```

`cy.session` guarda y restaura cookies y almacenamiento entre tests. Las credenciales van en `cypress.env.json` (fuera del repositorio) o variables `CYPRESS_*` en CI.

## Datos propios

```ts
beforeEach(() => {
  cy.request('POST', '/api/test/orders', { items: 1 }).its('body.id').as('orderId');
});

it('muestra el pedido creado', function () {
  cy.loginAs('reader');
  cy.visit(`/orders/${this.orderId}`);      // `function` para acceder a los alias con this
  cy.findByRole('heading', { name: /pedido/i }).should('be.visible');
});
```

Alternativa a los endpoints de prueba: `cy.task()` que ejecuta código Node (siembra directa en la base de datos de pruebas).

## Localizadores y esperas

- Instala `@testing-library/cypress` para `cy.findByRole`, `cy.findByLabelText`; si no, `[data-cy="…"]` antes que clases.
- Las aserciones `.should()` reintentan: `cy.findByRole('alert').should('have.text', 'Pago confirmado')`.
- Esperar respuestas: `cy.intercept('POST', '/api/orders').as('createOrder'); … cy.wait('@createOrder')`.
- `cy.wait(3000)` (con número) es el anti-patrón clásico; `cy.wait('@alias')` es lo correcto.
- `{ force: true }` en clics suele esconder un problema real (elemento tapado o deshabilitado).

## Red

```ts
cy.intercept('POST', 'https://api.stripe.com/**', { statusCode: 200, body: { status: 'succeeded' } });
```

Simula terceros; con `cy.intercept` sin respuesta solo se observa la petición real.

## Smoke, selección y paralelismo

- Etiquetas con `@cypress/grep`: `it('checkout', { tags: '@smoke' }, …)` y `--env grepTags=@smoke`.
- Paralelismo: Cypress Cloud (`--record --parallel`) o reparto de specs por job con herramientas de la comunidad (p. ej. `cypress-split`).
- Medir intermitencia: ejecutar el spec en bucle (`cypress-repeat` o un bucle en CI) y revisar el historial.

## Accesibilidad y visual

- `cypress-axe`: `cy.injectAxe(); cy.checkA11y();` en los estados clave.
- Regresión visual: plugins de comparación de capturas o servicios externos; misma imagen de contenedor para generar y comparar.
