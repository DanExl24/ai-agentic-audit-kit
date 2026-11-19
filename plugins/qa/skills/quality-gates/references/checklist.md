# Checklist de auditoría: puertas de calidad

Severidad orientativa; ajústala con [severity.md](../../../standards/severity.md).

## Etapas y bloqueo

- [ ] Los tests corren en cada PR y su fallo bloquea el merge (checks obligatorios). **[HIGH si los tests no bloquean o no corren en PR]**
- [ ] Cada riesgo alto tiene una etapa que lo verifica y bloquea. **[HIGH]**
- [ ] Hay smoke o comprobación tras desplegar que para o revierte el despliegue. **[MEDIUM]**
- [ ] Los jobs nocturnos que fallan generan trabajo con dueño. **[MEDIUM]**
- [ ] No hay `continue-on-error` / `allow_failure` en suites que deberían bloquear. **[HIGH si afecta a los tests principales]**

## Velocidad

- [ ] El pipeline de PR cabe en su presupuesto (≲ 15 min). **[MEDIUM]**
- [ ] Caché de dependencias, jobs en paralelo y sharding de las suites largas. **[LOW–MEDIUM]**
- [ ] Se cancelan ejecuciones obsoletas y hay timeouts por job. **[LOW]**

## Intermitencia

- [ ] Los reintentos (si existen) se informan como intermitentes, no como éxitos. **[MEDIUM; HIGH si esconden fallos en recorridos críticos]**
- [ ] Hay cuarentena con issue, responsable y caducidad, y no crece sin control. **[MEDIUM]**
- [ ] Los tests nuevos se repiten antes de aceptarse o la intermitencia se mide por semana. **[LOW–MEDIUM]**

## Umbrales e informes

- [ ] La cobertura que bloquea es la del código cambiado, no un total maquillable. **[MEDIUM]**
- [ ] Los umbrales no se bajan sin justificación registrada. **[LOW–MEDIUM]**
- [ ] Informes JUnit y artefactos de diagnóstico se suben también cuando el job falla. **[MEDIUM]**
- [ ] Sin secretos ni datos personales en logs o artefactos. **[HIGH; CRITICAL si se exponen credenciales de producción]**

## Datos, entornos y ramas

- [ ] Cada job usa servicios efímeros o datos aislados, no una base de datos compartida. **[MEDIUM]**
- [ ] La rama principal está protegida y los saltos de checks dejan rastro. **[HIGH si se puede hacer push directo sin checks]**
- [ ] CI detecta `test.only`, `describe.only` o tests desactivados sin issue. **[MEDIUM]**

## Cómo verificar

- Leer los archivos de pipeline y la configuración de protección de ramas (o preguntar al usuario si no hay acceso).
- Historial: duración media del pipeline de PR, % de ejecuciones con reintentos, merges con checks en rojo.
- Buscar `continue-on-error`, `allow_failure`, `retries`, `--passWithNoTests`, `|| true` en los pasos de test.
