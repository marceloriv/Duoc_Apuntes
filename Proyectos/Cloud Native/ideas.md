# Ideas Proyecto

## Aceptables

- Colegio
- Eventos
- Foro
- Adopción de animales
- Salud

## No Aceptables

- drogas
- tráfico de órganos
- e-commerce

## Criterios de aprobación (Cloud Native I)

Según [[2026/sexto semestre/Cloud Native I/Semana 1/2|Notas semana 1 - Cloud Native I]]:

- La **primera evaluación es un MVP**: Frontend + API Manager + BFF (como patrón de arquitectura).
- El foco del ramo es **construir el API Manager** (no los microservicios).
- Ya se puede comenzar por **Frontend** y **BFF**.
- **Versionado de API** (tema evaluado): se versiona por URL cuando cambia compatibilidad, seguridad, tipos de solicitud, políticas o headers de solicitud.
- **CORS**: una API pública permite todo (`*`); una API propia restringe a la URL del consumidor.

La idea elegida debe permitir lucir: roles/permisos naturales, políticas distintas según el consumidor, y al menos un caso real de versionado de API.

> Fecha de la primera evaluación: **semana 5** (ver [[2026/sexto semestre/Gestion de proyectos de Software/Semana 1/2|Gestión de proyectos de Software]]).

## Chat IA

Sí. Considerando que el API Manager es el foco del ramo, yo buscaría un dominio donde naturalmente existan roles, permisos, diferentes tipos de clientes, operaciones con distintas políticas y varios microservicios. Eso permite lucir el patrón sin caer en un e-commerce disfrazado.

Aquí van ideas distintas a las anteriores:

Ideas de proyectos

| Idea | Microservicios posibles | Por qué sirve para el proyecto | Señales para el API Manager |
| --- | --- | --- | --- |
| 🚒 Gestión de emergencias | Incidentes, usuarios, unidades, ubicaciones, notificaciones | Mucho routing, roles y prioridad | Policy por prioridad; rate limit en notificaciones |
| 🚌 Transporte público | Rutas, buses, conductores, recorridos, alertas | BFF puede combinar mucha información | BFF agrega recorridos + alertas; roles pasajero/conductor |
| 🅿️ Sistema de estacionamientos | Estacionamientos, reservas, usuarios, vehículos, pagos | Flujo sencillo y varios roles | Roles cliente/operador; rate limit en reservas |
| 🏢 Gestión de edificios/condominios | Residentes, espacios comunes, reservas, incidentes, visitas | Muy buen caso para permisos | AuthZ por rol (residente/conserje/admin); headers por consumidor |
| 🏛️ Gestión municipal | Ciudadanos, solicitudes, trámites, funcionarios, notificaciones | Excelente para roles y estados | Estados de trámites; policy por rol (ciudadano/funcionario) |
| 🗳️ Sistema de votaciones | Usuarios, elecciones, candidatos, votos, resultados | Seguridad y autorización son importantes | AuthZ estricta; CORS restringido; versionado de resultados |
| 📚 Biblioteca | Usuarios, libros, préstamos, multas, reservas | Simple de implementar pero permite buena arquitectura | Roles lector/bibliotecario; rate limit de préstamos |
| 🧑‍💼 Bolsa de trabajo | Usuarios, empresas, ofertas, postulaciones, notificaciones | No es e-commerce y tiene flujos claros | Roles candidato/empresa; rate limit de postulaciones |
| 🏠 Gestión de arriendos | Propiedades, arrendatarios, contratos, solicitudes | Buen ejemplo de BFF + roles | BFF por rol; versionado de contratos |
| 🛠️ Mesa de ayuda / soporte TI | Usuarios, tickets, técnicos, categorías, SLA | Excelente para demostrar estados y permisos | Rate limit por endpoint; PATCH status solo técnicos |
| 📦 Gestión de inventario interno | Productos, bodegas, movimientos, usuarios | Sin necesidad de vender productos | AuthZ por bodega; rate limit de movimientos |
| 🏗️ Gestión de proyectos de construcción | Proyectos, trabajadores, tareas, materiales, reportes | Bastantes dominios independientes | Roles por obra; rate limit de reportes |
| 🎓 Plataforma de cursos | Usuarios, cursos, matrículas, evaluaciones, progreso | Similar a colegio pero más flexible | Roles alumno/docente; versionado de progreso |
| 🏆 Gestión de torneos deportivos | Equipos, jugadores, partidos, resultados, tablas | Muy buena separación de microservicios | Versionado v1/v2 de matches; roles admin/árbitro |
| 🎵 Gestión de conciertos | Artistas, eventos, asistentes, accesos, notificaciones | Tiene eventos sin convertirse necesariamente en e-commerce | Roles artista/administrador; rate limit de asistentes |
| 🐾 Gestión de refugios animales | Animales, refugios, voluntarios, adopciones | Más administrativo que una tienda | Roles voluntario/adoptante; versionado de animales |
| 🧑‍🚒 Gestión de voluntariado | Voluntarios, organizaciones, actividades, turnos | Roles y asignaciones funcionan muy bien | Roles voluntario/coordinador/org; rate limit de inscripciones |
| 🏥 Sistema de turnos | Pacientes, profesionales, agendas, citas, notificaciones | Buen BFF, aunque relacionado con salud | AuthZ de agendas; versionado de turnos |
| 🏫 Sistema de transporte escolar | Alumnos, buses, conductores, rutas, apoderados | Muy bueno para permisos y datos agregados | Permisos apoderado/conductor; BFF agrega datos |
| 🌳 Gestión de parques | Parques, mantenimiento, reportes, trabajadores, reservas | Original y relativamente sencillo | Roles trabajador/visitante; rate limit de reportes |
| 🏙️ Reportes ciudadanos | Ciudadanos, reportes, ubicaciones, departamentos, estados | Excelente para API Manager | Policy por rol (ciudadano/funcionario/admin); versionado de reportes |
| 🔧 Servicio de mantenimiento | Clientes, técnicos, órdenes, agenda, estados | Similar a tickets, pero orientado a servicios | Estados de órdenes; rate limit de agenda |
| 🧪 Gestión de laboratorios | Usuarios, muestras, análisis, equipos, resultados | Buen dominio para permisos y trazabilidad | Permisos y trazabilidad; versionado de resultados |
| 🚗 Gestión de flotas | Vehículos, conductores, viajes, mantenimiento, alertas | Muy buena arquitectura de microservicios | Dashboards agregados; rate limit de alertas |
| ✈️ Gestión aeroportuaria | Vuelos, pasajeros, puertas, equipaje, alertas | Interesante, aunque puede ser más complejo | Roles aeropuerto/agencia; versionado de vuelos |
⭐ Algunas que yo consideraría especialmente

1. 🏙️ Sistema de reportes ciudadanos

Esta me parece muy buena para el ramo y bastante diferente de un e-commerce.

Un ciudadano podría reportar:

"Hay un semáforo defectuoso en esta ubicación."

El sistema genera un reporte y lo deriva al departamento correspondiente.

Arquitectura

```text
Frontend
   │
   ▼
API Manager
   │
   ▼
BFF
   │
   ├── User Service
   ├── Report Service
   ├── Department Service
   ├── Location Service
   └── Notification Service
```

El BFF podría tener:

GET /api/v1/citizens/dashboard

y combinar:

Report Service
+
Notification Service
+
Department Service

API Manager

Aquí pueden lucirse con:

/api/v1/reports
/api/v1/users
/api/v1/departments
/api/v1/notifications

Y aplicar distintas políticas según quién consume la API.

Por ejemplo:

Ciudadano
   ↓
API Manager
   ↓
Puede crear y consultar sus reportes

Funcionario
   ↓
API Manager
   ↓
Puede actualizar reportes de su departamento

Administrador
   ↓
API Manager
   ↓
Acceso completo

Es un proyecto donde los roles tienen sentido, no están puestos artificialmente.

2. 🛠️ Mesa de ayuda TI

Esta sería probablemente una de las más fáciles de implementar.

```text
Frontend
    ↓
API Manager
    ↓
BFF
    ├── User Service
    ├── Ticket Service
    ├── Technician Service
    ├── Category Service
    └── Notification Service
```

Un usuario crea:

Ticket #123
"Mi computador no tiene conexión a Internet"

El ticket pasa por estados:

OPEN
  ↓
ASSIGNED
  ↓
IN_PROGRESS
  ↓
RESOLVED
  ↓
CLOSED

Esto permite demostrar que el API Manager no solamente hace routing.

Por ejemplo:

POST /api/v1/tickets

requiere autenticación.

Mientras que:

GET /api/v1/tickets

puede tener un rate limit diferente.

Y:

PATCH /api/v1/tickets/{id}/status

solamente puede ser utilizado por técnicos.

3. 🚗 Gestión de flotas

También es muy buena porque no es un e-commerce, pero tiene bastantes dominios.

```text
                API Manager
                     │
                     ▼
                    BFF
                     │
       ┌─────────────┼─────────────┐
       ▼             ▼             ▼
   Vehicles      Drivers        Trips
       │             │             │
       └─────────────┼─────────────┘
                     ▼
               Maintenance
```

> [!summary]
> La base del ramo se concentra en construir el API Manager

Podrían administrar vehículos de una empresa:

Vehículos disponibles
Conductores
Viajes
Mantenimiento
Incidentes
Alertas

Un dashboard podría mostrar:

Vehículos activos
Viajes actuales
Vehículos en mantenimiento
Conductores disponibles
Alertas

Y ahí el BFF tiene mucho sentido, porque el frontend no necesita llamar directamente a cinco microservicios.

4. 🏢 Gestión de condominios

Esta tiene una ventaja: es fácil de explicar.

Roles:

Administrador
Residente
Conserje
Comité

Microservicios:

Residents
CommonAreas
Reservations
Visitors
Incidents
Notifications

Por ejemplo:

POST /api/v1/common-areas/{id}/reservations

El API Manager puede encargarse de:

autenticación
autorización
rate limiting
headers
logging
versionado

Y el BFF podría transformar múltiples servicios en:

GET /api/v1/resident/dashboard

5. 🏆 Gestión de torneos deportivos

Esta puede ser bastante entretenida para un frontend.

Por ejemplo, un torneo de fútbol:

Tournament Service
Team Service
Player Service
Match Service
Result Service

Un usuario consulta:

GET /api/v1/tournaments/{id}/dashboard

El BFF obtiene:

Tournament
   +
Teams
   +
Next Matches
   +
Results
   +
Standings

y entrega una única respuesta al frontend.

Además, permite versionar:

/api/v1/matches

y posteriormente:

/api/v2/matches

si cambia la estructura de los resultados.

6. 🧑‍🚒 Gestión de voluntariado

Esta me gusta porque es poco típica.

Una organización crea actividades:

"Recolección de alimentos"
"Limpieza de parque"
"Apoyo en emergencia"

Y los voluntarios se inscriben.

Microservicios:

User Service
Organization Service
Activity Service
Volunteer Service
Notification Service

Roles:

Voluntario
Organización
Administrador
Coordinador

Nuevamente, el API Manager puede controlar qué puede hacer cada tipo de consumidor.

Si quieren algo todavía más original

Yo miraría estas cinco:

🥇 Reportes ciudadanos

Muy buen equilibrio entre simpleza + arquitectura + API Manager.

🥈 Gestión de flotas

Muy buena separación de microservicios.

🥉 Mesa de ayuda TI

Probablemente la más sencilla de terminar correctamente.

4. Gestión de condominios

Fácil de explicar y con roles claros.

5. Gestión de voluntariado

Más original y menos probable que otros grupos tengan exactamente lo mismo.

## Decisión final

> [!info] Estado
> Ideas aún **en evaluación** (ninguna confirmada con el grupo). Favoritos actuales: 🏙️ **Reportes ciudadanos** (recomendado) y 🛠️ **Mesa de ayuda TI** (plan B). Próximo paso accionable: decidir en la semana 2, crear los repos y los contratos OpenAPI.

Comparativa de los 5 finalistas contra los criterios del ramo, el stack ya dominado en [[Proyectos/Ticketti|Ticketti]] y el esfuerzo para llegar al MVP de la semana 5.

| Criterio | 🏙️ Reportes ciudadanos | 🚗 Gestión de flotas | 🛠️ Mesa de ayuda TI | 🏢 Condominios | 🧑‍🚒 Voluntariado |
| --- | --- | --- | --- | --- | --- |
| Roles naturales | ✅ ciudadano/funcionario/admin | ✅ conductor/admin/flota | ✅ usuario/técnico/admin | ✅ residente/conserje/comité | ✅ voluntario/org/coordinador |
| Políticas distintas por consumidor | ✅ por rol | ✅ por rol | ✅ por endpoint y rol | ✅ por rol | ✅ por rol |
| Caso real de versionado | ✅ reportes v1 → v2 | ✅ viajes v1 → v2 | ✅ tickets v1 → v2 | ✅ reservas v1 → v2 | ✅ actividades v1 → v2 |
| BFF con agregación real | ✅ dashboard ciudadano | ✅ dashboard flotas | ✅ dashboard tickets | ✅ dashboard residente | ✅ dashboard voluntario |
| Esfuerzo para MVP semana 5 | ⚠️ medio | ⚠️ medio-alto | ✅ bajo | ✅ bajo | ✅ bajo |
| Reutiliza stack Ticketti (Spring Cloud Gateway + NestJS + React) | ✅ alta | ✅ alta | ✅ alta | ✅ alta | ✅ alta |
| Originalidad / evita repetir grupos | ✅ | ✅ | ⚠️ común | ⚠️ común | ✅ muy original |

**Veredicto:** 🏙️ **Reportes ciudadanos** es la mejor combinación para lucir el API Manager sin caer en e-commerce. 🛠️ **Mesa de ayuda TI** es el plan B si el grupo prioriza terminar a tiempo con menos riesgo.

## Entregables para la primera evaluación (E1)

MVP de la semana 5, según [[2026/sexto semestre/Gestion de proyectos de Software/Semana 1/2|Gestión de proyectos de Software]]:

- **Frontend**: 1 pantalla real por rol (ej. ciudadano + funcionario) consumiendo solo el API Manager.
- **API Manager**: autenticación (JWT), autorización por rol, rate limiting, CORS y al menos 1 política por consumidor.
- **BFF**: 1 endpoint de agregación (ej. `GET /api/v1/citizens/dashboard`) que combine 2-3 microservicios.
- **Microservicios**: 2-3 de dominio (ej. User, Report, Department) — no son el foco, lo mínimo viable.
- **Versionado**: usar `/v1` en la URL y documentar el caso de cambio a `/v2`.

Orden de construcción:

1. Semana 2: decisión + repos + frontend estático + contratos OpenAPI.
2. Semana 3: microservicios de dominio + BFF con agregación.
3. Semana 4: API Manager (auth, policies, rate limit, CORS).
4. Semana 5: pulir E1 + demo end-to-end.

### Si se elige Reportes ciudadanos

- Microservicios E1: `user-service`, `report-service`, `department-service`.
- BFF: `GET /api/v1/citizens/dashboard` (Report + Department + Notification).
- API Manager: ciudadano crea/consulta sus reportes; funcionario actualiza los de su departamento; admin acceso completo.

#### Matriz de políticas por consumidor (para el API Manager)

| Endpoint (vía API Manager) | Método | Consumidor | Auth / AuthZ | Rate limit (ej.) | CORS |
| --- | --- | --- | --- | --- | --- |
| `/api/v1/reports` | `POST` | ciudadano, funcionario | JWT | estricto (10/min) | frontend |
| `/api/v1/reports` | `GET` | ciudadano (solo los suyos) | JWT | laxo (60/min) | frontend |
| `/api/v1/reports/{id}/status` | `PATCH` | funcionario de su depto, admin | JWT + rol (`X-Rol-Usuario-Id`) | medio (20/min) | frontend |
| `/api/v1/citizens/dashboard` | `GET` | ciudadano | JWT | laxo (60/min) | frontend |
| `/api/v1/departments` | `GET` | público | sin auth | laxo | `*` |

#### Caso real de versionado v1 → v2

- `v1`: `GET /api/v1/reports/{id}` devuelve `priority: "ALTA"` (string simple).
- Cambio que rompe compatibilidad: por nueva política de SLA, `priority` pasa a ser un objeto `{ "level": "ALTA", "slaHoras": 24 }`. Cambian estructura de datos, política y headers → justifica una nueva URL `/v2`.
- Resultado: se mantiene `/v1` para clientes antiguos y se crea `GET /api/v2/reports/{id}`; ambos documentados en OpenAPI.

#### Story CORS (tema evaluado)

- **Público**: seguimiento de trámite `GET /api/v1/reports/{id}/status` permite `Access-Control-Allow-Origin: *` (cualquiera puede consultarlo).
- **Propio**: las rutas de gestión del frontend (crear reporte, `PATCH /status`, dashboard) restringen CORS al origin del frontend (ej. `https://ciudadanos.example.com`).

## Riesgos y supuestos (validar con el grupo)

- **Tamaño de equipo**: sin confirmar. Si son pocos, recortar a `user-service` + `report-service`; department y notification como datos seed o stub.
- **`notification-service` puede ser un stub** (log/mock) en E1: no es el foco evaluado.
- **Derivación por departamento**: usar regla simple `categoría → departamento`, sin flujo complejo.
- **Sin pagos ni multas en E1**: mantener el objeto principal como reportar/derivar/actualizar, no como una compra.
- **Fechas**: E1 en la semana 5 (validar con Gestión de proyectos de Software).

## Checklist: cómo lucirse en el API Manager

Reutilizar lo ya resuelto y auditado en [[Proyectos/Ticketti|Ticketti]] (Spring Cloud Gateway, JWT, BFF NestJS):

- [ ] Autenticación JWT en el gateway y validación de `iss`/`aud`.
- [ ] Autorización por rol: `PATCH /status` solo para técnicos/funcionarios (demostrar que no es solo routing).
- [ ] Rate limits distintos por endpoint/consumidor (ej. `POST` estricto, `GET` laxo).
- [ ] CORS: API pública `*` vs. ruta interna restringida a la URL del frontend (tema de ramo).
- [ ] Versionado por URL (`/v1`, `/v2`) y documentado en OpenAPI.
- [ ] Propagación de headers `X-Usuario`, `X-Usuario-Id`, `X-Rol-Usuario-Id` al BFF (patrón ya visto en Ticketti).
- [ ] Logging/trazabilidad con `X-Request-Id` por request.
- [ ] Circuit breaker / timeouts (Resilience4j) para evitar cascadas hacia el BFF.

Y evitaría estos enfoques

No porque estén mal, sino porque pueden terminar pareciendo un e-commerce:

❌ Marketplace
❌ Venta de entradas
❌ Tienda de videojuegos
❌ Tienda de ropa
❌ Delivery
❌ Marketplace de servicios
❌ Reservas con pago como función principal

En cambio, intentaría que el objeto principal del sistema no sea dinero ni una compra, sino algo como:

reportar, gestionar, coordinar, asignar, registrar, autorizar o consultar información.

Eso hace que el proyecto se sienta mucho más como un ejercicio de arquitectura distribuida y API Management, que parece ser precisamente lo que les interesa evaluar.
