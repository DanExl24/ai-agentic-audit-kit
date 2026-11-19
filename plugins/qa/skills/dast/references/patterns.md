# Patrones de seguridad dinámica

## Tipos de escaneo

| Tipo | Qué hace | Riesgo para el entorno | Dónde | Duración |
| :--- | :--- | :--- | :--- | :--- |
| **Pasivo (baseline)** | Navega (spider) y analiza respuestas sin atacar: cabeceras, cookies, divulgación de información, mezcla de contenidos | Bajo (solo peticiones normales) | Preview por PR, staging; producción solo con autorización explícita | Minutos |
| **Activo (completo)** | Envía ataques reales: inyecciones SQL y de comandos, XSS, path traversal, etc. | **Alto:** puede crear, modificar o borrar datos y degradar el servicio | Solo entornos aislados con datos de prueba | De 30 min a horas |
| **API** | Igual que el activo, guiado por la especificación OpenAPI (o GraphQL/SOAP) | Alto | Solo entornos aislados | Según el número de endpoints |

Orden recomendado: baseline primero; si está limpio o criban, activo contra staging.

## Alcance técnico

- **Incluir:** dominios y rutas de la aplicación; la especificación OpenAPI para no depender del spider.
- **Excluir** del escaneo activo: logout (cerraría la sesión), borrado de cuenta, acciones con efectos externos reales (pagos, emails, SMS), endpoints de administración peligrosos si no se quieren probar, dominios de terceros.
- **Límites de ritmo** (hilos, peticiones por segundo) para no saturar el entorno.

## Escaneo autenticado

Sin autenticación, el escáner solo ve la página de login. Opciones, de más simple a más completa:

| Opción | Cuándo |
| :--- | :--- |
| **Cabecera fija** (token de una cuenta de prueba inyectado en cada petición) | APIs con bearer token; la más sencilla y estable |
| **Cookie de sesión** obtenida por un script antes del escaneo | Apps web con sesión por cookie |
| **Contexto de autenticación de la herramienta** (formulario, script, verificación de sesión iniciada o cerrada) | Cuando la sesión caduca durante el escaneo o hay varios roles |

- Una cuenta de prueba **por rol** (usuario, admin) para encontrar fallos de autorización entre roles.
- Los tokens de prueba vienen de secretos de CI y caducan; nunca credenciales reales.

## Reglas y falsos positivos

- Cada alerta tiene un nivel de acción: **FAIL** (bloquea), **WARN** (avisa) o **IGNORE**.
- Un IGNORE o una supresión **lleva justificación escrita** (por qué no aplica en este sistema) y, si es temporal, fecha de revisión.
- Falsos positivos habituales: cabeceras en recursos estáticos que no las necesitan, "divulgación" de versiones que son públicas por diseño, alertas sobre rutas de terceros.
- Revisar periódicamente la lista de ignorados: lo que era falso positivo puede dejar de serlo.

## Integración en CI

| Etapa | Escaneo | Bloquea |
| :--- | :--- | :--- |
| PR (contra el preview del PR) | Baseline | Sí, en alertas de nivel FAIL |
| Nocturno o semanal (contra staging) | Completo o API, autenticado | Abre issues; bloquea el release si hay hallazgos confirmados altos |
| Antes de un release importante | Completo autenticado + revisión manual de lo encontrado | Criterio de salida |

Los informes (HTML, JSON) se guardan como artefactos; sin tokens ni datos sensibles dentro.

## Criba y verificación

1. Agrupa las alertas por tipo y por causa (una cabecera ausente en todas las rutas es **un** hallazgo).
2. Para cada alerta de riesgo medio o alto, **reprodúcela** con una petición (`curl` o el propio escáner) y confirma el impacto.
3. Clasifica con la escala del kit (impacto real en este sistema), no con el nivel de riesgo genérico de la herramienta.
4. Documenta: alerta y referencia (CWE, ID de la regla), URL, petición y respuesta, impacto, corrección y skill destino.
5. Tras corregir, repite el escaneo dirigido a esa ruta para cerrar el hallazgo.

## DAST, SAST, SCA y secretos

| Técnica | Qué mira | Encuentra bien | No ve |
| :--- | :--- | :--- | :--- |
| **SAST** (análisis estático) | El código | Patrones inseguros, flujos de datos | Configuración real del despliegue |
| **SCA** (dependencias) | Manifiestos y lockfiles | Vulnerabilidades conocidas en librerías | Si el código usa la parte vulnerable |
| **Detección de secretos** | Repositorio e historial | Claves y tokens versionados | Secretos inyectados en ejecución |
| **DAST** | La aplicación en marcha | Cabeceras, cookies, errores, inyecciones explotables, configuración del proxy | Código que el escáner no alcanza |

Juntas cubren más que cada una por separado; DAST no sustituye a una prueba de intrusión manual en sistemas de alto riesgo.

## Anti-patrones

| Anti-patrón | Problema | Alternativa |
| :--- | :--- | :--- |
| Escaneo activo contra producción | Datos corrompidos, caídas | Entorno aislado con datos de prueba |
| Escanear sistemas sin autorización | Riesgo legal y de bloqueo | Permiso y alcance por escrito |
| Escaneo sin autenticación | Solo prueba la página de login | Cuentas de prueba por rol |
| Ignorar alertas sin justificar | Vulnerabilidades escondidas | Supresión con motivo y revisión |
| Copiar el informe de la herramienta tal cual | Ruido y severidades genéricas | Criba, verificación y escala del kit |
| Un escaneo antes del lanzamiento y nunca más | Envejece con cada despliegue | Baseline continuo y completo programado |
