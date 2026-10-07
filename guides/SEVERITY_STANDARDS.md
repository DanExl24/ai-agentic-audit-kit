# 🚦 Escala Canónica de Severidad de Auditoría (Severity Matrix)

Para garantizar consistencia y objetividad técnica, todos los agentes del kit deben clasificar sus hallazgos siguiendo esta escala:

---

## 1. Niveles de Severidad

| Nivel | Nombre | Criterio de Activación | Acción Obligatoria |
| :---: | :--- | :--- | :--- |
| 🔴 **CRITICAL** | Bloqueo o Vulnerabilidad Crítica | Pérdida de datos, IDOR grave, escalamiento de privilegios, fugas de secretos en repo, desborde de memoria garantizado, caída del servidor en runtime, loop infinito de render. | **STOP THE LINE.** El despliegue debe detenerse de inmediato hasta aplicar el hotfix. |
| 🟠 **HIGH** | Defecto Grave de Integración o Rendimiento | Desajuste total de contrato (error 400/500 en flujos principales), consultas SQL sin índice en tablas de alto tráfico (> 1s), fugas de memoria en SPA al desmontar vistas, inyección de dependencias rota. | Bloquea el pase a producción del módulo afectado. Debe corregirse en el sprint actual. |
| 🟡 **MEDIUM** | Anti-patrón o Deuda Técnica Moderada | Código duplicado en más de 3 lugares, lógica de negocio en controladores o componentes de UI, uso de `any` en TypeScript, componentes no accesibles (sin labels ARIA), falta de paginación. | Registrar como deuda técnica prioritaria para el próximo ciclo. |
| 🔵 **LOW** | Mejora Estética o de Mantenimiento | Inconsistencias menores de nombrado, logs de depuración no removidos en desarrollo, selectores CSS no optimizados, falta de tipado estricto en variables locales no críticas. | Corrección oportunista durante refactorings rutinarios. |
| ℹ️ **INFO** | Observación Arquitectónica | Recomendaciones de estilo, oportunidades de optimización futura o sugerencias de librerías modernas sin defecto actual en código. | Informativo para los líderes de equipo. |
