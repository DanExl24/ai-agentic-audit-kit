# 📋 Checklist Forense — Testabilidad y Pruebas Unitarias (Testability & Unit Specialist)

- [ ] **1. Inversión de Dependencias y Desacoplamiento de Infraestructura**
  - ¿La lógica de negocio recibe sus colaboradores (repositorios, clientes HTTP, colas, reloj) vía constructor o parámetros, sin instanciarlos internamente con `new`?
  - ¿Existen interfaces o tipos abstractos para cada dependencia externa, permitiendo sustituirlos por mocks o test-doubles en memoria?
  - ¿La clase/módulo puede ser probado al 100% en un entorno aislado sin conexión a red ni base de datos activa?

- [ ] **2. Determinismo Temporal y Aislamiento de Efectos Secundarios**
  - ¿Las funciones que calculan fechas o plazos aceptan un proveedor de tiempo inyectable en lugar de invocar directamente `Date.now()` o `datetime.now()`?
  - ¿Las funciones son puras en la medida de lo posible, evitando mutar argumentos recibidos por referencia o depender de estado estático global?
  - ¿La suite de pruebas puede ejecutarse en orden aleatorio y en paralelo sin que una prueba afecte o contamine a otra?

- [ ] **3. Solidez y Calidad de las Aserciones**
  - ¿Cada test valida explícitamente el resultado esperado con aserciones rigurosas de igualdad o coincidencia de esquema, descartando chequeos superficiales (`toBeDefined()`, `toBeTruthy()`)?
  - ¿Se verifica el comportamiento ante ramas de error (excepciones lanzadas, tipos de error personalizados, códigos HTTP esperados)?
  - ¿La suite carece totalmente de tests tautológicos o pruebas que pasan independientemente del resultado de la operación?

- [ ] **4. Resistencia al Refactor y Mantenibilidad**
  - ¿Las pruebas evalúan contratos públicos y comportamiento de entrada/salida en lugar de inspeccionar variables o métodos privados?
  - ¿La relación entre líneas de configuración de mocks y líneas de aserción es equilibrada (menos de 15 líneas de setup por test)?
  - ¿La suite se ejecuta en menos de 100ms por archivo de prueba para garantizar retroalimentación instantánea en el bucle de desarrollo TDD?
