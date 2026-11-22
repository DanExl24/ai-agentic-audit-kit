---
name: traceability
description: "Construye y audita la trazabilidad de requisitos y reglas de negocio hasta historias, criterios de aceptación, código, pruebas y commits. Verifica enlaces y cobertura con evidencia, distingue trabajo previsto de implementado y analiza el impacto de cambiar un requisito."
---

# Trazabilidad de requisitos

## Cuándo usarla

- Saber qué historia, implementación o prueba respalda una regla.
- Detectar huecos, enlaces rotos o elementos sin origen.
- Estimar qué artefactos revisar ante un cambio propuesto.

## Paso 0

1. Define alcance, referencia de código si existe, punto de partida y etapas relevantes. Lee las fuentes aplicables: reglas, especificación, historias, criterios, código, pruebas e historial disponible. Lee `.sdlc/context.md` y el mapa existente cuando estén disponibles.
2. Carga [IDs y enlaces](../../standards/ids-and-links.md), [formatos](../../standards/output-formats.md), [contexto](../../standards/context.md) y [handoffs](../../standards/handoffs.md). Usa las convenciones del repositorio y conserva sus enlaces vigentes.

## Modo Construir

1. Forma el inventario de elementos con su ID, fuente y estado. Resuelve cada enlace relevante en ambas direcciones cuando corresponda. Comprueba que el destino existe y que su contenido respalda el vínculo. Para código cita ruta y símbolo. Para pruebas cita ruta, nombre y aserción pertinente. Para historial cita el commit o referencia comprobada.
2. Usa los estados de evidencia de [patterns.md](references/patterns.md). Una prueba que existe puede cubrir un criterio aunque todavía no se haya ejecutado en esta revisión. Un commit requiere evidencias que lo vinculen al artefacto. Registra por verificar cuando no puedas comprobarlo.
3. Usa [traceability-template.md](references/traceability-template.md) en la matriz existente o en `docs/product/trazabilidad.md`. Distingue brechas de cobertura para requisitos acordados o implementados y vacíos esperados por etapa o borrador. Registra inconsistencias y comprueba los anclajes. Cuando el usuario pida reparar enlaces, modifica solo los artefactos documentales dentro del alcance y cuyos destinos puedas verificar.
4. Si se plantea un cambio, recorre los enlaces hacia sus fuentes y hacia los artefactos que dependen de él. Enumera impactos directos, indirectos y por confirmar, junto con la evidencia y la verificación necesaria. Mantén el cambio como propuesta hasta recibir la aprobación correspondiente.
5. Guarda y verifica la matriz y el registro en el contexto existente con «no toques el código», según el estándar de contexto.

## Modo Auditar

1. Sigue el [checklist](references/checklist.md). Comprueba enlaces hacia adelante y hacia atrás en el alcance acordado. Si usas una muestra, indica sus límites y prioriza reglas críticas, cambios recientes y discrepancias conocidas.
2. Clasifica con [severidad](../../standards/severity.md) y entrega según [formatos](../../standards/output-formats.md) con código `PR-TRACE`. Enumera las comprobaciones pendientes y verifica el registro de contexto.

## Handoffs

| Disparador | Destino | Alcance |
| :--- | :--- | :--- |
| Una historia o especificación contradice una decisión vigente | `user-stories` o `specification` | IDs, documentos y discrepancia |
| Falta comprobar una regla acordada o la prueba no cubre el criterio | `qa:test-design` | Regla, criterio y evidencia de cobertura incompleta |
| Un cambio aprobado altera un contrato entre capas | `fullstack:contracts` | Interfaces, consumidores y enlaces afectados |

## Referencias

- [patterns.md](references/patterns.md) en ambos modos.
- [traceability-template.md](references/traceability-template.md) en Construir.
- [checklist.md](references/checklist.md) en Auditar.
