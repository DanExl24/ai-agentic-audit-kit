---
name: prioritization
description: "Construye y audita la priorización de oportunidades, épicas e historias. Usa MoSCoW, RICE, Kano o coste del retraso según la decisión y la evidencia. Define el corte del MVP y un plan de entregas con dependencias, nivel de preparación y decisiones trazables."
---

# Priorización de producto

## Cuándo usarla

- Decidir qué entra en el MVP y qué se pospone.
- Ordenar un backlog según objetivos, coste o compromisos.
- Auditar puntuaciones, dependencias o el fundamento de un plan de entregas.

## Paso 0

1. Define la decisión, el responsable, el horizonte, las restricciones y los objetivos. Lee el brief, el backlog, las reglas y las decisiones existentes según aplique. Usa IDs existentes.
2. Carga [IDs y enlaces](../../standards/ids-and-links.md), [formatos](../../standards/output-formats.md), [handoffs](../../standards/handoffs.md) y [contexto](../../standards/context.md). Lee `.sdlc/context.md` si existe.

## Modo Construir

1. Elige un método según la pregunta y la evidencia disponible. Explica en una frase la elección y define escala, unidades y horizonte antes de comparar. Usa [patterns.md](references/patterns.md).
2. Para cada candidato, registra evidencia, valor, esfuerzo si se conoce, dependencias y preparación. Identifica estimaciones y datos pendientes. Si un dato requerido falta, conserva el candidato sin puntuar y explica qué información falta. Evita convertir datos desconocidos en ceros.
3. Aplica el método de forma consistente. Revisa empates y opciones sensibles a una estimación. Explica los ajustes al orden por dependencias, obligaciones o restricciones operativas. Separa la prioridad de la preparación para desarrollar. Contrasta la preparación del backlog con cada dependencia necesaria y la evidencia de que está disponible o queda incluida en el mismo incremento listo y ordenado. Registra las discrepancias con el estado del backlog.
4. Traza el corte del MVP como recorrido completo ligado a un objetivo o hipótesis. Evalúa por separado si hay un incremento útil y ejecutable que cumpla ese recorrido o entregue valor por sí mismo con sus salvaguardas. Contrasta también el comportamiento de los casos que quedan fuera con las decisiones y reglas acordadas. Si el corte solo funciona cambiando una regla acordada, descríbelo como alternativa que requiere aprobación y deja bloqueado ese alcance. Si no hay un incremento ejecutable, indícalo y registra qué lo habilitaría. Incluye capacidad o fechas solo si están respaldadas.
5. Guarda la propuesta con [priority-template.md](references/priority-template.md) en el backlog existente o en `docs/product/backlog/priorizacion.md` y registra de inmediato la ejecución, el estado de propuesta y los handoffs pendientes en el contexto existente. «No toques el código» permite ambas escrituras. Verifica que el documento y el contexto se guardaron y reporta sus rutas. Solo tras la aprobación registra el corte como acordado con su `DEC`. Si el usuario limita explícitamente la tarea a una respuesta en el chat, sigue la excepción del [estándar de contexto](../../standards/context.md).
6. **Verifica la coherencia del corte antes de cerrar.** Si el recorrido cambia una regla acordada, marca «incremento ejecutable: no» y cita la regla y la decisión pendiente. Un aviso o una salvaguarda que no preserve la regla no resuelve el bloqueo. Usa el mismo estado en el documento, el plan, el contexto y el resumen. Conserva el relevo de refinamiento y deja sin alcance ejecutable cualquier handoff previo que contradiga el bloqueo.

## Modo Auditar

1. Recalcula una muestra representativa y revisa los candidatos cercanos al corte. Contrasta supuestos, escalas, dependencias, preparación y alcance con el [checklist](references/checklist.md).
2. Usa [severidad](../../standards/severity.md) y [formatos](../../standards/output-formats.md) con código `PR-PRIOR`. Señala qué no se pudo verificar y actualiza el contexto según su estándar.

## Handoffs

| Disparador | Destino | Alcance |
| :--- | :--- | :--- |
| Una historia prioritaria requiere división o criterios | `user-stories` | `HU` o `EP`, objetivo, dependencia y pendiente |
| Una decisión depende de evidencia de uso o de una necesidad sin confirmar | `discovery` o `elicitation` | Candidatos afectados, `OBJ`, `SUP` o `PRE` |
| Hay corte acordado y un incremento ejecutable entre capas que respeta las reglas vigentes | `fullstack:feature` | Historias listas en orden, criterios acordados y evidencia de que las dependencias necesarias están disponibles o incluidas en ese incremento |

## Referencias

- [patterns.md](references/patterns.md) en ambos modos.
- [priority-template.md](references/priority-template.md) en Construir.
- [checklist.md](references/checklist.md) en Auditar.
