---
name: test-strategy
description: "Diseña y audita la estrategia y el plan de pruebas de un proyecto o de un release a partir del riesgo: mapa de riesgos por área (impacto × probabilidad × detección), forma de la pirámide adecuada al tipo de proyecto, qué automatizar y qué explorar, criterios de entrada y salida, definición de terminado de calidad, trazabilidad criterios de aceptación → casos → tests y plan de pruebas de un release. Úsala al arrancar un proyecto, antes de un release importante, cuando no está claro qué probar o cuando la cobertura no refleja el riesgo. No para escribir los tests de una capa (frontend:testing, backend:testing) ni para diseñar casos concretos (test-design)."
---

# Estrategia y plan de pruebas

Probar todo es imposible y probar lo que es fácil es inútil. Una estrategia decide **dónde invertir el esfuerzo de pruebas según el riesgo** y cómo se sabe que algo está listo. Sin ella, la cobertura crece donde los tests son baratos (utilidades, componentes simples) y se queda vacía donde los fallos cuestan (pagos, permisos, migraciones).

## Cuándo usarla

- Arrancar un proyecto o un módulo grande y decidir qué tipos de prueba tendrá.
- Preparar el plan de pruebas de un release o de una funcionalidad con riesgo.
- La suite es grande pero los bugs siguen llegando a producción.
- Definir criterios de terminado o de salida de un release.
- Auditar si la cobertura real corresponde al riesgo del producto.

**No es para:** escribir tests unitarios, de componentes o de integración → `frontend:testing`, `backend:testing` · elegir los casos concretos de una funcionalidad → `test-design` · suites E2E → `e2e` · qué corre en cada etapa de CI → `quality-gates`.

## Paso 0: contexto (ambos modos)

1. **Producto y riesgo de negocio:** qué hace, quién lo usa, qué cuesta un fallo (dinero, datos, reputación, cumplimiento), frecuencia de despliegue.
2. **Inventario de pruebas existente:** herramientas, número y tipo de tests por capa, tiempos de ejecución, qué corre en CI, tests intermitentes conocidos, cómo se prueba hoy un release (manual, scripts, nada).
3. **Historial de defectos** si existe (issues, commits `fix:`, incidentes): dónde fallan las cosas de verdad.
4. Si existe `.sdlc/context.md`, léelo y respeta sus convenciones y decisiones ([context.md](../../standards/context.md)).

## Modo Construir

1. **Mapa de riesgos:** áreas del producto puntuadas por impacto, probabilidad de fallo y dificultad de detección. Ver [patterns.md § Mapa de riesgos](references/patterns.md#mapa-de-riesgos).
2. **Forma de la cobertura** según el tipo de proyecto (pirámide, trofeo, diamante) y qué nivel cubre cada riesgo. Ver [patterns.md § Forma](references/patterns.md#forma-de-la-cobertura).
3. **Automatizar o explorar:** qué se automatiza (regresión, reglas, contratos), qué se explora (usabilidad, combinaciones nuevas) y qué se prueba en producción (monitorización, canary).
4. **Criterios:** definición de terminado de calidad y criterios de entrada y salida de un release. Ver [patterns.md § Criterios](references/patterns.md#criterios-de-terminado-y-de-salida).
5. **Trazabilidad:** de cada criterio de aceptación a sus casos y tests, en el nivel de detalle que el equipo pueda mantener.
6. **Plan de release** si aplica, con [plan-template.md](references/plan-template.md).
7. Entrega según [output-formats.md § Construir](../../standards/output-formats.md#modo-construir): un documento corto y vivo, no un manual que nadie lee.

## Modo Auditar

1. Construye el mapa de riesgos (aunque sea aproximado) y superpón la cobertura real por área y nivel.
2. Busca los desajustes: riesgo alto con cobertura baja, cobertura alta en áreas triviales, niveles invertidos (todo E2E o nada de integración).
3. Revisa criterios de terminado y de salida, y cómo se decidió el último release.
4. Recorre [checklist.md](references/checklist.md).
5. Clasifica con [severity.md](../../standards/severity.md) y entrega según [output-formats.md § Auditar](../../standards/output-formats.md#modo-auditar) con código `QA-STRAT`.

## Principios

1. **El riesgo decide el esfuerzo,** no la facilidad de escribir el test.
2. **Cada riesgo tiene un control:** un test, una verificación manual, una alerta o una decisión explícita de aceptarlo.
3. **El nivel más bajo que detecte el fallo:** unitario si basta, integración si el riesgo está en la frontera, E2E solo para el recorrido completo.
4. **Criterios antes del release,** no improvisados el día de la entrega.
5. **Documento corto y vivo:** se actualiza con cada incidente o cambio de producto.

## Handoffs

Según [handoffs.md](../../standards/handoffs.md): profundidad máxima de 2, alcance acotado, sin reinvocar skills ya aplicadas y registro de pendientes.

| Disparador (observable) | Skill | Alcance y contexto que se pasa |
| :--- | :--- | :--- |
| Un área de riesgo alto necesita casos concretos (reglas con límites, estados, combinaciones) | `test-design` | Área, reglas y criterios de aceptación |
| Riesgos de usabilidad o combinaciones nuevas que no compensa automatizar | `exploratory-testing` | Áreas y objetivos de sesión |
| Huecos de tests unitarios o de componentes en el frontend | `frontend:testing` | Módulos y riesgos |
| Huecos de tests de integración, contrato o concurrencia en el backend | `backend:testing` | Módulos y riesgos |
| Riesgo de rendimiento o capacidad sin ninguna prueba | `load-testing` | Endpoints críticos y volumen esperado |
| El historial muestra regresiones repetidas o correcciones concentradas en un módulo | `defect-analysis` | Commits o issues y módulos afectados |
| Riesgos que cruzan capas (contrato, sesión) sin control | `fullstack:contracts` | Endpoints y consumidores |

## Referencias

| Archivo | Cuándo cargarlo |
| :--- | :--- |
| [patterns.md](references/patterns.md) | Siempre: mapa de riesgos, forma de la cobertura, automatizar o explorar, criterios y trazabilidad. |
| [plan-template.md](references/plan-template.md) | Al escribir una estrategia o un plan de release. |
| [checklist.md](references/checklist.md) | Modo Auditar. |

## Skills relacionadas

- `test-design`: casos concretos para las áreas de riesgo.
- `exploratory-testing`: lo que no compensa automatizar.
- `frontend:testing` y `backend:testing`: implementación de los tests de cada capa.
- `fullstack:audit` y los `audit` de capa: su ruta pre-release usa los criterios de salida definidos aquí.
