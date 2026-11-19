# Plugin `qa`

Skills de **calidad a lo largo del SDLC**: lo que no es escribir los tests de una capa (eso lo hacen `frontend:testing` y `backend:testing`), sino decidir qué probar según el riesgo, diseñar los casos que encuentran defectos, explorar lo que nadie automatizó, las pruebas contra el sistema en marcha (E2E, carga, seguridad dinámica) y el proceso (puertas de calidad, análisis de defectos), con un orquestador que mide la madurez de QA.

- Modos **Construir** y **Auditar**, como el resto del kit.
- Las skills de proceso no tienen notas por stack; las que dependen de una herramienta tienen notas por herramienta (`playwright.md`, `k6.md`, `zap.md`…), no por lenguaje.
- Comparte escala, formatos, handoffs y contexto compartido en [`standards/`](standards/) (códigos `QA-*`).
- Trabaja con los otros plugins mediante handoffs (`frontend:testing`, `backend:testing`, `fullstack:flow-diagnosis`…); si alguno no está instalado, el handoff queda como pendiente.

## Uso

```bash
/plugin marketplace add <ruta-o-repo-de-este-kit>
/plugin install qa@sdlc-skills
```

```text
/qa:test-strategy prepara el plan de pruebas del release 2.0
/qa:test-design casos para la regla de descuentos de src/billing/discounts.ts
/qa:exploratory-testing explora el checkout en staging antes del release
/qa:e2e crea la suite E2E del login y el checkout con Playwright
/qa:quality-gates revisa por qué el pipeline de PR tarda 35 minutos
/qa:load-testing prueba de carga del checkout en staging antes de la campaña
/qa:dast añade un baseline de ZAP contra el preview de cada PR
/qa:defect-analysis analiza por qué vuelven los bugs del checkout este trimestre
/qa:audit ¿cómo estamos de calidad? quiero una línea base
```

## Catálogo

| Skill | Estado | Cubre |
| :--- | :---: | :--- |
| `test-strategy` | ✅ | Mapa de riesgos (impacto × probabilidad × detección), forma de la cobertura, automatizar / explorar / vigilar, definición de terminado, criterios de salida, trazabilidad y plan de release |
| `test-design` | ✅ | Particiones, valores límite, tablas de decisión, transiciones de estado, pairwise, negativos, property-based testing y Gherkin |
| `exploratory-testing` | ✅ | Charters, heurísticas, notas de sesión, reportes de bug reproducibles, severidad frente a prioridad; ejecutable por un agente con navegador |
| `e2e` | ✅ | Qué merece E2E, fixtures y page objects ligeros, localizadores por rol, datos propios por test, sesión reutilizada, red, entornos, intermitencia, smoke tras desplegar, visual y axe (notas `playwright.md`, `cypress.md`) |
| `quality-gates` | ✅ | Etapas (PR, merge, nocturno, release, tras desplegar), presupuestos de tiempo, tests afectados, sharding, cuarentena con caducidad, cobertura del diff y mutación, informes, entornos efímeros, protección de ramas (notas `github-actions.md`, `gitlab-ci.md`) |
| `load-testing` | ✅ | Tipos de prueba, modelo abierto o cerrado, escenarios con mezcla real y datos parametrizados, umbrales desde los SLO, entorno autorizado, observación e interpretación, smoke en CI (notas `k6.md`, `locust.md`, `gatling.md`) |
| `dast` | ✅ | Autorización y alcance escritos, baseline / completo / API, escaneo autenticado, reglas y supresiones justificadas, CI, criba y verificación, relación con SAST/SCA (nota `zap.md`) |
| `defect-analysis` | ✅ | Defectos escapados y regresiones: clasificación y motivo de escape, hotspots, 5 porqués, Ishikawa en Mermaid (5 ramas), Pareto 80/20, matriz Kaizen (Quick Win, Táctico, Estratégico con dificultad, plazo, impacto y KPI), criterios de cierre y métricas |
| `audit` | ✅ | Orquestador: 6 rutas, aplicabilidad por contexto, madurez de QA 0–100 por 5 pilares con nivel, dictamen y remediación por lotes |

## Estructura de una skill

```text
skills/<skill>/
├── SKILL.md              # cuándo usarla, modos, flujo, principios y handoffs
└── references/
    ├── patterns.md       # técnicas, plantillas y anti-patrones
    └── checklist.md      # checklist de auditoría con severidad orientativa
```
