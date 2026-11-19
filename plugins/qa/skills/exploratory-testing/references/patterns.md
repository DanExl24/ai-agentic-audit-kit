# Patrones de pruebas exploratorias

## Charters

Formato: **Explorar** <área> **con** <recursos, datos o heurística> **para descubrir** <tipo de información>.

| Bueno | Malo |
| :--- | :--- |
| Explorar el checkout **con** cupones caducados, combinados y de otro país **para descubrir** descuentos aplicados mal | Probar el checkout |
| Explorar la edición de perfil **con** dos pestañas abiertas y la red lenta **para descubrir** pérdidas de datos o estados inconsistentes | Ver si el perfil funciona |
| Explorar el panel de administración **con** un usuario de rol "lector" **para descubrir** acciones que no debería poder hacer | Revisar permisos |

Un charter cabe en una sesión; si no, se divide.

## Heurísticas

| Heurística | Qué hacer | Encuentra |
| :--- | :--- | :--- |
| **CRUD completo** | Crear, leer, editar, borrar y volver a crear el mismo elemento; editar lo borrado desde otra pestaña | Restos de datos, unicidad, cachés obsoletas |
| **Interrupciones** | Recargar a mitad de flujo, botón atrás, cerrar la pestaña, perder la red, dejar caducar la sesión | Estados a medias, dobles envíos, pérdidas de datos |
| **Datos extremos** | Vacíos, muy largos, Unicode y emojis, espacios, cero, negativos, fechas límite, archivos enormes o de tipo falso | Validaciones, desbordes, errores 500 |
| **Concurrencia** | Dos pestañas o dos usuarios sobre el mismo recurso; doble clic rápido | Condiciones de carrera, duplicados |
| **Roles y permisos** | Repetir el flujo con cada rol; cambiar IDs en la URL | Accesos indebidos (IDOR), botones visibles sin permiso |
| **Estados** | Recorrer el ciclo de vida y forzar saltos (cancelar algo ya pagado) | Transiciones prohibidas posibles |
| **Configuraciones** | Idioma, zona horaria, tema oscuro, tamaño de pantalla, zoom al 200 % | Textos rotos, fechas desplazadas, layouts |
| **Tour del dinero** | Seguir todo lo que suma, resta o cobra | Redondeos, totales incoherentes |
| **Tour del nuevo usuario** | Usar la app sin datos previos, sin onboarding | Estados vacíos, dependencias ocultas |
| **Comparación** | La misma acción por dos caminos (lista y detalle, web y API) | Inconsistencias |

## Notas de sesión

```markdown
# Sesión — <charter>
- Fecha, duración, entorno, build, rol de usuario
- Cobertura: <qué se probó, con qué datos y heurísticas>
- Bugs: <IDs de los reportes>
- Preguntas: <comportamientos dudosos para negocio>
- Riesgos y siguientes pasos: <qué merece un test automatizado o otra sesión>
```

## Reporte de bug

```markdown
### <Título: qué falla, dónde y en qué condición>
- **Entorno:** <URL/entorno, build o commit, navegador y dispositivo, rol>
- **Pasos para reproducir:**
  1. …
  2. …
- **Resultado esperado:** <qué debería pasar, según qué regla>
- **Resultado real:** <qué pasa>
- **Frecuencia:** siempre / intermitente (n de m intentos)
- **Evidencia:** captura, vídeo, petición y respuesta de red, consola
- **Severidad:** <impacto, con la escala del kit> · **Prioridad:** <cuándo arreglarlo>
- **Notas:** <datos de prueba usados, cómo minimizar el caso>
```

Un buen reporte es **mínimo** (el menor número de pasos que reproduce el fallo), **concreto** (datos reales usados) y **verificable** (esperado con su fuente).

## Severidad frente a prioridad

| | Prioridad alta | Prioridad baja |
| :--- | :--- | :--- |
| **Severidad alta** | Cobro duplicado en el checkout: arreglar ya | Fallo grave en una función que casi nadie usa: planificar |
| **Severidad baja** | Errata en el nombre de la empresa en la portada: arreglar ya | Desalineación de 2 px en una pantalla interna: oportunista |

La severidad la decide el impacto (escala del kit); la prioridad, negocio con esa información.

## Informe de sesión

```markdown
# Exploración — <área o release>
| Charter | Duración | Bugs (por severidad) | Cobertura | Riesgos pendientes |
| :--- | :-: | :--- | :--- | :--- |

## Bugs encontrados
<lista con enlace a cada reporte>

## Propuestas de automatización
<bugs o comportamientos que merecen test, con el nivel sugerido>

## Preguntas abiertas
<para producto o negocio>
```
