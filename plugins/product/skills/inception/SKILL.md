---
name: inception
description: "Orquesta Producto desde una idea o documentación parcial hasta un backlog o PRD/SRS listo para revisión o desarrollo. Reutiliza descubrimiento, levantamiento, modelado, historias, priorización, especificación y trazabilidad según los vacíos del proyecto. Declara los bloqueos y prepara el relevo a fullstack:feature cuando haya un incremento ejecutable."
---

# Incepción de producto

## Cuándo usarla

- Llevar una idea nueva a una decisión sobre qué construir.
- Completar documentación previa a desarrollo a partir de un brief, reglas o backlog existentes.
- Preparar un relevo trazable para construir un incremento aprobado.

## Paso 0

1. Define objetivo, módulo, decisor y entregable final. Si el usuario no elige formato, usa un backlog para un incremento pequeño y una SRS o PRD cuando el alcance o las interfaces requieran mayor detalle.
2. Lee [IDs y enlaces](../../standards/ids-and-links.md), [formatos](../../standards/output-formats.md), [contexto](../../standards/context.md) y [handoffs](../../standards/handoffs.md). Si existe `.sdlc/context.md`, úsalo para localizar evidencia y decisiones. Comprueba en los documentos fuente que las referencias y sus estados siguen vigentes.
3. Inspecciona las entradas usando [routes.md](references/routes.md). Presenta un plan breve con etapas, entregables reutilizados y preguntas que bloquean. Reutiliza un artefacto vigente si satisface la etapa. Una ruta puede empezar en distintos puntos.

## Modo Construir

1. Ejecuta solo las etapas necesarias del plan. Para cada skill seleccionada, carga su `SKILL.md` y las referencias del modo Construir que apliquen. Pásale el alcance, los IDs y decisiones relevantes. Si falta una skill o una fuente, registra el motivo y completa las etapas independientes.
2. Respeta el intercambio de [elicitation](../elicitation/SKILL.md) cuando haya entrevista. Espera cada respuesta y confirmación. Si falta una decisión, continúa solo con trabajo que pueda quedar como propuesta o borrador trazable.
3. Usa las salidas verificadas de cada etapa en la siguiente. Conserva IDs y estados, y actualiza el avance en el contexto para una tarea encadenada. Si dos fuentes discrepan, registra la discrepancia y quién la resuelve. Una propuesta puede explorarse sin cambiar una decisión vigente.
4. Verifica las [condiciones del relevo](references/routes.md#condiciones-del-relevo). Completa el [resumen de entrega](references/delivery-template.md) con los documentos, preguntas, decisiones y dependencias. Deja un resultado explícito: listo para desarrollo, listo para revisión de producto o bloqueado, con evidencia.
5. Guarda los artefactos de Producto dentro del alcance y el resumen en la ubicación del proyecto o en `docs/product/inception.md`. Verifica las rutas y el contexto según su estándar. Con «no toques el código», entrega y registra los documentos de Producto. Si el encargo limita la escritura, entrega los resultados y las entradas de contexto propuestas en la respuesta.

## Handoffs

El plan coordina las skills internas. Los disparadores fuera del plan se registran como pendientes según [handoffs.md](../../standards/handoffs.md). Para `fullstack:feature`, entrega solo el incremento que cumple todas las condiciones del relevo. La ejecución de ese orquestador requiere la autorización aplicable según el estándar. Si el alcance está bloqueado o sigue en propuesta, indica qué debe resolverse antes de pasar a desarrollo.

## Referencias

- [routes.md](references/routes.md) para elegir y verificar etapas.
- [delivery-template.md](references/delivery-template.md) para cerrar el trabajo.
