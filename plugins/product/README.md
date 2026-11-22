# Plugin `product`

Skills de **producto y requisitos** para validar ideas, levantar requisitos, modelar reglas de negocio, redactar historias, priorizar entregas, formalizar especificaciones y comprobar la trazabilidad. Dos orquestadores coordinan la preparación del trabajo y la auditoría de requisitos.

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
/product:user-stories convierte las reglas acordadas del buzón en historias con criterios verificables
/product:prioritization propone el corte del MVP a partir del backlog del buzón
/product:specification redacta una SRS de la caducidad de notas a partir de reglas, historias y decisiones
/product:traceability verifica la cobertura de las reglas del buzón en historias, código y pruebas
/product:inception prepara un incremento de caducidad a partir de los documentos existentes del buzón
/product:audit evalúa si los requisitos de caducidad están listos para desarrollo
```

## Estado de las olas

- **Ola 1 cerrada.** Probada en VELTRIX con Gemini 4 Hydrogen Medium. Incluyó descubrimiento en Construir, levantamiento en Construir y modelado en Auditar y Construir. Se verificaron escritura del contexto, preguntas abiertas, reglas en borrador, unicidad de IDs y métricas sin línea base. La revisión de anclas de `0.1.4` se verificó en el brief generado.
- **Ola 2 cerrada.** Se probó en VELTRIX con Gemini 4 Hydrogen Medium usando las reglas de caducidad de la ola 1. Se verificaron las historias y sus criterios, el registro de la propuesta y del contexto, y el bloqueo del relevo a desarrollo cuando el corte contradice reglas acordadas. La prueba cubrió el modo Construir de ambas skills.
- **Ola 3 cerrada.** Se probaron `specification` y `traceability` en modo Construir con Gemini 4 Hydrogen Medium en VELTRIX. Se verificaron la separación entre requisitos y técnicas de implementación, la cobertura respaldada por evidencia, el análisis de impacto y la consistencia del contexto en la repetición.
- **Ola 4 cerrada.** Se probaron `inception` en Construir y `audit` en Auditar con Gemini 4 Hydrogen Medium en VELTRIX. `inception` reutilizó los artefactos existentes y registró el bloqueo del relevo a desarrollo. Con `0.4.1`, la repetición de `audit` obtuvo 93/100 (26 de 28 puntos, con los 14 criterios aplicables evaluados), justificó los dos puntos descontados y mantuvo bloqueado el incremento. Los hallazgos quedaron registrados en el contexto del proyecto y los documentos auditados se conservaron intactos.

## Catálogo

| Skill | Estado | Cubre |
| :--- | :---: | :--- |
| `discovery` | ✅ | Problema y evidencia, segmentos y trabajos por hacer, propuesta de valor, Lean Canvas (o versión interna), supuestos de mayor riesgo con experimento, alcance del MVP, objetivos y métricas |
| `elicitation` | ✅ | Mapa de interesados, técnicas, guion de entrevista, entrevista al usuario en el chat por bloques, análisis del sistema existente, registros de preguntas, supuestos y decisiones, conflictos |
| `domain-modeling` | ✅ | Glosario, modelo conceptual, ciclo de vida y estados, eventos y módulos, catálogo de reglas de negocio atómicas con ejemplos, motivo, origen y enlaces |
| `user-stories` | Ola 2 · probada en Construir | Épicas, story mapping, historias INVEST, división vertical, criterios de aceptación, casos de uso, Definition of Ready |
| `prioritization` | Ola 2 · probada en Construir | MoSCoW, RICE, Kano, coste del retraso, corte del MVP y plan de entregas |
| `specification` | Ola 3 · probada en Construir | PRD o SRS, requisitos funcionales y no funcionales verificables, restricciones e interfaces |
| `traceability` | Ola 3 · probada en Construir | Matriz de requisitos y reglas a historias, criterios, código, pruebas y commits, con brechas y análisis de impacto |
| `inception` | Ola 4 · probada en Construir | Orquestador que prepara un backlog o especificación y verifica si el incremento puede pasar a `fullstack:feature` |
| `audit` | Ola 4 · probada en Auditar | Orquestador que audita calidad de requisitos con puntuación, cobertura y remediación |

## Estructura de una skill

```text
skills/<skill>/
├── SKILL.md              # cuándo usarla, modos, flujo, principios y handoffs
└── references/
    ├── patterns.md       # técnicas, ejemplos y anti-patrones
    ├── <plantilla>.md    # brief, guion de entrevista, regla de negocio…
    └── checklist.md      # checklist de auditoría con severidad orientativa
```
