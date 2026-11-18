# Escala de severidad (frontend)

Toda skill del plugin clasifica sus hallazgos con esta escala. Se juzga el **impacto real para el usuario o el negocio**, no lo feo que se vea el código.

| Nivel | Criterio | Ejemplos frontend | Acción |
| :--- | :--- | :--- | :--- |
| 🔴 **CRITICAL** | Pérdida o corrupción de datos, fuga de información sensible, la app queda inutilizable. | Doble envío que crea cobros duplicados; token de acceso expuesto en el bundle; loop infinito de render; datos de un usuario visibles para otro por caché compartida en SSR. | Detener el despliegue hasta corregir. |
| 🟠 **HIGH** | Un flujo principal falla o se degrada gravemente para muchos usuarios. | Refresh token sin cola que desloguea al usuario en ráfagas de 401; fuga de memoria al navegar entre vistas; respuestas fuera de orden que muestran datos de otro filtro; errores 422 tragados sin feedback. | Corregir antes de liberar el módulo afectado. |
| 🟡 **MEDIUM** | Deuda técnica que ya causa fricción o hará que el próximo cambio falle. | `any` en contratos de API; llamadas HTTP directas en componentes; datos del servidor duplicados a mano en un store global; dependencias circulares entre features. | Planificar en el siguiente ciclo. |
| 🔵 **LOW** | Mejora de mantenibilidad sin impacto actual. | Nombres inconsistentes; tipos locales poco precisos; barrel files que podrían simplificarse. | Corregir de forma oportunista. |
| ℹ️ **INFO** | Observación u oportunidad, sin defecto. | Valorar migrar a TanStack Query; activar `noUncheckedIndexedAccess`. | Informativo. |

## Reglas de clasificación

1. **Impacto × alcance.** Un defecto grave en una pantalla interna poco usada puede bajar un nivel; uno leve en el checkout puede subir uno. Justifica el ajuste en una línea.
2. **Sin evidencia no hay hallazgo.** Si no puedes señalar archivo y líneas, o reproducir el escenario, es una pregunta abierta, no un hallazgo.
3. **No infles.** Si dudas entre dos niveles, elige el menor y explica qué haría falta para subirlo.
