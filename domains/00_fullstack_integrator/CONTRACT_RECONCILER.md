# 📜 Guía Metodológica de Reconciliación de Contratos (Contract Reconciler)

Esta guía define el procedimiento forense que aplica el **Agente Integrador Fullstack** para verificar que la interfaz de usuario y la API del servidor estén 100% sincronizadas.

---

## 1. Las 5 Dimensiones del Desajuste de Contrato

Al auditar la frontera Frontend ↔ Backend, debes revisar:

### Dimensión 1: Sintaxis y Nomenclatura (Case Mismatches)
* **El problema:** Backend devuelve campos en `snake_case` (ej. `user_id`, `created_at`), pero el Frontend los consume esperando `camelCase` (`userId`, `createdAt`).
* **Consecuencia:** En JavaScript/TypeScript, acceder a `user.userId` devuelve silenciosamente `undefined` sin lanzar error inmediato, causando pantallas en blanco o datos vacíos.

### Dimensión 2: Envoltura de Respuesta (Envelope Wrapping)
* **El problema:** Backend devuelve `{ data: { items: [...] }, success: true }`, pero el cliente Axios asume que la respuesta directa es el array o accede a `response.data.items` saltándose el wrapper `data`.

### Dimensión 3: Tipos Primitivos y Coerción Numérica
* **El problema:** Backend almacena IDs o montos monetarios como `string` o `bigint` (ej. `"10500"`), y Frontend realiza operaciones aritméticas tratándolos como `number`, produciendo concatenaciones inesperadas (`"10500" + 50 = "1050050"`).

### Dimensión 4: Errores y Status Codes
* **El problema:** El backend emite `422 Unprocessable Entity` o `400 Bad Request` con un array de errores `{ errors: [{ field: "email", message: "inválido" }] }`, pero el interceptor del frontend solo sabe leer `error.response.data.message`.
* **Consecuencia:** El usuario ve alertas genéricas como "Ocurrió un error inesperado" sin saber qué campo falló.

### Dimensión 5: Estados de Sesión y Headers
* **El problema:** Discrepancia en el header de autorización (`Bearer <token>` vs `token: <jwt>`), cookies `SameSite` bloqueadas por diferencias de dominio/puerto (CORS), o refresco de token no sincronizado.

---

## 2. Técnica de Auditoría Paso a Paso

1. **Paso 1: Mapear Rutas del Backend.** Localiza la definición de endpoints (`routes.ts`, `controller.ts`, OpenAPI o schemas Zod).
2. **Paso 2: Mapear Consumidores del Frontend.** Busca llamadas `apiClient.get/post`, `fetch` o stores donde se invoca cada ruta.
3. **Paso 3: Construcción de la Tabla de Cruce.**
   | Endpoint | Método | Request Payload (Back) | Request Payload (Front) | ¿Coincide? | Response Payload (Back) | Response Payload (Front) | ¿Coincide? |
   | :--- | :---: | :--- | :--- | :---: | :--- | :--- | :---: |
4. **Paso 4: Veredicto de Remediación.** Si hay divergencia, determinar si la corrección debe hacerse en el DTO del backend, en el cliente del frontend o extrayendo un contrato compartido a una capa `shared/`.
