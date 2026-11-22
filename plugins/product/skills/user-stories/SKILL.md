---
name: user-stories
description: "Construye y audita épicas, mapas de historias, historias de usuario, criterios de aceptación y casos de uso a partir de objetivos, requisitos y reglas de negocio. Divide el trabajo en incrementos utilizables y verifica la Definition of Ready antes de pasar a desarrollo. Úsala para convertir un brief o levantamiento en backlog, refinar historias existentes o revisar su cobertura."
---

# Historias de usuario

## Cuándo usarla

- Convertir requisitos y reglas en incrementos comprobables.
- Refinar historias demasiado grandes o revisar un backlog existente.
- Documentar un caso de uso cuando hay flujos alternativos o varios actores.

## Paso 0

1. Delimita objetivo, módulo, actores y alcance acordado. Lee el brief, las decisiones, los requisitos, las reglas y el backlog existentes según aplique. Conserva `PRE` y `SUP` abiertos con su origen.
2. Carga los estándares de [IDs y enlaces](../../standards/ids-and-links.md), [formatos](../../standards/output-formats.md), [contexto](../../standards/context.md) y [handoffs](../../standards/handoffs.md). Si existe `.sdlc/context.md`, léelo. Busca IDs previos también en notas de sesión y respeta las convenciones del proyecto.

## Modo Construir

1. Agrupa el trabajo por resultado y, cuando ayude a entender el recorrido, dibuja un mapa de actividades, tareas y cortes de entrega. Crea épicas `EP` solo si agrupar historias aporta claridad.
2. Redacta historias `HU` con actor, capacidad y beneficio. Divide por incrementos que se puedan usar y comprobar de extremo a extremo. Explicita las dependencias inevitables.
3. Añade criterios `CA` observables para el flujo principal y las alternativas, fallos o límites que cambien el resultado. Cita las reglas y decisiones aplicadas. Si el flujo merece un caso de uso `CU`, enlázalo con sus historias y criterios.
4. Evalúa la Definition of Ready de [patterns.md](references/patterns.md). Para cada dependencia necesaria, identifica qué parte requiere la historia y verifica su estado con evidencia, incluidas las dependencias que impiden entregar el recorrido. Criterios pendientes de negocio quedan en borrador con su `PRE` o `SUP`. Si la historia está definida pero su dependencia sigue bloqueada, conserva el estado documental y marca la preparación como `bloqueada`. Evalúa un corte menor solo si tiene valor verificable y mantiene las salvaguardas del recorrido.
5. Usa [backlog-template.md](references/backlog-template.md) en el backlog existente o en `docs/product/backlog/`. Añade enlaces de vuelta cuando ambos artefactos estén en el repositorio y dentro del alcance. Comprueba unicidad, anclas, estados y fuentes. Actualiza el contexto y registra qué historias están listas y cuáles siguen pendientes.

## Modo Auditar

1. Revisa las historias frente a los objetivos, reglas y decisiones vigentes. Usa el [checklist](references/checklist.md) para detectar criterios ambiguos, rutas sin cobertura, dependencias ocultas y declaraciones de preparación sin evidencia.
2. Reporta por historia o criterio según [severidad](../../standards/severity.md) y [formatos](../../standards/output-formats.md) con código `PR-STORIES`. Registra y verifica el contexto según su estándar.

## Handoffs

| Disparador | Destino | Alcance |
| :--- | :--- | :--- |
| Una ambigüedad de negocio bloquea una historia | `elicitation` o `domain-modeling` | `HU`, `PRE` y regla afectada |
| Hay historias comparables y hace falta decidir orden o corte | `prioritization` | IDs, objetivos, dependencias, preparación y estimaciones disponibles |
| Una historia lista cruza capas y sus dependencias quedaron verificadas | `fullstack:feature` | `HU` lista, criterios acordados, reglas, restricciones y dependencias disponibles o incluidas en el mismo incremento listo |
| Hay criterios o reglas acordados que requieren casos de prueba | `qa:test-design` | `CA`, `RN`, límites y excepciones |
| Se detectan enlaces rotos o cobertura transversal incompleta | `traceability` | IDs y evidencia de la brecha |

## Referencias

- [patterns.md](references/patterns.md) en ambos modos.
- [backlog-template.md](references/backlog-template.md) en Construir.
- [checklist.md](references/checklist.md) en Auditar.
