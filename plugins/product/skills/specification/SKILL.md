---
name: specification
description: "Construye y audita especificaciones de producto o de requisitos de software (PRD o SRS). Convierte objetivos, decisiones, reglas, historias y restricciones en requisitos funcionales y no funcionales verificables, con interfaces, fuentes y estados. Úsala para formalizar un alcance o revisar si una especificación puede guiar la implementación y las pruebas."
---

# Especificación de requisitos

## Cuándo usarla

- Formalizar un alcance acordado o redactar un borrador con decisiones pendientes.
- Definir requisitos no funcionales que puedan medirse.
- Revisar una especificación existente, sus restricciones y sus interfaces.

## Paso 0

1. Delimita el producto o módulo, el alcance solicitado y la persona que puede aprobarlo. Lee las fuentes pertinentes: brief, entrevistas, reglas, historias, corte de MVP y contratos existentes. Distingue objetivos del producto, comportamiento observado, decisiones aprobadas y propuestas.
2. Lee [IDs y enlaces](../../standards/ids-and-links.md), [formatos](../../standards/output-formats.md), [contexto](../../standards/context.md) y [handoffs](../../standards/handoffs.md). Respeta la estructura existente y busca las definiciones de IDs que vas a asignar, incluidas las notas de sesión. Lee `.sdlc/context.md` si existe.

## Modo Construir

1. Elige PRD si la decisión es de producto, usuarios, resultado o alcance. Elige SRS si el equipo necesita un contrato verificable de comportamiento, calidad, restricciones e interfaces. Sigue el formato existente si cubre la necesidad. Usa [patterns.md](references/patterns.md).
2. Declara alcance dentro y fuera, actores, dependencias, restricciones y estado del documento. Si el corte sigue propuesto o bloqueado, mantenlo así. Separa lo que se puede especificar con evidencia de lo que requiere decisión.
3. Redacta cada `RF` con condición y resultado verificable. Cita `RN`, `HU`, `CA`, `DEC` u otra fuente aplicable. Conserva en borrador una condición o efecto pendiente y enlaza el `PRE` o `SUP` que lo bloquea. Separa el borrador de la parte acordada cuando sean verificables por separado.
4. Para cada `RNF`, registra escenario, métrica, umbral, condiciones de medición y cómo se verificará. Si el umbral, la carga o el entorno están pendientes, identifícalos como tales sin inventarlos. Distingue restricciones aprobadas de opciones de diseño. Para cada interfaz relevante, cita el contrato vigente o registra qué está por definir.
5. Entrega según [specification-template.md](references/specification-template.md) en la ubicación existente o en `docs/product/especificacion/`. Verifica IDs, enlaces y evidencias de estado. Con «no toques el código», guarda la especificación y verifica su registro en el contexto existente según el estándar.
6. Antes de cerrar, revisa los requisitos que nombran una tecnología, algoritmo o técnica de implementación. Conserva ese detalle como restricción acordada solo si una fuente vigente lo exige de forma explícita. Si solo hay un precedente en el código, muévelo a una referencia de diseño y formula el requisito y su verificación en términos del resultado esperado.

## Modo Auditar

1. Contrasta la especificación con sus fuentes vigentes y recorre el [checklist](references/checklist.md). Revisa alcance, contradicciones, requisitos verificables, métricas, interfaces y dependencias.
2. Registra hallazgos según [severidad](../../standards/severity.md) y [formatos](../../standards/output-formats.md) con código `PR-SPEC`. Indica lo que queda por verificar y actualiza el contexto según su estándar.

## Handoffs

| Disparador | Destino | Alcance |
| :--- | :--- | :--- |
| Falta una decisión o una medición para acordar un requisito | `elicitation` o `discovery` | `RF` o `RNF`, fuente y `PRE` o `SUP` |
| Hay discrepancias entre interfaces o falta concretar un contrato entre capas | `fullstack:contracts` | Requisito, interfaz y evidencia del desajuste |
| Se necesitan escenarios para verificar requisitos acordados | `qa:test-design` | Requisitos, criterios, límites y método de verificación |
| Se necesita comprobar cobertura o impacto entre artefactos | `traceability` | IDs, fuentes y alcance de la revisión |

## Referencias

- [patterns.md](references/patterns.md) en ambos modos.
- [specification-template.md](references/specification-template.md) en Construir.
- [checklist.md](references/checklist.md) en Auditar.
