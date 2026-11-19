# Patrones de puertas de calidad

## Etapas

| Etapa | Qué corre | Presupuesto | Bloquea |
| :--- | :--- | :-: | :-: |
| **Local / pre-commit** | Formato, lint de lo cambiado, tests unitarios afectados | < 1 min | No (ayuda) |
| **Pull request** | Lint, tipos, unitarios, integración, contrato, E2E críticos (o afectados), escaneo de dependencias | **< 10–15 min** | **Sí** |
| **Merge a la rama principal** | Lo del PR sobre el resultado del merge (o cola de merge), build del artefacto | < 15 min | Sí (despliegue) |
| **Nocturno** | E2E completa en varios navegadores, mutación, carga ligera, DAST completo, tests de larga duración | Horas | Abre issue, avisa |
| **Release** | Regresión completa, criterios de salida (`test-strategy`) | Lo necesario | Sí (go / no-go) |
| **Tras desplegar** | Smoke (`e2e`), comprobaciones de salud, métricas del canary | < 5 min | Revierte o para el despliegue |

Regla: cada riesgo alto tiene al menos una etapa que lo verifica **y bloquea**. Lo nocturno que falla genera trabajo con dueño, no un email que nadie lee.

## Velocidad

| Técnica | Efecto |
| :--- | :--- |
| Caché de dependencias y de builds | Minutos menos por job |
| Jobs en paralelo (lint, unitarios, integración a la vez) | El pipeline dura lo que el job más largo |
| Sharding de suites largas (E2E, integración) | Reparte una suite en N máquinas |
| Selección de tests afectados (`nx affected`, `turbo --filter`, `vitest --changed`, `jest --changedSince`, `playwright --only-changed`) | En PR solo lo que el cambio puede romper; la suite completa al hacer merge o por la noche |
| Filtros por rutas | No correr la suite del backend si solo cambió documentación |
| Cancelar ejecuciones obsoletas del mismo PR | No gastar máquinas en commits ya superados |
| Timeouts por job | Un job colgado no bloquea horas |

Medir antes de optimizar: duración por job y por test (los 10 tests más lentos suelen ser la mitad del tiempo).

## Política de intermitencia

1. **Detección:** el informe distingue "pasó al reintentar" (intermitente) de "pasó"; ejecución repetida de tests nuevos o modificados antes de aceptarlos (burn-in: 5–10 repeticiones).
2. **Cuarentena:** el test intermitente se marca (etiqueta o lista), sigue ejecutándose pero no bloquea, y **tiene issue, responsable y fecha de caducidad** (p. ej. 2 semanas). Al caducar: se corrige o se borra.
3. **Reintentos:** como mucho 1–2 y solo con informe que marque el test como intermitente. Nunca reintentos que convierten el rojo en verde sin rastro, ni "re-run job" manual como costumbre.
4. **Métrica:** tasa de intermitencia por suite y semana; objetivo < 1 % de ejecuciones.

## Umbrales

| Umbral | Recomendación |
| :--- | :--- |
| Cobertura total del repositorio | Informativa, no bloqueante (se maquilla con tests sin valor) |
| **Cobertura del código cambiado** (diff) | Bloqueante en PR, p. ej. ≥ 80 % de las líneas nuevas, con excepciones justificadas |
| **Mutación incremental** en módulos críticos | Informativa o bloqueante en dominio y cálculos; sobre lo cambiado para que sea asumible |
| Tiempo de la suite | Alerta si supera el presupuesto |
| Nuevos avisos de seguridad (dependencias, secretos) | Bloqueantes según severidad |

Un umbral que se baja cada vez que molesta no es un umbral: documenta quién puede cambiarlo y por qué.

## Informes y artefactos

- **JUnit XML** de cada suite para el resumen en el PR (la plataforma muestra qué tests fallaron).
- **Informes HTML, trazas, capturas y vídeos** de E2E como artefactos, con retención limitada.
- Subir artefactos **también cuando el job falla** (condición `always`).
- Sin secretos ni datos personales en logs ni artefactos.

## Datos y entornos de prueba

- Servicios efímeros por job (base de datos, caché, colas en contenedor) en lugar de una base de datos compartida.
- Migraciones y siembra reproducibles al arrancar el job.
- Entornos de preview por PR para E2E contra el código del PR.
- Datos de prueba sintéticos; nunca copias de producción sin anonimizar (`backend:data-privacy`).

## Protección de la rama principal

- Checks obligatorios: los jobs bloqueantes del PR (por nombre estable).
- Ramas actualizadas con la principal antes del merge, o cola de merge.
- Sin push directo; las excepciones (administradores) dejan rastro y se revisan.
- Los tests desactivados (`skip`, `only` olvidado) se detectan en CI.

## Anti-patrones

| Anti-patrón | Problema | Alternativa |
| :--- | :--- | :--- |
| Todo en un job secuencial de 40 min | Nadie espera | Paralelo, sharding, afectados |
| Reintentar hasta que pase | Bugs escondidos | Cuarentena visible con caducidad |
| Umbral global de cobertura | Tests sin valor para cumplir | Cobertura del diff + mutación en lo crítico |
| Nocturno que falla siempre | Ruido ignorado | Issue automática con dueño o eliminar el job |
| Base de datos de pruebas compartida | Interferencias entre jobs | Servicios efímeros por job |
| `continue-on-error` en suites "importantes" | Nunca bloquean | Bloquear o declararlas informativas |
