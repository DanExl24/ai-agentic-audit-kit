---
name: dast
description: "Planifica, ejecuta y audita pruebas de seguridad dinámicas (DAST) contra una aplicación en marcha, con OWASP ZAP como herramienta principal: alcance y autorización por escrito, entorno aislado, escaneo pasivo (baseline), activo (completo) y de API a partir de OpenAPI, escaneo autenticado, reglas y supresión justificada de falsos positivos, integración en CI (baseline en PR, completo programado), verificación manual de los hallazgos y relación con SAST, SCA y detección de secretos. Úsala antes de publicar, para añadir seguridad dinámica al pipeline o para verificar en ejecución lo que el código promete. No para revisar la seguridad en el código (backend:api-security, frontend:security) ni para pruebas de intrusión manuales completas."
---

# Seguridad dinámica (DAST)

Leer el código dice cómo **debería** comportarse la aplicación; un escaneo dinámico comprueba cómo **se comporta de verdad** en ejecución: qué cabeceras envía el servidor real (no las del middleware que se olvidó registrar), qué devuelve un error 500, si una cookie lleva sus atributos tras pasar por el proxy, qué responde la API ante entradas maliciosas. Es un complemento de la revisión de código, no un sustituto.

## Cuándo usarla

- Antes de publicar una aplicación o una versión con cambios de seguridad.
- Añadir seguridad dinámica al pipeline (baseline en PR, completo programado).
- Verificar en ejecución lo que las skills de código dicen (cabeceras, cookies, CORS, errores).
- Auditar la configuración y los resultados de un DAST existente.

**No es para:** revisar autenticación, autorización o inyecciones en el código → `backend:authentication`, `backend:authorization`, `backend:api-security`, `frontend:security` · pruebas de intrusión manuales completas o red team (requieren un profesional y un contrato) · escaneo de dependencias y secretos → `frontend:tooling`, `backend:tooling`.

## Paso 0: alcance y autorización (obligatorio, ambos modos)

1. **Autorización:** solo se escanean aplicaciones **del usuario o con permiso escrito de su propietario**, con el alcance (dominios, rutas, entornos) acordado. Sin esto, no se ejecuta nada: un escaneo activo contra un sistema ajeno puede ser ilegal.
2. **Entorno:** el escaneo **activo** envía ataques reales (inyecciones, formularios con datos basura) y puede **modificar o borrar datos y saturar el servicio**: solo en un entorno aislado (local, preview, staging) con datos de prueba y copia de seguridad. En producción, como mucho el escaneo **pasivo** y con autorización explícita.
3. **Aviso:** el equipo de operaciones o seguridad sabe cuándo se escanea (para que no lo confundan con un ataque) y qué IP lo hace.
4. **Cuentas de prueba** por rol para el escaneo autenticado, nunca cuentas reales.
5. **Herramienta:** OWASP ZAP; carga [zap.md](references/zap.md). Si el proyecto usa otra (Burp, Nuclei), aplica [patterns.md](references/patterns.md) con ella.
6. Si existe `.sdlc/context.md`, léelo y respeta sus convenciones y decisiones ([context.md](../../standards/context.md)).

## Modo Construir

1. **Elige el tipo de escaneo** según el objetivo y el entorno. Ver [patterns.md § Tipos](references/patterns.md#tipos-de-escaneo).
2. **Alcance técnico:** URL base, rutas incluidas y excluidas (logout, borrado de cuenta, endpoints de pago reales), especificación OpenAPI para APIs.
3. **Autenticación** para cubrir lo que hay tras el login. Ver [patterns.md § Escaneo autenticado](references/patterns.md#escaneo-autenticado).
4. **Reglas:** qué alertas fallan, cuáles avisan y cuáles se ignoran **con justificación escrita**. Ver [patterns.md § Reglas](references/patterns.md#reglas-y-falsos-positivos).
5. **Integración en CI:** baseline en cada PR contra el entorno de preview; completo programado contra staging. Ver [patterns.md § CI](references/patterns.md#integración-en-ci).
6. **Ejecuta, verifica a mano** los hallazgos relevantes (reproducir con una petición) y clasifica. Ver [patterns.md § Criba](references/patterns.md#criba-y-verificación).
7. Entrega según [output-formats.md § Construir](../../standards/output-formats.md#modo-construir): configuración, informe cribado y handoffs de corrección.

## Modo Auditar

1. Revisa si existe DAST, qué tipo, contra qué entorno, con qué frecuencia y si está autenticado.
2. Revisa las reglas ignoradas y su justificación, y si los hallazgos se corrigen o se acumulan.
3. Si el usuario autoriza un escaneo, empieza por el **baseline (pasivo)** contra un entorno no productivo.
4. Recorre [checklist.md](references/checklist.md).
5. Clasifica con [severity.md](../../standards/severity.md) y entrega según [output-formats.md § Auditar](../../standards/output-formats.md#modo-auditar) con código `QA-DAST`. Las vulnerabilidades confirmadas se documentan con la petición que las reproduce y su referencia (CWE, alerta de ZAP).

## Principios

1. **Autorización y alcance por escrito** antes de cualquier escaneo.
2. **El escaneo activo solo en entornos aislados** con datos de prueba.
3. **Autenticado o incompleto:** lo importante suele estar tras el login.
4. **Cada alerta se verifica** antes de declararla vulnerabilidad; cada supresión, se justifica.
5. **DAST complementa al código,** no lo sustituye: la corrección se hace en la causa raíz con la skill de código.
6. **Continuo:** un escaneo único envejece con el siguiente despliegue.

## Handoffs

Según [handoffs.md](../../standards/handoffs.md): profundidad máxima de 2, alcance acotado, sin reinvocar skills ya aplicadas y registro de pendientes.

| Disparador (observable) | Skill | Alcance y contexto que se pasa |
| :--- | :--- | :--- |
| Cabeceras de seguridad ausentes, errores 500 con trazas o CORS permisivo en las respuestas reales | `backend:http-layer` | Alertas, URLs y respuestas observadas |
| Inyecciones, SSRF, subida de archivos o exposición de datos confirmadas | `backend:api-security` | Petición que lo reproduce y endpoint |
| Cookies de sesión sin `HttpOnly`/`Secure`/`SameSite`, login sin límite de intentos | `backend:authentication` | Cookies, endpoints y respuestas |
| Acceso a recursos de otro usuario o rol durante el escaneo autenticado | `backend:authorization` | Rol, recurso y petición |
| CSP ausente o permisiva, XSS reflejado o basado en DOM | `frontend:security` | Páginas, alertas y carga útil |
| El escaneo debe convertirse en puerta de CI | `quality-gates` | Tipo de escaneo, reglas y etapa |

## Referencias

| Archivo | Cuándo cargarlo |
| :--- | :--- |
| [patterns.md](references/patterns.md) | Siempre: tipos de escaneo, alcance, autenticación, reglas, CI, criba y relación con SAST y SCA. |
| [zap.md](references/zap.md) | Con OWASP ZAP. |
| [checklist.md](references/checklist.md) | Modo Auditar. |

## Skills relacionadas

- `backend:api-security`, `backend:http-layer`, `backend:authentication`, `frontend:security`: la corrección en el código.
- `quality-gates`: dónde corre el escaneo y qué bloquea.
- `frontend:tooling` y `backend:tooling`: SAST, SCA y secretos.
