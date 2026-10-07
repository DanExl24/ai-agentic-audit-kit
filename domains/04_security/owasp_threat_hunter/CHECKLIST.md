# 📋 Checklist Forense — Cazador de Amenazas OWASP (AppSec)

- [ ] **1. Control de Acceso y Blindaje Anti-IDOR (A01: Broken Access Control)**
  - ¿Toda consulta que modifica o lee un recurso por ID valida que `recurso.tenant_id == token.tenant_id` o `recurso.user_id == token.user_id`?
  - ¿Los roles y permisos se validan en el servidor y nunca se confía en un flag enviado en el body (ej. `{ isAdmin: true }`)?

- [ ] **2. Inyecciones y Manejo de Entradas (A03: Injection)**
  - ¿Todas las consultas SQL utilizan parámetros tipados (`$1`, `$2`) o query builders seguros, evitando concatenaciones?
  - ¿Las llamadas al sistema operativo usan arrays de argumentos sanitizados (`execFile` / `spawn`) en vez de `exec` con strings crudos?
  - ¿En el frontend se sanitiza cualquier HTML inyectado dinámicamente con DOMPurify?

- [ ] **3. Criptografía y Gestión de Secretos (A02: Cryptographic Failures)**
  - ¿Las contraseñas se almacenan con algoritmos seguros y salt (Argon2id, bcrypt) y nunca en texto plano o MD5/SHA1?
  - ¿El código fuente está 100% libre de credenciales, passwords, JWT secrets o private keys hardcodeadas?
  - ¿Los tokens de sesión tienen expiración corta y rotación o lista negra de revocación?

- [ ] **4. Fallas de Configuración y CORS (A05: Security Misconfiguration)**
  - ¿CORS restringe estrictamente los dominios autorizados y no usa comodín `*` en entornos autenticados?
  - ¿Se devuelven cabeceras de protección básicas (`Content-Security-Policy`, `X-Content-Type-Options`, `Strict-Transport-Security`)?
