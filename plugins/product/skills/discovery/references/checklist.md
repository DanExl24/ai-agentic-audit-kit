# Checklist de auditoría: descubrimiento de producto

Severidad orientativa; ajústala con [severity.md](../../../standards/severity.md).

## Problema y usuarios

- [ ] El problema está escrito sin mencionar la solución, con quién lo tiene y cuándo. **[MEDIUM; HIGH si no hay ningún enunciado y se está construyendo]**
- [ ] Se declara la evidencia del problema (observada, entrevistas u opinión). **[MEDIUM]**
- [ ] Se conoce la alternativa actual del usuario y qué le cuesta. **[MEDIUM]**
- [ ] El segmento es concreto y hay early adopters identificados. **[MEDIUM]**
- [ ] Las proto-personas están marcadas como supuestos o validadas con usuarios reales. **[LOW–MEDIUM]**

## Propuesta de valor y modelo

- [ ] La propuesta de valor dice qué cambia para el usuario y en qué se diferencia de su alternativa. **[MEDIUM]**
- [ ] El canvas (o su versión interna) no tiene huecos rellenos con texto sin marcar como supuesto. **[LOW–MEDIUM]**

## Supuestos y MVP

- [ ] Los supuestos de mayor riesgo están identificados y clasificados por importancia y evidencia. **[HIGH si el supuesto central no está identificado antes de construir]**
- [ ] Cada supuesto crítico tiene experimento, criterio de éxito definido antes y resultado registrado. **[HIGH si el MVP depende de uno sin validar; MEDIUM si ya hay usuarios reales]**
- [ ] El MVP dice qué supuesto valida y tiene listas explícitas de dentro y fuera. **[MEDIUM]**

## Objetivos

- [ ] Los objetivos tienen métrica, valor actual (o plan para medirlo), meta y plazo. **[MEDIUM]**
- [ ] Hay una métrica de control y ninguna métrica principal es de vanidad. **[LOW–MEDIUM]**

## Vigencia

- [ ] El brief describe lo que se está construyendo hoy (sin funcionalidades principales ausentes ni descartadas que sigan apareciendo). **[MEDIUM]**
- [ ] Cada elemento tiene estado y origen (confirmado, inferido, supuesto). **[LOW]**

## Cómo verificar

- Buscar material: `docs/`, `README.md`, archivos con "visión", "brief", "canvas", "PRD", presentaciones enlazadas.
- Comparar el alcance descrito con los módulos y rutas que existen en el código.
- En un proyecto personal, el autor es el interesado: la falta de entrevistas no es hallazgo, pero sí la falta de problema y objetivos escritos si se planea abrirlo a otros usuarios.
