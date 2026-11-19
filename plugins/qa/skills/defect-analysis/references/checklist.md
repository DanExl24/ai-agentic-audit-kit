# Checklist de auditoría: gestión y análisis de defectos

Severidad orientativa; ajústala con [severity.md](../../../standards/severity.md).

## Registro de defectos

- [ ] Los defectos se registran con pasos para reproducir, esperado y real, entorno y severidad. **[LOW–MEDIUM]**
- [ ] Se distingue qué defectos escaparon (producción, usuarios, release) y en qué fase se detectaron. **[MEDIUM]**
- [ ] Las correcciones enlazan su defecto (issue en el commit o en el PR). **[LOW]**

## No regresión

- [ ] Cada corrección de un defecto añade o ajusta un test que falla con el comportamiento anterior. **[HIGH en flujos principales; MEDIUM en secundarios]**
- [ ] No hay regresiones repetidas sobre el mismo comportamiento en el historial reciente. **[HIGH si se repiten en un flujo principal]**
- [ ] Los reverts y hotfixes se analizan, no solo se aplican. **[MEDIUM]**

## Causa raíz

- [ ] Los defectos graves o recurrentes tienen análisis de causa raíz (5 porqués, Ishikawa) que cubre por qué se introdujeron **y por qué escaparon**. **[MEDIUM; HIGH si hay defectos CRITICAL escapados sin análisis]**
- [ ] El análisis es sin culpables: las causas son controles, herramientas e información, no personas. **[MEDIUM]**
- [ ] Los hotspots (módulos con más correcciones) están identificados y tienen cobertura acorde a su riesgo. **[MEDIUM]**
- [ ] Las prioridades se basan en frecuencias reales (Pareto con fuente), no en impresiones. **[LOW–MEDIUM]**

## Acciones y cierre

- [ ] Las acciones son concretas, con categoría (Quick Win, Táctico, Estratégico), dificultad, plazo, impacto y KPI. **[MEDIUM]**
- [ ] Las acciones se siguen hasta terminarse y su KPI se revisa. **[MEDIUM; HIGH si un defecto grave se repitió con su acción pendiente]**
- [ ] Un defecto se cierra con test de no regresión, un periodo sin recurrencia (14 días o un release) y la lección incorporada al checklist o al CI. **[MEDIUM]**

## Métricas

- [ ] Se mide al menos la tasa de escape o la de regresión, comparando periodos. **[LOW–MEDIUM]**

## Cómo verificar

- Historial: `git log -i -E --grep="fix|bug|hotfix|revert"` en el periodo; abrir una muestra de correcciones y comprobar si incluyen tests.
- Gestor de issues (si hay acceso): etiquetas de severidad y origen, reabiertos, enlaces a commits.
- Documentación: post-mortems o análisis previos y el estado de sus acciones.
- Lo que no se pueda consultar (gestor de issues privado) va en "Por verificar".
