# Checklist de auditoría: diseño de casos

Severidad orientativa; ajústala con [severity.md](../../../standards/severity.md). Cita el test (o su ausencia) y la regla que debería cubrir.

## Reglas y entradas

- [ ] Las reglas del área están escritas o se pudieron reconstruir sin contradicciones. **[MEDIUM; HIGH si el código y los requisitos se contradicen en dinero o permisos]**
- [ ] Cada entrada relevante tiene sus clases válidas e inválidas identificadas. **[MEDIUM]**

## Cobertura de técnica

- [ ] Hay casos en los límites de cada rango y longitud (borde y vecinos). **[MEDIUM; HIGH en validaciones de dinero, permisos o datos externos]**
- [ ] Cada regla de las decisiones con varias condiciones tiene un caso. **[MEDIUM–HIGH según el impacto]**
- [ ] Las transiciones válidas están probadas y las prohibidas más peligrosas también. **[HIGH si una transición prohibida tiene impacto económico]**
- [ ] Los parámetros combinables tienen al menos cobertura por pares en las áreas de riesgo. **[LOW–MEDIUM]**
- [ ] Existen casos negativos: vacíos, nulos, enormes, caracteres especiales, fechas límite, concurrencia, fallos de dependencias, permisos. **[MEDIUM; HIGH si solo hay camino feliz en un flujo principal]**

## Calidad de los casos

- [ ] El resultado esperado es concreto (valor, estado, código de error). **[MEDIUM]**
- [ ] No hay tests sin aserciones o que pasan con la funcionalidad rota. **[HIGH en flujos principales]**
- [ ] Los casos parametrizados sustituyen a los copiados. **[LOW]**
- [ ] Los escenarios Gherkin describen comportamiento en lenguaje de negocio y verifican un resultado observable. **[LOW–MEDIUM]**

## Cómo verificar

- Busca los valores límite en los tests (`17`, `18`, `65`, longitudes máximas) frente a las constantes del código.
- Para "tests que pasan con la funcionalidad rota": rompe a mano la regla (cambia `>=` por `>`) o usa mutación (Stryker, mutmut, PIT) en el módulo y comprueba si algún test falla.
