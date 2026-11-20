# Escala de severidad (producto y requisitos)

Misma escala que el resto del kit. Aquí se juzga **el coste de construir lo equivocado**: un requisito ambiguo, ausente o contradictorio se convierte en código incorrecto, retrabajo o un producto que nadie necesita. Cuanto más tarde se descubre, más caro es.

| Nivel | Criterio | Ejemplos de producto | Acción |
| :--- | :--- | :--- | :--- |
| 🔴 **CRITICAL** | Un requisito ausente, contradictorio o erróneo llevaría a construir algo que pierde dinero, expone datos, incumple la ley o rompe la seguridad. | Regla de reembolso contradictoria entre dos documentos; ningún requisito sobre consentimiento en un producto con datos de salud; permisos de un rol definidos al revés. | Resolver antes de construir. |
| 🟠 **HIGH** | Un flujo principal está ambiguo, incompleto o sin criterios verificables, o el supuesto central del producto no se ha validado. | Historia del checkout sin criterios de aceptación; regla de negocio con "aproximadamente" o "rápido"; MVP construido sobre un supuesto de demanda nunca contrastado. | Resolver antes de empezar ese flujo. |
| 🟡 **MEDIUM** | Huecos que causarán retrabajo o dudas en flujos secundarios, o documentación que ya no coincide con el producto. | Términos usados con dos significados; reglas sin motivo ni origen; documentación funcional desfasada respecto al código en un módulo secundario; preguntas abiertas sin responsable. | Siguiente ciclo. |
| 🔵 **LOW** | Claridad o formato sin riesgo de construir mal. | Plantilla inconsistente; IDs sin estado; redacción mejorable. | Oportunista. |
| ℹ️ **INFO** | Oportunidad. | Añadir un mapa de historias; métricas de éxito más finas. | Informativo. |

## Reglas

1. **Coste × probabilidad de malentendido:** pesa el impacto del área (dinero, datos, permisos, flujo principal) y la probabilidad de que dos personas lo entiendan distinto.
2. **Evidencia:** documento y sección, cita del texto ambiguo o contradictorio, o la ausencia concreta ("ninguna regla define qué pasa si el pago se rechaza"). "Faltan requisitos" sin decir cuáles no es un hallazgo.
3. **El código manda sobre la documentación:** si discrepan, se describe la discrepancia y qué hace el código hoy; no se asume cuál es la intención correcta sin preguntar.
4. **No infles;** ante la duda, el nivel menor.

## Calibración en casos frontera

| Situación | Severidad | Sube si… |
| :--- | :--- | :--- |
| Supuesto central del producto sin validar | HIGH antes de construir; MEDIUM si ya hay usuarios reales usándolo | — |
| Regla de negocio inferida del código y no confirmada | LOW–MEDIUM (se marca "inferido") | HIGH si afecta a dinero, permisos o datos personales |
| Documentación funcional desfasada respecto al código | MEDIUM | HIGH si describe una regla de seguridad o de dinero distinta de la implementada |
| Ausencia de levantamiento formal (entrevistas, interesados) en un proyecto de una sola persona | No es hallazgo: el propio autor es el interesado; se registra como contexto | MEDIUM si hay usuarios o clientes externos sin consultar |
| Término ambiguo en el glosario | LOW–MEDIUM | HIGH si cambia el resultado de una regla de dinero o permisos |
| Requisito no funcional sin cifra ("rápido", "seguro") | MEDIUM | HIGH en un requisito contractual o regulado |
