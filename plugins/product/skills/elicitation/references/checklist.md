# Checklist de auditoría: levantamiento de requisitos

Severidad orientativa; ajústala con [severity.md](../../../standards/severity.md).

## Interesados

- [ ] Hay un mapa de interesados con rol, interés e influencia, incluidos sistemas y normativa relevantes. **[MEDIUM; no es hallazgo en un proyecto de una sola persona sin usuarios externos]**
- [ ] Está identificado quién decide ante requisitos en conflicto. **[MEDIUM; HIGH si hay conflictos abiertos sin decisor]**
- [ ] Se consultó a quien usará el producto, no solo a quien lo pide. **[MEDIUM–HIGH en productos con usuarios externos]**

## Origen y registro

- [ ] Cada requisito tiene origen (interesado, documento, código). **[MEDIUM]**
- [ ] Lo inferido del código o de documentos está marcado y tiene pregunta de confirmación. **[LOW–MEDIUM; HIGH si afecta a dinero, permisos o datos personales]**
- [ ] Las preguntas abiertas tienen responsable, fecha y estado. **[MEDIUM]**
- [ ] Las decisiones tienen contexto, opciones, motivo, quién decidió y fecha. **[MEDIUM]**

## Calidad de lo levantado

- [ ] Las excepciones y casos límite del proceso están levantados, no solo el camino normal. **[MEDIUM; HIGH en flujos de dinero o permisos]**
- [ ] Hay números donde importan (volúmenes, plazos, límites, importes). **[MEDIUM]**
- [ ] No hay requisitos contradictorios entre documentos o entre documentos y código sin una pregunta abierta. **[HIGH en flujos principales; MEDIUM en secundarios]**
- [ ] Los conflictos entre interesados están registrados con su resolución o su pregunta. **[MEDIUM]**

## Cómo verificar

- Buscar actas, notas, documentos de requisitos, `docs/`, tickets con etiquetas de requisitos.
- Muestrear 5–10 requisitos y comprobar si se puede saber de dónde salen.
- Comparar reglas documentadas con validaciones del código (límites, permisos, estados).
