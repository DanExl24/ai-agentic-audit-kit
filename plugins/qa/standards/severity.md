# Escala de severidad (QA)

Misma escala que el resto del kit. En QA se juzga **el riesgo de que un defecto llegue a producción sin que nadie lo detecte**, y su impacto cuando llega.

| Nivel | Criterio | Ejemplos de QA | Acción |
| :--- | :--- | :--- | :--- |
| 🔴 **CRITICAL** | Un flujo con impacto en dinero, datos o seguridad puede romperse sin que ninguna prueba ni control lo detecte. | Cobros sin ningún test ni verificación previa al release; escaneo dinámico que confirma una vulnerabilidad explotable; plan de release que omite la migración de datos. | Detener el release. |
| 🟠 **HIGH** | Un flujo principal está sin cubrir o su cobertura no detecta fallos reales. | Login o checkout sin casos negativos; tests que pasan con la funcionalidad rota (aserciones vacías); suite E2E intermitente que el equipo ignora; release sin criterios de salida. | Corregir antes de liberar. |
| 🟡 **MEDIUM** | Huecos de cobertura o de proceso que ya causan fricción o dejarán escapar el próximo defecto. | Solo camino feliz en módulos secundarios; sin valores límite en validaciones; bugs reportados sin pasos para reproducir; estrategia no documentada. | Siguiente ciclo. |
| 🔵 **LOW** | Mejora de mantenibilidad o claridad sin riesgo actual. | Casos redundantes; nombres de tests poco descriptivos. | Oportunista. |
| ℹ️ **INFO** | Oportunidad. | Adoptar property-based testing en reglas de cálculo. | Informativo. |

## Reglas

1. **Riesgo × detección:** un hueco de cobertura pesa según el impacto del área y la probabilidad de que el defecto pase desapercibido (hay otro control que lo detectaría, como tipos, contratos o monitorización).
2. **Evidencia:** archivo de tests, caso ausente concreto, ejecución o reporte. "Faltan tests" sin decir cuáles no es un hallazgo.
3. **Todo CRITICAL está verificado** y el informe dice cómo.
4. **No infles;** ante la duda, el nivel menor.

## Calibración en casos frontera

| Situación | Severidad | Sube a CRITICAL si… |
| :--- | :--- | :--- |
| Área sin ningún test | HIGH en flujos principales; MEDIUM en secundarios | mueve dinero, permisos o datos personales y tampoco hay otros controles |
| Test intermitente conocido | MEDIUM; HIGH si está en un flujo crítico o el equipo ya lo ignora o reintenta hasta que pasa | — |
| Solo camino feliz | MEDIUM; HIGH en validaciones de dinero, permisos o datos de entrada externos | — |
| Estrategia o plan de pruebas no escrito | MEDIUM en equipos pequeños con buena cobertura; HIGH si hay releases sin criterios de salida | — |
| Fallo que solo ocurre en el entorno de pruebas (datos, entorno, herramientas) con producción sana | MEDIUM | — · sube a HIGH si impide verificar un release |
| Bug sin pasos para reproducir | LOW–MEDIUM según su gravedad | — |
