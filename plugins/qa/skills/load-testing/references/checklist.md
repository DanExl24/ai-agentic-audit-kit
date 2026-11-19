# Checklist de auditoría: pruebas de carga

Severidad orientativa; ajústala con [severity.md](../../../standards/severity.md).

## Objetivo y seguridad

- [ ] Cada prueba tiene una pregunta y umbrales derivados de SLO o expectativas de negocio. **[MEDIUM]**
- [ ] Se ejecuta contra un entorno propio y autorizado; los terceros se simulan. **[HIGH si se carga producción o un servicio de terceros sin autorización]**
- [ ] Los sistemas críticos para el negocio (pagos, lanzamientos) tienen alguna prueba de carga antes de picos previstos. **[HIGH si se espera un pico y no hay ninguna verificación]**

## Diseño

- [ ] El modelo de carga encaja con el sistema (abierto para APIs públicas). **[MEDIUM]**
- [ ] La mezcla de operaciones refleja el tráfico real o esperado. **[MEDIUM]**
- [ ] Los datos están parametrizados (usuarios, IDs, búsquedas distintos). **[MEDIUM]**
- [ ] Hay think time en los escenarios de usuarios; la autenticación se reutiliza por usuario virtual. **[LOW–MEDIUM]**
- [ ] Las respuestas se comprueban (estado y contenido), no solo el tiempo. **[MEDIUM]**

## Ejecución e interpretación

- [ ] El entorno es representativo o la diferencia está documentada. **[MEDIUM]**
- [ ] El generador de carga no está saturado y corre fuera del sistema bajo prueba. **[MEDIUM]**
- [ ] Se observan métricas del servidor y de la base de datos durante la prueba. **[MEDIUM]**
- [ ] Los resultados se expresan en percentiles y tasa de errores, con conclusión respecto a la pregunta. **[MEDIUM]**
- [ ] La duración es acorde al tipo (resistencia ≥ 2 h). **[LOW–MEDIUM]**

## Automatización

- [ ] Hay un smoke de rendimiento con umbrales en CI o programado. **[LOW–MEDIUM]**
- [ ] Los scripts están versionados junto al código y se mantienen cuando cambia la API. **[LOW]**

## Cómo verificar

- Buscar scripts: `*.k6.js`, `load/`, `perf/`, `locustfile.py`, `src/test/**/simulations`, `*Simulation.java|scala`.
- Revisar en el script: umbrales (`thresholds`, `assertions`, código de salida), fuentes de datos, pausas, ejecutor o modelo de inyección.
- Si se puede ejecutar: solo un smoke (1–2 usuarios, 1 minuto) contra un entorno autorizado por el usuario, nunca una prueba completa sin acordarlo.
