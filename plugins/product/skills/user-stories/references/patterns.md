# Patrones para historias de usuario

## Mapa y división vertical

Ordena de izquierda a derecha las actividades del actor. Debajo enumera las tareas y variantes. Un corte horizontal agrupa las historias que permiten completar un recorrido para un actor concreto. Una épica agrupa historias por resultado y puede enlazar a varios cortes.

Parte por recorrido básico, actores, reglas, variantes de entrada o niveles de servicio cuando cada corte entregue valor. Una división en «hacer la tabla», «hacer la API» y «hacer la pantalla» describe el plan técnico de una historia. Si un habilitador debe precederla, anota la dependencia y su resultado verificable.

Usa INVEST como guía de revisión: independiente en lo posible, negociable, valiosa, estimable, pequeña y comprobable. Cuando una dependencia sea real, declárala en vez de forzar independencia artificial.

## Criterios y casos de uso

- Un criterio describe una condición y un resultado visible o verificable. Puede ser una frase precisa o un escenario Dado/Cuando/Entonces. Separa resultados independientes y cita la regla que los respalda.
- Cubre los límites cuando alteren una decisión. Por ejemplo, para una regla acordada de 4.000 caracteres, documenta el comportamiento esperado con 4.000 y con 4.001. Si falta decidir cómo se cuentan, registra la pregunta antes de fijar el criterio.
- Un caso de uso aporta valor si hay varios actores, extensiones o pasos con orden significativo. Indica disparador, precondiciones, recorrido principal, alternativas y postcondiciones. Enlaza a las historias que lo entregan y evita duplicar las reglas.
- Conecta `OBJ` o requisito de origen → `HU` → `CA` → `RN` o `DEC` según corresponda. Un criterio inferido del código describe el estado observado hasta que se confirme como comportamiento deseado.

## Definition of Ready

Marca **lista** solo si hay resultado y actor claros, alcance acotado, criterios verificables con fuentes y ninguna pregunta que cambie lo que se implementaría. El equipo debe poder estimarla con la evidencia disponible, aunque todavía no tenga una cifra.

Para cada dependencia necesaria, registra el ID, la capacidad concreta requerida y la evidencia de que ya está disponible o de que se incluye en el mismo incremento listo, con un orden viable. Revisa los bloqueos indirectos que afecten a ese incremento. Si la dependencia necesaria está en refinamiento, no está disponible o no hay evidencia de ella, la historia queda **bloqueada** y su relevo de implementación queda pendiente. Si solo necesita una parte de la dependencia, delimita esa parte y demuestra que es utilizable y está lista antes de habilitar la historia.

El estado documental (`borrador`, `acordado`, `implementado`, `obsoleto`) y la preparación para desarrollar son campos distintos. Una historia acordada puede seguir pendiente de refinamiento. Una regla en borrador puede motivar una historia futura y permanecer fuera del alcance ejecutable.
