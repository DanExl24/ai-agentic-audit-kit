# Notas: Gatling

Simulaciones en Java, Kotlin o Scala que corren en la JVM; modelos abierto y cerrado explícitos, aserciones que fallan el build e informes HTML detallados. Encaja en equipos JVM y en CI con Maven o Gradle.

## Simulación con modelo abierto (DSL de Java)

```java
// src/test/java/simulations/CheckoutSimulation.java
package simulations;

import static io.gatling.javaapi.core.CoreDsl.*;
import static io.gatling.javaapi.http.HttpDsl.*;

import io.gatling.javaapi.core.*;
import io.gatling.javaapi.http.*;
import java.time.Duration;

public class CheckoutSimulation extends Simulation {

  HttpProtocolBuilder httpProtocol = http
      .baseUrl(System.getProperty("baseUrl", "http://localhost:8080"))
      .acceptHeader("application/json");

  FeederBuilder<String> products = csv("data/products.csv").random();

  ScenarioBuilder shopper = scenario("Comprador")
      .exec(http("login")
          .post("/api/auth/login")
          .body(StringBody("{\"email\":\"#{loadUser}\",\"password\":\"#{loadPassword}\"}")).asJson()
          .check(jsonPath("$.token").saveAs("token")))
      .feed(products)
      .exec(http("ver producto")
          .get("/api/products/#{id}")
          .header("Authorization", "Bearer #{token}")
          .check(status().is(200), jsonPath("$.price").exists()))
      .pause(Duration.ofSeconds(1), Duration.ofSeconds(4));

  {
    setUp(
        shopper.injectOpen(
            rampUsersPerSec(1).to(50).during(Duration.ofMinutes(5)),
            constantUsersPerSec(50).during(Duration.ofMinutes(15))))
        .protocols(httpProtocol)
        .assertions(
            global().responseTime().percentile(95.0).lt(300),
            global().failedRequests().percent().lt(1.0));
  }
}
```

- `injectOpen` (llegadas por segundo) frente a `injectClosed` (usuarios concurrentes): elige según el sistema.
- Feeders (`csv`, `jsonFile`, generadores) para datos distintos en cada usuario; `.random()`, `.circular()` o `.queue()`.
- Las credenciales (`loadUser`, `loadPassword`) se inyectan en la sesión desde variables de entorno o un feeder fuera del repositorio, no en el código.
- Las aserciones incumplidas hacen fallar la ejecución (y el build).

## Ejecución

```bash
mvn gatling:test -Dgatling.simulationClass=simulations.CheckoutSimulation -DbaseUrl=https://staging.example.com
./gradlew gatlingRun --simulation simulations.CheckoutSimulation
```

El informe HTML queda en `target/gatling/` o `build/reports/gatling/`: percentiles por petición, distribución de tiempos y peticiones activas en el tiempo.

## Otros

- `group("catálogo") { ... }` para agrupar peticiones y poner aserciones por grupo (`details("catálogo")`).
- `throttle(...)` limita el throughput máximo independientemente de la inyección.
- Smoke en CI: una simulación con `atOnceUsers(1)` o pocos usuarios y las mismas aserciones.
