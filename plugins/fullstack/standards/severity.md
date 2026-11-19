# Escala de severidad (fullstack)

Misma escala que los plugins `frontend` y `backend`, aplicada a problemas que **cruzan capas**. Se juzga el impacto real sobre datos, dinero, seguridad, disponibilidad y usuarios.

| Nivel | Criterio | Ejemplos entre capas | Acción |
| :--- | :--- | :--- | :--- |
| 🔴 **CRITICAL** | Pérdida o corrupción de datos, acceso a datos ajenos, pérdida económica, flujo principal imposible. | El cliente calcula el precio y el backend lo acepta; el frontend oculta un botón de admin y la API no autoriza; un cambio de contrato rompe el pago en producción. | Detener el despliegue. |
| 🟠 **HIGH** | Un flujo principal falla o se degrada gravemente. | Desajuste de nombres (`userId` vs `user_id`) que deja datos vacíos en pantalla; errores 422 que el cliente no sabe leer; token en `localStorage` + API sin protección CSRF coherente. | Corregir antes de liberar. |
| 🟡 **MEDIUM** | Deuda que ya causa fricción o romperá el próximo cambio. | Tipos duplicados a mano en ambas capas; formatos de fecha distintos por endpoint; envelopes inconsistentes. | Siguiente ciclo. |
| 🔵 **LOW** | Mantenibilidad sin impacto actual. | Nombres inconsistentes entre capas sin fallo visible. | Oportunista. |
| ℹ️ **INFO** | Oportunidad. | Adoptar un contrato compartido generado. | Informativo. |

## Reglas

1. **Impacto × alcance;** justifica cualquier ajuste en una línea.
2. **Evidencia en las dos capas:** un hallazgo de contrato cita el archivo del servidor **y** el del cliente.
3. **Todo CRITICAL está verificado** y el informe dice cómo.
4. **No infles;** ante la duda, el nivel menor.
5. **Calibración:** se aplican las tablas de casos frontera de `frontend` y `backend` (`standards/severity.md` de cada plugin) a la parte de cada capa, y estas entre capas:

## Calibración en casos frontera

| Situación | Severidad | Sube a CRITICAL si… |
| :--- | :--- | :--- |
| Fallo que solo ocurre en desarrollo (proxy, puertos, certificados locales) con producción sana | MEDIUM: bloquea al equipo, no a los usuarios | — · sube a HIGH si también afecta a staging o al despliegue real |
| Colección con límite fijo sin paginación | LOW–MEDIUM si es un límite intencionado de "últimos N" (buzón, recientes) y lo demás sigue accesible | — · sube a HIGH si el usuario pierde acceso a datos que necesita (no hay otra forma de llegar a ellos) |
| Tipos del cable duplicados a mano que hoy coinciden | INFO (MEDIUM si ya divergen y causan fallos) | — |
| Contrato incompatible con clientes en circulación (apps móviles, pestañas abiertas) | HIGH | rompe pagos, acceso o escritura de datos para esos clientes |
