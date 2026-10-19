# 📋 Checklist Forense — Contratos de Integración y Suites E2E (Contract & E2E Specialist)

- [ ] **1. Robustez de Localizadores E2E (Semántica y Accesibilidad)**
  - ¿Los selectores de Playwright/Cypress utilizan roles accesibles (`getByRole`, `getByLabel`, `getByPlaceholder`) antes de recurrir a IDs o atributos genéricos?
  - ¿Está completamente erradicado el uso de clases CSS de utilitarios (Tailwind/Bootstrap) y rutas XPath absolutas para interactuar con la interfaz?
  - ¿Los elementos interactivos poseen nombres accesibles claros y predecibles?

- [ ] **2. Control de Sincronización y Anti-Flakiness**
  - ¿El código está 100% libre de `waitForTimeout`, `time.sleep` o retardos de tiempo fijos?
  - ¿Se emplean auto-waiting nativo, aserciones web (`await expect(locator).toBeVisible()`) o esperas de respuestas de red (`waitForResponse`)?
  - ¿Cada test o suite genera su propio estado inicial (datos aislados, usuario efímero o base de datos de test limpia) sin depender de secuencias preexistentes?

- [ ] **3. Validación Estricta de Contratos API y DTOs**
  - ¿Las respuestas del backend se validan mediante esquemas de runtime tipados (Zod, TypeBox, Joi, Pydantic) antes de ser consumidas por la capa de presentación?
  - ¿Los tipos TypeScript / interfaces reflejan estrictamente el contrato OpenAPI/Swagger sin usar `any` o conversiones inseguras (`as unknown as Type`)?
  - ¿Existen pruebas de contrato automatizadas que alerten si un cambio en el backend quiebra campos requeridos por el frontend?

- [ ] **4. Análisis de Valores Límite (BVA) y Manejo de Errores**
  - ¿Se prueban explícitamente los límites numéricos (0, -1, valor máximo permitido), campos de texto de longitud cero o excesiva y caracteres especiales (emojis, inyecciones de prueba)?
  - ¿Se validan visual y funcionalmente las respuestas ante fallos de red (estado offline, respuestas 401/403 que redireccionan a login, mensajes de error 422)?
  - ¿Las aserciones verifican la experiencia del usuario (mensajes de error amigables para el usuario) además del código de estado HTTP?
