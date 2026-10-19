# 🚦 Escala Canónica de Severidad de Auditoría (Severity Matrix)

Para garantizar consistencia y objetividad técnica, todos los agentes del kit deben clasificar sus hallazgos siguiendo esta escala:

---

## 1. Niveles de Severidad

| Nivel | Nombre | Criterio de Activación General y de QA | Acción Obligatoria |
| :---: | :--- | :--- | :--- |
| 🔴 **CRITICAL** | Bloqueo o Vulnerabilidad Crítica | Pérdida de datos, IDOR grave, escalamiento de privilegios, fugas de secretos en repo, desborde de memoria garantizado, caída del servidor en runtime, loop infinito de render. **En QA:** Ausencia total de validación y tests en flujos transaccionales de pago, o agotamiento garantizado del pool de BD bajo carga concurrente mínima. | **STOP THE LINE.** El despliegue debe detenerse de inmediato hasta aplicar el hotfix. |
| 🟠 **HIGH** | Defecto Grave de Integración o Rendimiento | Desajuste total de contrato (error 400/500 en flujos principales), consultas SQL sin índice en tablas de alto tráfico (> 1s), fugas de memoria en SPA al desmontar vistas, inyección de dependencias rota. **En QA:** Tests unitarios sin aserciones reales que enmascaran regresiones graves, endpoints de login sin rate-limiting (fuerza bruta), o suites E2E con esperas fijas que rompen el CI de forma intermitente. | Bloquea el pase a producción del módulo afectado. Debe corregirse en el sprint actual. |
| 🟡 **MEDIUM** | Anti-patrón o Deuda Técnica Moderada | Código duplicado en más de 3 lugares, lógica de negocio en controladores o componentes de UI, uso de `any` en TypeScript, componentes no accesibles (sin labels ARIA), falta de paginación. **En QA:** Acoplamiento directo a infraestructura sin Inversión de Dependencias (código intesteable), selectores E2E basados en clases CSS en lugar de roles accesibles (`getByRole`), omisión de umbrales p95/p99 en endpoints de lectura. | Registrar como deuda técnica prioritaria para el próximo ciclo. |
| 🔵 **LOW** | Mejora Estética o de Mantenimiento | Inconsistencias menores de nombrado, logs de depuración no removidos en desarrollo, selectores CSS no optimizados, falta de tipado estricto en variables locales no críticas. **En QA:** Suites unitarias lentas (>200ms por archivo), mocks excesivos por falta de granularidad, parametrización incompleta de datos en scripts k6. | Corrección oportunista durante refactorings rutinarios. |
| ℹ️ **INFO** | Observación Arquitectónica | Recomendaciones de estilo, oportunidades de optimización futura o sugerencias de librerías modernas sin defecto actual en código. **En QA:** Recomendación de adopción de pruebas de mutación (Stryker), migración a Vitest o adopción de contratos Pact/OpenAPI. | Informativo para los líderes de equipo. |
