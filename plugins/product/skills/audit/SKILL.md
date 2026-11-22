---
name: audit
description: "Orquesta la auditoría de calidad de requisitos de Producto. Selecciona las skills aplicables a la etapa y al alcance, consolida hallazgos con evidencia y puntúa la calidad de 0 a 100. Distingue falta de cobertura, requisitos en borrador y bloqueos para desarrollo."
---

# Auditoría de requisitos

## Cuándo usarla

- Evaluar si la documentación de un producto o módulo permite tomar la siguiente decisión.
- Revisar preparación del backlog, del MVP o de la SRS cuando intervienen varias skills.
- Detectar contradicciones entre requisitos, reglas, historias y evidencias de implementación.

Para revisar una sola área, usa el checklist de su skill. Esta auditoría coordina y consolida las comprobaciones seleccionadas.

## Paso 0

1. Define el objetivo de la auditoría, el alcance y la etapa según evidencia. Lee el contexto existente y contrasta su vigencia con las fuentes. Si la petición es abierta, revisa los pilares aplicables con los artefactos disponibles e indica los límites de la muestra.
2. Lee [IDs y enlaces](../../standards/ids-and-links.md), [formatos](../../standards/output-formats.md), [severidad](../../standards/severity.md), [contexto](../../standards/context.md) y [handoffs](../../standards/handoffs.md). Antes de puntuar, identifica qué criterios de la [rúbrica](references/rubric.md) aplican y por qué.

## Modo Auditar

1. Selecciona las skills de la rúbrica que correspondan. Para cada una, lee su `SKILL.md` y checklist de Auditar. Acota por módulo, etapa e IDs. Una fuente esperada y ausente puede justificar un hallazgo. Una comprobación que no pudiste realizar queda por verificar.
2. Consolida hallazgos por causa y evidencia. Conserva las referencias de origen y señala qué requisito, historia o decisión afecta cada hallazgo. Si el mismo problema aparece en varios documentos, registra una corrección común y las ubicaciones afectadas. Mantén comprobaciones y puntuaciones separadas por criterio.
3. Puntúa con [rubric.md](references/rubric.md). Informa aplicabilidad, cobertura y resultado por pilar. Si falta evidencia de algún criterio aplicable, publica un intervalo provisional. Un corte en propuesta, una contradicción abierta sobre su alcance o una regla pendiente que cambia la implementación mantiene el incremento fuera del relevo ejecutable, cualquiera que sea la puntuación.
4. Entrega [report-template.md](references/report-template.md) con veredicto, hallazgos, evidencia revisada y orden de remediación. Usa los códigos de cada skill y `PR-AUDIT` para hallazgos transversales propios. Registra y verifica hallazgos, ejecución y relevos en el contexto existente con «no toques el código», de acuerdo con su estándar.

## Handoffs

Consolida los hallazgos de las skills seleccionadas en el informe y registra acciones de remediación con alcance, evidencia y motivo. Un hallazgo abierto no autoriza la implementación y la auditoría conserva los documentos revisados.

## Referencias

- [rubric.md](references/rubric.md) para cobertura, aplicabilidad y puntuación.
- [report-template.md](references/report-template.md) para la entrega.
