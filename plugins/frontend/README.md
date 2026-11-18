# Plugin `frontend`

Skills para diseñar, construir y auditar aplicaciones frontend en **Vue, React y Angular**. Cada skill:

- Tiene dos modos: **Construir** (crear o refactorizar) y **Auditar** (revisar código existente y emitir un informe con severidades).
- Detecta el stack del proyecto y carga solo las notas del framework correspondiente.
- Comparte la escala de severidad, el formato de informe y la matriz de viewports de [`standards/`](standards/).
- `ux-review` y `responsive-layout` no llevan notas por framework (evalúan la interfaz y el CSS); las demás incluyen `vue.md`, `react.md` y `angular.md`.

## Uso

```bash
/plugin marketplace add <ruta-o-repo-de-este-kit>
/plugin install frontend@sdlc-skills
```

Invocación explícita: `/frontend:<skill> <qué quieres hacer>`, por ejemplo:

```text
/frontend:forms audita los formularios de src/features/checkout
/frontend:data-fetching monta el cliente HTTP con refresh token y TanStack Query
```

Claude también las activa solo cuando la petición encaja con la descripción de la skill.

## Catálogo

| Skill | Estado | Cubre |
| :--- | :---: | :--- |
| `architecture` | ✅ | Estructura por features, límites y dependencias, API pública por feature, monorepo, ADRs |
| `typescript` | ✅ | tsconfig estricto, cero `any`, contratos de API tipados y validados, uniones discriminadas, tipado de componentes |
| `data-fetching` | ✅ | Cliente HTTP, interceptores, refresh token, errores, cancelación, server state (TanStack Query), tiempo real |
| `state-management` | ✅ | Clasificación del estado, stores, derivados, fugas de memoria, reactividad, re-renders, SSR |
| `forms` | ✅ | Schemas, momento de validación, envío e idempotencia, errores del servidor, wizards, listas dinámicas, archivos |
| `ux-review` | ✅ | Crítica UI/UX sin código y diseño de la UX de pantallas nuevas: jerarquía, densidad, coherencia, responsive percibido, estados, flujos, Antes/Después |
| `design-system` | ✅ | Tokens en tres niveles, temas claro/oscuro, componentes base, variantes (CVA), matriz de estados, resiliencia de layout |
| `accessibility` | ✅ | WCAG 2.2 AA: teclado y foco, ARIA (patrones APG), lectores de pantalla, contraste, pruebas automáticas y manuales |
| `responsive-layout` | ✅ | Correcciones de layout sin rediseñar en 13 viewports, jerarquía de intervención de 5 niveles |
| `performance` | 🔜 ola 3 | Core Web Vitals, bundle, imágenes, fuentes |
| `rendering-and-seo` | 🔜 ola 3 | CSR/SSR/SSG, hidratación, metadatos |
| `routing` | 🔜 ola 3 | Guards, lazy routes, estado en la URL |
| `security` | 🔜 ola 3 | XSS, tokens, CSP, dependencias |
| `testing` | 🔜 ola 3 | Tests de componentes, MSW, regresión visual |
| `observability` | 🔜 ola 4 | Error boundaries, Sentry, RUM |
| `i18n` / `tooling` | 🔜 ola 4 | Traducciones; Vite, entorno, lint |
| `audit` | 🔜 ola 4 | Orquestador: diagnostica, elige skills y consolida (migración de `00_frontend_director`) |

## Estructura de una skill

```text
skills/<skill>/
├── SKILL.md              # cuándo usarla, modos, flujo y principios
└── references/
    ├── patterns.md       # patrones de construcción y anti-patrones
    ├── checklist.md      # checklist de auditoría con severidad orientativa
    ├── vue.md
    ├── react.md
    └── angular.md
```
