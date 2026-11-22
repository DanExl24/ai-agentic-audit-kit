# Rúbrica de calidad de requisitos

Cada fila tiene dos criterios de igual valor. Define la etapa y la aplicabilidad antes de asignar puntos. Si un criterio es indispensable para el objetivo actual, aplica aunque el documento que debería sustentarlo todavía no exista. Si la etapa o el encargo deja el criterio fuera, marca N/A con su motivo.

| Pilar / skill | Criterio A | Criterio B |
| :--- | :--- | :--- |
| Problema y valor / `discovery` | Problema, actores y alternativa actual respaldados por evidencia. | Objetivos, hipótesis y medición proporcionales a la etapa. |
| Levantamiento / `elicitation` | Requisitos con origen e interlocutor identificado. | Decisiones, conflictos y preguntas abiertos con estado y responsable. |
| Modelo / `domain-modeling` | Términos y estados coherentes con el dominio. | Reglas verificables con origen, guardas y excepciones. |
| Historias / `user-stories` | Historias de valor con fuentes y criterios comprobables. | Dependencias y preparación comprobadas, con borradores fuera del alcance ejecutable. |
| Corte / `prioritization` | Prioridad y orden explicados con evidencia. | Corte coherente con reglas, dependencias, aprobación y estado ejecutable. |
| Especificación / `specification` | Alcance y requisitos verificables con estados y fuentes. | Condiciones de calidad, restricciones e interfaces medibles o identificadas como pendientes. |
| Trazabilidad / `traceability` | Vínculos válidos entre requisitos, reglas, historias y criterios. | Evidencia de cobertura o impacto cuando el objetivo lo pide, distinguida del trabajo previsto. |

## Cálculo

- **2:** cumple con evidencia suficiente. **1:** cumple en parte con evidencia de lo comprobado y de la brecha. **0:** la evidencia confirma el incumplimiento o la ausencia de un artefacto esperado. **Por verificar:** no hay elementos suficientes para juzgar. **N/A:** excluido por etapa o alcance con motivo.
- Sea **N** el total de criterios aplicables, **S** la suma de puntos comprobados y **U** los criterios aplicables por verificar. Cobertura = `100 × (N − U) / N`.
- Si `U = 0`, puntuación = `100 × S / (2 × N)`. Si `U > 0`, intervalo provisional = `[100 × S / (2 × N), 100 × (S + 2 × U) / (2 × N)]`. Redondea al entero más cercano al final de cada cálculo. Para un pilar, usa sus propios N, S y U. Si `N = 0`, informa sin puntuación.
- Ejemplo: 5 criterios aplicables, 6 puntos comprobados y 1 criterio por verificar dan 80 % de cobertura e intervalo de 60–80. Un criterio ausente con evidencia vale 0 y sí cuenta como examinado.
- Una puntuación orienta las prioridades de remediación. El veredicto sobre pasar a desarrollo se determina con la evidencia de aprobación, dependencias y reglas aplicables. Conserva los bloqueos explícitos incluso si el resto obtiene una puntuación alta.
