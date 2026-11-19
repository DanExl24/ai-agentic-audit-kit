# Patrones de estrategia de pruebas

## Mapa de riesgos

Una fila por área funcional o técnica (no por archivo). Puntúa de 1 a 3:

| Área | Impacto (1–3) | Probabilidad (1–3) | Detección (1 fácil – 3 difícil) | Riesgo = I × P × D | Control actual | Control propuesto |
| :--- | :-: | :-: | :-: | :-: | :--- | :--- |
| Checkout y cobro | 3 | 2 | 3 | 18 | 2 tests E2E de camino feliz | Integración del cálculo de importes, casos de pago fallido, idempotencia, smoke tras desplegar |
| Permisos por tenant | 3 | 2 | 3 | 18 | Ninguno | Matriz de permisos automatizada (`backend:testing`) |
| Listado con filtros | 2 | 2 | 1 | 4 | Tests de componente | Suficiente |
| Página "Acerca de" | 1 | 1 | 1 | 1 | Ninguno | Ninguno (riesgo aceptado) |

- **Impacto:** 3 = dinero, datos personales, seguridad o bloqueo del uso principal; 2 = flujo importante degradado; 1 = molestia.
- **Probabilidad:** 3 = código nuevo, complejo, con historial de bugs o dependencias externas; 1 = estable y simple.
- **Detección:** 3 = el fallo es silencioso (un importe mal calculado, datos de otro tenant); 1 = salta a la vista o lo detectan los tipos o la monitorización.
- Riesgo ≥ 12: control automatizado obligatorio. 6–11: automatizado o verificación explícita. ≤ 4: puede aceptarse, por escrito.

Fuentes para puntuar: historial de defectos (commits `fix:` por módulo), complejidad y churn del código, dependencias externas, opinión del equipo y de negocio.

## Forma de la cobertura

| Forma | Cuándo encaja | Reparto aproximado |
| :--- | :--- | :--- |
| **Pirámide** | Backend con mucha lógica de dominio; librerías | Muchos unitarios, bastantes de integración, pocos E2E |
| **Trofeo** | Frontend o apps donde el riesgo está en la integración de piezas | Análisis estático + muchos tests de integración (componente con red simulada), menos unitarios y pocos E2E |
| **Diamante** | Microservicios o sistemas de integración | Pocos unitarios, muchos de integración y contrato, pocos E2E |
| **Pirámide invertida (anti-patrón)** | — | Casi todo E2E: lento, intermitente, caro de mantener |

Regla práctica: cada riesgo se cubre **en el nivel más bajo que lo detecta**. Un cálculo de impuestos se prueba con unitarios y tablas de decisión; que el impuesto aparezca en la factura, con integración; que el usuario pueda pagar, con un E2E.

## Automatizar, explorar o vigilar

| Tipo de verificación | Automatizar | Explorar | Vigilar en producción |
| :--- | :-: | :-: | :-: |
| Reglas de negocio y cálculos | ✅ | | |
| Regresión de flujos críticos | ✅ | | ✅ smoke tras desplegar |
| Contratos entre capas o servicios | ✅ | | |
| Usabilidad, textos, sensación de la interfaz | | ✅ | |
| Combinaciones nuevas, casos raros no imaginados | | ✅ | |
| Rendimiento real, errores en dispositivos reales | parcial (pruebas de carga) | | ✅ métricas, alertas, canary |

Lo que no se automatiza ni se vigila es un riesgo aceptado: se escribe en el plan.

## Criterios de terminado y de salida

**Definición de terminado de calidad (por historia o PR):**
- Criterios de aceptación con casos verificados (automatizados cuando el riesgo lo pide).
- Tests nuevos en el nivel adecuado, pasando en CI; ningún test desactivado sin issue.
- Casos negativos y límites de las validaciones nuevas.
- Sin nuevos avisos de tipos, lint o seguridad.

**Criterios de entrada a pruebas de release:** build desplegado en un entorno estable, datos de prueba preparados, cambios del release listados.

**Criterios de salida (go / no-go):**
- 0 defectos CRITICAL abiertos; HIGH abiertos solo con aceptación explícita y nominal.
- Flujos de riesgo ≥ 12 verificados en este build.
- Smoke y regresión automatizada en verde; tests intermitentes del release investigados, no reintentados.
- Plan de vuelta atrás conocido (y probado si hay migraciones).

## Trazabilidad

El nivel de detalle debe poder mantenerse:

| Equipo | Trazabilidad suficiente |
| :--- | :--- |
| Pequeño, despliegue continuo | El criterio de aceptación en la descripción del PR enlaza a los tests añadidos |
| Mediano | Etiquetas o nombres de test con el ID de la historia (`@US-123`), informe de CI agrupado |
| Regulado | Matriz requisito → caso → test → ejecución, generada desde herramientas, no a mano |

## Anti-patrones

| Anti-patrón | Problema | Alternativa |
| :--- | :--- | :--- |
| Objetivo de cobertura global (80 %) | Se prueba lo fácil para llegar al número | Cobertura por área según riesgo; cobertura del código cambiado |
| Plan de pruebas de 40 páginas | Nadie lo lee ni lo actualiza | Mapa de riesgos + criterios en una página |
| "QA lo prueba al final" | Los defectos llegan tarde y caros | Calidad en la definición de terminado de cada historia |
| Releases decididos por fecha sin criterios | Riesgos invisibles | Go / no-go con criterios escritos |
