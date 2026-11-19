# Plugin `qa`

Skills de **calidad a lo largo del SDLC**: lo que no es escribir los tests de una capa (eso lo hacen `frontend:testing` y `backend:testing`), sino decidir qué probar según el riesgo, diseñar los casos que encuentran defectos, explorar lo que nadie automatizó y, en las próximas olas, las pruebas contra el sistema en marcha (E2E, carga, seguridad dinámica) y el proceso (puertas de calidad, análisis de defectos).

- Modos **Construir** y **Auditar**, como el resto del kit.
- Las skills de proceso no tienen notas por stack; las que dependen de una herramienta tendrán notas por herramienta (`playwright.md`, `k6.md`, `zap.md`…), no por lenguaje.
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
```

## Catálogo

| Skill | Estado | Cubre |
| :--- | :---: | :--- |
| `test-strategy` | ✅ | Mapa de riesgos (impacto × probabilidad × detección), forma de la cobertura, automatizar / explorar / vigilar, definición de terminado, criterios de salida, trazabilidad y plan de release |
| `test-design` | ✅ | Particiones, valores límite, tablas de decisión, transiciones de estado, pairwise, negativos, property-based testing y Gherkin |
| `exploratory-testing` | ✅ | Charters, heurísticas, notas de sesión, reportes de bug reproducibles, severidad frente a prioridad; ejecutable por un agente con navegador |
| `e2e` | ⏳ Ola 2 | Arquitectura de suites E2E con Playwright o Cypress |
| `quality-gates` | ⏳ Ola 2 | Qué corre en cada etapa de CI, tests intermitentes, informes, umbrales |
| `load-testing` | ⏳ Ola 3 | Pruebas de carga con k6, Locust o Gatling |
| `dast` | ⏳ Ola 3 | Seguridad dinámica con OWASP ZAP |
| `defect-analysis` | ⏳ Ola 4 | Defectos escapados y regresiones: hotspots, Ishikawa, Pareto y matriz Kaizen |
| `audit` | ⏳ Ola 4 | Orquestador con madurez de QA 0–100 |

## Estructura de una skill

```text
skills/<skill>/
├── SKILL.md              # cuándo usarla, modos, flujo, principios y handoffs
└── references/
    ├── patterns.md       # técnicas, plantillas y anti-patrones
    └── checklist.md      # checklist de auditoría con severidad orientativa
```
