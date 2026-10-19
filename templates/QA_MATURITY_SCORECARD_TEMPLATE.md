# 📊 QA & Testing Maturity Scorecard

> **Propósito:** Evaluar y calificar cuantitativamente (de 0 a 100 puntos) la madurez de las prácticas de calidad de software, testabilidad y resiliencia de un repositorio o sistema bajo auditoría.

---

## 🎯 Resumen Ejecutivo de Madurez

| Métrica Global | Puntuación Obtenida | Nivel de Madurez | Estado de CI/CD |
| :--- | :--- | :--- | :--- |
| **Score Total QA** | `[SCORE_GLOBAL] / 100` | `[NIVEL_ALCANZADO]` | `[BLOQUEANTE / ADVISORY / INEXISTENTE]` |

### Escala de Madurez:
- **0 – 39 Puntos:** **Nivel 1 — Caótico / Reactivo.** Pruebas inexistentes o decorativas, acoplamiento extremo, regresiones frecuentes en producción.
- **40 – 69 Puntos:** **Nivel 2 — Básico / En Transición.** Tests unitarios presentes pero frágiles, aserciones superficiales, validaciones manuales de release.
- **70 – 89 Puntos:** **Nivel 3 — Maduro / Proactivo.** Arquitectura desacoplada y testeable, contratos DTO validados, suites E2E estables con localizadores semánticos.
- **90 – 100 Puntos:** **Nivel 4 — World-Class / Continuo.** TDD internalizado, umbrales p95/p99 en CI, escaneos DAST automáticos y ciclos Kaizen sistemáticos.

---

## 🔬 Evaluación Detallada por Pilares (20 Puntos c/u)

### Pilar 1: Testabilidad y Desacoplamiento Arquitectónico (`[P1_SCORE] / 20`)
- [ ] Inversión de dependencias (DI) en capas de negocio y servicios (+5)
- [ ] Determinismo temporal (reloj y dependencias no deterministas inyectables) (+5)
- [ ] Aislamiento de colaboradores externos (fácil sustitución por stubs/fakes) (+5)
- [ ] Baja complejidad ciclomática (< 10 por método) (+5)

### Pilar 2: Calidad y Rigor de Pruebas Unitarias (`[P2_SCORE] / 20`)
- [ ] Ausencia total de tests sin aserciones (*assertion-free*) o tautológicos (+5)
- [ ] Aserciones exhaustivas sobre el estado resultante y ramas de error (+5)
- [ ] Pruebas orientadas al comportamiento observable y no a métodos privados (+5)
- [ ] Ejecución ultrarrápida (< 100ms por suite en local) (+5)

### Pilar 3: Contratos DTO y Resiliencia de Suites E2E (`[P3_SCORE] / 20`)
- [ ] Validación de contratos en tiempo de ejecución (Zod / TypeBox / Pydantic) (+5)
- [ ] Uso exclusivo de localizadores semánticos accesibles (`getByRole`, etc.) (+5)
- [ ] Erradicación total de `sleep()` o esperas de tiempo fijo (cero flakiness) (+5)
- [ ] Cobertura explícita de valores límite (BVA) y códigos de error HTTP 4xx/5xx (+5)

### Pilar 4: Rendimiento Operativo y Seguridad Dinámica DAST (`[P4_SCORE] / 20`)
- [ ] Definición y verificación de SLAs p95 / p99 en endpoints transaccionales (+5)
- [ ] Existencia de scripts de carga k6 automatizados con escenarios escalonados (+5)
- [ ] Bastionado de cabeceras HTTP (`CSP`, `HSTS`, `X-Frame-Options`, `nosniff`) (+5)
- [ ] Protección contra fuerza bruta (rate-limiting) y enmascaramiento de trazas 500 (+5)

### Pilar 5: Cultura Kaizen y Automatización en CI/CD (`[P5_SCORE] / 20`)
- [ ] Canalización de CI/CD con ejecución de pruebas bloqueante previo al merge (+5)
- [ ] Registro y análisis forense de causa raíz (Ishikawa) en incidentes mayores (+5)
- [ ] Identificación y resolución sistemática del 20% crítico según Pareto (+5)
- [ ] Matriz de acciones correctivas con seguimiento y KPIs de regresión (+5)

---

## 📈 Conclusiones y Próximos Pasos Prioritarios
1. **Acción Inmediata (Quick Win):** `[DETALLAR_QUICK_WIN]`
2. **Refuerzo de Suite Crítica:** `[DETALLAR_SUITE_A_REFORZAR]`
3. **Revisión de Arquitectura:** `[DETALLAR_REFACTOR_TESTABILIDAD]`
