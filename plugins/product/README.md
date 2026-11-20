# Plugin `product`

Skills de **producto y requisitos**: lo que se hace antes de crear software y lo que mantiene alineado lo que se construye con lo que se necesita. Validar la idea, levantar requisitos con quien tiene el problema, fijar el lenguaje y las reglas del negocio y, en las próximas olas, escribir historias con criterios de aceptación, priorizar, especificar (SRS o PRD) y trazar cada requisito hasta el código y los tests.

- Modos **Construir** y **Auditar**, como el resto del kit. El modo Auditar sirve también para revisar la documentación funcional de un proyecto existente.
- Sin notas por stack: las plantillas son por formato (brief y Lean Canvas, guion de entrevista, reglas de negocio…). Todo se entrega en Markdown dentro del repositorio, con diagramas Mermaid.
- **IDs estables y enlaces** comunes a todas las skills ([`standards/ids-and-links.md`](standards/ids-and-links.md)): `OBJ`, `SUP`, `INT`, `PRE`, `DEC`, `RN`, `HU`, `CA`, `RF`, `RNF`. Si el proyecto ya tiene su convención, se respeta.
- **No inventa datos de negocio:** pregunta lo que bloquea y marca el resto como supuesto o pregunta abierta.
- Comparte escala, formatos, handoffs y contexto en [`standards/`](standards/) (códigos `PR-*`). Entrega el relevo a `fullstack:feature`, `qa:test-design`, `backend:domain-logic` y otros mediante handoffs.

## Uso

```bash
/plugin marketplace add <ruta-o-repo-de-este-kit>
/plugin install product@sdlc-skills
```

```text
/product:discovery tengo una idea: una app para que los despachos contables gestionen nóminas
/product:elicitation entrevístame para levantar los requisitos del módulo de facturación
/product:elicitation documenta los requisitos del sistema actual a partir del código de src/billing
/product:domain-modeling glosario, modelo y reglas de negocio del módulo de pedidos
/product:domain-modeling audita docs/modules/*/reglas_negocio.md
```

## Catálogo

| Skill | Estado | Cubre |
| :--- | :---: | :--- |
| `discovery` | ✅ | Problema y evidencia, segmentos y trabajos por hacer, propuesta de valor, Lean Canvas (o versión interna), supuestos de mayor riesgo con experimento, alcance del MVP, objetivos y métricas |
| `elicitation` | ✅ | Mapa de interesados, técnicas, guion de entrevista, entrevista al usuario en el chat por bloques, análisis del sistema existente, registros de preguntas, supuestos y decisiones, conflictos |
| `domain-modeling` | ✅ | Glosario, modelo conceptual, ciclo de vida y estados, eventos y módulos, catálogo de reglas de negocio atómicas con ejemplos, motivo, origen y enlaces |
| `user-stories` | ⏳ Ola 2 | Épicas, story mapping, historias INVEST, división vertical, criterios de aceptación, casos de uso, Definition of Ready |
| `prioritization` | ⏳ Ola 2 | MoSCoW, RICE, Kano, coste del retraso, corte del MVP y plan de releases |
| `specification` | ⏳ Ola 3 | SRS (IEEE 29148) o PRD, requisitos no funcionales medibles (ISO 25010), restricciones e interfaces |
| `traceability` | ⏳ Ola 3 | Matriz RN ↔ HU ↔ CA ↔ código ↔ tests ↔ commits, huecos, enlaces rotos y análisis de impacto |
| `inception` | ⏳ Ola 4 | Orquestador de construcción: de la idea a un backlog o SRS listo para `fullstack:feature` |
| `audit` | ⏳ Ola 4 | Orquestador de auditoría de la calidad de los requisitos, con puntuación |

## Estructura de una skill

```text
skills/<skill>/
├── SKILL.md              # cuándo usarla, modos, flujo, principios y handoffs
└── references/
    ├── patterns.md       # técnicas, ejemplos y anti-patrones
    ├── <plantilla>.md    # brief, guion de entrevista, regla de negocio…
    └── checklist.md      # checklist de auditoría con severidad orientativa
```
