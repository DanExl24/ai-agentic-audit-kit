# Plugin `backend`

Skills para diseñar, construir y auditar backends en **Node.js/TypeScript (Express, Fastify, NestJS), Python (FastAPI, Django) y Java (Spring Boot)**. Cada skill:

- Tiene dos modos: **Construir** (crear o refactorizar) y **Auditar** (revisar código existente y emitir un informe con severidades).
- Tiene una base agnóstica de lenguaje y notas por stack (`node.md`, `python.md`, `java.md`) que solo se cargan cuando aplican.
- Comparte la escala de severidad y el formato de informe de [`standards/`](standards/) (códigos `BE-*`).

Incluye el acceso a datos y el esquema de base de datos, y en las próximas olas la seguridad de servidor: lo que un desarrollador de backend toca dentro de su servicio.

## Uso

```bash
/plugin marketplace add <ruta-o-repo-de-este-kit>
/plugin install backend@sdlc-skills
```

```text
/backend:data-access revisa las condiciones de carrera en src/modules/inventory
/backend:schema-and-migrations prepara la migración para añadir full_name sin downtime
```

## Catálogo

| Skill | Estado | Cubre |
| :--- | :---: | :--- |
| `http-layer` | ✅ | Validación en la frontera, mass assignment, DTOs de salida, pipeline de middlewares, error handler, límites, timeouts, CORS, graceful shutdown |
| `domain-logic` | ✅ | Casos de uso, invariantes, máquinas de estado, value objects (dinero), errores de dominio, efectos tras el commit |
| `data-access` | ✅ | N+1, límites y paginación, transacciones y aislamiento, concurrencia (atómicas, optimista, pesimista, upsert), pool y timeouts |
| `schema-and-migrations` | ✅ | Tipos y constraints, índices desde las consultas, EXPLAIN, migraciones sin downtime (expand/contract, concurrentes, backfills) |
| `authentication` | 🔜 ola 2 | Sesiones vs tokens, JWT, OAuth/OIDC, hashing, reset, MFA, fuerza bruta |
| `authorization` | 🔜 ola 2 | RBAC/ABAC, autorización por objeto (IDOR), multi-tenant |
| `api-security` | 🔜 ola 2 | OWASP API Top 10: inyección, SSRF, consumo de recursos, uploads, dependencias |
| `architecture` | 🔜 ola 3 | Capas, monolito modular, hexagonal pragmática, módulos, ADRs |
| `api-design` | 🔜 ola 3 | Recursos, códigos, errores RFC 9457, paginación, versionado, idempotencia, OpenAPI |
| `async-messaging` | 🔜 ola 3 | Colas, jobs, reintentos, DLQ, consumidores idempotentes, outbox |
| `integrations` | 🔜 ola 3 | APIs de terceros, webhooks, timeouts, reintentos, circuit breaker |
| `caching` | 🔜 ola 3 | Cache-aside, invalidación, stampede, HTTP caching |
| `observability` | 🔜 ola 4 | Logs estructurados, métricas, trazas, health checks, SLOs |
| `performance` | 🔜 ola 4 | Profiling, concurrencia del runtime, memoria, streaming |
| `testing` | 🔜 ola 4 | Integración con BD real, tests de API, contract testing |
| `tooling` | 🔜 ola 4 | Entorno reproducible, configuración validada, secretos, CI |
| `data-privacy` | 🔜 ola 4 | PII, retención y borrado, auditoría, cifrado por campo |
| `audit` | 🔜 ola 4 | Orquestador de auditorías con puntuación |

## Estructura de una skill

```text
skills/<skill>/
├── SKILL.md              # cuándo usarla, modos, flujo y principios
└── references/
    ├── patterns.md       # patrones de construcción y anti-patrones
    ├── checklist.md      # checklist de auditoría con severidad orientativa
    ├── node.md
    ├── python.md
    └── java.md
```
