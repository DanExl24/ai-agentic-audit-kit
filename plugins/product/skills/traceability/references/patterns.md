# Patrones de trazabilidad

## Recorrido

Usa la cadena que corresponda al proyecto: objetivo o decisión → requisito o regla → historia y criterio → implementación → prueba y cambio. Un requisito puede tener varios criterios y un criterio puede depender de varias reglas. Muestra la relación sin forzar correspondencias uno a uno.

- Para un enlace de documentación, abre el archivo y la sección del ID. Una mención en otro sitio puede ser una referencia, no una definición nueva.
- Para código, contrasta el resultado de la regla con el archivo y símbolo. Para pruebas, localiza el escenario y la aserción. Un nombre parecido, una búsqueda sin lectura contextual o el hecho de que un archivo cambió no demuestran cobertura.
- Para un commit, verifica el hash y el cambio o referencia que lo relaciona con el requisito. Si el historial no está disponible o el trabajo no se ha confirmado en Git, indica esa limitación.

## Evidencia por vínculo

| Estado | Qué significa |
| :--- | :--- |
| Verificado | Destino y relación comprobados con una fuente localizable. |
| Previsto | Hay un plan, tarea o criterio que apunta a trabajo futuro. |
| Por verificar | El destino o la relación podrían existir y falta evidencia. |
| Ausente | La revisión confirma que el elemento esperado no existe en el alcance revisado. |
| No aplica | El artefacto no corresponde a la etapa, alcance o naturaleza de la regla. Anota el motivo. |

Para una regla en borrador, la falta de código puede ser esperada. Para una regla declarada implementada, un enlace a un símbolo inexistente es una brecha verificable. Para una prueba identificada por lectura, indica «no ejecutada en esta revisión» cuando corresponda.

## Impacto

Cita la regla que cambia, su estado y los artefactos afectados. Distingue impactos directos por un enlace verificado, indirectos por una dependencia intermedia, y candidatos por verificar. Para cada impacto relevante indica por qué importa y qué tendría que comprobarse. Si el recálculo de vencimientos cambia, revisa criterios de cambio de política, guardas del ciclo de vida, rutinas de cálculo y pruebas límite. Si todavía no hay código, señala el impacto previsto sobre el diseño o los casos de prueba.
