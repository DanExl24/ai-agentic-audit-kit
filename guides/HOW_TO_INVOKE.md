# 🚀 Manual Operativo de Invocación por Dominio (Domain Audit Playbook)

> **Guía exhaustiva para saber qué hace cada agente, cuándo activarlo, cuándo NO usarlo y cómo pasarle el contexto exacto.**

Este manual sirve como brújula para cualquier desarrollador o líder técnico que desee auditar un proyecto con el kit. Cada agente está diseñado con **visión hiper-especializada**: sabe mucho de su área y rechaza distraerse con otras capas.

---

## 🧭 1. Árbol de Decisión Rápido (Triage de Problemas)

| Si tu síntoma o necesidad es... | El agente indicado es... | Ruta en el Kit |
| :--- | :--- | :--- |
| Un formulario envía datos pero el servidor rechaza con 400 Bad Request, campos vacíos o nombres que no coinciden entre capas. | **skill `/fullstack:contracts`** | `plugins/fullstack/skills/contracts/` |
| Un flujo falla (UI → red → API → BD) y no sabes en qué capa está la culpa. | **skill `/fullstack:flow-diagnosis`** | `plugins/fullstack/skills/flow-diagnosis/` |
| El repositorio con frontend y backend tiene carpetas desordenadas, tipos duplicados o no sabes cómo estructurarlo. | **skill `/fullstack:topology`** | `plugins/fullstack/skills/topology/` |
| Quieres construir una funcionalidad que toca varias áreas o ambas capas (pagos, CRUD con permisos, subida de archivos…). | **skill `/fullstack:feature`** | `plugins/fullstack/skills/feature/` |
| Quieres auditar la aplicación completa (frontend + backend) o saber si está lista para producción. | **skill `/fullstack:audit`** | `plugins/fullstack/skills/audit/` |
| Quieres auditar un módulo de frontend completo, saber si está listo para publicar o no sabes qué skill aplicar. | **skill `/frontend:audit`** | `plugins/frontend/skills/audit/` |
| La interfaz es incómoda, fea o no sabes si funciona bien en móvil, tablet y laptop (sin código). | **skill `/frontend:ux-review`** | `plugins/frontend/skills/ux-review/` |
| Estructura caótica de carpetas frontend, dependencias circulares, features acopladas. | **skill `/frontend:architecture`** | `plugins/frontend/skills/architecture/` |
| Tipos `any`, contratos de API sin tipar o sin validar, tsconfig laxo. | **skill `/frontend:typescript`** | `plugins/frontend/skills/typescript/` |
| Llamadas directas de axios en vistas, refresh token, caché, datos obsoletos, respuestas fuera de orden. | **skill `/frontend:data-fetching`** | `plugins/frontend/skills/data-fetching/` |
| La página se congela, la memoria RAM del navegador no para de subir o hay re-renders infinitos. | **skill `/frontend:state-management`** | `plugins/frontend/skills/state-management/` |
| Formularios complejos, validación Zod, prevención de doble clic y errores 422. | **skill `/frontend:forms`** | `plugins/frontend/skills/forms/` |
| Colores hardcodeados, quiebres de Dark/Light mode, variantes CVA, componentes base duplicados. | **skill `/frontend:design-system`** | `plugins/frontend/skills/design-system/` |
| Trampas de teclado, focus trap/restoration en modales, contraste WCAG, ARIA, lectores de pantalla. | **skill `/frontend:accessibility`** | `plugins/frontend/skills/accessibility/` |
| El diseño está aprobado pero se desborda en laptop 1366x768 o móvil (sin rediseñar). | **skill `/frontend:responsive-layout`** | `plugins/frontend/skills/responsive-layout/` |
| La app carga lento, los clics responden tarde, el contenido salta o el bundle no para de crecer. | **skill `/frontend:performance`** | `plugins/frontend/skills/performance/` |
| ¿SPA, SSR o SSG? Errores de hidratación, páginas que no indexan o vistas previas vacías al compartir. | **skill `/frontend:rendering-and-seo`** | `plugins/frontend/skills/rendering-and-seo/` |
| Se ve contenido protegido antes de redirigir, filtros que se pierden al recargar, botón atrás que falla. | **skill `/frontend:routing`** | `plugins/frontend/skills/routing/` |
| HTML de usuarios renderizado, tokens en localStorage, secretos en el bundle, scripts de terceros. | **skill `/frontend:security`** | `plugins/frontend/skills/security/` |
| Tests de componentes frágiles, lentos o intermitentes; qué probar y cómo en el frontend. | **skill `/frontend:testing`** | `plugins/frontend/skills/testing/` |
| Pantallas en blanco tras un error, errores de usuarios que no llegan al equipo o llegan sin contexto. | **skill `/frontend:observability`** | `plugins/frontend/skills/observability/` |
| Varios idiomas o países: textos sin traducir, plurales, fechas, monedas, RTL. | **skill `/frontend:i18n`** | `plugins/frontend/skills/i18n/` |
| CI lento o débil, builds no reproducibles, variables de entorno caóticas, lint y formato. | **skill `/frontend:tooling`** | `plugins/frontend/skills/tooling/` |
| Peticiones colgadas, endpoints sin validación, errores 500 con stack trace, respuestas que filtran campos internos. | **skill `/backend:http-layer`** | `plugins/backend/skills/http-layer/` |
| Controladores gigantes, reglas de negocio duplicadas, estados imposibles, dinero en float. | **skill `/backend:domain-logic`** | `plugins/backend/skills/domain-logic/` |
| N+1, consultas sin límite, operaciones sin transacción, sobreventa o saldos incorrectos bajo concurrencia, pool agotado. | **skill `/backend:data-access`** | `plugins/backend/skills/data-access/` |
| Faltan índices, consultas lentas en EXPLAIN, migraciones que bloquean tablas o cambios de esquema en producción. | **skill `/backend:schema-and-migrations`** | `plugins/backend/skills/schema-and-migrations/` |
| Código del servicio enredado, módulos que tocan tablas ajenas, ¿monolito o microservicios? | **skill `/backend:architecture`** | `plugins/backend/skills/architecture/` |
| Diseñar o revisar el contrato de la API: códigos, errores, paginación, idempotencia, versionado. | **skill `/backend:api-design`** | `plugins/backend/skills/api-design/` |
| Jobs duplicados o perdidos, eventos entre módulos, cron con varias instancias, colas atascadas. | **skill `/backend:async-messaging`** | `plugins/backend/skills/async-messaging/` |
| Integrar pagos, email u otras APIs; webhooks; caídas en cascada por un proveedor lento. | **skill `/backend:integrations`** | `plugins/backend/skills/integrations/` |
| Añadir caché, datos obsoletos tras guardar, datos de otro usuario en caché, picos al expirar claves. | **skill `/backend:caching`** | `plugins/backend/skills/caching/` |
| Incidentes difíciles de diagnosticar, logs inútiles, alertas ruidosas, health checks que reinician pods sanos. | **skill `/backend:observability`** | `plugins/backend/skills/observability/` |
| Endpoints lentos, p99 alta, memoria creciente, preparación de un pico de tráfico. | **skill `/backend:performance`** | `plugins/backend/skills/performance/` |
| Tests de backend que mockean la BD, suites intermitentes, permisos o concurrencia sin probar. | **skill `/backend:testing`** | `plugins/backend/skills/testing/` |
| Builds no reproducibles, configuración caótica, CI sin tests de integración, imagen como root. | **skill `/backend:tooling`** | `plugins/backend/skills/tooling/` |
| Datos personales en logs o staging, borrado de cuentas, exportación de datos, cifrado, RGPD o ley local. | **skill `/backend:data-privacy`** | `plugins/backend/skills/data-privacy/` |
| Revisar un servicio backend completo o decidir si está listo para producción. | **skill `/backend:audit`** | `plugins/backend/skills/audit/` |
| Login, sesiones, JWT, reset de contraseña, MFA o API keys. | **skill `/backend:authentication`** | `plugins/backend/skills/authentication/` |
| ¿Un usuario puede ver o modificar datos ajenos (IDOR)? Roles, permisos, aislamiento entre tenants. | **skill `/backend:authorization`** | `plugins/backend/skills/authorization/` |
| Inyecciones, SSRF, uploads, rate limiting, secretos en el repo, configuración insegura, dependencias vulnerables. | **skill `/backend:api-security`** | `plugins/backend/skills/api-security/` |
| Quieres saber cómo está la calidad y las pruebas del proyecto, si un release está listo o no sabes qué skill de QA aplicar. | **skill `/qa:audit`** | `plugins/qa/skills/audit/` |
| No sabes qué probar ni cuánto: mapa de riesgos, definición de terminado, criterios de salida de un release. | **skill `/qa:test-strategy`** | `plugins/qa/skills/test-strategy/` |
| Necesitas casos que encuentren defectos: valores límite, tablas de decisión, estados, combinaciones, Gherkin. | **skill `/qa:test-design`** | `plugins/qa/skills/test-design/` |
| Los tests pasan pero los usuarios encuentran fallos; quieres explorar antes de un release. | **skill `/qa:exploratory-testing`** | `plugins/qa/skills/exploratory-testing/` |
| Tests E2E rotos o intermitentes, selectores frágiles, esperas fijas, o crear la suite de recorridos críticos. | **skill `/qa:e2e`** | `plugins/qa/skills/e2e/` |
| Pipeline lento, fallos ignorados, reintentos hasta que pasa, qué bloquea el merge y qué no. | **skill `/qa:quality-gates`** | `plugins/qa/skills/quality-gates/` |
| ¿Aguanta el tráfico esperado? Pruebas de carga con k6, Locust o Gatling y umbrales desde los SLO. | **skill `/qa:load-testing`** | `plugins/qa/skills/load-testing/` |
| Seguridad en ejecución: cabeceras, cookies y errores reales con OWASP ZAP contra un entorno propio. | **skill `/qa:dast`** | `plugins/qa/skills/dast/` |
| Bugs que vuelven o se escapan a producción: hotspots, Ishikawa, Pareto 80/20 y matriz de acciones Kaizen. | **skill `/qa:defect-analysis`** | `plugins/qa/skills/defect-analysis/` |
| Tienes una idea y quieres saber qué problema resuelve, para quién, qué se está suponiendo y cuál es el MVP. | **skill `/product:discovery`** | `plugins/product/skills/discovery/` |
| Requisitos vagos o contradictorios; hay que entrevistar a usuarios o documentar lo que hace un sistema existente. | **skill `/product:elicitation`** | `plugins/product/skills/elicitation/` |
| Palabras con dos significados, reglas de negocio dispersas o sin cifras, falta un glosario o un modelo del dominio. | **skill `/product:domain-modeling`** | `plugins/product/skills/domain-modeling/` |
| Hay reglas o requisitos acordados y necesitas historias con criterios verificables. | **skill `/product:user-stories`** | `plugins/product/skills/user-stories/` |
| Necesitas decidir qué historias entran en el MVP y en qué orden entregarlas. | **skill `/product:prioritization`** | `plugins/product/skills/prioritization/` |

---

## 🏛️ 2. Guía Detallada Agente por Agente

---

### 🔗 DOMINIO 00: FULLSTACK (plugin `fullstack`)

Las skills que cruzan frontend y backend están en `plugins/fullstack/skills/`. Requieren los plugins `frontend` y `backend` (invocan a sus skills) y comparten escala y formato en `plugins/fullstack/standards/` (códigos `FS-*`, con evidencia en servidor y cliente). Catálogo: [`plugins/fullstack/README.md`](../plugins/fullstack/README.md).

| Skill | Qué cubre | Sustituye a |
| :--- | :--- | :--- |
| `/fullstack:contracts` | Tabla de cruce endpoint ↔ consumidor, 5 dimensiones de desajuste, contrato compartido (OpenAPI o esquemas), codegen, orden de despliegue de cambios. | `CONTRACT_RECONCILER` |
| `/fullstack:topology` | Monolito modular, monorepo con paquetes o hexagonal; dependencias ilegítimas; migración strangler por fases. | `TOPOLOGY_REFACTORER` |
| `/fullstack:flow-diagnosis` | Seguir un flujo UI → red → API → BD para localizar la capa culpable y corregir en la causa raíz. | diagnóstico E2E del `SYSTEM_PROMPT` |
| `/fullstack:feature` | Orquestador de construcción: plan por capas con recetas, aviso de coste, contrato primero, pasos verificados, registro en `.sdlc/context.md`. | 🆕 |
| `/fullstack:audit` | Orquestador conjunto: un aviso de coste, `frontend:audit` + `backend:audit` + skills entre capas, deduplicación y puntuación conjunta. | `ONE_SHOT_PROMPT` |

* **¿Cuándo NO usarlas?** Para problemas de una sola capa: contraste de color → `/frontend:accessibility`; una consulta lenta ya identificada → `/backend:data-access`; fugas de memoria en el cliente → `/frontend:state-management`.

---

### 🎨 DOMINIO 01: FRONTEND (plugin `frontend`)

Todos los especialistas del frontend son ahora **skills de Claude Code** en `plugins/frontend/skills/`. Cada una tiene dos modos (construir/diseñar y auditar), notas por stack (Vue, React, Angular) cuando aplica, y comparte con las demás la escala de severidad, el formato de informe y la matriz de 13 viewports (`plugins/frontend/standards/`). Se invocan con `/frontend:<skill>` o se activan solas cuando la petición encaja con su descripción. Catálogo completo: [`plugins/frontend/README.md`](../plugins/frontend/README.md).

| Skill | Qué cubre | Sustituye a |
| :--- | :--- | :--- |
| `/frontend:ux-review` | Crítica UI/UX sin código: jerarquía, densidad, coherencia visual, responsive percibido, estados, flujos, Antes/Después. También diseña la UX de pantallas nuevas. | `01_senior_design_critic` |
| `/frontend:architecture` | Estructura por features, límites entre módulos, dependencias circulares, monorepo, ADRs. | parte de `01_arch_and_network` |
| `/frontend:typescript` | tsconfig estricto, eliminar `any`, contratos de API tipados y validados, uniones discriminadas. | parte de `01_arch_and_network` |
| `/frontend:data-fetching` | Cliente HTTP, interceptores, refresh token single-flight, cancelación, TanStack Query, tiempo real. | parte de `01_arch_and_network` |
| `/frontend:state-management` | Dónde vive cada dato, stores, fugas de memoria, reactividad, re-renders, estado en SSR. | `02_state_and_reactivity` |
| `/frontend:forms` | Schemas, doble envío, idempotencia, errores 422 por campo, wizards, listas dinámicas, archivos. | `03_forms_and_data_flow` |
| `/frontend:design-system` | Tokens en tres niveles, temas, componentes base, variantes (CVA), matriz de estados, resiliencia de layout. | `04_design_system_and_styling` |
| `/frontend:accessibility` | WCAG 2.2 AA: teclado, foco, ARIA (patrones APG), lectores de pantalla, contraste, pruebas con axe y manuales. | `05_accessibility_and_wcag` |
| `/frontend:responsive-layout` | Correcciones de layout sin rediseñar en 13 viewports con jerarquía de 5 niveles. | `06_responsive_layout_specialist` |
| `/frontend:performance` | Core Web Vitals (LCP, INP, CLS), bundle y code splitting, imágenes, fuentes, terceros, presupuestos en CI. | nueva |
| `/frontend:rendering-and-seo` | CSR/SSR/SSG/ISR, hidratación, aislamiento en SSR, metadatos, canonical, sitemap, datos estructurados, 404 reales. | nueva |
| `/frontend:routing` | Rutas tipadas, lazy loading, guards (y sus límites), retorno seguro tras login, estado en la URL validado, 404/403. | nueva |
| `/frontend:security` | XSS y sanitización, sesión y tokens, CSRF, secretos en el bundle, CSP, postMessage, dependencias. | nueva |
| `/frontend:testing` | Testing Library, MSW, tests de formularios, stores y guards, estabilidad, regresión visual. E2E en `/qa:e2e`. | nueva |
| `/frontend:observability` | Capas de manejo de errores, UX de error, Sentry (source maps, releases, sin datos personales), RUM, trazas con el backend, desfase de versión. | nueva |
| `/frontend:i18n` | Claves y ICU, sin concatenar, formatos con `Intl`, zonas horarias, detección de idioma, URLs por idioma, RTL, flujo de traducción. | nueva |
| `/frontend:tooling` | Node y lockfile fijados, scripts estándar, entorno validado, ESLint/Prettier/Biome, hooks, CI, source maps, despliegue estático. | nueva |
| `/frontend:audit` | Orquestador: triage, elige una de 11 rutas, aplica las skills, deduplica, puntúa por área y global (0–100) y propone (o ejecuta) la remediación por lotes. | `00_frontend_director` |

---
### ⚙️ DOMINIO 02: BACKEND (plugin `backend`, incluye base de datos)

Los antiguos agentes `02_backend/api_rest_gateway`, `02_backend/domain_business_logic` y `03_database/query_performance_indexer` son ahora **skills de Claude Code** en `plugins/backend/skills/`, con modos construir y auditar y notas para Node/TypeScript, Python y Java/Spring. Se invocan con `/backend:<skill>`. Catálogo y hoja de ruta: [`plugins/backend/README.md`](../plugins/backend/README.md).

| Skill | Qué cubre | Sustituye a |
| :--- | :--- | :--- |
| `/backend:http-layer` | Validación en la frontera, mass assignment, DTOs de salida, pipeline de middlewares, error handler único, límites, timeouts, CORS, graceful shutdown. | `api_rest_gateway` |
| `/backend:domain-logic` | Casos de uso, invariantes, máquinas de estado, value objects (dinero), errores de dominio, efectos tras el commit. | `domain_business_logic` |
| `/backend:data-access` | N+1, límites y paginación por cursor, transacciones y aislamiento, concurrencia (atómicas, optimista, pesimista, upsert), pool y timeouts. | `query_performance_indexer` (parte de código) + transacciones de `domain_business_logic` |
| `/backend:schema-and-migrations` | Tipos y constraints, índices desde las consultas, EXPLAIN, migraciones sin downtime (expand/contract, índices concurrentes, backfills por lotes). | `query_performance_indexer` (índices) |
| `/backend:architecture` | Monolito modular vs microservicios, módulos con API pública y tablas propias, capas, puertos, DI, verificación de dependencias, strangler fig. | nueva (+ arquetipos de backend del integrador fullstack) |
| `/backend:api-design` | Recursos, códigos de estado, RFC 9457, convenciones, paginación por cursor, Idempotency-Key, ETag, versionado y deprecación, OpenAPI. | nueva |
| `/backend:async-messaging` | Jobs, colas y eventos: encolar tras el commit, outbox/inbox, consumidores idempotentes, reintentos y DLQ, cron único, sagas. | nueva |
| `/backend:integrations` | APIs de terceros con timeouts, reintentos seguros, circuit breaker y bulkhead; webhooks entrantes y salientes. | nueva |
| `/backend:caching` | Cuándo cachear, cache-aside con TTL, claves con tenant/usuario, invalidación tras el commit, stampede, HTTP caching. | nueva |
| `/backend:observability` | Logs estructurados con redacción, trazas OpenTelemetry, métricas RED/USE, health checks, SLOs y alertas por síntomas. | nueva |
| `/backend:performance` | Diagnóstico con trazas y profiling, runtime (event loop, GIL, hilos), dimensionado de workers y pools, streaming, memoria, carga. | parte de código de QA `03_performance_load_audit` |
| `/backend:testing` | BD real con Testcontainers, tests de API, simulación de externos, casos críticos (tenants, idempotencia, concurrencia, migraciones), contrato. | parte de backend de QA `01_testability_and_unit_audit` |
| `/backend:tooling` | Runtime y lockfile fijados, configuración validada, lint y tipos, entorno local, CI con integración y escaneos, imagen sin root. | nueva |
| `/backend:data-privacy` | Mapa de datos personales, minimización, retención, supresión y exportación, cifrado por campo con KMS, auditoría. | nueva |
| `/backend:audit` | Orquestador: triage, 10 rutas, deduplicación, puntuación 0–100 y remediación por lotes. | nueva (no había director de backend) |

---
### 🛡️ SEGURIDAD DE SERVIDOR (plugin `backend`)

El antiguo agente `04_security/owasp_threat_hunter` se ha repartido en tres skills del plugin `backend` que cubren el OWASP API Security Top 10 (2023). La seguridad del cliente (XSS, CSP, tokens en el navegador) está en `/frontend:security`.

| Skill | Qué cubre |
| :--- | :--- |
| `/backend:authentication` | Sesiones vs tokens, verificación de JWT, refresh rotativo con detección de reutilización, OIDC, hashing (Argon2id/bcrypt), login sin enumeración y con límites, reset de contraseña, MFA, API keys. |
| `/backend:authorization` | RBAC/ABAC/ReBAC, autorización por objeto (IDOR), por función y por propiedad, multi-tenant con row-level security, listados y exportaciones, tests de matriz de permisos. |
| `/backend:api-security` | Inyecciones (SQL, NoSQL, comandos, rutas, plantillas), consumo de recursos y rate limiting, flujos de negocio, SSRF, uploads, deserialización, secretos, configuración de producción, inventario, dependencias. |

---
### 🧪 DOMINIO 05: QA (plugin `qa`)

Las skills de calidad a lo largo del SDLC están en `plugins/qa/skills/`: decidir qué probar según el riesgo, diseñar casos, explorar, las pruebas contra el sistema en marcha (E2E, carga, seguridad dinámica) y el proceso (puertas de calidad, análisis de defectos). Las que dependen de una herramienta tienen notas por herramienta (`playwright.md`, `k6.md`, `zap.md`…), no por lenguaje. Comparten escala, formatos, handoffs y contexto en `plugins/qa/standards/` (códigos `QA-*`). Catálogo: [`plugins/qa/README.md`](../plugins/qa/README.md).

| Skill | Qué cubre | Sustituye a |
| :--- | :--- | :--- |
| `/qa:test-strategy` | Mapa de riesgos (impacto × probabilidad × detección), forma de la cobertura, automatizar / explorar / vigilar, definición de terminado, criterios de salida, plan de release. | nueva |
| `/qa:test-design` | Particiones, valores límite, tablas de decisión, transiciones de estado, pairwise, negativos, property-based testing, Gherkin. | BVA de `02_contract_and_e2e_audit` |
| `/qa:exploratory-testing` | Charters, heurísticas, notas de sesión, reportes de bug reproducibles; ejecutable por un agente con navegador. | nueva |
| `/qa:e2e` | Recorridos críticos, fixtures, localizadores por rol, datos propios por test, instancia desechable, intermitencia, smoke tras desplegar (Playwright, Cypress). | `02_contract_and_e2e_audit` |
| `/qa:quality-gates` | Etapas del pipeline, presupuestos de tiempo, tests afectados, sharding, cuarentena con caducidad, cobertura del diff, checks obligatorios (GitHub Actions, GitLab CI). | parte de CI del `00_qa_director` |
| `/qa:load-testing` | Tipos de prueba, modelo de carga, escenarios realistas, umbrales desde los SLO, entorno autorizado, interpretación, smoke en CI (k6, Locust, Gatling). | `03_performance_load_audit` |
| `/qa:dast` | Autorización y alcance, baseline / completo / API, escaneo autenticado, reglas y supresiones justificadas, criba (OWASP ZAP). | `04_dast_security_zap_audit` |
| `/qa:defect-analysis` | Defectos escapados y regresiones: clasificación, hotspots, 5 porqués, Ishikawa en Mermaid (5 ramas), Pareto 80/20, matriz Kaizen (Quick Win, Táctico, Estratégico con dificultad, plazo, impacto y KPI), criterios de cierre. | `05_root_cause_kaizen_audit` |
| `/qa:audit` | Orquestador: triage, 6 rutas, aplicabilidad por contexto, madurez de QA 0–100 por 5 pilares con nivel (Reactivo, Básico, Gestionado, Continuo), remediación por lotes. | `00_qa_director` |

* **¿Cuándo NO usarlas?** Para escribir los tests de una capa → `/frontend:testing` o `/backend:testing`; para corregir el código que el escaneo o la prueba señalan → la skill de la capa (`/backend:api-security`, `/backend:performance`…); para incidentes de operación (caídas, guardias, SLO) → futuro dominio SRE.

---

### 💡 DOMINIO 06: PRODUCTO Y REQUISITOS (plugin `product`, en construcción)

Las skills cubren descubrimiento, levantamiento, modelado de reglas, historias con criterios de aceptación y priorización. La especificación y la trazabilidad transversal se añadirán en olas posteriores. Todas las skills usan [IDs y enlaces estables](../plugins/product/standards/ids-and-links.md) y registran las dudas de negocio. Catálogo en [Producto](../plugins/product/README.md).

| Skill | Qué cubre |
| :--- | :--- |
| `/product:discovery` | Problema y evidencia, segmentos y trabajos por hacer, propuesta de valor, Lean Canvas (o versión interna), supuestos de mayor riesgo con experimento, MVP, objetivos y métricas. |
| `/product:elicitation` | Interesados, técnicas, guion de entrevista, entrevista al usuario en el chat por bloques, análisis del sistema existente, registros de preguntas, supuestos y decisiones. |
| `/product:domain-modeling` | Glosario, modelo conceptual, estados, eventos y módulos, reglas de negocio atómicas con ejemplos, motivo, origen y enlaces al código. |
| `/product:user-stories` | Épicas, mapas e historias divididas por valor, criterios de aceptación, casos de uso y Definition of Ready. |
| `/product:prioritization` | Método y evidencia de priorización, dependencias, corte del MVP y plan de entregas. |

* **¿Cuándo NO usarlas?** Para el esquema de base de datos → `/backend:schema-and-migrations`; para implementar reglas → `/backend:domain-logic`; para el diseño visual de pantallas → `/frontend:ux-review`.

---

## 🔁 3. Escalado entre capas

Si una skill de capa detecta que la causa raíz está en la otra capa, o que la corrección necesita las dos:

1. Reúne la evidencia de la skill (archivo, petición, respuesta, pasos).
2. Invoca `/fullstack:contracts` si es un desajuste de contrato, o `/fullstack:flow-diagnosis` si es un flujo concreto, con las rutas de ambas capas.
3. La skill entrega el hallazgo `FS-*` con la corrección en cada capa y el orden de despliegue.

Para una revisión completa de punta a punta, `/fullstack:audit` hace todo esto en una sola pasada.

Las reglas de encadenamiento (profundidad máxima de 2, sin reinvocar, aviso de coste, plan B si falta un plugin) y el contexto compartido `.sdlc/context.md` están en `standards/handoffs.md` y `standards/context.md` de cada plugin (idénticos en los cinco plugins; p. ej. [`plugins/fullstack/standards/handoffs.md`](../plugins/fullstack/standards/handoffs.md)). Cada skill de los cinco plugins tiene una sección `Handoffs` con sus disparadores concretos.
