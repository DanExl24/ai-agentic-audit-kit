# Checklist de auditoría: pruebas exploratorias y reportes

Severidad orientativa; ajústala con [severity.md](../../../standards/severity.md).

## Práctica

- [ ] Se explora de forma deliberada (sesiones con charter) antes de los releases o tras funcionalidades nuevas. **[MEDIUM; HIGH si un producto con usuarios se publica sin ninguna verificación más allá de los tests]**
- [ ] Las sesiones dejan notas de cobertura, no solo bugs. **[LOW–MEDIUM]**
- [ ] Las heurísticas cubren los riesgos del área (interrupciones, roles, concurrencia, datos extremos). **[MEDIUM]**
- [ ] Se explora en entornos seguros, sin datos reales ni efectos irreversibles. **[HIGH si se prueba sobre producción con datos reales sin autorización]**

## Reportes de bug

- [ ] Los reportes tienen pasos reproducibles, esperado y real, entorno y evidencia. **[MEDIUM]**
- [ ] Severidad y prioridad se distinguen y la severidad sigue una escala común. **[LOW–MEDIUM]**
- [ ] Los reportes son mínimos (sin pasos irrelevantes) y no duplican otros. **[LOW]**

## Cierre del ciclo

- [ ] Los bugs encontrados por exploración que pueden volver tienen un test de regresión. **[MEDIUM; HIGH en flujos de dinero o permisos]**
- [ ] Las preguntas abiertas de las sesiones llegan a producto y se resuelven. **[LOW–MEDIUM]**

## Cómo verificar

- Muestra de 10 bugs recientes del gestor de issues: ¿cuántos se pueden reproducir solo con el reporte?
- Buscar notas o informes de sesión de los últimos releases.
- Para 3 bugs cerrados, comprobar si existe el test que los cubre.
