# Checklist de auditoría: estrategia de pruebas

Severidad orientativa; ajústala con [severity.md](../../../standards/severity.md).

## Riesgo y cobertura

- [ ] Existe un mapa de riesgos (escrito o reconstruible) con las áreas críticas identificadas. **[MEDIUM; HIGH si hay áreas de dinero, permisos o datos personales sin identificar]**
- [ ] Cada área de riesgo alto tiene un control automatizado o una verificación explícita. **[HIGH; CRITICAL si mueve dinero o permisos y no hay ningún control]**
- [ ] La cobertura no se concentra en áreas triviales mientras las críticas están vacías. **[MEDIUM]**
- [ ] La forma de la cobertura encaja con el proyecto (no casi todo E2E, no cero integración en un sistema de integraciones). **[MEDIUM]**
- [ ] Los riesgos aceptados están escritos, con quién los aceptó. **[LOW–MEDIUM]**

## Criterios

- [ ] Hay una definición de terminado que incluye calidad (casos de aceptación, negativos, tests en CI). **[MEDIUM]**
- [ ] Los releases tienen criterios de salida escritos y se aplican. **[HIGH si se publica sin criterios en un producto con usuarios]**
- [ ] Los tests desactivados o intermitentes tienen issue y dueño. **[MEDIUM]**

## Trazabilidad y aprendizaje

- [ ] Los criterios de aceptación se pueden seguir hasta sus tests al nivel que el equipo mantiene. **[LOW–MEDIUM]**
- [ ] Los defectos escapados a producción actualizan el mapa de riesgos o los tests. **[MEDIUM]**
- [ ] Lo que no se automatiza se explora o se vigila en producción de forma deliberada. **[MEDIUM]**

## Cómo verificar

- Inventario rápido: contar tests por tipo y carpeta (`**/*.test.*`, `**/*.spec.*`, `e2e/`), leer la configuración de CI.
- Historial: `git log --oneline --grep="fix" -- <ruta>` por área para estimar la probabilidad.
- Último release: buscar notas, checklist o issue de release y comprobar qué se verificó.
