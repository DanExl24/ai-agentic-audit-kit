# 📋 Checklist Forense — Seguridad Dinámica en Runtime (DAST & OWASP ZAP Specialist)

- [ ] **1. Bastionado de Cabeceras HTTP (Hardening de Respuesta)**
  - ¿La aplicación incluye `Content-Security-Policy` bloqueando scripts inline no autorizados y orígenes externos desconocidos?
  - ¿Está configurada `Strict-Transport-Security: max-age=31536000; includeSubDomains; preload` en todas las respuestas HTTPS?
  - ¿Se envía `X-Content-Type-Options: nosniff` en todos los assets y respuestas API?
  - ¿Se protegen las vistas contra embebido en iframes (`X-Frame-Options: DENY` o `frame-ancestors 'none'`)?
  - ¿Se eliminan o deshabilitan las cabeceras `X-Powered-By` y `Server` en middlewares de producción (ej. `helmet()`)?

- [ ] **2. Prevención de Ataques de Fuerza Bruta y Rate Limiting**
  - ¿Existe un middleware de limitación de tasa (ej. `express-rate-limit`, Redis Token Bucket) en endpoints de autenticación y cambio de credenciales?
  - ¿Se bloquean o retardan progresivamente las IPs que acumulan más de 5 intentos fallidos consecutivos de login?
  - ¿Los endpoints que emiten códigos OTP o tokens por correo/SMS cuentan con enfriamiento obligatorio (*cooldown*) entre solicitudes?

- [ ] **3. Protección de Cookies y Mitigación CSRF**
  - ¿Toda cookie que contiene identificadores de sesión o tokens JWT lleva el atributo `HttpOnly` para evitar su lectura mediante JavaScript malicioso?
  - ¿Las cookies tienen el flag `Secure` activado para ser transmitidas únicamente a través de canales TLS/HTTPS?
  - ¿El atributo `SameSite` está explícitamente configurado como `Strict` o `Lax` para neutralizar ataques de Cross-Site Request Forgery?

- [ ] **4. Enmascaramiento de Errores y Fuga Forense**
  - ¿Cualquier excepción no controlada (HTTP 500) retorna un identificador de error anónimo o mensaje genérico sin exponer trazas de código o llamadas a la base de datos?
  - ¿Los errores 404/400 no exponen nombres de tablas, campos internos o tecnologías subyacentes?
  - ¿El entorno de producción deshabilita totalmente los paneles de depuración interactivos y endpoints de profiling desprotegidos?
