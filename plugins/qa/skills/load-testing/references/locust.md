# Notas: Locust

Scripts en Python; modelo **cerrado** por defecto (usuarios que repiten tareas). Encaja en equipos Python y cuando el escenario necesita lógica compleja.

## Usuario con mezcla de tareas

```python
# locustfile.py
import os
import random
from locust import HttpUser, task, between, events

PRODUCT_IDS = [line.strip() for line in open("data/product_ids.txt")]

class Shopper(HttpUser):
    wait_time = between(1, 4)          # think time

    def on_start(self):
        res = self.client.post("/api/auth/login", json={
            "email": os.environ["LOAD_USER"], "password": os.environ["LOAD_PASSWORD"],
        })
        self.client.headers["Authorization"] = f"Bearer {res.json()['token']}"

    @task(7)
    def view_product(self):
        pid = random.choice(PRODUCT_IDS)
        with self.client.get(f"/api/products/{pid}", name="/api/products/:id", catch_response=True) as res:
            if res.status_code != 200 or "price" not in res.json():
                res.failure("respuesta inesperada")

    @task(2)
    def search(self):
        self.client.get("/api/search", params={"q": random.choice(["mesa", "silla", "lámpara"])}, name="/api/search")

    @task(1)
    def checkout(self):
        self.client.post("/api/orders", json={"items": [{"id": random.choice(PRODUCT_IDS), "qty": 1}]}, name="/api/orders")
```

- `@task(peso)` define la mezcla; `name=` agrupa URLs con IDs.
- `catch_response=True` permite marcar como fallo una respuesta 200 con contenido incorrecto.

## Umbrales que fallan la ejecución

Locust no tiene umbrales declarativos; se comprueban al terminar y se fija el código de salida:

```python
@events.quitting.add_listener
def _(environment, **kwargs):
    stats = environment.stats.total
    if stats.fail_ratio > 0.01:
        environment.process_exit_code = 1
    elif stats.get_response_time_percentile(0.95) > 300:
        environment.process_exit_code = 1
```

## Ejecución

```bash
locust -f locustfile.py --headless -u 200 -r 20 -t 20m --host https://staging.example.com --csv results/run
```

- `-u` usuarios, `-r` usuarios nuevos por segundo, `-t` duración; `--csv` deja estadísticas y percentiles por endpoint.
- Formas de carga personalizadas (escalones, picos): una clase `LoadTestShape` con un `tick()` que devuelve `(usuarios, ritmo)`.
- Distribuido: un proceso `--master` y varios `--worker` cuando un solo proceso no genera suficiente carga (Locust usa un núcleo por proceso).

## Modelo abierto

Para aproximar llegadas constantes, `wait_time = constant_throughput(n)` (n tareas por segundo por usuario) con suficientes usuarios; si el objetivo principal es una tasa de llegadas exacta, k6 o Gatling lo modelan de forma más directa.
