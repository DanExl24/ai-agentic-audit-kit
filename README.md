# 🛡️ AI Agentic Audit Kit → SDLC Skills

> **Repositorio de skills por dominio para todo el ciclo de vida del software: diseñar, construir, auditar y operar.**

El kit nació como un conjunto de prompts de auditoría (patrón *Hub & Spoke*: especialistas verticales + integrador fullstack). Ahora se está migrando a **skills de Claude Code** empaquetadas como **un plugin por dominio** dentro de un marketplace. Cada skill sirve tanto para construir como para auditar, y es agnóstica de framework, con notas específicas por stack.

---

## 🧭 Estado de la migración

| Dominio | Formato | Estado |
| :--- | :--- | :--- |
| **Frontend** | Plugin `plugins/frontend/` | ✅ Migrado: 18 skills (17 especialistas + el orquestador `audit`). Pendiente de validar sobre proyectos reales. |
| **Backend** (incluye database y security de servidor) | Plugin `plugins/backend/` | ✅ Migrado: 18 skills (17 especialistas + el orquestador `audit`). Pendiente de validar sobre proyectos reales. Absorbe los antiguos `02_backend`, `03_database` y `04_security` (la parte de cliente está en `frontend:security`). |
| **Fullstack** (entre capas) | Plugin `plugins/fullstack/` | ✅ Migrado: 5 skills (`contracts`, `topology`, `flow-diagnosis`, el orquestador de construcción `feature` y el orquestador `audit`, que combina las auditorías de frontend y backend), más el estándar de handoffs y el contexto compartido `.sdlc/context.md`. Requiere los plugins `frontend` y `backend`. |
| QA & Testing | Prompts en `domains/05_qa_testing_engineering/` | ⏳ Pendiente |

Catálogos: [`plugins/frontend/README.md`](plugins/frontend/README.md) · [`plugins/backend/README.md`](plugins/backend/README.md) · [`plugins/fullstack/README.md`](plugins/fullstack/README.md).

---

## 🗂️ Estructura

```text
ai-agentic-audit-kit/
├── .claude-plugin/
│   └── marketplace.json          # marketplace "sdlc-skills": lista los plugins por dominio
│
├── plugins/                      # ✅ NUEVO FORMATO: un plugin por dominio
│   ├── frontend/
│   │   ├── .claude-plugin/plugin.json
│   │   ├── standards/            # severidad, formato de informes y matriz de viewports
│   │   └── skills/
│   │       ├── audit/                # orquestador: elige skills, puntúa y consolida
│   │       ├── ux-review/
│   │       ├── architecture/
│   │       ├── typescript/
│   │       ├── data-fetching/
│   │       ├── state-management/
│   │       ├── forms/
│   │       ├── design-system/
│   │       ├── accessibility/
│   │       ├── responsive-layout/
│   │       ├── performance/
│   │       ├── rendering-and-seo/
│   │       ├── routing/
│   │       ├── security/
│   │       ├── testing/
│   │       ├── observability/
│   │       ├── i18n/
│   │       └── tooling/
│   ├── backend/
│   │   ├── .claude-plugin/plugin.json
│   │   ├── standards/            # severidad y formato de informes (códigos BE-*)
│   │   └── skills/
│   │       ├── http-layer/
│   │       ├── domain-logic/
│   │       ├── data-access/
│   │       ├── schema-and-migrations/
│   │       ├── authentication/
│   │       ├── authorization/
│   │       ├── api-security/
│   │       ├── architecture/
│   │       ├── api-design/
│   │       ├── async-messaging/
│   │       ├── integrations/
│   │       ├── caching/
│   │       ├── observability/
│   │       ├── performance/
│   │       ├── testing/
│   │       ├── tooling/
│   │       ├── data-privacy/
│   │       └── audit/                # orquestador
│   └── fullstack/                # requiere frontend y backend
│       ├── .claude-plugin/plugin.json
│       ├── standards/
│       └── skills/
│           ├── contracts/
│           ├── topology/
│           ├── flow-diagnosis/
│           ├── feature/              # orquestador de construcción
│           └── audit/                # orquestador conjunto
│
├── domains/                      # ⏳ FORMATO ANTIGUO: prompts pendientes de migrar
│   └── 05_qa_testing_engineering/
│
├── protocols/                    # protocolo de interoperabilidad del formato antiguo
├── templates/                    # plantillas de informes del formato antiguo
└── guides/                       # guía de invocación y matriz de severidad
```

---

## ⚡ Uso

### Skills (formato nuevo)

Desde Claude Code:

```bash
/plugin marketplace add <ruta-local-o-repo-github-de-este-kit>
/plugin install frontend@sdlc-skills
/plugin install backend@sdlc-skills
/plugin install fullstack@sdlc-skills
```

Instala solo los plugins de los dominios que use cada proyecto (cada plugin añade sus descripciones al contexto de la sesión).

Después:

```text
/frontend:forms audita los formularios de src/features/checkout
/backend:data-access revisa las condiciones de carrera en src/modules/inventory
```

Las skills también se activan automáticamente cuando la petición encaja con su descripción.

### Prompts (formato antiguo, dominios pendientes)

1. Entra a la carpeta del agente (ej. `domains/05_qa_testing_engineering/03_performance_load_audit/`).
2. Abre `ONE_SHOT_PROMPT.md`, copia el prompt y reemplaza la ruta del archivo o módulo.
3. El agente devuelve un informe de hallazgos con severidad y corrección.

Guía detallada de cada agente y skill: [`guides/HOW_TO_INVOKE.md`](guides/HOW_TO_INVOKE.md).

---

## ⚖️ Licencia
MIT License.
