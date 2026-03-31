# Documento de Arquitectura de Solución: Plataforma SmartLogix

**Cliente:** SmartLogix Startup  
**Proyecto:** Modernización Logística eCommerce v3.0

---

## Contenido

- [Documento de Arquitectura de Solución: Plataforma SmartLogix](#documento-de-arquitectura-de-solución-plataforma-smartlogix)
  - [Contenido](#contenido)
  - [1. Contexto y Objetivos de Negocio](#1-contexto-y-objetivos-de-negocio)
  - [2. Requerimientos Extendidos del Sistema](#2-requerimientos-extendidos-del-sistema)
    - [2.1 Requerimientos Funcionales (RF) - Detalle Operativo](#21-requerimientos-funcionales-rf---detalle-operativo)
      - [RF-1: Gestión Transaccional de Pedidos (Flujo de Ciclo de Vida)](#rf-1-gestión-transaccional-de-pedidos-flujo-de-ciclo-de-vida)
      - [RF-2: Sincronización de Inventario (Real-Time y Multialmacén)](#rf-2-sincronización-de-inventario-real-time-y-multialmacén)
      - [RF-3: Operación de Sucursal (Fulfillment)](#rf-3-operación-de-sucursal-fulfillment)
      - [RF-4: Omnicanalidad y Frentes de Usuario](#rf-4-omnicanalidad-y-frentes-de-usuario)
    - [2.2 Requerimientos No Funcionales (RNF) - Atributos de Calidad](#22-requerimientos-no-funcionales-rnf---atributos-de-calidad)
      - [RNF-1: Resiliencia Crítica y Tolerancia a Fallos](#rnf-1-resiliencia-crítica-y-tolerancia-a-fallos)
      - [RNF-2: Escalabilidad Horizontal y Despliegue](#rnf-2-escalabilidad-horizontal-y-despliegue)
      - [RNF-3: Seguridad y Cumplimiento](#rnf-3-seguridad-y-cumplimiento)
      - [RNF-4: Eficiencia Operativa y Asincronía](#rnf-4-eficiencia-operativa-y-asincronía)
  - [3. Arquitectura de Software y Ecosistema Front](#3-arquitectura-de-software-y-ecosistema-front)
    - [3.1 Ecosistema Frontend](#31-ecosistema-frontend)
    - [3.2 Capa de Agregación (BFF)](#32-capa-de-agregación-bff)
    - [3.3 Capa de Backend y Microservicios](#33-capa-de-backend-y-microservicios)
      - [A. Dominio de Identidad y Acceso (MS-Auth \& Users)](#a-dominio-de-identidad-y-acceso-ms-auth--users)
      - [B. Dominio de Ventas (MS-Orders)](#b-dominio-de-ventas-ms-orders)
      - [C. Dominio de Inventario (MS-Inventory)](#c-dominio-de-inventario-ms-inventory)
      - [D. Dominio Logístico (MS-Shipping)](#d-dominio-logístico-ms-shipping)
      - [E. Dominio de Notificaciones (MS-Notifications)](#e-dominio-de-notificaciones-ms-notifications)
    - [3.4 Diagrama de Arquitectura de Solución (Vista de Componentes)](#34-diagrama-de-arquitectura-de-solución-vista-de-componentes)
      - [Descripción de Componentes](#descripción-de-componentes)
    - [3.5 Diagrama de Flujo de Eventos (Core Logics)](#35-diagrama-de-flujo-de-eventos-core-logics)
      - [Explicación Técnica del Comportamiento de las Colas](#explicación-técnica-del-comportamiento-de-las-colas)
    - [3.6 Arquitectura de Red y Alta Disponibilidad (Multi-AZ)](#36-arquitectura-de-red-y-alta-disponibilidad-multi-az)
      - [Explicación del Diseño de Infraestructura](#explicación-del-diseño-de-infraestructura)
    - [3.7 Estrategia de Automatización: Pipeline de CI/CD](#37-estrategia-de-automatización-pipeline-de-cicd)
      - [Flujo del Pipeline](#flujo-del-pipeline)
  - [4. Matriz de Herramientas y Justificación Técnica](#4-matriz-de-herramientas-y-justificación-técnica)
    - [4.1 Infraestructura y Orquestación](#41-infraestructura-y-orquestación)
    - [4.2 Desarrollo y Lenguajes](#42-desarrollo-y-lenguajes)
    - [4.3 Comunicación y Persistencia](#43-comunicación-y-persistencia)
    - [4.4 Calidad y Observabilidad](#44-calidad-y-observabilidad)
  - [5. Evaluación Ética y Técnica del Diseño](#5-evaluación-ética-y-técnica-del-diseño)
    - [5.1 Sostenibilidad Ambiental (Green Computing)](#51-sostenibilidad-ambiental-green-computing)
    - [5.2 Privacidad y Protección de Datos (Privacy by Design)](#52-privacidad-y-protección-de-datos-privacy-by-design)
    - [5.3 Equidad y Transparencia Algorítmica](#53-equidad-y-transparencia-algorítmica)
    - [5.4 Inclusión y Accesibilidad Digital](#54-inclusión-y-accesibilidad-digital)

---

## 1. Contexto y Objetivos de Negocio

SmartLogix requiere una infraestructura digital de alta disponibilidad capaz de gestionar el ciclo de vida completo de la logística para PYMEs. El objetivo es eliminar la fragmentación de datos de los sistemas monolíticos actuales, permitiendo escalabilidad elástica durante eventos de alta demanda (CyberDay) y una integración fluida entre los canales de venta, la operación en bodega y la administración central.

---

## 2. Requerimientos Extendidos del Sistema

Esta sección detalla las capacidades operativas y técnicas necesarias para la plataforma SmartLogix, segmentadas por su naturaleza funcional y atributos de calidad.

### 2.1 Requerimientos Funcionales (RF) - Detalle Operativo

Los RF definen *qué* debe hacer el sistema para satisfacer las necesidades del negocio de SmartLogix y sus clientes (PYMEs).

#### RF-1: Gestión Transaccional de Pedidos (Flujo de Ciclo de Vida)

- **RF-1.1 Orquestación de Checkout:** El sistema debe capturar el pedido del carrito del cliente, validar datos de envío y configurar la orden inicial.
- **RF-1.2 Transición de Estados:** El sistema debe gestionar el flujo completo de estados: `Pendiente → Pagado → En Preparación → Despachado → En Ruta → Entregado` (o `Cancelado / Devuelto`).
- **RF-1.3 Integración de Pasarela de Pagos:** Soportar la conexión síncrona con procesadores de pago externos y gestionar respuestas de éxito, rechazo o error.
- **RF-1.4 Generación de Eventos de Orden:** Al cambiar a estado "Pagado", el sistema debe publicar un evento asíncrono (`Order.Paid`) para disparar procesos de inventario y logística.

#### RF-2: Sincronización de Inventario (Real-Time y Multialmacén)

- **RF-2.1 Reserva de Stock Transaccional:** Al iniciar el checkout, el sistema debe bloquear temporalmente las unidades solicitadas para evitar *overselling* (ventas sin stock).
- **RF-2.2 Confirmación o Liberación de Reserva:** Si el pago es exitoso, la reserva se convierte en descuento definitivo. Si el pago falla o el tiempo expira, la reserva se libera automáticamente.
- **RF-2.3 Gestión Multialmacén:** Soportar la definición de múltiples bodegas físicas (sucursales o centros de distribución) y asignar stock a cada una.
- **RF-2.4 Sincronización vía API (ERP/WMS):** Proveer endpoints para recibir actualizaciones masivas de stock desde sistemas externos (ERP) de las PYMEs.

#### RF-3: Operación de Sucursal (Fulfillment)

- **RF-3.1 Generación de Picking Lists:** Permitir a los operarios agrupar pedidos pagados y generar listas de recolección optimizadas por ubicación dentro de la bodega.
- **RF-3.2 Verificación de Packing (Escaneo):** Soportar el escaneo de SKUs durante el empaquetado para asegurar que los artículos correctos estén en la caja correcta.
- **RF-3.3 Impresión de Etiquetas:** Integrar con el servicio de *Shipping* para generar e imprimir etiquetas de despacho (courier) y *packing slips* internos.

#### RF-4: Omnicanalidad y Frentes de Usuario

- **RF-4.1 Portal eCommerce:** Interfaz para cliente final; debe mostrar catálogo, precios, stock disponible y permitir el flujo de compra.
- **RF-4.2 Sucursal Virtual:** Interfaz para el operario de la PYME; debe permitir gestionar pedidos, ver inventario local y realizar fulfillment.
- **RF-4.3 Panel de Administración:** Interfaz para SmartLogix; debe gestionar altas de PYMEs, configurar couriers y visualizar dashboards de rendimiento.

---

### 2.2 Requerimientos No Funcionales (RNF) - Atributos de Calidad

Los RNF definen *cómo* debe comportarse el sistema para ser confiable, escalable y seguro.

#### RNF-1: Resiliencia Crítica y Tolerancia a Fallos

- **RNF-1.1 Patrón Circuit Breaker:** La comunicación con servicios externos (Pagos, Couriers) debe estar protegida por cortocircuitos. Si el servicio externo falla consecutivamente, las peticiones deben "fallar rápido" sin bloquear el sistema.
- **RNF-1.2 Aislamiento de Microservicios:** El fallo completo de un microservicio no debe degradar la funcionalidad de los otros. Ejemplo: el fallo de MS-Shipping no debe impedir la captura de pedidos en MS-Orders.
- **RNF-1.3 Reintentos con Backoff:** Implementar políticas de reintentos para comunicaciones asíncronas fallidas (colas), incrementando el tiempo entre reintentos para no saturar los servicios.

#### RNF-2: Escalabilidad Horizontal y Despliegue

- **RNF-2.1 Orquestación en Kubernetes (K8s):** El sistema debe desplegarse en un cluster de K8s, permitiendo el auto-escalado de pods de microservicios basado en métricas de CPU/Memoria.
- **RNF-2.2 Microservicios Stateless (Sin Estado):** Los microservicios no deben guardar estado en memoria local; deben persistir datos en la base de datos distribuida o cachés como Redis para permitir el escalado.

#### RNF-3: Seguridad y Cumplimiento

- **RNF-3.1 Autenticación Centralizada (OAuth2/OIDC):** Usar un proveedor de identidad centralizado (Auth0, Keycloak) que emita tokens JWT para autenticar usuarios y servicios a través del API Gateway.
- **RNF-3.2 Cifrado de PII:** Datos de Identificación Personal (PII) de clientes (Nombres, Direcciones, RUT/DNI) deben estar cifrados en tránsito (TLS 1.3) y en reposo (AES-256 en la base de datos).

#### RNF-4: Eficiencia Operativa y Asincronía

- **RNF-4.1 Arquitectura EDA (Event-Driven):** Tareas que no requieren respuesta inmediata (Notificaciones por Email, Generación de PDFs) deben procesarse de forma asíncrona mediante colas de mensajería (RabbitMQ/Kafka).
- **RNF-4.2 Tiempo de Respuesta de API:** Las APIs sincrónicas del Gateway deben responder en menos de 300ms para el 95% de las peticiones bajo carga normal, exceptuando validaciones complejas de pagos.

---

## 3. Arquitectura de Software y Ecosistema Front

Siguiendo la estrategia de "Estrategias y Herramientas para Microservicios", la solución se divide para asegurar flexibilidad.

### 3.1 Ecosistema Frontend

Para SmartLogix se requieren interfaces diseñadas para cada rol:

1. **Sales Web (Next.js):** Enfocada en la velocidad y el SEO para que las PYMEs vendan más.
2. **Sucursal Virtual (React):** Optimizada para el trabajo rápido en bodega (recepción y despacho).
3. **Admin Panel (React):** Para la gestión global de la plataforma y visualización de datos.
4. **UI-Lib (Librería de Componentes):** Catálogo compartido de botones, formularios y estilos para que las tres aplicaciones se vean y funcionen igual (Consistencia).

### 3.2 Capa de Agregación (BFF)

Cada frente tendrá su propio **BFF (Backend for Frontend)**. Su función es reunir la información de varios microservicios y entregarla "lista para usar" al frontend, evitando que el navegador del usuario tenga que hacer demasiadas peticiones al servidor.

### 3.3 Capa de Backend y Microservicios

La arquitectura se basa en el **Desacoplamiento de Componentes**, donde cada microservicio es independiente, tiene su propia base de datos (PostgreSQL) y se comunica mediante protocolos estándar (REST/JSON) o eventos.

---

#### A. Dominio de Identidad y Acceso (MS-Auth & Users)

**Responsabilidad:** Gestión centralizada de usuarios, roles (Admin, PYME, Cliente) y seguridad.

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| POST | `/auth/login` | Autenticación y entrega de token JWT. |
| POST | `/users/register` | Registro de nuevas PYMEs o clientes finales. |
| GET | `/users/profile` | Obtención de datos de perfil y permisos. |

---

#### B. Dominio de Ventas (MS-Orders)

**Responsabilidad:** Orquestar el ciclo de vida de la compra y la transacción económica.

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| POST | `/orders/checkout` | **(Transaccional)** Inicia la orden, valida el pago y dispara la reserva de stock. |
| GET | `/orders/{id}` | Consulta del estado actual y detalle del pedido. |
| PATCH | `/orders/{id}/status` | Cambio de estado (ej. de "Pagado" a "En Preparación"). |
| GET | `/orders/history/{userId}` | Historial de pedidos para el cliente o la PYME. |

---

#### C. Dominio de Inventario (MS-Inventory)

**Responsabilidad:** Control de existencias físicas en múltiples bodegas y catálogo de productos.

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| GET | `/products` | Catálogo con filtros de categoría y búsqueda. |
| PATCH | `/inventory/reserve` | **(Transaccional)** Bloqueo temporal de unidades para evitar ventas sin stock real. |
| PATCH | `/inventory/commit` | Confirmación definitiva del descuento de stock tras el pago. |
| POST | `/inventory/adjust` | Ajuste manual de stock por ingreso de mercadería o mermas. |

---

#### D. Dominio Logístico (MS-Shipping)

**Responsabilidad:** Gestión de despachos, cálculo de tarifas y conexión con couriers.

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| POST | `/shipping/quote` | Cálculo de costo de envío (usa el patrón **Factory Method** para elegir el Courier). |
| POST | `/shipping/label` | Generación de la etiqueta de despacho (conecta con Serverless para el PDF). |
| GET | `/shipping/track/{trackingId}` | Seguimiento en tiempo real de la ubicación del paquete. |

---

#### E. Dominio de Notificaciones (MS-Notifications)

**Responsabilidad:** Comunicación con el cliente final mediante canales externos.

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| POST | `/notifications/send` | Envío de correos o alertas push. |

> **Nota:** Este servicio funciona principalmente de forma **asíncrona**, escuchando eventos de la cola (RabbitMQ) como "Pedido Despachado".

---

### 3.4 Diagrama de Arquitectura de Solución (Vista de Componentes)

El diagrama detalla la interacción entre las capas de presentación, acceso, servicios y persistencia. Se destaca el uso de **Sidecars** para observabilidad y un bus de eventos para el desacoplamiento total.

#### Descripción de Componentes

1. **Capa de Clientes (Frontend):** Aplicaciones desacopladas que consumen una UI-Lib común para asegurar consistencia visual. Implementación de Next.js en el portal de ventas para optimizar el SEO mediante SSR.

2. **API Gateway (Entrada Única):** Actúa como el punto de entrada controlado. Gestiona la seguridad mediante **Auth JWT** y protege los servicios internos de saturación mediante **Rate Limiting**.

3. **BFF (Backend for Frontend):** Capa de agregación que adapta las respuestas de los microservicios a las necesidades específicas de cada interfaz, reduciendo la latencia y el consumo de datos en el cliente.

4. **Cluster Kubernetes (K8s):** Orquestador que gestiona los Pods de cada microservicio. Cada Pod incluye un **Sidecar (Envoy/Proxy)** encargado de tareas transversales como monitoreo, logging y trazabilidad distribuida, sin intervenir en la lógica de negocio.

5. **Comunicación Asíncrona (RabbitMQ):** El "corazón" del desacoplamiento. Los servicios publican eventos (ej: `Pedido.Pagado`) que otros consumen cuando están disponibles, garantizando la **Resiliencia** del sistema.

6. **Capa de Persistencia:** Implementación del patrón **Database per Service** con PostgreSQL, asegurando que un fallo en la base de datos de un dominio no afecte a los demás.

7. **Servicios Serverless (AWS Lambda / Azure Functions):** Ejecución de tareas pesadas bajo demanda (Generación de Guías de Despacho en PDF) para optimizar costos y escalabilidad.

---

### 3.5 Diagrama de Flujo de Eventos (Core Logics)

Este diagrama representa cómo el sistema sobrevive a una alta carga (CyberDay) procesando tareas pesadas fuera de la línea de tiempo del usuario.

#### Explicación Técnica del Comportamiento de las Colas

La arquitectura transita de un flujo sincrónico (donde el usuario espera) a un flujo asíncrono (donde el sistema procesa en segundo plano), logrando el **desacoplamiento total** de los microservicios:

**1. Flujo Sincrónico (Capa de Acceso)**

- **(1)** El Cliente inicia el checkout y el **BFF-Sales** envía una petición REST/JSON al microservicio **MS-Orders**.
- **(2)** MS-Orders valida internamente la orden y **(3)** retorna una **respuesta inmediata** al BFF ("Pago Procesando..."), liberando la conexión del navegador del usuario. El cliente no percibe latencia por los procesos lentos de bodega o notificaciones.

**2. Publicación de Eventos (Capa de Mensajería)**

- Simultáneamente, MS-Orders publica un evento crítico: `Order.Paid`. Este mensaje no se envía a otro microservicio, sino a un componente central de RabbitMQ llamado **Exchange: OrderEvents**.
- El Exchange actúa como distribuidor inteligente: toma el evento `Order.Paid` y lo copia en múltiples colas suscritas, basándose en reglas de enrutamiento definidas.

**3. Consumo Asíncrono (Capa de Microservicios)**

Cada microservicio consumidor opera de forma independiente y a su propio ritmo:

- El Exchange copia el mensaje en tres colas: `Queue: InventorySync`, `Queue: ShippingRequest` y `Queue: CustomerNotify`.
- **MS-INVENTORY:** Escucha su cola y ejecuta el **(5) Commit de Stock** en su base de datos PostgreSQL, asegurando la integridad del inventario.
- **MS-SHIPPING:** Escucha su cola y dispara el proceso de **(6) Generar Guía de Despacho** (conectando con servicios Serverless para el PDF).
- **MS-NOTIFICATIONS:** Escucha su cola y ejecuta el **(7) Envío de Emails o Alertas Push** para confirmar la compra al cliente.

---

### 3.6 Arquitectura de Red y Alta Disponibilidad (Multi-AZ)

Para cumplir con el requerimiento de **Resiliencia Crítica**, SmartLogix se distribuye en diferentes centros de datos físicos para asegurar que, si uno falla, los otros mantengan el negocio en operación.

#### Explicación del Diseño de Infraestructura

**1. Punto de Entrada y Seguridad Exterior**

- **Punto de Entrada Global (Load Balancer):** Cara visible en Internet. Recibe a los clientes y distribuye el tráfico hacia el API Gateway dentro del cluster, evitando que los microservicios queden expuestos directamente a la red pública.
- **Zonas de Disponibilidad (AZ):** Tres DataCenters separados físicamente. Si uno falla, el sistema automáticamente usa los otros dos, garantizando la **Alta Disponibilidad**.

**2. Segmentación por Subnets (Capas de Seguridad)**

- **Subnets Públicas:** Zona de tránsito. Solo contiene herramientas de red (NAT Gateways) que permiten que el sistema acceda a recursos externos, pero no permiten acceso entrante a los datos.
- **Subnets Privadas (El Cluster K8s):** Núcleo de SmartLogix. Los Pods de los microservicios (Java/Spring Boot) están repartidos en las 3 zonas. Si un Pod muere, Kubernetes lo revive en otra zona automáticamente (**Self-healing**).
- **Subnets de Datos:** Zona más protegida. Aquí están las bases de datos. Los datos se escriben en la zona A y se replican instantáneamente a la B y C. Si se pierde la zona A, la información permanece segura en las otras.

**3. Servicios Serverless**

Fuera del cluster principal se ejecutan las tareas "pesadas" (generar PDFs, envío masivo de correos), evitando que el cluster se ralentice durante picos de demanda.

---

### 3.7 Estrategia de Automatización: Pipeline de CI/CD

Para asegurar que la plataforma SmartLogix sea mantenible y que cada cambio en el código no rompa el sistema, se implementa un flujo de entrega automatizado. Este proceso garantiza el **60% de cobertura de pruebas** exigido en el proyecto.

#### Flujo del Pipeline

1. **Construcción (Build):** Al subir código, **Maven** compila el proyecto y gestiona las dependencias de los microservicios Java/Spring Boot.
2. **Calidad de Código (Análisis Estático):** **SonarQube** escanea el código en busca de vulnerabilidades y errores lógicos ("Code Smells"). **No se permite el despliegue si la cobertura de pruebas unitarias es menor al 60%.**
3. **Contenedorización:** Una vez aprobado el análisis, se genera una imagen de **Docker** con el microservicio listo para ejecutar.
4. **Registro:** La imagen se guarda en un repositorio privado (Container Registry) con una versión específica (tag).
5. **Despliegue (Deploy):** El pipeline actualiza el Cluster de Kubernetes (K8s) mediante un *Rolling Update* para que el sistema nunca deje de funcionar durante la instalación de la nueva versión.

---

## 4. Matriz de Herramientas y Justificación Técnica

Para garantizar la alta disponibilidad y el desacoplamiento de SmartLogix, se ha seleccionado un stack tecnológico robusto que permite el crecimiento elástico y la mantenibilidad a largo plazo.

### 4.1 Infraestructura y Orquestación

| Herramienta | Rol en la Solución | Justificación Técnica |
|-------------|-------------------|----------------------|
| Docker | Contenedores | Garantiza que cada microservicio (Java, Node, etc.) corra en un entorno aislado e inmutable, eliminando el problema de "en mi computador funciona". |
| Kubernetes (K8s) | Orquestador | Gestiona el ciclo de vida de los contenedores. Permite el Auto-scaling (levantar más instancias en un CyberDay) y el Self-healing (reiniciar servicios que fallan). |
| API Gateway (Kong) | Puerta de Enlace | Centraliza la seguridad (SSL), el control de tráfico (Rate Limiting) y la autenticación, protegiendo a los microservicios de ataques externos. |

### 4.2 Desarrollo y Lenguajes

| Herramienta | Rol en la Solución | Justificación Técnica |
|-------------|-------------------|----------------------|
| Java 17 + Spring Boot 3 | Backend Core | Ofrece un ecosistema maduro para sistemas transaccionales pesados (Pedidos, Inventario) con alta concurrencia y tipado fuerte para evitar errores en producción. |
| Node.js (NestJS) | Capa BFF | Ideal para la capa de agregación (BFF) debido a su modelo de I/O no bloqueante, lo que permite manejar múltiples peticiones a microservicios de forma ultra rápida. |
| Next.js / React | Ecosistema Front | Next.js para el portal público (SEO y carga rápida) y React para los paneles operativos por su manejo eficiente del estado de la interfaz. |
| Maven | Gestión de Dependencias | Automatiza la construcción del proyecto y asegura que todas las librerías de los microservicios estén estandarizadas y actualizadas. |

### 4.3 Comunicación y Persistencia

| Herramienta | Rol en la Solución | Justificación Técnica |
|-------------|-------------------|----------------------|
| PostgreSQL | Base de Datos Relacional | Elegida por su robustez en integridad referencial y soporte nativo para JSON, ideal para el patrón Database per Service. |
| RabbitMQ | Message Broker | Facilita el procesamiento asíncrono y el desacoplamiento. Permite que un servicio envíe un mensaje y siga trabajando sin esperar a que el otro responda. |
| AWS Lambda / Serverless | Computación bajo demanda | Utilizada para tareas esporádicas de alto consumo (como generar un PDF), evitando gastar recursos del cluster de Kubernetes en procesos lentos. |

### 4.4 Calidad y Observabilidad

| Herramienta | Rol en la Solución | Justificación Técnica |
|-------------|-------------------|----------------------|
| SonarQube | Análisis de Código | Valida la calidad del software antes de pasar a producción, detectando vulnerabilidades, errores lógicos y asegurando la cobertura de pruebas. |
| Prometheus & Grafana | Monitoreo | Permite visualizar en tiempo real la salud de los microservicios (CPU, Memoria, Errores HTTP) para actuar antes de que el cliente note un fallo. |

---

## 5. Evaluación Ética y Técnica del Diseño

La arquitectura de SmartLogix no solo busca eficiencia técnica, sino que se fundamenta en principios de **Software Responsable** y **Ética en Microservicios**, asegurando un impacto positivo en el ecosistema digital de las PYMEs.

### 5.1 Sostenibilidad Ambiental (Green Computing)

El diseño basado en Kubernetes y Serverless (AWS Lambda) permite una gestión inteligente de los recursos de cómputo:

- **Escalado Dinámico:** A diferencia de los sistemas antiguos que mantenían servidores encendidos 24/7 "por si acaso", SmartLogix consume energía solo cuando hay demanda real, reduciendo la huella de carbono de la infraestructura.
- **Eficiencia de Contenedores:** Al usar Docker, se optimiza el uso de CPU y memoria al compartir el kernel del sistema operativo, permitiendo una mayor densidad de servicios en menos hardware físico.

### 5.2 Privacidad y Protección de Datos (Privacy by Design)

Dado que se gestionan datos sensibles de clientes finales y transacciones comerciales de PYMEs:

- **Cifrado de PII:** Implementación del cifrado de Información de Identificación Personal (PII) mediante AES-256 en reposo y TLS 1.3 en tránsito.
- **Aislamiento de Dominios:** Al usar el patrón Database per Service, se limita el radio de impacto. Si un servicio se ve comprometido, los datos de los otros dominios permanecen aislados y seguros.
- **Tokenización (JWT):** Se evita viajar con credenciales de usuario (passwords) en cada petición, utilizando tokens de sesión con tiempo de expiración limitado y alcance específico (scopes).

### 5.3 Equidad y Transparencia Algorítmica

En la logística, la asignación de pedidos y costos puede generar sesgos si no se diseña correctamente:

- **Transparencia en el Despacho:** El uso del patrón **Factory Method** en el microservicio de envíos garantiza que la selección de couriers sea auditable y basada en reglas de negocio claras (precio, tiempo, cobertura), evitando favoritismos algorítmicos ocultos.
- **Logs de Auditoría Inmutables:** Gracias al Sidecar de Logging, cada cambio de estado en un pedido queda registrado con un *timestamp* y el actor que realizó la acción, permitiendo resolver disputas de forma justa para la PYME y el cliente.

### 5.4 Inclusión y Accesibilidad Digital

El **Core UI-Lib** (Librería de Componentes) no es solo estética, es una herramienta de inclusión:

- **Estándares WCAG:** Todos los componentes frontales están diseñados para ser operables por personas con diversas capacidades (navegación por teclado, contraste de colores y compatibilidad con lectores de pantalla). Esto asegura que cualquier emprendedor, sin importar sus capacidades físicas, pueda gestionar su negocio en la Sucursal Virtual.
