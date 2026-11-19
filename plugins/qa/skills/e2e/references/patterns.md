# Patrones de suites E2E

## Qué merece E2E

| Sí | No (bájalo de nivel) |
| :--- | :--- |
| Registro, login y recuperación de cuenta | Cada mensaje de validación de un formulario → componente |
| Recorrido de compra o pago completo | Cálculo de importes con muchas combinaciones → unitario |
| Crear, editar y borrar la entidad principal del producto | Estados de carga y error de un componente → componente con red simulada |
| Permisos: un rol no puede ver o hacer algo (un par de casos representativos) | Matriz completa de permisos → integración en el backend |
| Integración entre capas que nada más verifica | Formatos del contrato → `fullstack:contracts` y tests de contrato |

Orden de magnitud sano: decenas de tests E2E, no cientos; la suite completa en menos de 10–15 minutos con paralelismo.

## Estructura

```text
e2e/
├── fixtures/          # datos, usuarios autenticados, páginas (extensiones del test)
├── pages/             # page objects ligeros, solo para interacciones repetidas
├── journeys/          # un archivo por recorrido (checkout.spec.ts, auth.spec.ts)
└── setup/             # autenticación inicial, siembra global si hace falta
```

- **Fixtures** para lo que cada test necesita (un usuario con sesión, un pedido creado): se declaran y se limpian solas.
- **Page objects ligeros:** métodos de intención (`checkout.payWith(card)`), sin aserciones escondidas ni herencias profundas. Si un page object tiene 50 métodos, sobra.
- El test se lee como el recorrido: `dado` (fixtures), `cuando` (acciones), `entonces` (aserciones visibles para el usuario).

## Localizadores y esperas

Prioridad de localizadores:

1. **Rol y nombre accesible:** botón "Pagar", campo "Correo electrónico".
2. **Etiqueta o texto visible.**
3. **`data-testid`** cuando no hay rol o texto estable (iconos, listas dinámicas).
4. Nunca: clases de estilo (`.btn-primary`, clases de Tailwind), XPath posicional, `nth-child`.

Esperas:

- Aserciones que reintentan hasta cumplirse (`toBeVisible`, `toHaveText`) en lugar de comprobar una vez.
- Esperar respuestas de red concretas cuando la UI depende de ellas, no un tiempo.
- `sleep`/`waitForTimeout`/`cy.wait(3000)` solo como diagnóstico temporal, nunca en la suite.

## Datos y aislamiento

- Cada test **crea sus datos** por API (o base de datos) en su preparación: usuario, pedido, producto. Nada de depender de "el usuario de prueba que alguien creó a mano".
- **Datos únicos** por test (sufijos aleatorios o del worker) para poder correr en paralelo.
- **Limpieza:** borrar lo creado en la fixture o usar un entorno efímero que se descarta.
- Ningún test depende del orden ni del resultado de otro.
- Endpoints o comandos de siembra **solo en entornos de prueba**, protegidos y desactivados en producción.

## Autenticación

- Un test cubre el **login real por la interfaz** (y el logout, y el error de credenciales).
- El resto **reutiliza la sesión**: login por API una vez por rol, se guarda el estado (cookies, almacenamiento) y se carga en cada test.
- Usuarios por rol (admin, lector, otro tenant) como fixtures.

## Red: qué simular

| Se usa lo real | Se simula |
| :--- | :--- |
| Backend propio, base de datos de prueba | Pasarelas de pago (modo test del proveedor o simulación), email, SMS |
| Flujos de autenticación propios | Fallos difíciles de provocar (500, timeouts) en tests específicos de resiliencia |
| | Servicios de terceros lentos o con límites de uso |

Si se simula el backend propio, ya no es E2E: es un test de componente o de integración del frontend.

## Entornos

| Entorno | Para qué |
| :--- | :--- |
| Local (la herramienta arranca app y API) | Desarrollo de los tests, ejecución antes de subir |
| Preview efímero por PR | Suite completa contra el código del PR con datos limpios |
| Staging | Regresión antes del release, datos más realistas |
| Producción | Solo smoke de solo lectura o con cuentas de prueba |

## Intermitencia

| Causa | Síntoma | Corrección |
| :--- | :--- | :--- |
| Espera fija o comprobación sin reintento | Falla en CI lento | Aserciones que reintentan, esperar la respuesta de red |
| Datos compartidos entre tests | Falla en paralelo o según el orden | Datos propios y únicos por test |
| Animaciones y transiciones | Clic en un elemento que se mueve | Desactivar animaciones en el entorno de test, esperar al estado estable |
| Carrera real en la aplicación | Falla también para usuarios, a veces | Es un bug de la app → `fullstack:flow-diagnosis` |
| Dependencia externa inestable | Fallos agrupados en el tiempo | Simularla o aislarla en tests de resiliencia |
| Reloj y zona horaria | Falla a ciertas horas o fechas | Fijar el reloj o la zona en el test |

Política: un test intermitente se **pone en cuarentena con issue y fecha de caducidad** (ver `quality-gates`), se investiga con su traza y se corrige o se elimina. Los reintentos automáticos solo se aceptan si el informe marca el test como intermitente.

## Smoke tras desplegar

- 3–10 tests etiquetados (`@smoke`) de los recorridos vitales: la app carga, se puede iniciar sesión, la página principal muestra datos, el checkout llega hasta el pago (sin pagar).
- De solo lectura o con cuentas de prueba marcadas; sin efectos irreversibles en producción.
- Corre tras cada despliegue y bloquea o revierte si falla.

## Regresión visual y accesibilidad

- **Visual:** capturas comparadas de pantallas clave; ejecutar siempre en el mismo sistema y navegador (contenedor) para evitar diferencias de renderizado; enmascarar fechas y datos dinámicos.
- **Accesibilidad:** pasar axe en los estados principales de cada recorrido; los fallos se tratan con `frontend:accessibility`. No sustituye a la revisión manual.

## Anti-patrones

| Anti-patrón | Problema | Alternativa |
| :--- | :--- | :--- |
| Cientos de E2E que prueban validaciones | Suite lenta e intermitente | Bajar a componente o unitario |
| Login por la interfaz en cada test | Lento y frágil | Sesión reutilizada |
| Tests encadenados (el 2 usa lo que creó el 1) | Orden obligatorio, sin paralelismo | Datos propios por test |
| Selectores por clases CSS | Se rompen con cada cambio de estilo | Rol, etiqueta, texto, `data-testid` |
| `sleep(3000)` | Lento y aun así intermitente | Esperar condiciones |
| Reintentos silenciosos | Esconden bugs reales | Cuarentena visible e investigación |
| Simular el backend propio | Ya no prueba la integración | Backend real; simular solo terceros |
