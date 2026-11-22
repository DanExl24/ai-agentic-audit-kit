# Handoffs entre skills

Una skill no trabaja aislada: cuando encuentra algo que pertenece a otra, **se lo pasa** con el contexto necesario en lugar de ignorarlo o resolverlo a medias. Este estándar define cuándo y cómo se hace, para que las cadenas sean útiles y no se disparen sin control.

## Handoff frente a "skills relacionadas"

| | Skills relacionadas | Handoffs |
| :--- | :--- | :--- |
| Qué es | Lista orientativa de skills cercanas | Disparadores concretos que activan otra skill |
| Cuándo actúa | Nunca por sí sola | Cuando el disparador se cumple en el código o en el objetivo |
| Resultado | Una mención | Trabajo de la otra skill sobre un alcance acotado, o un pendiente registrado |

## Formato en cada SKILL.md

Sección `## Handoffs`, después de "Principios":

```markdown
## Handoffs

| Disparador (observable) | Skill | Alcance y contexto que se pasa |
| :--- | :--- | :--- |
| Una consulta usa un ID de la petición sin filtrar por tenant o propietario | `backend:authorization` | La consulta, el endpoint y el modelo de tenancy detectado |
| El cliente lee campos que la API no devuelve con ese nombre | `fullstack:contracts` | El endpoint y el consumidor (archivo y líneas) |
```

Un disparador es **concreto y comprobable** en el código o en el objetivo ("un endpoint de escritura sin `Idempotency-Key` y con efectos de pago"), nunca genérico ("si hay temas de seguridad"). Entre 3 y 8 por skill, los de mayor valor.

## Reglas

1. **Profundidad máxima de 2.** La skill invocada por el usuario puede pasar a otra (nivel 1) y esta a una tercera (nivel 2). Los disparadores del nivel 2 no se ejecutan: se registran como pendientes.
2. **No se reinvoca una skill ya aplicada** en la misma tarea. Si su alcance cambia, se amplía el trabajo existente en lugar de repetirlo.
   - **Nunca hay handoffs de una skill a sí misma:** lo que la skill detecta fuera del alcance pedido es un **hallazgo abierto**, con el código y la numeración de su plugin (`BE-AUTHN-001`, no `BE-AUTHN-PLAIN`), no un handoff.
3. **Alcance acotado.** Un handoff no es una auditoría ni un desarrollo completo de la otra skill: se aplica solo a lo que activó el disparador.
   - En modo **Auditar**, la skill destino aplica los puntos de su `checklist.md` que tocan ese alcance y emite hallazgos con su propio código (`BE-*`, `FE-*`, `FS-*`).
   - En modo **Construir**, aplica su `patterns.md` a la pieza concreta.
   - Si el destino va a implementar un comportamiento, enumera los IDs acordados que entran en el alcance. Usa un rango solo si todos sus elementos están acordados. Registra aparte qué borradores siguen pendientes y qué `PRE` o `SUP` los bloquea. Puedes compartirlos como contexto para análisis o aclaración.
4. **Coste a la vista.**
   - Un handoff dentro de la tarea en curso se ejecuta declarándolo en una línea ("paso a `backend:authorization` para la consulta X").
   - **Más de dos skills añadidas a la tarea** (cuentan tanto las cadenas en profundidad como varios handoffs en paralelo desde la misma skill), o un handoff hacia un orquestador (`audit`, `feature`), **se proponen con su coste y esperan confirmación**, salvo que el usuario haya pedido expresamente seguir los handoffs.
   - Si la ejecución no es interactiva, los handoffs que requieren confirmación se registran como pendientes.
5. **Plugin ausente.** Si la skill destino es de un plugin no instalado (o su archivo no existe), se avisa, se registra como pendiente con el disparador y la evidencia, y se continúa.
6. **Dentro de un orquestador** (`audit`, `feature`), los handoffs no se disparan por separado: el orquestador ya planifica qué skills se aplican. Los disparadores hacia skills que no están en el plan se recogen como "escalado sugerido" en su informe o como pasos opcionales del plan.
7. **Traza.** Toda entrega termina con los handoffs hechos y los pendientes, y se registran en el [contexto compartido](context.md) si existe. Actualizar `.sdlc/context.md` no es modificar código: se hace también en auditorías de solo lectura, salvo que el usuario prohíba escribir archivos; en ese caso la entrega incluye el bloque "Contexto propuesto" ([context.md](context.md)).

## Cómo invocar la skill destino

- Con herramienta de skills: por nombre, `<plugin>:<skill>` (p. ej. `backend:authorization`).
- Sin ella: lee `plugins/<plugin>/skills/<skill>/SKILL.md` (o la ruta que indique el índice del proyecto, p. ej. `.sdlc-skills/INDEX.md`) y las referencias que esa skill indique.
- Pásale siempre: el alcance (archivos y líneas), el modo, el disparador y lo ya decidido, para que no empiece de cero.

## Bloque de traza en la entrega

```markdown
## Handoffs
- Hechos: `backend:authorization` (consulta `orders.repo.ts:40`) → BE-AUTHZ-001
- Pendientes: `frontend:forms` — errores 422 por campo sin mostrar en `OrderForm.vue` (profundidad máxima alcanzada)
```
