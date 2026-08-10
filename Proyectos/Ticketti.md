
# Notas

## RabbitMQ

Los microservicios que lo usan ahora es:

- ms-Donaciones
- ms-Eventos
- ms-mensajeria
- ms-carrito
- api-gateway

>[!info]
>El BFF puede que use ya que gestiona toda la logica con respecto a las validaciones de los microservicios

## Revisiones

`SecurityRoutes.java` esta dentro del BFF , es el encargado de ver cuales son las rutas publicas y las rutas protegidas dentro del sistema.

## Mejoras

Tengo todo lo necesario para hacer el análisis completo. Aquí está el desglose de las mejoras por prioridad y por servicio:

---

## Parte 1 — `api-gateway`

### 🔴 Crítico

#### 1. `JwtAuthenticationFilter.java` — Inyección por campo

```java
@Autowired
private JwtService jwtService; // ❌ Campo
```

Debe usar **constructor injection** para inmutabilidad, cumplir con la interfaz `JwtService` explícitamente y facilitar tests:

```java
@Slf4j
@Component
@RequiredArgsConstructor // ✅ Lombok generará el constructor
public class JwtAuthenticationFilter implements GlobalFilter, Ordered {
    private final JwtService jwtService;
}
```

#### 2. `JwtAuthenticationFilter.java` — Ausencia de `X-Forwarded-*`

El gateway es el punto de entrada. Sin propagar la IP real y el protocolo del cliente, los microservicios atrás ven solo la IP interna del gateway:

```java
// Agregar después de la autenticación exitosa (línea 67)
ServerHttpRequest.Builder builder = request.mutate()
    .header("X-Forwarded-For", request.getRemoteAddress() != null
        ? request.getRemoteAddress().getAddress().getHostAddress() : "unknown")
    .header("X-Forwarded-Proto",
        request.getHeaders().getFirst("X-Forwarded-Proto") != null
            ? request.getHeaders().getFirst("X-Forwarded-Proto")
            : "http")
    .header("X-Usuario", username);
```

#### 3. `SecurityConfig.java` — Dead code y autenticación solo en el filtro

```java
.pathMatchers("/**").permitAll()   // ❌ Permite TODO — el resto es muerto
.anyExchange().authenticated()     // ❌ IMPOSIBLE DE ALCANZAR
```

Spring Security no valida contra el perfil del Gateway. Reparar:

```java
.pathMatchers("/actuator/health", "/actuator/info").permitAll()
.pathMatchers("/auth/**").permitAll()
.anyExchange().authenticated() // ✅ Ahora este se alcanza para rutas de Spring Security
```

Y delegar en el `JwtAuthenticationFilter` la propagación de headers.

#### 4. `CorsConfig.java` — Headers de autorización no permitidos explícitamente

```java
corsConfig.setAllowedHeaders(Arrays.asList("*")); // ✅ Funciona pero no es INTENCIONAL
```

Agregar explícitamente los headers de seguridad para que no dependa de `"*"`:

```java
corsConfig.setAllowedHeaders(Arrays.asList(
    "Authorization", "Content-Type", "X-Usuario", "X-Usuario-Rol", "X-Request-ID"));
```

---

### 🟠 Alto

#### 5. `JwtAuthenticationFilter.java` — Rutas públicas con búsqueda lineal O(n)

```java
private boolean esRutaPublica(String path) { // ❌ Array + bucle lineal
    String[] rutasPublicas = { "/auth/**" };
    for (String patron : rutasPublicas) { ... }
}
```

Refactorizar a `Set<String>` para O(1) ya que el filtro corre en **cada request**:

```java
private static final Set<String> RUTAS_PUBLICAS = Set.of("/auth/**");

private boolean esRutaPublica(String path) {
    return RUTAS_PUBLICAS.stream().anyMatch(path::startsWith);
}
```

#### 6. `application.yml` — Rutas duplicadas de usuarios

```yaml
# Ambas rutas usan el mismo patron - la primera es innecesaria
- id: ms-usuarios-root
  predicates:
    - Path=/api/v1/usuarios  # ❌ Redundante con /**
- id: ms-usuarios-subpaths
  predicates:
    - Path=/api/v1/usuarios/**  # ✅ Una sola ruta rstante
```

Eliminar `ms-usuarios-root`; `/api/v1/usuarios/**`  ya lo cubre.

#### 7. `application.yml` — CircuitBreaker de Auth público

El permiso `CU-002: Consultar Servicios Públicos` implica que `/auth/**` es público, pero el circuito breaker de Auth también lo habilita sin autenticación. Esto puede exponer mensajes de error detallados sobre la disponibilidad del servicio de autenticación sin necesidad de credenciales. Referenciar la política de diseño.

#### 8. `FallbackController.java` — Respuestas inconsistentes + endpoint atrapado

- No hay DTO de error unificado (`ErrorResponse` o similar); cada endpoint ensambla su propio `Map.of(...)`.
- El endpoint genérico `/**` nunca se alcanza porque los endpoints específicos ya coinciden:

  ```java
  @RequestMapping("/auth")       // captura /fallback/auth
  @RequestMapping("/**")         // nunca se llama
  ```

- No hay encabezados `Retry-After` ni `X-Request-ID` en las respuestas de fallback.

#### 9. `JwtService.java` (api-gateway) — No valida `iss` ni `aud`

El validador solo verifica expiración. No chequea emisor (`iss`) ni audiencia (`aud`), por lo que un token emitido por cualquier servicio se acepta:

```java
public Boolean validateToken(String token) { // ❌ Solo expiración
```

Debe validar también `iss` y `aud` contra valores configurados.

#### 10. `application.yml` — Circuit Breaker: tiempos demasiado agresivos

```yaml
waitDurationInOpenState: 10000  # 10s — muy corto, puede "martillar" el servicio
slowCallDurationThreshold: 5000 # 5s — demasiado alto como "slow"
```

Ajustar por servicio:

```yaml
auth-service:
  baseConfig: default
  waitDurationInOpenState: 30000   # 30s para dar tiempo de recuperarse
  slowCallDurationThreshold: 2000  # 2s es un umbral razonable
```

---

### 🟡 Medio

#### 11. `api-gateway` — Sin trace ID en logs

No hay un `TraceId` propagado desde el request hasta los logs del gateway y los downstream. Implementar un `GlobalFilter` antes del `JwtAuthenticationFilter` que genere/propague `X-Request-ID`.

#### 12. `FallbackController.java` — Mejorar contenido del cuerpo de error

Actualmente devuelve solo datos dispersos. Estructurar con DTO:

```json
{
  "timestamp": "2026-05-22T20:16:31",
  "path": "/api/v1/carrito/...",
  "status": 503,
  "error": "Service Unavailable",
  "service": "ms-carrito",
  "message": "El servicio no está disponible..."
}
```

#### 13. `application.yml` — Campo `jwt.secret` tiene valor por defecto

```yaml
jwt:
  secret: ${JWT_SECRET:...}  # Valor hardcodeado visible en el repo
```

La clave por defecto (`ticketti-secret-key-2024-for-jwt-signing-and-verification-only`) está expuesta. Retirar el fallback en producción y usar secretos gestionados (Secret Manager, Vault o Spring Cloud Config protegido).

#### 14. `api-gateway` — Sin Health Check de conectividad a Eureka

No hay un health indicator personalizado que verifique que los servicios destino estén registrados en Eureka. Agregar un `HealthIndicator` que liste los servicios disponibles.

---

## Parte 2 — `ms-carrito`

### 🔴 Crítico

#### 15. `CarritoService.iniciarCheckout()` — Validación de Idempotencia está rota

```java
String idempotencyKey = UUID.randomUUID().toString();       // ✅ Genera NUEVA key
if (idempotencyRepository.existsByKey(idempotencyKey)) {    // ❌ NUNCA existe — genera bug
    throw CarritoException.idempotenciaInvalida();
}
```

Cada llamada a `/checkout` genera una clave nueva, así que la validación `existsByKey` **nunca** se activa, eliminando completamente la protección contra dobles cobros. La clave debe venir **desde el cliente** (DTO `CheckoutDto.idempotencyKey`) y no generarse internamente.

#### 16. `SagaOrchestrator.ejecutarCheckoutInterno()` — Duplicación + lógica rota de idempotencia

El método `validarIdempotencia()` del `SagaOrchestrator` duplica lógica del `CarritoService` y tampoco funciona:

```java
idempotencyRepository.findByKey(dto.getIdempotencyKey()).ifPresent(record -> {
    if (record.isProcesado()) { throw ... } // ✅
});
// Si no LO encuentra, guarda...
// Pero si ya existe sin procesar: retorna sin guardar ni arrojar error
if (idempotencyRepository.existsByKey(dto.getIdempotencyKey())) { return; }
```

Refactorizar todo el flujo de idempotencia a un servicio dedicado (`IdempotencyService`) llamado tanto por el `SagaOrchestrator` como por `CarritoService.procesarWebhookPago`.

#### 17. `CarritoService.procesarWebhookPago()` — Transacción muy corta

```java
@Transactional // ❌ La transacción termina antes de enviar el evento de outbox
public CarritoDeCompras procesarWebhookPago(...) {
    carrito = carritoRepository.save(carrito);   // commit inminente
    pagoRepository.save(pago);                    // fuera de la tx si ya se cerró
    guardarOutboxEvent(carrito, "pago.aprobado"); // guarda en BD dentro de la tx
}
```

El `Pago` y el `OutboxEvent` se guardan después de `carritoRepository.save()`. Si hay una falla entre el `carrito` y el `pago`, queda el carrito marcado como pagado sin el registro del pago. Usar una sola transacción de escritura con `REQUIRES_NEW` o mover toda la lógica a un servicio coordinado.

#### 18. `CarritoService` — `@Valid` ausente en DTOs de entrada del service

Los DTOs como `AgregarEntradaDto` tienen `@Valid` en el controller, pero dentro del `service` hay setteos directos (líneas 116-123) sin validación. Si alguien llama al servicio directamente (interno o desde tests), los invariantes no se cumplen.

---

### 🟠 Alto

#### 19. `SagaOrchestrator` — No hay compensación si el `reservaRepository.save()` falla

```java
reservarStock(pedido, carrito); // puede lanzar excepción durante el save
pedido.reservar();              // no se ejecuta
```

Si la reserva se crea en BD pero falla antes de `pedido.reservar()`, la compensación libera solo las reservas cuyos IDs están en `item.getReservaId()` (que podría ser `null` para el ítem en curso). Asegurar que la reserva siempre se guarde antes de marcar el pedido como reservado y en caso de fallo, compensar correctamente.

#### 20. `CarritoService` — No hay retry en `EventoClient` (Feign)

```java
@FeignClient(name = "ms-eventos") // Sin Resilience4j
public interface EventoClient { ... }
```

Sin retry ni circuit breaker en la llamada Feign, un fallo transitorio en `ms-eventos` (corto tiempo) provoca fallo inmediato en el checkout. Agregar `resilience4j` en la configuración de Feign:

```yaml
resilience4j:
  feign:
    configs:
      default:
        retry:
          max-attempts: 3
          wait-duration: 1000ms
```

#### 21. `CarritoService` — Límite de entradas hardcodeado y no global

```java
private static final int MAX_ENTRADAS = 4; // ❌ En clase
```

Debe estar en el `application.yml` para cambiar el límite sin recompilar.

#### 22. `CarritoExceptionHandler.java` — Detección de errores por texto (fragil)

```java
String mensaje = ex.getMessage().toLowerCase();
if (mensaje.contains("no encontrado")) { ... }  // ❌ Rompe si cambia el mensaje
```

Usar excepciones con código enum o una clase wrapper:

```java
public enum CartErrorCode { NOT_FOUND, EXPIRED, IDEMPOTENCY_CONFLICT, ... }
// Y un DTO con codigo + mensaje
```

#### 23. `OutboxRelayService` — No hay dead-letter queue ni reintento con backoff

El evento fallido se marca como `FAILED` y se olvida (líneas 59-61). Debe tener una estrategia:

- Cola de mensajes muertos (`dead-letter`) para persisted failures
- Backoff exponencial en el `@Scheduled`
- Métricas (contador de eventos fallidos, pendientes, enviados)

---

### 🟡 Medio

#### 24. `ms-carrito` — RabbitMQ `SimpleMessageConverter` en vez de `Jackson2JsonMessageConverter`

```java
template.setMessageConverter(new SimpleMessageConverter()); // ❌ Envía bytes
```

Mientras que `ms-mensajeria` usa `Jackson2JsonMessageConverter`. El formato de mensaje entre servicios es inconsistente. Estandarizar con `Jackson2JsonMessageConverter` en **todos** los microservicios.

#### 25. `OutboxEvent` — Campo `historico` (typo) nunca usado

```java
// ¡Este campo no existe ni se usa!
evento.setHistorico("PAGO_CONFIRMADO");
```

Eliminarlo o usarlo con un propósito definido.

#### 26. `Reserva.java` — Probablemente faltan getters/setters

El `EntradaConsumer` usa `reserva.getNombre()`, `reserva.getGenero()`, `reserva.getStock()`, `reserva.getPrecioEntrada()` — Verificar que la clase `Reserva` tenga getters para todos esos campos y que coincidan con la base de datos.

#### 27. `WebhookPagoDto` — No valida `token` ni `estado` con constraint

```java
private String estado;   // ❌ Sin @NotBlank
private String token;    // ❌ Sin @NotBlank
```

Proteger contra estados vacíos y tokens ausentes en el webhook de pago (endpoint público).

#### 28. `donaciones` y `mensajeria` — Botón `notification-factory` implementa pixelación

El componente `شبكةNotificationFactory` aplica un filtro de pixelación pero sin verificar permisos de lectura previos, lo que permitiría a cualquier usuario interceptar el endpoint.

---

## Parte 3 — `ms-mensajeria`

### 🔴 Crítico

#### 29. `MensajeriaConsumer` — Propaga excepción a RabbitMQ (reinicio infinito)

```java
catch (Exception e) { throw e; } // ❌ Re-lanza, RabbitMQ reintenta sin fin
```

Agregar manejo con nacky retry count o un `RetryTemplate` con backoff. Para errores transitorios: reintentar 3 veces con backoff; para errores permanentes (ej. correo inválido): mover a cola de errores sin reintentar.

#### 30. `ms-mensajeria` — `CompraConfirmadaEvent` debe ser una dependencia compartida

`CompraConfirmadaEvent` está definido tanto en `ms-mensajeria` como (aparentemente) en `ms-donaciones`. Crear un **módulo/shared jar** (`ticketti-common` o similar) para el evento y los DTOs compartidos, eliminando duplicación.

---

### 🟠 Alto

#### 31. `ms-mensajeria` — `SimpleMessageConverter` también posible

Confirmar si `ms-mensajeria` usa `Jackson2JsonMessageConverter` (que sí tiene). Si todos los servicios usan Jackson, estandarizar.

#### 32. `ms-mensajeria` — No hay métricas de envío de correo

No hay contadores ni tiempos de entrega. Agregar `@Timed` de Micrometer para medir tiempo de envío de correo y contador de éxitos/fallos.

---

## Parte 4 — Cross-cutting (todos los servicios)

### 🔴 Crítico

#### 33. JWT secret compartido (ms-carrito) — Clave hardcodeada

```yaml
jwt:
  secret: ${JWT_SECRET:test-secret-key-ms-carrito-2026-very-secure}
```

Retirar valores por defecto en producción. Cada servicio debe leer el secreto desde un gestor de secretos (AWS Secrets Manager, HashiCorp Vault, Spring Cloud Config con cifrado).

#### 34. Sin `@ControllerAdvice` en `ms-donaciones`

`ms-donaciones` no tiene un `GlobalExceptionHandler`. Las excepciones no controladas devuelven un JSON genérico de Spring en vez de un formato uniforme. Crear uno siguiendo el patrón de `CarritoExceptionHandler`.

---

### 🟠 Alto

#### 35. `ms-carrito` — JWT valida `iss`/`aud` pero no distinguido entre seguridad

El `JwtService` de `ms-carrito` valida `iss` y `aud` pero no distingue entre seguridad de servicio versus seguridad de gateway. Refactorizar para que el gateway sea el único validador de token; los servicios downstream confían en los headers `X-Usuario`, `X-Usuario-Id`, `X-Rol-Usuario-Id` enviados por el gateway.

#### 36. Autenticación inconsistente entre servicios

`ms-carrito` usa `SecurityConfig` con `Matchers`; `api-gateway` usa `JwtAuthenticationFilter` de reactive. Los servicios downstream no comparten la misma estrategia. Centralizar en un `security-common` o en el gateway como único punto de autenticación.

#### 37. `CarritoService.iniciarCheckout()` — No propagación de traza a microservicios externos

```java
reservaId = Long.valueOf(eventoClient.crearReserva(...));
```

Las excepciones de Feign no propagan información de traza para el `SagaOrchestrator`. Envolver las excepciones externas en `CarritoException` con causa original:

```java
catch (FeignException e) {
    throw CarritoException.stockNoDisponible(detalle.getEventoId(), e);
}
```

#### 38. Sin paginación en endpoints de listado

`CarritoController.listarCarritos()` y todos los endpoints de listado (`DonacionController`) devuelven la lista completa sin paginación. Para producción agregar `Pageable` + `@PageableDefault`.

#### 39. EntradaConsumer en `ms-eventos` — Solo imprime a consola

```java
System.out.println(...) // ❌ No loguea
```

Cambiar a SLF4J y reemplazar por lógica real de negocio o eliminar el consumer hasta tener el uso definido.

---

### 🟡 Medio

#### 40. `ms-eventos` — DTO `EventoDTO` usa `Integer id` en vez de `Long`

Inconsistencia con el resto del proyecto que usa `Long` para IDs:

```java
private Integer id; // ❌ Cambiar a Long
```

#### 41. `ResumenCarritoDto.fromCarrito()` — Duplicación de totales en vez de usar `recalcularTotales()`

```java
this.subtotal = detalles.stream()
    .map(DetalleCarrito::getSubtotal)
    .reduce(BigDecimal.ZERO, BigDecimal::add);
// Ya existe CarritoDeCompras.recalcularTotales()
```

Delegar la lógica al modelo para evitar duplicación.

#### 42. `IdempotencyRecord` clave primaria es `idempotencyKey` (cadena)

Funciona, pero si la clave supera 255 caracteres, falla. Agregar un ID numérico auto-generado como PK y usar `idempotencyKey` como índice único.

#### 43. Sin monitoreo de colas RabbitMQ

No hay chequeos de salud para las colas de RabbitMQ (profundidad de cola, consumidores activos ni colas bloqueadas). Agregar `RabbitMQHealthIndicator`.

#### 44. `ms-carrito` — `Reserva` con enumerado `EstadoReserva` sin constantes string

```java
public enum EstadoReserva { RESERVA_INICIADA, RESERVA_CONFIRMADA, RESERVA_CANCELADA }
```

Agregar constantes tipo `public static final String RESERVA_INICIADA = "RESERVA_INICIADA"` o usar `@JsonValue` en el enum para mapeo explícito a JSON.

---

## Resumen por Prioridad

| #   | Servicio        | Archivo                              | Problema                       | Esfuerzo |
| --- | --------------- | ------------------------------------ | ------------------------------ | -------- |
| 1   | api-gateway     | `JwtAuthenticationFilter`            | Field injection → constructor  | 5min     |
| 2   | api-gateway     | `JwtAuthenticationFilter`            | Sin `X-Forwarded-For`          | 5min     |
| 3   | api-gateway     | `SecurityConfig`                     | Dead code, todo permitido      | 5min     |
| 4   | api-gateway     | `CorsConfig`                         | Headers de seguridad           | 5min     |
| 5   | ms-carrito      | `CarritoService`                     | Idempotencia rota (nueva key)  | 30min    |
| 6   | ms-carrito      | `SagaOrchestrator`                   | Idempotencia duplicada + rota  | 30min    |
| 7   | `ms-carrito`    | `CarritoService.procesarWebhookPago` | Transacción muy corta          | 15min    |
| 8   | `api-gateway`   | `JwtAuthenticationFilter`            | Rutas públicas O(n) → O(1)     | 5min     |
| 9   | `api-gateway`   | `application.yml`                    | Rutas usuarios duplicadas      | 5min     |
| 10  | `ms-carrito`    | `CarritoService`                     | Feign sin retry/breaker        | 15min    |
| 11  | `api-gateway`   | `application.yml`                    | `jwt.secret` fallback expuesto | 15min    |
| 12  | `ms-carrito`    | `OutboxRelayService`                 | Sin dead-letter + métricas     | 45min    |
| 13  | `ms-carrito`    | todos                                | Sin paginación en listados     | 30min    |
| 14  | `ms-mensajeria` | `MensajeriaConsumer`                 | Re-lanza excepción a RabbitMQ  | 15min    |
| 15  | `api-gateway`   | `FallbackController`                 | Sin DTO de error unificado     | 20min    |
| 16  | `ms-carrito`    | security                             | JWT validador en cada servicio | 60min    |

## Docker

Voy a crear un archivo central `infra/docker-compose.yml` que defina RabbitMQ y la red `ticketti-network`, y además eliminar el bloque `rabbitmq` del docker-compose.yml del BFF para evitar duplicados. Luego explico cómo usarlo. Aplico los cambios.

Read [](file:///c%3A/Users/Marcelo-HP/Desktop/Codigo/Proyectos/Ticketti/Microservicios/BFF-Back-for-Frontend/docker-compose.yml)

Generating patch (28 lines) in [](file:///c%3A/Users/Marcelo-HP/Desktop/Codigo/Proyectos/Ticketti/Microservicios/infra/docker-compose.yml)


```

```


Generating patch (38 lines) in [](file:///c%3A/Users/Marcelo-HP/Desktop/Codigo/Proyectos/Ticketti/Microservicios/BFF-Back-for-Frontend/docker-compose.yml)


```

```


Se ha agregado una tarea pendiente

He creado la opción B: un compose central de infraestructura y quité RabbitMQ del compose del BFF para evitar duplicados.

Qué hice
- Añadí docker-compose.yml (servicio `rabbitmq` + red `ticketti-network`).
- Eliminé el bloque `rabbitmq` del docker-compose.yml y quité la dependencia `depends_on` (ahora el BFF asume que RabbitMQ está provisto por la infraestructura).
- Mantengo la red `ticketti-network` declarada como `external: true` en los compose de las apps (ya existía o se creó antes).

Contenido clave (resumido)
- docker-compose.yml define:
  - service `rabbitmq` usando `rabbitmq:4-management`
  - expose puertos `5672` (AMQP) y `15672` (management)
  - network `ticketti-network` con name `ticketti-network` (la crea si no existe cuando lo levantamos aquí)
- Los otros services usan la red `ticketti-network` con `external: true`, por tanto deben arrancar después de que la red exista y RabbitMQ esté en ella.

Cómo funciona (explicación breve)
- El compose docker-compose.yml actúa como el “proveedor” de la infraestructura compartida:
  - Al ejecutar `docker compose -f docker-compose.yml up -d` se crea la red `ticketti-network` y el contenedor `rabbitmq`.
  - Las demás aplicaciones (ms-carrito, ms-donaciones, ms-mensajeria, BFF, etc.) usan `ticketti-network` como red externa: cuando las levantes con sus propios docker-compose.yml se unirán a esa red y podrán resolver el host `rabbitmq`.
- Ventajas:
  - Evitas servicios duplicados de RabbitMQ en varios compose.
  - Compartes una sola red DNS interna para que las apps resuelvan `rabbitmq`.
  - Facilita levantamientos parciales (infra por separado, apps por separado).
- Recomendaciones operativas:
  1. Levantar primero la infraestructura:
     ```bash
     docker compose -f infra/docker-compose.yml up -d
     ```
  2. Luego, en cada servicio (ms-carrito, ms-donaciones, ms-mensajeria, BFF, etc.):
     ```bash
     cd ms-carrito
     docker compose up -d
     # o docker compose -f docker-compose.yml up -d
     ```
  3. Verificar que cada servicio resuelve RabbitMQ y que no hay conflictos de puertos en el host.

Notas importantes y pasos siguientes
- Conflicto de puertos: revisa docker-compose.yml, tiene `- "8081:8080"` (host 8081) y BFF también mapea host 8081; ajusta ms-usuarios a otro puerto si necesitas correr ambos localmente, por ejemplo `8082:8080`.
- Consistencia de variables: estandariza env vars RabbitMQ a `SPRING_RABBITMQ_HOST/PORT/USERNAME/PASSWORD` o asegura que cada servicio lea las que defines en su compose.
- Si quieres, puedo:
  - A) modificar docker-compose.yml para unirse a `ticketti-network` y cambiar su puerto host (p. ej. 8082), o
  - B) lanzar la infraestructura y luego levantar ms-carrito, ms-donaciones y ms-mensajeria para una prueba E2E.

## Pasos 

Los siguientes pasos son estos:

1. Levantar la infraestructura central:
   ```bash
   docker compose -f infra/docker-compose.yml up -d
   ```
   Esto deja arriba RabbitMQ compartido en la red `ticketti-network`.

2. Levantar el orden base de servicios:
   - config-server
   - discovery-server
   - BFF-Back-for-Frontend
   - ms-usuarios
   - ms-eventos
   - ms-carrito
   - ms-donaciones
   - ms-mensajeria

3. Verificar que cada servicio quedó en su puerto esperado:
   - API Gateway: 8222
   - BFF: 8081
   - Config Server: 8888
   - Discovery Server: 8761
   - ms-usuarios: 8080
   - ms-eventos: 8083
   - ms-donaciones: 8084
   - ms-mensajeria: 8085
   - ms-carrito: 8082

4. Hacer la prueba de negocio:
   - crear carrito
   - confirmar pago
   - revisar que salga el evento por RabbitMQ
   - confirmar que ms-donaciones registre la donación
   - confirmar que ms-mensajeria envíe la notificación

5. Revisar logs si algo falla:
   - primero el relay del outbox en ms-carrito
   - luego los consumidores de ms-donaciones y ms-mensajeria
   - finalmente RabbitMQ Management en `http://localhost:15672`

Si quieres, el siguiente paso lo hago yo: levantar primero la infraestructura y después guiarte en la prueba E2E servicio por servicio.


Voy a actualizar la lista de tareas con pasos E2E inmediatos (levantar infra, servicios y pruebas).

Se ha agregado una tarea pendiente


1) Crear/red comprobar (si no existe)
```bash
docker network ls | findstr ticketti-network || docker network create ticketti-network
```

2) Levantar infra (config-server trae RabbitMQ)
```powershell
Set-Location 'c:\Users\Marcelo-HP\Desktop\Codigo\Proyectos\Ticketti\Microservicios\config-server'
docker compose up -d
docker compose ps
```
- Espera a que `rabbitmq` esté healthy (healthcheck configurado). Abre http://localhost:15672 (usuario `guest` / `guest`) para ver queues.

3) Levantar servicios core
```powershell
Set-Location '..\discovery-server'; docker compose up -d; docker compose ps
Set-Location '..\ms-usuarios';    docker compose up -d; docker compose ps
Set-Location '..\ms-eventos';     docker compose up -d; docker compose ps
Set-Location '..\ms-carrito';     docker compose up -d; docker compose ps
```

4) Levantar servicios auxiliares + gateway
```powershell
Set-Location '..\ms-donaciones';  docker compose up -d; docker compose ps
Set-Location '..\ms-mensajeria';  docker compose up -d; docker compose ps
Set-Location '..\BFF-Back-for-Frontend'; docker compose up -d; docker compose ps
Set-Location '..\api-gateway';    docker compose up -d; docker compose ps
```

5) Verificar logs y salud rápida (en cada carpeta)
```powershell
# Dentro de cada servicio usar:
docker compose logs -f --tail=100
# o para cerrar inmediatamente:
docker compose logs --tail=50
```
- Busca en ms-carrito logs del `OutboxRelayService` indicando "Outbox relay completado" o "publicado".
- Busca en ms-donaciones y ms-mensajeria mensajes como "Evento recibido" o entradas de sus consumers.

6) Ejecutar flujo de prueba (simular pago aprobado)
- Crea un carrito / agrega entradas usando la API (puedes usar api-gateway en `http://localhost:8222` o ms-carrito directo `http://localhost:8082`).
- Simula webhook pago aprobado (ejemplo, ajusta `carritoId` y `timestamp`):
```bash
curl -X POST http://localhost:8082/api/v1/Carrito/123/webhook \
  -H "Content-Type: application/json" \
  -d '{"estado":"aprobado","token":"tok-demo","timestamp":"2026-05-31T13:10:00","nonce":"abc123"}'
```
- Alternativa: llamar al endpoint de checkout y luego el webhook desde el frontend o Postman.

7) Verificar colas en RabbitMQ Management
- En http://localhost:15672:
  - Mira que existan `pago.aprobado` y `mensajeria.queue`.
  - Observa rates, mensajes en cola, y consumers conectados.

8) Si algo falla: recopila evidencias
```powershell
# Obtener últimos 200 logs de un servicio (ejemplo ms-carrito)
Set-Location 'ms-carrito'
docker compose logs --tail=200 > ../ms-carrito-logs.txt
# Repetir para ms-donaciones y ms-mensajeria
```
- Revisa excepciones Jackson, errores Feign o nulls en campos esperados.
- Copia los mensajes de error y dímelos; yo te indico la corrección exacta.

¿Quieres que lo haga ahora (levante los servicios y compruebe logs)?

## Error en el docker-compose , con respecto al mail -ms-mensajjeria

Voy a hacer tail de los logs del servicio `app` en ms-mensajeria para ver consumo de `CompraConfirmadaEvent`.

Ran terminal command: Set-Location 'C:\Users\Marcelo-HP\Desktop\Codigo\Proyectos\Ticketti\Microservicios\ms-mensajeria' ; docker compose logs -f --tail=200 app

Read [](file:///c%3A/Users/Marcelo-HP/AppData/Roaming/Code/User/workspaceStorage/2680f9ff7c74465f834fab65a893d565/GitHub.copilot-chat/chat-session-resources/ab217761-0d4e-4395-a04b-293165123c29/call_5bPto6YDLW9hCj5giDpT0LCR__vscode-1780247177600/content.txt)

Compacted conversationEstoy tailing los logs; hay un error recurrente que impide que ms-mensajeria arranque: falta la propiedad `spring.mail.username` (BeanCreationException en `mailConfig`), por eso la app reinicia en bucle.

Opciones rápidas para arreglarlo:
- Añadir variables de mail al compose (`SPRING_MAIL_USERNAME`, `SPRING_MAIL_PASSWORD`, `SPRING_MAIL_HOST`, `SPRING_MAIL_PORT`) en docker-compose.yml.  
- Hacer la configuración de mail tolerante a valores faltantes (usar `@Value("${spring.mail.username:}")` o condicionar el bean) en el código para ignorar mail en local.  
- Desactivar la carga de `MailConfig` con un perfil o property (`spring.mail.enabled=false`) si no se usa ahora.

Dime cuál prefieres y lo aplico (puedo parchear el compose y reiniciar containers, o editar el código y reconstruir).