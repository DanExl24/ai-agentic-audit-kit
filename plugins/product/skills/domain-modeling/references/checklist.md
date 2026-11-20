# Checklist de auditoría: modelo del dominio

Severidad orientativa; ajústala con [severity.md](../../../standards/severity.md).

## Glosario y lenguaje

- [ ] Existe un glosario con los términos principales, definición y ejemplo. **[MEDIUM; LOW en productos muy pequeños]**
- [ ] Cada término tiene un único significado en documentos, interfaz y código (o una correspondencia documentada). **[MEDIUM; HIGH si cambia el resultado de una regla de dinero o permisos]**
- [ ] No hay definiciones circulares ni términos clave sin definir. **[LOW–MEDIUM]**

## Modelo y estados

- [ ] Hay un modelo conceptual con entidades, relaciones y cardinalidades. **[MEDIUM]**
- [ ] El modelo usa conceptos del negocio, no detalles de persistencia. **[LOW]**
- [ ] Las entidades con estados tienen su ciclo de vida: transiciones, quién las provoca, guardas y transiciones prohibidas. **[MEDIUM; HIGH si el flujo principal depende de estados no definidos]**

## Reglas de negocio

- [ ] Las reglas están en un catálogo con IDs estables, no solo dentro de historias o del código. **[MEDIUM]**
- [ ] Cada regla es atómica y verificable: sin adjetivos sin cifra, con unidades. **[MEDIUM; HIGH en dinero, permisos o datos personales]**
- [ ] Cada regla tiene motivo, origen y estado. **[LOW–MEDIUM]**
- [ ] Las reglas con límites tienen ejemplos, incluidos los valores límite. **[MEDIUM]**
- [ ] Las excepciones están escritas dentro de la regla o como reglas propias. **[MEDIUM]**
- [ ] No hay reglas contradictorias entre sí ni entre módulos. **[HIGH en flujos principales; CRITICAL si afectan a dinero, datos o seguridad]**
- [ ] Las reglas implementadas coinciden con el código (archivo y símbolo enlazados). **[MEDIUM; HIGH si es una regla de seguridad o dinero distinta]**
- [ ] Las reglas inferidas del código están marcadas y tienen pregunta de confirmación cuando son dudosas. **[LOW–MEDIUM]**

## Cómo verificar

- Buscar catálogos (`reglas`, `business rules`, `RN-`), glosarios y diagramas en `docs/`.
- Para una muestra de reglas implementadas, abrir el archivo y el símbolo citados y comparar límites, condiciones y mensajes.
- Buscar el mismo concepto con nombres distintos en el código (`grep` de sinónimos) y en los textos de la interfaz.
