# Rutas de auditoría de QA

Cada ruta es una secuencia de skills aplicadas en modo Auditar sobre el mismo alcance. Las áreas que no aplican al contexto (Paso 0) se saltan y se declaran.

## Pilares de madurez

| Pilar | Qué mide | Áreas (skills) |
| :--- | :--- | :--- |
| **1. Estrategia y diseño** | Se decide qué probar según el riesgo y los casos encuentran defectos | `test-strategy`, `test-design` |
| **2. Automatización por niveles** | Tests fiables en cada capa y recorridos críticos de punta a punta | `frontend:testing`, `backend:testing`, `e2e` |
| **3. Pipeline y puertas** | Las pruebas corren donde y cuando deben y bloquean lo que deben | `quality-gates` |
| **4. Calidad en ejecución** | Rendimiento y seguridad verificados contra la aplicación en marcha | `load-testing`, `dast` |
| **5. Exploración y aprendizaje** | Se busca lo que nadie automatizó y se aprende de los defectos | `exploratory-testing`, `defect-analysis` |

## Selección rápida

| Petición | Ruta |
| :--- | :---: |
| "¿Cómo estamos de calidad y pruebas?" / línea base | 0 |
| "¿Está listo este release?" | 1 |
| "Los bugs vuelven" / "se nos escapan defectos a producción" | 2 |
| "El pipeline es lento" / "los tests fallan a ratos y nadie se fía" | 3 |
| "¿Aguanta y es seguro en ejecución?" antes de exponerlo | 4 |
| "No sabemos qué probar" / "tenemos tests pero no detectan nada" | 5 |

---

## Ruta 0 — Madurez integral

```text
1. test-strategy        → riesgos, forma de la cobertura, DoD y criterios de salida
2. test-design          → calidad de los casos (muestra)
3. frontend:testing     (si hay frontend y el plugin está instalado)
4. backend:testing      (si hay backend y el plugin está instalado)
5. e2e
6. quality-gates
7. load-testing         (si aplica)
8. dast                 (si aplica)
9. exploratory-testing
10. defect-analysis
```
**Cuándo:** línea base de un proyecto, antes de invertir en calidad o para comparar en el tiempo. Entrega la madurez por pilares y global.

## Ruta 1 — Control previo a un release

```text
test-strategy (criterios de salida) → quality-gates (checks en verde y obligatorios) → e2e (recorridos críticos) → exploratory-testing (sobre lo que cambió) → load-testing / dast (si el release los requiere)
```
**Cuándo:** antes de publicar. Entrega un **sí/no por bloque** y los riesgos aceptados.

## Ruta 2 — Regresiones y defectos escapados

```text
defect-analysis → test-strategy (mapa de riesgos con los hotspots) → test-design (casos de no regresión) → quality-gates (dónde se habrían detectado)
```
**Cuándo:** "este bug ya lo habíamos arreglado", defectos frecuentes en producción, tras un defecto grave.

## Ruta 3 — Pipeline e intermitencia

```text
quality-gates → e2e → frontend:testing / backend:testing (tests intermitentes de su capa)
```
**Cuándo:** pipeline lento, fallos ignorados, reintentos hasta que pasa, cuarentenas sin caducidad.

## Ruta 4 — Calidad en ejecución

```text
load-testing → dast → quality-gates (smoke de rendimiento y baseline en CI)
```
**Cuándo:** antes de exponer una aplicación o de un pico de tráfico. Solo se audita la configuración salvo autorización expresa para ejecutar.

## Ruta 5 — Cimientos

```text
test-strategy → test-design → frontend:testing / backend:testing
```
**Cuándo:** hay tests pero no detectan defectos, o no se sabe por dónde empezar.

---

## Escalado a otros dominios

| Problema | Dónde |
| :--- | :--- |
| Defectos en el código del cliente (seguridad, estado, accesibilidad) | plugin `frontend` (`frontend:audit` o la skill concreta) |
| Defectos en el código del servidor (seguridad, datos, contratos) | plugin `backend` (`backend:audit` o la skill concreta) |
| Contratos divergentes o un fallo que cruza capas | plugin `fullstack` (`contracts`, `flow-diagnosis`) |
| Incidentes de operación, SLO, guardias, despliegue | futuros dominios SRE y DevOps |
