# Patrones de pruebas de carga

## Tipos de prueba

| Tipo | Pregunta | Forma de la carga | Duración |
| :--- | :--- | :--- | :--- |
| **Smoke** | ¿El script funciona y el sistema responde sin errores con carga mínima? | 1–5 usuarios | 1–2 min |
| **Carga** | ¿Cumple los SLO con el tráfico normal esperado? | Subida gradual hasta el nivel esperado y meseta | 15–60 min |
| **Estrés** | ¿Cómo se degrada por encima de lo esperado y se recupera? | Escalones por encima del nivel esperado | 20–60 min |
| **Pico** | ¿Aguanta una subida brusca (campaña, notificación masiva)? | Salto repentino y vuelta | 10–20 min |
| **Resistencia (soak)** | ¿Se degrada con el tiempo (fugas, conexiones, colas)? | Nivel normal sostenido | 2–12 h |
| **Punto de ruptura** | ¿Dónde está el límite de capacidad? | Subida continua hasta incumplir umbrales | Hasta romper |

Empieza siempre por el smoke; no tiene sentido un estrés con un script que falla.

## Modelo de carga

| Modelo | Qué controla | Cuándo |
| :--- | :--- | :--- |
| **Abierto** (tasa de llegadas) | Peticiones o iteraciones por segundo, independientemente de lo que tarde el sistema | APIs públicas y webs: los usuarios llegan aunque el sistema vaya lento. Es el que revela la saturación real |
| **Cerrado** (usuarios concurrentes) | N usuarios que repiten el escenario; si el sistema va lento, llegan menos peticiones | Sistemas con un número fijo de clientes (terminales, empleados, jobs) |

Error típico: probar una API pública con modelo cerrado; cuando el sistema se ralentiza, la carga baja sola y parece que aguanta.

Conversión orientativa (ley de Little): usuarios concurrentes ≈ llegadas por segundo × (tiempo de respuesta + think time).

## Escenarios realistas

- **Mezcla de operaciones** según el tráfico real: si el 70 % son lecturas de catálogo, el 20 % búsquedas y el 10 % compras, el script respeta esas proporciones (pesos por tarea o escenarios separados).
- **Datos parametrizados:** usuarios, IDs y búsquedas distintos en cada iteración (ficheros CSV o JSON, generadores). Con el mismo ID siempre, solo se prueba la caché.
- **Think time** entre acciones de un mismo usuario (aleatorio, p. ej. 1–5 s) en modelos cerrados.
- **Autenticación** como en la realidad: login una vez por usuario virtual y reutilización del token, no un login por petición (salvo que se pruebe el login).
- **Correlación:** extraer valores dinámicos (IDs creados, tokens CSRF) de las respuestas y reutilizarlos.
- **Terceros simulados** (pagos, email, SMS) para no generar costes ni bloqueos.

## Umbrales

Derivados de los SLO, por endpoint o grupo cuando tengan objetivos distintos:

| Métrica | Ejemplo |
| :--- | :--- |
| Latencia p95 / p99 | p95 < 300 ms, p99 < 800 ms en lecturas; p95 < 800 ms en escrituras |
| Tasa de errores | < 1 % (y 0 % de errores 5xx en el smoke) |
| Throughput alcanzado | ≥ 95 % de la tasa objetivo (si no, el generador o el sistema no llegan) |
| Comprobaciones funcionales | > 99 % de respuestas con el contenido esperado |

Los umbrales hacen que la herramienta **termine con código de error**, lo que permite usarla como puerta en CI.

## Entorno

- **Representativo:** misma topología y tamaños proporcionales a producción (número de instancias, tamaño de la base de datos, configuración de pools); si es más pequeño, dilo y extrapola con prudencia.
- **Datos:** volumen realista en la base de datos; una tabla con 100 filas no muestra los problemas de una con 10 millones.
- **Generador de carga:** fuera del sistema bajo prueba, con CPU y red suficientes; si su CPU pasa del ~80 %, los resultados no son fiables (reparte entre varias máquinas).
- **Aislamiento y aviso:** sin otras pruebas a la vez, con el equipo de operaciones avisado y las alertas identificadas.

## Observar durante la prueba

Del lado del sistema, como mínimo: CPU y memoria por instancia, conexiones y tiempos de la base de datos, pool de conexiones, longitud de colas, tasa de errores y latencia del servidor, recolección de basura o event loop (→ `backend:observability`). Sin esto, la prueba dice "se degradó a 300 usuarios" pero no por qué.

## Interpretación

- **Percentiles, no medias:** una media de 120 ms puede esconder un p99 de 4 s.
- **Punto de inflexión:** la carga a partir de la cual la latencia sube rápido o aparecen errores; la capacidad útil está por debajo.
- **Saturación:** qué recurso llega primero al límite (CPU, conexiones de base de datos, un servicio externo, el pool de hilos) → `backend:performance`.
- **Recuperación:** tras el estrés o el pico, ¿vuelve la latencia a la normalidad? Si no, hay colas, fugas o bloqueos.
- **Errores:** clasifícalos (timeouts, 5xx, 429 por rate limiting propio, errores del generador).
- **Duración suficiente:** una prueba de 2 minutos no muestra fugas ni efectos de caché fría y caliente.

## Informe

```markdown
# Prueba de carga — <sistema> — <fecha>
- Pregunta: <qué se quería saber>
- Entorno: <dónde, tamaño respecto a producción, autorización>
- Escenario: <tipo, modelo, mezcla, datos, duración>
- Umbrales: <SLO usados>

| Nivel de carga | RPS logrados | p95 | p99 | Errores | Observación del sistema |
| :--- | :-: | :-: | :-: | :-: | :--- |

## Conclusión
<respuesta a la pregunta; capacidad útil; recurso que satura primero>

## Siguientes pasos
<correcciones (→ backend:performance), repetir tras corregir, puerta de CI>
```

## Anti-patrones

| Anti-patrón | Problema | Alternativa |
| :--- | :--- | :--- |
| Sin umbrales | Nadie sabe si "pasó" | Umbrales de los SLO que hacen fallar la prueba |
| Mismos datos en cada iteración | Solo se mide la caché | Datos parametrizados |
| Sin think time en modelo cerrado | Carga irreal y concentrada | Pausas aleatorias entre acciones |
| Modelo cerrado para una API pública | La carga baja cuando el sistema se ralentiza | Modelo abierto (tasa de llegadas) |
| Medias en lugar de percentiles | Esconde la cola de latencia | p95 y p99 |
| Generador en la misma máquina que el sistema | Compiten por recursos | Generador separado y vigilado |
| Probar contra producción o terceros sin permiso | Caídas, costes, bloqueos | Entorno propio autorizado y terceros simulados |
| Conclusiones de 2 minutos de prueba | Sin efectos de tiempo | Duración acorde al tipo |
