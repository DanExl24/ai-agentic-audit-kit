# 🛡️ AI Agentic Audit Kit → SDLC Skills

> **Repositorio de skills por dominio para todo el ciclo de vida del software: diseñar, construir, auditar y operar.**

El kit nació como un conjunto de prompts de auditoría (patrón *Hub & Spoke*: especialistas verticales + integrador fullstack). Ahora son **skills de Claude Code** empaquetadas como **un plugin por dominio** dentro de un marketplace. Cada skill sirve tanto para construir como para auditar, y es agnóstica de framework, con notas específicas por stack o por herramienta. Todos los dominios del formato antiguo están migrados; los nuevos (SRE, DevOps…) se añadirán como plugins.

---

## 🧭 Estado

| Dominio | Formato | Estado |
| :--- | :--- | :--- |
| **Frontend** | Plugin `plugins/frontend/` | ✅ 18 skills (17 especialistas + el orquestador `audit`). Probado sobre proyectos reales. |
| **Backend** (incluye database y security de servidor) | Plugin `plugins/backend/` | ✅ 18 skills (17 especialistas + el orquestador `audit`). Probado sobre proyectos reales. Absorbe los antiguos `02_backend`, `03_database` y `04_security` (la parte de cliente está en `frontend:security`). |
| **Fullstack** (entre capas) | Plugin `plugins/fullstack/` | ✅ 5 skills (`contracts`, `topology`, `flow-diagnosis`, el orquestador de construcción `feature` y el orquestador `audit`, que combina las auditorías de frontend y backend), más el estándar de handoffs y el contexto compartido `.sdlc/context.md`. Requiere los plugins `frontend` y `backend`. |
| **QA** (calidad en todo el SDLC) | Plugin `plugins/qa/` | ✅ 9 skills: `test-strategy`, `test-design`, `exploratory-testing`, `e2e`, `quality-gates`, `load-testing`, `dast`, `defect-analysis` (con Ishikawa, Pareto y matriz Kaizen) y el orquestador `audit` (madurez de QA 0–100 por pilares). Sustituye a `05_qa_testing_engineering`. |
| **Producto y requisitos** (antes de construir) | Plugin `plugins/product/` | 🚧 Ola 1 de 4: `discovery`, `elicitation` y `domain-modeling`, con IDs estables y enlaces para la trazabilidad. Pendientes: `user-stories`, `prioritization`, `specification`, `traceability`, `inception` y `audit`. |

Catálogos: [`plugins/frontend/README.md`](plugins/frontend/README.md) · [`plugins/backend/README.md`](plugins/backend/README.md) · [`plugins/fullstack/README.md`](plugins/fullstack/README.md) · [`plugins/qa/README.md`](plugins/qa/README.md) · [`plugins/product/README.md`](plugins/product/README.md).

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
│   ├── fullstack/                # requiere frontend y backend
│   │   ├── .claude-plugin/plugin.json
│   │   ├── standards/
│   │   └── skills/
│   │       ├── contracts/
│   │       ├── topology/
│   │       ├── flow-diagnosis/
│   │       ├── feature/              # orquestador de construcción
│   │       └── audit/                # orquestador conjunto
│   ├── qa/                       # calidad en todo el SDLC
│   │   ├── .claude-plugin/plugin.json
│   │   ├── standards/
│   │   └── skills/
│   │       ├── test-strategy/
│   │       ├── test-design/
│   │       ├── exploratory-testing/
│   │       ├── e2e/
│   │       ├── quality-gates/
│   │       ├── load-testing/
│   │       ├── dast/
│   │       ├── defect-analysis/
│   │       └── audit/                # orquestador con madurez por pilares
│   └── product/                  # producto y requisitos, antes de construir (en construcción)
│       ├── .claude-plugin/plugin.json
│       ├── standards/            # incluye ids-and-links.md: IDs estables y enlaces
│       └── skills/
│           ├── discovery/
│           ├── elicitation/
│           └── domain-modeling/
│
└── guides/                       # guía de invocación: qué skill usar según el síntoma
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
/plugin install qa@sdlc-skills
/plugin install product@sdlc-skills
```

Instala solo los plugins de los dominios que use cada proyecto (cada plugin añade sus descripciones al contexto de la sesión).

Después:

```text
/frontend:forms audita los formularios de src/features/checkout
/backend:data-access revisa las condiciones de carrera en src/modules/inventory
/qa:audit ¿está listo el release 2.0?
/product:discovery tengo una idea: una app para gestionar nóminas en despachos pequeños
```

Las skills también se activan automáticamente cuando la petición encaja con su descripción.

### Con otras herramientas (Gemini, Cursor…)

Copia `plugins/<dominio>/` dentro del proyecto (p. ej. en `.sdlc-skills/`, excluido de git) con un `INDEX.md` que mapee `<plugin>:<skill>` a su `SKILL.md`, y pide: «Lee .sdlc-skills/INDEX.md y aplica qa:test-strategy en modo Auditar». Las skills son Markdown: cualquier agente que lea archivos puede seguirlas.

Guía detallada de cada skill: [`guides/HOW_TO_INVOKE.md`](guides/HOW_TO_INVOKE.md).

---

## ⚖️ Licencia
MIT License.
