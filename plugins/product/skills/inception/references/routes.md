# Rutas de inception

La inspección inicial permite empezar en la primera etapa con una brecha que afecte al encargo. El orden expresa dependencias entre entregables y admite iteración cuando aparecen preguntas nuevas. Registra una comprobación parcial cuando solo hayas inspeccionado parte de un artefacto.

| Etapa | Skill | Qué permite avanzar |
| :--- | :--- | :--- |
| Problema y valor | `discovery` | Objetivo, usuarios, evidencia del problema y supuestos pendientes. |
| Necesidades e interesados | `elicitation` | Requisitos candidatos, origen, decisiones y preguntas. |
| Reglas y estados | `domain-modeling` | Reglas y excepciones comprobables, glosario y ciclo de vida si aplica. |
| Historias y aceptación | `user-stories` | Historias con criterios, fuente, dependencias y preparación. |
| Corte y orden | `prioritization` | Corte propuesto o aprobado, dependencias y alcance ejecutable. |
| Especificación | `specification` | PRD o SRS si el encargo lo requiere, con requisitos y estados verificables. |
| Cobertura de vínculos | `traceability` | Matriz o comprobación acotada cuando hacen falta vínculos transversales o análisis de impacto. |

- **Desde una idea:** comienza por problema y valor. Completa el levantamiento y las reglas relevantes antes de definir el corte. Una propuesta de backlog sigue siendo útil si la aprobación queda pendiente.
- **Desde documentación existente:** verifica estado y vigencia de sus fuentes. Por ejemplo, desde un catálogo de reglas acordadas puedes pasar directamente a historias. Desde un backlog con discrepancias empieza por la etapa que pueda resolverlas.
- **Desde una SRS o un corte:** comprueba las condiciones del relevo antes de ampliar alcance. Si el usuario solo necesita saber qué falta, entrega la evaluación y los pendientes.
- Coordina cada etapa una vez en el plan. Si surge nueva evidencia, actualiza la etapa afectada y sus referencias sin repetir lecturas vigentes.

## Condiciones del relevo

Todas deben cumplirse para calificar un incremento como listo para desarrollo:

1. El decisor aprobó el corte concreto y hay una fuente que lo acredita.
2. Las historias o requisitos del incremento tienen criterios verificables y fuentes acordadas. El alcance conserva las reglas vigentes o cita las excepciones aprobadas.
3. Las dependencias necesarias están disponibles o incluidas en el mismo incremento con orden viable y evidencia.
4. Ningún `PRE`, `SUP`, requisito en borrador o discrepancia abierta cambia la implementación de ese incremento. Las dudas ajenas al incremento siguen registradas.
5. El resultado conserva las salvaguardas necesarias y define cómo verificar el recorrido de extremo a extremo.

Por ejemplo, si un backlog llama listo al selector y la priorización encuentra que su corte incumple una regla de recálculo acordada, registra la discrepancia. El relevo queda bloqueado hasta ajustar el corte o contar con una excepción aprobada.
