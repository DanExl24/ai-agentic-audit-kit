# 📋 Checklist Forense — Auditor de API Gateway y Middlewares

- [ ] **1. Validación Estricta de Entradas**
  - ¿Todo endpoint POST, PUT, PATCH valida el body con un esquema formal (Zod/Joi/Pydantic) antes de entrar al controller?
  - ¿Los parámetros de URL numéricos (`/:id`) se validan contra inyección de strings no numéricos o NaN?
  - ¿Los query params de paginación (`limit`, `offset`) tienen topes máximos forzosos para evitar denegación de servicio (DoS)?

- [ ] **2. Integridad de Middlewares y Cadena de Control**
  - ¿Todos los middlewares garantizan que `next()` o `res.send()` se ejecutan exactamente una vez en cada ruta lógica?
  - ¿Se manejan errores asíncronos (`express-async-errors` o handlers nativos) sin provocar 'unhandled promise rejections'?
  - ¿Existe un middleware de Rate Limiting activo en rutas de autenticación y transacciones críticas?

- [ ] **3. Estandarización de Respuestas y Errores**
  - ¿Todas las respuestas de éxito usan el mismo envelope (ej. `{ success: true, data: ... }`)?
  - ¿Todas las respuestas de error usan `{ success: false, error: { code, message } }`?
  - ¿Los errores 500 ocultan el stack trace y detalles internos de la base de datos en entorno productivo?

- [ ] **4. Seguridad Perimetral y Cabeceras**
  - ¿CORS está configurado con una lista blanca explícita de orígenes?
  - ¿Se aplican cabeceras de seguridad básicas (`X-Content-Type-Options: nosniff`, `X-Frame-Options: DENY`)?
