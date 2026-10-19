# 📋 Checklist Forense — Rendimiento, Carga y Concurrencia (Performance & Load Specialist)

- [ ] **1. Contratos de Nivel de Servicio (SLAs y Umbrales p95/p99)**
  - ¿Existen umbrales cuantificados para el percentil 95 (p95 < 200-500ms) y percentil 99 (p99 < 1000ms) en rutas de lectura y escritura?
  - ¿Se define un umbral máximo de tasa de fallo tolerable (menor al 1% de errores HTTP 5xx bajo carga nominal)?
  - ¿Se monitorean métricas de throughput (solicitudes por segundo - RPS) esperadas en horas pico?

- [ ] **2. Concurrencia y Gestión de Pools de Recursos**
  - ¿El pool de conexiones a base de datos tiene límites configurados (`max`, `min`, `idleTimeoutMillis`, `connectionTimeoutMillis`) acordes al hardware y número de instancias?
  - ¿Se garantiza la liberación inmediata de conexiones y cursores incluso cuando una petición es abortada o lanza una excepción no controlada?
  - ¿Las operaciones asíncronas no concurrentes están acotadas (ej. `Promise.all` acotado con `p-limit` o chunks para evitar saturar el stack de red)?

- [ ] **3. Protección del Event Loop y Uso de Memoria**
  - ¿El servidor procesa payloads grandes mediante streams en vez de cargarlos completos en búferes de memoria RAM?
  - ¿Se evitan bucles anidados $O(n^2)$ o expresiones regulares catastróficas (ReDoS) en el procesamiento de requests concurrentes?
  - ¿Se detectan posibles fugas de memoria (variables en closures de larga duración, listeners de eventos no removidos)?

- [ ] **4. Modelado Realista de Carga con k6**
  - ¿Los scripts de prueba incorporan fases de calentamiento (*warm-up*), rampa de subida escalonada (*ramp-up*) y rampa de bajada (*ramp-down*)?
  - ¿Se simula aleatoriedad y variabilidad en los datos de entrada (IDs distintos, tokens de usuario diversos) para evitar sesgos de caché artificial en disco o memoria?
  - ¿Se incluye *think-time* realista (`sleep(Math.random() * 2 + 1)`) entre interacciones para reflejar el comportamiento real de usuarios humanos?
