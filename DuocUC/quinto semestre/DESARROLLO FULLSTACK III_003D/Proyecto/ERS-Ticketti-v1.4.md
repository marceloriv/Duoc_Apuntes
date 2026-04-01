# Especificación de Requisitos de Software

**Proyecto:** Ticketti  
**Versión:** 1.10.5  
**Fecha:** 30/03/2026  
**Estándar:** IEEE 830

**Integrantes:**

- Marcelo Rivera
- Ingrid Nuñez
- Meritxell Arroyo
- Pamela Alvarez

---

## Contenido

- [Especificación de Requisitos de Software](#especificación-de-requisitos-de-software)
  - [Contenido](#contenido)
  - [Control de Versiones](#control-de-versiones)
  - [1. Contexto y Objetivos de Negocio](#1-contexto-y-objetivos-de-negocio)
    - [1.1 Propósito](#11-propósito)
    - [1.2 Ámbito del Sistema](#12-ámbito-del-sistema)
      - [Lo que el Sistema Hará](#lo-que-el-sistema-hará)
      - [Lo que el Sistema NO Hará](#lo-que-el-sistema-no-hará)
      - [Beneficios, Objetivos y/o Metas](#beneficios-objetivos-yo-metas)
  - [2. Requerimientos Extendidos del Sistema](#2-requerimientos-extendidos-del-sistema)
    - [2.1 Perspectiva del Producto](#21-perspectiva-del-producto)
    - [2.2 Funciones del Producto](#22-funciones-del-producto)
    - [2.3 Características de los Usuarios](#23-características-de-los-usuarios)
    - [2.4 Restricciones](#24-restricciones)
    - [2.5 Suposiciones y Dependencias](#25-suposiciones-y-dependencias)
    - [2.6 Requisitos Futuros](#26-requisitos-futuros)
  - [3. Requisitos Específicos del Sistema](#3-requisitos-específicos-del-sistema)
    - [3.1 Requisitos comunes de las interfaces](#31-requisitos-comunes-de-las-interfaces)
      - [3.1.1 Interfaces de usuario](#311-interfaces-de-usuario)
      - [3.1.2 Interfaces de hardware](#312-interfaces-de-hardware)
      - [3.1.3 Interfaces de software](#313-interfaces-de-software)
    - [3.2 Requisitos Funcionales (RF)](#32-requisitos-funcionales-rf)
      - [RF-1: Gestión de cuentas y autenticación (MSUsuarios)](#rf-1-gestión-de-cuentas-y-autenticación-msusuarios)
      - [RF-2: Gestión de eventos e inventario (MSEventos)](#rf-2-gestión-de-eventos-e-inventario-mseventos)
      - [RF-3: Compra de entradas e inventario (MSCarrito)](#rf-3-compra-de-entradas-e-inventario-mscarrito)
      - [RF-4: Gestión de causas sociales y donaciones (MSDonaciones)](#rf-4-gestión-de-causas-sociales-y-donaciones-msdonaciones)
      - [RF-5: Sistema de notificaciones automatizadas (MSMensajeria)](#rf-5-sistema-de-notificaciones-automatizadas-msmensajeria)
      - [RF-6: Seguridad de pagos, datos sensibles y sesiones (Transversal)](#rf-6-seguridad-de-pagos-datos-sensibles-y-sesiones-transversal)
    - [3.3 Requisitos no Funcionales](#33-requisitos-no-funcionales)
    - [3.4 Otros Requisitos](#34-otros-requisitos)
    - [3.5 Patrones de diseño obligatorios](#35-patrones-de-diseño-obligatorios)
    - [3.6 Matriz de trazabilidad RF a criterios de aceptación](#36-matriz-de-trazabilidad-rf-a-criterios-de-aceptación)
  - [4. Arquitectura de Software y Ecosistema Front](#4-arquitectura-de-software-y-ecosistema-front)
    - [4.1 Ecosistema Frontend](#41-ecosistema-frontend)
    - [4.2 Capa de Agregación (BFF)](#42-capa-de-agregación-bff)
    - [4.3 Capa de Backend y Microservicios](#43-capa-de-backend-y-microservicios)
      - [4.3.1 Estrategia de actualización entre bases de datos](#431-estrategia-de-actualización-entre-bases-de-datos)
      - [4.3.2 Catálogo de eventos de dominio](#432-catálogo-de-eventos-de-dominio)
      - [A. Microservicio de Usuarios (MSUsuarios)](#a-microservicio-de-usuarios-msusuarios)
      - [B. Microservicio de Eventos (MSEventos)](#b-microservicio-de-eventos-mseventos)
      - [C. Microservicio de Carrito de Compras (MSCarrito)](#c-microservicio-de-carrito-de-compras-mscarrito)
      - [D. Microservicio de Donaciones (MSDonaciones)](#d-microservicio-de-donaciones-msdonaciones)
      - [E. Microservicio de Mensajería (MSMensajeria)](#e-microservicio-de-mensajería-msmensajeria)
    - [4.4 Diagramas de arquitectura de solución](#44-diagramas-de-arquitectura-de-solución)
      - [Diagrama de Package](#diagrama-de-package)
      - [Diagrama de Microservicios](#diagrama-de-microservicios)
      - [Descripción de Componentes](#descripción-de-componentes)
    - [4.5 Diagrama de flujo de eventos (Core Logics)](#45-diagrama-de-flujo-de-eventos-core-logics)
      - [Explicación técnica del comportamiento de colas](#explicación-técnica-del-comportamiento-de-colas)
    - [4.6 Arquitectura de red y alta disponibilidad (Multi-AZ)](#46-arquitectura-de-red-y-alta-disponibilidad-multi-az)
      - [Explicación del diseño de infraestructura](#explicación-del-diseño-de-infraestructura)
    - [4.7 Estrategia de automatización: Pipeline CI/CD](#47-estrategia-de-automatización-pipeline-cicd)
      - [Flujo del pipeline](#flujo-del-pipeline)
  - [5. Matriz de Herramientas y Justificación Técnica](#5-matriz-de-herramientas-y-justificación-técnica)
    - [5.1 Infraestructura y Orquestación](#51-infraestructura-y-orquestación)
    - [5.2 Desarrollo y Lenguajes](#52-desarrollo-y-lenguajes)
    - [5.3 Comunicación y Persistencia](#53-comunicación-y-persistencia)
    - [5.4 Calidad y Observabilidad](#54-calidad-y-observabilidad)
  - [6. Evaluación Ética y Técnica del Diseño](#6-evaluación-ética-y-técnica-del-diseño)
    - [6.1 Sostenibilidad Ambiental (Green Computing)](#61-sostenibilidad-ambiental-green-computing)
    - [6.2 Privacidad y Protección de Datos (Privacy by Design)](#62-privacidad-y-protección-de-datos-privacy-by-design)
    - [6.3 Equidad y Transparencia Algorítmica](#63-equidad-y-transparencia-algorítmica)
    - [6.4 Inclusión y Accesibilidad Digital](#64-inclusión-y-accesibilidad-digital)

---

## Control de Versiones

| Fecha         | Revisión | Autor                        | Modificación                                                                                                                                                                                          |
| ------------- | -------- | ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 19/03/2026    | 1.0      | Marcelo Rivera, Ingrid Núñez | Inicio de construcción de ERS.                                                                                                                                                                        |
| 21–22/03/2026 | 1.1      | Meritxell Arroyo             | Requisitos funcionales y no funcionales.                                                                                                                                                              |
| 22/03/2026    | 1.2      | Pamela Alvarez               | Completados 1.2, 2.1, 2.4, 2.5, 2.6, 3.1.1, 3.1.2, 3.1.3, 3.4. RNF con valores de industria. 3.2 pasado a tabla.                                                                                      |
| 24/03/2026    | 1.3      | Ingrid Núñez                 | Integración de sistema de notificaciones como RF. Inicio del desarrollo de 4.1, 4.2, 4.3.                                                                                                             |
| 24/03/2026    | 1.4      | Pamela Alvarez               | 3.2: reestructuración de requisitos, separados por módulos.                                                                                                                                           |
| 26/03/2026    | 1.5      | Pamela Alvarez               | 3.2: ajuste de requisitos a los microservicios finales.                                                                                                                                               |
| 26/03/2026    | 1.6      | Ingrid Núñez                 | Desarrollo del diagrama de Package.                                                                                                                                                                   |
| 30/03/2026    | 1.7      | Equipo Ticketti              | Ajustes de arquitectura: BFF definido, RNF medibles, patrones obligatorios (Repository, Factory Method, Circuit Breaker), y cierre de contradicciones de negocio.                                     |
| 30/03/2026    | 1.8      | Equipo Ticketti              | Definición de seguridad de pagos (idempotencia, tokenización y webhook firmado), consistencia distribuida con Saga y cierre adicional de puntos críticos.                                             |
| 30/03/2026    | 1.9      | Equipo Ticketti              | Normalización integral de la ERS: coherencia RF/RNF, política de supresión por fases, contratos API alineados a reglas de negocio, seguridad avanzada de sesión/webhooks y cierre de puntos abiertos. |
| 30/03/2026    | 1.9.1    | Equipo Ticketti              | Cierre de ambigüedades de RF (devoluciones, visibilidad, idempotencia, QR, bloqueo de login, fondo general) y matriz de trazabilidad con criterios de aceptación.                                     |
| 30/03/2026    | 1.9.2    | Equipo Ticketti              | Alineación de nomenclatura entre Funciones del Producto y encabezados RF, con trazabilidad explícita Función-RF.                                                                                      |
| 30/03/2026    | 1.9.3    | Equipo Ticketti              | Definición formal de estrategia de actualización entre bases de datos por microservicio (Saga, Outbox/Inbox, idempotencia, reconciliación y SLO de convergencia).                                     |
| 30/03/2026    | 1.9.4    | Equipo Ticketti              | Incorporación del catálogo de eventos de dominio con productor, consumidor, clave idempotente, política de retry y DLQ.                                                                               |
| 30/03/2026    | 1.10     | Equipo Ticketti              | Adaptación de formato estructural para alineación con Arquitectura_SmartLogix (secciones de arquitectura extendida, matriz de herramientas y evaluación ética/técnica).                                |
| 30/03/2026    | 1.10.1   | Equipo Ticketti              | Profundización técnica de la sección Multi-AZ con componentes concretos de red, orquestación, mensajería, persistencia y continuidad operacional.                                                      |
| 30/03/2026    | 1.10.2   | Equipo Ticketti              | Corrección de coherencia funcional por rol en cancelación de eventos, fortalecimiento operativo de seguridad webhook y formalización de continuidad operacional como RNF.                                |
| 30/03/2026    | 1.10.3   | Equipo Ticketti              | Cierre de brechas de formato: separación de frentes frontend, BFF por frente, descripción técnica de componentes (4.4) y flujo de eventos detallado por fases (4.5).                                    |
| 30/03/2026    | 1.10.4   | Equipo Ticketti              | Estandarización del stack frontend con React Bootstrap para portales por rol y librería visual compartida.                                                                                               |
| 30/03/2026    | 1.10.5   | Equipo Ticketti              | Cierre de brechas de profundidad y consistencia: numeración correlativa del flujo 4.5, stack/runtime explícito en frontend y BFF, Swagger reubicado como artefacto API, CI/CD detallado por herramientas, matriz técnica ampliada y evaluación ética desarrollada en prosa. |

---

## 1. Contexto y Objetivos de Negocio

### 1.1 Propósito

Detallar los requerimientos necesarios para construir un software de gestión de eventos que permite visualizar eventos por categoría, comprar tickets de forma rápida y segura, recibir notificaciones y destinar un porcentaje de cada venta a organizaciones sin fines de lucro. Este documento está dirigido principalmente al equipo de desarrolladores, para garantizar una comprensión clara del sistema y asegurar su correcta funcionalidad. El desarrollo será entregado al cliente para su evaluación.

### 1.2 Ámbito del Sistema

**Nombre del sistema:** Ticketti

#### Lo que el Sistema Hará

- Permitir la visualización y búsqueda de eventos disponibles, organizados por categoría, fecha y ubicación.
- Gestionar la compra de entradas de forma rápida y segura, con control de stock para evitar sobreventas.
- Enviar notificaciones automáticas al usuario ante acciones relevantes, tales como la confirmación de compra, devoluciones aprobadas y recomendaciones personalizadas.
- Destinar automáticamente un 10% fijo de cada venta a organizaciones sin fines de lucro registradas en la plataforma.
- Permitir a organizadores crear, publicar y administrar sus eventos, incluyendo la definición de tipos de entradas, cupos y restricciones.

#### Lo que el Sistema NO Hará

- El sistema no gestionará la logística física ni la distribución de productos tangibles asociados a los eventos.
- El sistema no operará como pasarela de pago independiente ni procesará transacciones en monedas extranjeras.

#### Beneficios, Objetivos y/o Metas

- Generar un canal de impacto social medible, vinculando el consumo cultural con donaciones a causas de bien público.
- Reducir la fricción en el proceso de compra de entradas, ofreciendo una experiencia digital simple e intuitiva, alineada con los estándares de la industria.
- Proporcionar a los organizadores herramientas de gestión de eventos sin necesidad de infraestructura tecnológica propia.
- Aumentar la visibilidad y captación de fondos de organizaciones sin fines de lucro registradas en la plataforma.
- Diferenciarse de plataformas de ticketing tradicionales mediante la integración del propósito social como parte central del modelo de negocio.

---

## 2. Requerimientos Extendidos del Sistema

### 2.1 Perspectiva del Producto

Ticketti es un sistema independiente de gestión de venta de entradas a eventos con impacto social, diseñado para operar como plataforma digital de uso público. El sistema no reemplaza pasarelas de pago externas, sino que se integra con ellas para completar las transacciones de forma segura. Internamente, la plataforma cuenta con una interfaz web accesible desde distintos dispositivos y un conjunto de servicios backend orientados a la escalabilidad y la disponibilidad. Adicionalmente, el sistema se integra con un servicio de notificaciones para la comunicación con los usuarios y gestiona la persistencia de datos mediante bases de datos relacionales por microservicio.

### 2.2 Funciones del Producto

| Nombre de la Función                     | Descripción de la Función                                                                                                                              | RF Asociado |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------- |
| Gestión de cuentas                       | Registro e inicio de sesión de usuario mediante credenciales, eliminación de cuenta de usuario, soporte para administrador, comprador y organizador.   | RF-1        |
| Gestión de eventos                       | Creación, edición y publicación de eventos por organizadores; cancelación de eventos publicados solo por administrador.                                | RF-2        |
| Compra de entradas                       | Permite al usuario comprar entradas del evento de su preferencia.                                                                                      | RF-3        |
| Gestión de inventario                    | Control de stock por tipo de entrada con cupo límite para evitar sobreventas en compras simultáneas.                                                   | RF-3        |
| Sistema de notificaciones                | Envío de alertas sobre compras, devoluciones y recomendaciones a los usuarios.                                                                         | RF-5        |
| Devolución de entradas                   | Procesamiento de reembolsos según política de devolución del evento, con notificación al comprador.                                                    | RF-3        |
| Filtros y categoría                      | Permite buscar eventos según filtros y categorías, ubicación o fecha.                                                                                  | RF-2        |
| Visualización de estadísticas de compras | Permite visualizar el historial y estado de compras del usuario comprador.                                                                             | RF-3        |
| Apoyo a causas sociales                  | Permite al usuario comprador seleccionar durante la compra una organización sin fines de lucro a la cual se destinará un porcentaje de su transacción. | RF-4        |

> Regla de concordancia: toda función definida en 2.2 debe mapear al menos a un RF de 3.2.

### 2.3 Características de los Usuarios

| Nombre del Usuario | Habilidades Digitales | Experiencia Técnica |
|--------------------|----------------------|---------------------|
| Administrador | Experiencia media | Computación Alta |
| Comprador | Experiencia mínima | Computación Básica |
| Organizador | Experiencia media | Computación Media |
| Invitado | Variable | Varía según familiaridad con la tecnología |

### 2.4 Restricciones

- El sistema será desarrollado utilizando tecnologías web modernas del ecosistema Java y Javascript, según las decisiones técnicas adoptadas por el equipo de desarrollo al inicio del proyecto.
- El procesamiento de pagos no será implementado de forma nativa; el sistema delegará esta responsabilidad a una pasarela de pago externa certificada (Transbank/Webpay).

### 2.5 Suposiciones y Dependencias

- Se asume que los organizadores de eventos cuentan con acceso a internet y un dispositivo compatible para gestionar sus eventos a través de la plataforma, sin requerir capacitación técnica especializada.
- El correcto funcionamiento del módulo de pagos depende de la disponibilidad y estabilidad del servicio de la pasarela de pago externa integrada (Transbank/Webpay).

### 2.6 Requisitos Futuros

- En una versión posterior, se contempla la implementación de un motor de recomendaciones personalizadas de eventos, basado en el historial de compras y las preferencias registradas de cada usuario.
- Se proyecta la integración con redes sociales para que los compradores puedan compartir eventos y entradas adquiridas, ampliando el alcance orgánico de la plataforma.

---

## 3. Requisitos Específicos del Sistema

### 3.1 Requisitos comunes de las interfaces

#### 3.1.1 Interfaces de usuario

La interfaz de Ticketti será web y completamente responsiva, adaptada para su uso en dispositivos móviles, tablets y computadoras de escritorio. El diseño seguirá principios de usabilidad reconocidos por la industria, con navegación clara, paleta de colores consistente con la identidad de marca y formularios con validación en tiempo real. Los usuarios accederán a la plataforma desde cualquier navegador web moderno, sin necesidad de instalar software adicional.

#### 3.1.2 Interfaces de hardware

El sistema será desplegado en servidores con sistema operativo Linux, haciendo uso de tecnologías de contenedores para garantizar portabilidad y facilitar el mantenimiento. Los usuarios finales accederán a la plataforma desde sus propios dispositivos (smartphones, tablets, laptops o computadoras de escritorio), sin requerir hardware especializado ni configuraciones adicionales de su parte.

#### 3.1.3 Interfaces de software

- **Base de datos relacional (MySQL):** almacenamiento persistente de usuarios, eventos, compras y donaciones.
- **Sistema operativo del servidor (Linux/Ubuntu):** plataforma de despliegue con soporte para contenedores.
- **Servicio de notificaciones por correo (SMTP/SendGrid):** envío de confirmaciones, alertas y recomendaciones a los usuarios.

---

### 3.2 Requisitos Funcionales (RF)

#### RF-1: Gestión de cuentas y autenticación (MSUsuarios)

● **RF-1.1 Registro por rol:** El sistema debe permitir registrar usuarios diferenciando flujo por rol (Comprador u Organizador) con aceptación de términos según corresponda.

● **RF-1.2 Autenticación:** El sistema debe autenticar usuarios por correo y contraseña, bloqueando la cuenta por 15 minutos tras 3 intentos fallidos.

● **RF-1.3 Eliminación de cuenta:** El sistema debe permitir eliminar cuenta en fases: bloqueo inmediato, retención de 30 días y purga irreversible.

● **RF-1.4 Exportar datos:** El sistema debe permitir descargar datos personales en JSON o PDF con enlace que expira en 1 hora.

● **RF-1.5 Revocar consentimiento:** El sistema debe permitir revocar consentimientos opcionales (notificaciones, recomendaciones) desde privacidad.

● **RF-1.6 Gestión de usuarios (Admin):** El administrador debe consultar, activar, suspender y cambiar rol de usuarios.

#### RF-2: Gestión de eventos e inventario (MSEventos)

● **RF-2.1 Crear evento:** El organizador debe poder crear eventos definiendo nombre, descripción, categoría, ubicación y capacidad máxima.

● **RF-2.2 Editar y publicar evento:** El organizador debe editar eventos en borrador y publicarlos. Solo administrador puede cancelar publicados.

● **RF-2.3 Visualizar evento:** Cualquier usuario debe poder listar y visualizar detalles completos del evento (nombre, fecha, locación, disponibilidad, precios, causas activas).

● **RF-2.4 Buscar y filtrar:** El sistema debe permitir buscar eventos por nombre, artista, ubicación y categoría con ranking auditable.

#### RF-3: Compra de entradas e inventario (MSCarrito)

● **RF-3.1 Seleccionar entradas:** El comprador debe poder seleccionar máximo 4 entradas por compra, validando disponibilidad en tiempo real.

● **RF-3.2 Gestionar carrito:** El sistema debe permitir agregar, modificar y eliminar entradas, recalculando subtotal + 10% donación automáticamente.

● **RF-3.3 Confirmar compra:** Al confirmar, el sistema valida stock, procesa pago por pasarela externa y publica eventos hacia donaciones y notificaciones.

● **RF-3.3.1 Reserva de stock:** El sistema debe reservar stock por 5 minutos (renovable 1 vez por 2 minutos). Si expira, la reserva se libera automáticamente.

● **RF-3.4 Solicitar devolución:** El comprador puede solicitar devolución con reembolso del 85% si el evento no ha ocurrido y se realiza hasta 48 horas antes.

● **RF-3.4.1 Cálculo de devolución:** La devolución se calcula solo sobre entradas; el 10% donado es no reembolsable.

● **RF-3.5 Historial de compras:** El comprador debe visualizar su historial con estado, detalle de entradas y montos pagados/donados.

#### RF-4: Gestión de causas sociales y donaciones (MSDonaciones)

● **RF-4.1 Calcular donación 10%:** El sistema debe calcular automáticamente 10% fijo de la compra como donación, sin posibilidad de modificación.

● **RF-4.2 Seleccionar causa:** El comprador debe poder seleccionar la causa social a la que destinar el 10%, o usar fondo general si no hay causas activas.

● **RF-4.3 Persistir donación:** El sistema debe registrar la donación vinculada a la transacción, causa y monto para auditoría.

● **RF-4.4 Administrar causas:** El administrador debe crear, activar y desactivar causas. Las causas desactivadas no aparecen en nuevas compras pero conservan donaciones históricas.

#### RF-5: Sistema de notificaciones automatizadas (MSMensajeria)

● **RF-5.1 Enviar QR:** Al confirmar compra, el sistema genera y envía QR único por entrada como credencial de acceso de un solo uso.

● **RF-5.2 Confirmación de compra:** El sistema envía confirmación con detalle: entradas, evento, fecha, precio total, monto donado y causa beneficiada.

● **RF-5.3 Notificación de devolución:** Al resolver devolución, el sistema notifica el resultado, monto reembolsado y plazo de acreditación.

● **RF-5.4 Recomendaciones:** El sistema envía recomendaciones personalizadas únicamente si el usuario tiene consentimiento explícito.

#### RF-6: Seguridad de pagos, datos sensibles y sesiones (Transversal)

● **RF-6.1 Tokenización de pago:** El sistema no debe almacenar números completos de tarjeta; debe usar tokenización de pasarela externa.

● **RF-6.2 Idempotencia:** Toda operación de cobro debe incluir clave de idempotencia única por transacción con vigencia mínima de 24 horas.

● **RF-6.3 Validación de webhook:** Todo callback de confirmación de pago debe validar firma HMAC-SHA256. Eventos inválidos se rechazan.

● **RF-6.4 HTTPS/TLS:** Toda operación de autenticación, compra y descarga de datos personales debe operar sobre HTTPS.

● **RF-6.5 Timeout en pasarela:** Las llamadas a pasarela de pago tienen timeout máximo de 10 segundos con política de retry exponencial.

● **RF-6.6 Refresh token seguro:** El refresh token se almacena en cookie HttpOnly + Secure + SameSite con protección CSRF.

● **RF-6.7 Anti-replay:** Todo webhook incluye timestamp y nonce para impedir replay. Eventos duplicados se descartan.

● **RF-6.8 Rotación de tokens:** El sistema implementa rotación de refresh token por uso y revocación inmediata ante cierre de sesión.

---

### 3.3 Requisitos no Funcionales

Atributos de Calidad según ISO 25010 (16 unidades):

| Id. | Nombre Corto | Descripción | Atributo de Calidad |
|-----|-------------|-------------|---------------------|
| RNF01 | Concurrencia mínima | El sistema debe soportar al menos 300 usuarios concurrentes en flujo de compra y 1.000 usuarios concurrentes en navegación de catálogo, manteniendo estabilidad funcional. | Rendimiento |
| RNF02 | Latencia de respuesta | El tiempo de respuesta del flujo crítico (búsqueda de eventos y resumen de compra) debe ser <= 2 segundos en el percentil 95. | Rendimiento |
| RNF03 | Compatibilidad web | El sistema debe operar correctamente en las dos últimas versiones estables de Chrome, Edge y Firefox. | Compatibilidad |
| RNF04 | Recuperación de compra | El estado del carrito y compra debe recuperarse tras fallos transitorios en un máximo de 5 minutos. | Fiabilidad |
| RNF05 | Disponibilidad del servicio | El sistema debe mantener una disponibilidad mensual de al menos 99.5%. | Fiabilidad |
| RNF06 | Seguridad de datos | El sistema debe cifrar datos en tránsito (HTTPS/TLS) y proteger credenciales con hash fuerte (bcrypt/Argon2). | Seguridad |
| RNF07 | Resiliencia entre servicios | Las llamadas críticas entre microservicios deben implementar timeout, retry y circuit breaker. | Fiabilidad |
| RNF08 | Mantenibilidad del código | Cada microservicio debe separar capas Controller, Service, Repository y mantener cobertura unitaria >= 60%. | Mantenibilidad |
| RNF09 | Portabilidad de despliegue | Cada microservicio debe poder desplegarse en contenedores Docker sin dependencia de entorno local. | Portabilidad |
| RNF10 | Observabilidad | El sistema debe registrar trazas, métricas y errores técnicos para auditoría y diagnóstico operacional. | Mantenibilidad |
| RNF11 | Métricas de experiencia web | El frontend debe cumplir LCP <= 2.5s, FID <= 100ms y CLS <= 0.1 en condiciones normales de red. | Rendimiento |
| RNF12 | SLO de checkout | El flujo de checkout (validar stock + iniciar pago) debe responder en <= 3 segundos en percentil 95, excluyendo latencia de entidad financiera externa. | Rendimiento |
| RNF13 | Integridad de eventos asíncronos | Los eventos críticos de compra y donación deben garantizar entrega al menos una vez y deduplicación en consumidor mediante clave idempotente. | Fiabilidad |
| RNF14 | Recuperación operativa | El sistema debe contar con DLQ y reproceso controlado de mensajes, con tiempo objetivo de recuperación operacional <= 15 minutos para incidentes recuperables. | Fiabilidad |
| RNF15 | Convergencia de datos interservicio | Tras una compra confirmada, los estados de compra, stock y donación deben converger entre microservicios en <= 60 segundos en percentil 95, con monitoreo de lag y alertas. | Fiabilidad |
| RNF16 | Continuidad operacional | La plataforma debe cumplir RPO <= 15 minutos y RTO <= 60 minutos para servicios críticos, con simulacros de recuperación al menos mensuales y evidencia auditada de resultados. | Fiabilidad |

### 3.4 Otros Requisitos

- El sistema deberá cumplir con la Ley N°21.719 sobre Protección y Tratamiento de los Datos Personales, vigente en Chile desde el 13 de diciembre de 2024, aplicando los principios de consentimiento explícito, minimización de datos, privacidad por diseño y notificación de brechas de seguridad.
- El porcentaje destinado a organizaciones sin fines de lucro será fijo en 10% por transacción completada, conforme a RF-4.1.

### 3.5 Patrones de diseño obligatorios

- **Repository Pattern (obligatorio):** Cada microservicio debe implementar capa Repository para persistencia y acceso a datos, desacoplando lógica de negocio de la tecnología de base de datos.
- **Factory Method (obligatorio):** La creación de entidades de dominio y objetos de aplicación debe centralizarse en fábricas para evitar inicializaciones inconsistentes.
- **Circuit Breaker (obligatorio):** Toda comunicación crítica entre microservicios o con servicios externos debe usar Circuit Breaker con timeout y fallback definidos.

### 3.6 Matriz de trazabilidad RF a criterios de aceptación

La siguiente matriz define criterios verificables en formato Given/When/Then para asegurar pruebas funcionales reproducibles.

| RF | Given | When | Then |
|----|-------|------|------|
| RF-1.1 | Un usuario nuevo inicia registro por rol | Acepta términos requeridos y envía formulario | Se crea la cuenta y se registra evidencia auditable de consentimiento (idUsuario, versión aceptada, timestamp, IP y acción), además del estado vigente de consentimiento |
| RF-1.2 | Una cuenta existente intenta autenticarse | Ocurren 3 fallos consecutivos por cuenta | La cuenta queda bloqueada por 15 minutos y se aplica rate limiting por IP/dispositivo |
| RF-1.3 | Un usuario autenticado solicita eliminación | Confirma reautenticación | La cuenta se bloquea de inmediato, se inicia retención técnica y se agenda purga irreversible a 30 días |
| RF-1.4 | Un usuario solicita portabilidad de datos | Se genera enlace de exportación | El enlace expira en 1 hora o tras una descarga exitosa |
| RF-1.5 | Un usuario tiene consentimientos opcionales activos | Revoca consentimiento en privacidad | Se detiene el envío de recomendaciones/notificaciones opcionales sin bloquear funciones principales |
| RF-1.6 | Un administrador autenticado gestiona usuarios | Activa, suspende o cambia rol de una cuenta | La acción se ejecuta y queda auditada con actor, fecha y hora |
| RF-2.1 | Un organizador crea un evento en borrador | Define categoría, locación y capacidad por ticket | El evento se persiste y su capacidad queda disponible para consulta de carrito |
| RF-2.2 | Existe un evento publicado con ventas activas | Un organizador intenta cambiar capacidad o cancelar | El cambio de capacidad se rechaza y solo administrador puede cancelar con motivo obligatorio |
| RF-2.3 | Un visitante sin sesión accede al catálogo | Solicita detalle de un evento | Visualiza nombre, fecha, locación, stock, precio, restricciones y causas activas |
| RF-2.4 | Existen eventos de múltiples organizadores en una categoría | Se consulta la primera página de resultados | El ranking aplica rotación y límite de exposición repetida, con métricas de impresiones auditables |
| RF-3.1 | Un comprador autenticado agrega entradas al carrito | Supera el límite permitido | El sistema rechaza cantidades mayores a 4 entradas por compra |
| RF-3.2 | Un carrito tiene entradas seleccionadas | Se agrega, modifica o elimina un ítem | El resumen recalcula subtotal y 10% de donación en tiempo real |
| RF-3.3 | Hay stock reservado y pago disponible | El comprador confirma checkout con idempotencia | Se procesa cobro, se confirma rebaja de stock y se emiten eventos Outbox a donaciones/mensajería |
| RF-3.3.1 | Un comprador inicia checkout | Solicita reserva de stock y no confirma a tiempo | La reserva expira (5 min + 2 min renovación única) y el estado pasa a Expirado |
| RF-3.4 | Una entrada pertenece a evento no ocurrido | El comprador solicita devolución fuera de plazo o dentro de 48h previas | Dentro del plazo se aprueba con reembolso 85%; fuera de plazo se rechaza |
| RF-3.4.1 | Existe una devolución aprobada | Se emite comprobante | Se informa monto reembolsable y donación como no reembolsable |
| RF-3.5 | Un comprador tiene compras históricas | Consulta su historial | Visualiza estado, detalle de entradas, monto pagado y monto donado por transacción |
| RF-4.1 | Una compra válida se confirma | Se calcula componente social | La donación corresponde al 10% fijo no editable |
| RF-4.2 | No existen causas sociales activas | El usuario confirma compra | Se imputa donación a fondo general con trazabilidad de transacción y conciliación |
| RF-4.3 | Una compra se confirma correctamente | Se dispara evento de donación | MSDonaciones persiste monto, causa y transacción para auditoría |
| RF-4.4 | Un administrador gestiona causas | Activa o desactiva una causa | Se actualiza disponibilidad para nuevas compras y se preserva historial existente |
| RF-5.1 | Una compra está confirmada | Se genera credencial de acceso | Se envía QR único de un solo uso, revocable y con reemisión que invalida el anterior |
| RF-5.2 | Compra y donación confirmadas | Se construye mensaje de confirmación | El comprador recibe detalle de entradas, evento, monto total y causa beneficiada |
| RF-5.3 | Existe una devolución resuelta | Se gatilla notificación | El comprador recibe resultado, monto reembolsado y plazo estimado de acreditación |
| RF-5.4 | Usuario sin consentimiento de recomendaciones | Se intenta envío de recomendación | El envío se bloquea automáticamente |
| RF-6.1 | Se inicia una transacción de pago | El sistema prepara payload de cobro | Solo se transmite token de pago, sin almacenar PAN completo |
| RF-6.2 | Se reintenta un cobro con misma clave | El payload es idéntico o distinto | Con payload idéntico retorna resultado previo; con payload distinto responde conflicto auditado |
| RF-6.3 | La pasarela envía webhook de confirmación | Firma HMAC, timestamp o nonce son inválidos | El evento se rechaza, no muta estado y se registra intento |
| RF-6.4 | Un usuario opera autenticación o compra | La comunicación ocurre entre cliente y servicios | Todo el tránsito usa HTTPS/TLS |
| RF-6.5 | Una llamada a pasarela supera SLA | Se agota timeout o retry exponencial | El flujo aplica fallback controlado y registra incidente |
| RF-6.6 | Existe refresh token en navegador | Se solicita renovación de sesión | Solo se acepta cookie HttpOnly/Secure/SameSite con validación CSRF |
| RF-6.7 | Llega un webhook previamente procesado | Se detecta replay por nonce/timestamp | Se descarta el evento y se registra duplicado |
| RF-6.8 | El usuario cierra sesión o se detecta compromiso | Se emite nueva sesión o revocación | Se rota o revoca refresh token de forma inmediata |

---

## 4. Arquitectura de Software y Ecosistema Front

Para garantizar una solución escalable y centrada en el usuario, Ticketti adopta una arquitectura de microservicios desacoplados. Esta estructura permite que cada componente sea independiente en su despliegue y escalabilidad, gestionando su propia lógica de negocio y persistencia de datos (MySQL), comunicándose entre sí mediante protocolos REST y mensajería en formato JSON.

Cada microservicio debe operar con el principio **Database per Service** (esquema o base propia), sin acceso directo entre tablas de otros dominios. La integración entre dominios se realiza exclusivamente por API o eventos.

### 4.1 Ecosistema Frontend

Para este proyecto se han diseñado interfaces especializadas según el rol y el contexto de uso.

| Componente | Tecnología | Función / Propósito |
|------------|-----------|---------------------|
| Portal Comprador | Vite + React Router (React) + React Bootstrap + Node.js 20 LTS | Interfaz pública para explorar eventos, comprar entradas y gestionar historial personal. |
| Portal Organizador | Vite + React Router (React) + React Bootstrap + Node.js 20 LTS | Interfaz de operación para crear, publicar y administrar eventos. |
| Panel Administrador | Vite + React Router (React) + React Bootstrap + Node.js 20 LTS | Interfaz de gobierno para usuarios, causas sociales, cancelaciones y métricas de plataforma. |
| UI-Lib Ticketti | React Bootstrap + tema corporativo | Librería compartida de componentes para consistencia visual y funcional entre los tres frentes. |

Lineamiento de implementación frontend: los componentes base de interfaz (formularios, tablas, navegación, modales, alertas y layout responsivo) se construirán sobre React Bootstrap para mantener uniformidad visual, accesibilidad y velocidad de desarrollo.

### 4.2 Capa de Agregación (BFF)

Ticketti implementa BFF por frente para optimizar payload, seguridad y desacoplamiento por contexto de uso. Todos los BFF se desarrollan en Node.js 20 LTS con NestJS, exponiendo APIs REST versionadas:

- BFF-Comprador: catálogo, checkout, historial y notificaciones de compra.
- BFF-Organizador: gestión de eventos, capacidades y métricas de ventas por evento.
- BFF-Administrador: gobierno de usuarios, causas sociales, auditoría y operaciones críticas.

Todos los BFF comparten responsabilidades transversales:

- Autenticación y autorización basada en JWT para clientes web.
- Agregación de respuestas de múltiples microservicios para reducir llamadas desde frontend.
- Validación de entrada y estandarización de errores HTTP para consumo del cliente.
- Aplicación de políticas de resiliencia (timeout, retry y circuit breaker) antes de invocar microservicios.
- Trazabilidad de solicitudes mediante identificador de correlación por request.
- Gestión de sesión con access token de corta duración y refresh token en cookie HttpOnly.
- Protección CSRF para operaciones de renovación de sesión y rotación de refresh token por uso.

### 4.3 Capa de Backend y Microservicios

La arquitectura del software Ticketti se fundamenta en un modelo de microservicios desacoplados. Cada componente mantiene su propia lógica de negocio y persistencia (MySQL), con capas Controller, Service y Repository. La comunicación entre servicios combina REST para consulta y comandos síncronos, y mensajería JSON para eventos de dominio asíncronos. Para consistencia de operaciones distribuidas (compra, stock, donación, notificación), se utiliza consistencia eventual con patrón Saga.

Para operaciones críticas de dinero e inventario, la Saga se implementa con **orquestación** liderada por MSCarrito. Para notificaciones y procesos no críticos, se permite **coreografía** orientada a eventos. El broker de mensajería seleccionado para el proyecto es RabbitMQ, con colas de reintento y Dead Letter Queue para fallos no recuperables. Los eventos críticos deben publicarse con patrón Outbox y consumirse con deduplicación por idempotencia.

#### 4.3.1 Estrategia de actualización entre bases de datos

Dado que cada microservicio mantiene su propia base de datos, Ticketti no utiliza transacciones distribuidas globales (2PC). La sincronización entre dominios se asegura mediante consistencia eventual controlada con las siguientes reglas:

- **Consistencia local fuerte por servicio:** cada microservicio garantiza atomicidad en su propia BD para cambios de su dominio.
- **Patrón Outbox en productor:** el cambio de estado y el evento de dominio se persisten en la misma transacción local antes de publicar al broker.
- **Patrón Inbox/idempotencia en consumidor:** cada consumidor registra `eventId` o `idempotencyKey` para evitar procesamiento duplicado.
- **Reintentos y DLQ:** todo evento fallido sigue política de retry exponencial y deriva a Dead Letter Queue cuando no es recuperable automáticamente.
- **Compensaciones Saga:** si falla un paso crítico posterior, se ejecutan acciones compensatorias (por ejemplo, liberar reserva de stock o revertir estado de compra) para mantener integridad de negocio.
- **Reconciliación operacional:** procesos programados validan divergencias entre dominios (compra-stock-donación) y generan correcciones auditables.
- **SLO de convergencia:** la propagación de estados entre servicios debe cumplir RNF15 con monitoreo de lag por cola y alarmas de incumplimiento.

#### 4.3.2 Catálogo de eventos de dominio

Convención de nomenclatura: los nombres de eventos y colas del dominio se definen en español.

| Nombre del evento | Productor | Consumidor(es) | Clave idempotente | Política de retry | DLQ |
|-------------------|-----------|----------------|-------------------|-------------------|-----|
| `compra.checkout.solicitado.v1` | MSCarrito | MSEventos | `idTransaccion` | 3 reintentos exponenciales (2s, 4s, 8s) | `dlq.compra.checkout.solicitado` |
| `stock.reservado.v1` | MSEventos | MSCarrito | `idReserva` | 3 reintentos exponenciales (2s, 4s, 8s) | `dlq.stock.reservado` |
| `pago.aprobado.v1` | MSCarrito | MSEventos, MSDonaciones, MSMensajeria | `idPago` | 5 reintentos exponenciales (2s, 4s, 8s, 16s, 32s) | `dlq.pago.aprobado` |
| `pago.rechazado.v1` | MSCarrito | MSEventos, MSMensajeria | `idPago` | 5 reintentos exponenciales (2s, 4s, 8s, 16s, 32s) | `dlq.pago.rechazado` |
| `stock.confirmado.v1` | MSEventos | MSCarrito, MSMensajeria | `idReserva` | 3 reintentos exponenciales (2s, 4s, 8s) | `dlq.stock.confirmado` |
| `donacion.registrada.v1` | MSDonaciones | MSCarrito, MSMensajeria | `idDonacion` | 3 reintentos exponenciales (2s, 4s, 8s) | `dlq.donacion.registrada` |
| `entrada.qr.generada.v1` | MSMensajeria | MSCarrito | `idEntrada` | 3 reintentos exponenciales (2s, 4s, 8s) | `dlq.entrada.qr.generada` |
| `reembolso.solicitado.v1` | MSCarrito | MSEventos | `idReembolso` | 3 reintentos exponenciales (2s, 4s, 8s) | `dlq.reembolso.solicitado` |
| `reembolso.aprobado.v1` | MSCarrito | MSMensajeria, MSDonaciones | `idReembolso` | 5 reintentos exponenciales (2s, 4s, 8s, 16s, 32s) | `dlq.reembolso.aprobado` |

Regla obligatoria: cada consumidor debe persistir la clave idempotente en su Inbox antes de aplicar cambios de estado para garantizar consistencia de negocio ante duplicados.

---

#### A. Microservicio de Usuarios (MSUsuarios)

**Responsabilidad:** Gestión de cuentas, perfiles y seguridad por roles.

**Base URL:** `/api/v1/Usuario`

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| POST | `/registro` | Registro y creación de nuevos perfiles (Asistentes u Organizadores). |
| GET | `/lista` | Consulta de listado global de usuarios (Solo Administrador). |
| GET | `/{id}` | Obtención de información de perfil y permisos de un usuario. |
| PUT | `/actualizar` | Actualización de datos personales y configuración de cuenta. |
| DELETE | `/{id}` | Inicio de proceso de eliminación por fases (bloqueo inmediato, retención temporal, purga final). |

---

#### B. Microservicio de Eventos (MSEventos)

**Responsabilidad:** Gestión básica de eventos.

**Base URL:** `/api/v1/Evento`

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| POST | `/crearEvento` | Creación de un nuevo evento con sus atributos (nombre, fecha, locación, capacidad, categoría). |
| GET | `/lista` | Listar todos los eventos disponibles. |
| GET | `/{id}` | Ver detalle de un evento específico (locación, capacidad y fechas). |
| PUT | `/{id}` | Actualiza los datos de un evento existente. |
| PATCH | `/{id}/estado` | Cambia estado del evento (borrador, publicado, cancelado). Cancelación solo administrador con motivo obligatorio. |
| POST | `/{id}/reservas` | Crea reserva temporal de stock para proceso de compra. |
| DELETE | `/{id}/reservas/{reservaId}` | Libera reserva de stock expirada o cancelada. |

---

#### C. Microservicio de Carrito de Compras (MSCarrito)

**Responsabilidad:** Gestión de la compra de entradas: agregado, eliminación y confirmación.

El carrito se implementa como microservicio con persistencia propia para garantizar recuperación ante fallos, trazabilidad y soporte multi-dispositivo.

**Base URL:** `/api/v1/Carrito`

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| POST | `/crearVentaCarrito` | Realiza una compra de entrada(s). |
| GET | `/listarVentasCarrito` | Muestra el registro de todas las ventas efectuadas. |
| GET | `/ventas/{id}` | Obtiene una venta específica por id. |
| DELETE | `/vaciarCarrito/{id}` | Elimina por completo la venta de entrada del usuario, por id. |
| PUT | `/actualizarVentaCarrito/{id}` | Actualiza cantidad y tipo de entradas del carrito, respetando máximo 4 entradas por compra y vigencia de reserva. |
| POST | `/checkout/{id}` | Inicia orquestación Saga de compra y procesa pago con idempotencia. |
| POST | `/devoluciones/{id}` | Solicita devolución de entradas según política vigente. |

> **Nota de integración:** MSCarrito consume MSEventos para validar disponibilidad de stock antes de confirmar la compra. Ante una compra exitosa, dispara eventos asincrónicos hacia MSDonaciones y MSMensajeria.

---

#### D. Microservicio de Donaciones (MSDonaciones)

**Responsabilidad:** Gestión del porcentaje solidario integrado en cada transacción.

**Base URL:** `/api/v1/Donacion`

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| POST | `/registrar` | Persiste la donación vinculada al ID de transacción, causa y monto. |
| GET | `/causas` | Lista las causas sociales activas disponibles. |
| GET | `/historial/{userId}` | Consulta el historial de donaciones de un usuario. |
| POST | `/causas` | Crea una nueva causa social (Administrador). |
| PUT | `/causas/{id}` | Activa o desactiva una causa social (Administrador). |

---

#### E. Microservicio de Mensajería (MSMensajeria)

**Responsabilidad:** Gestión de la comunicación saliente de forma asíncrona hacia los usuarios finales.

**Base URL:** `/api/v2/mensajeria`

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| POST | `/enviar-ticket` | Envía el correo con el QR tras confirmar la compra. |
| POST | `/notificar` | Envía alertas push o avisos generales al celular. |
| GET | `/historial/{id}` | Revisa qué correos se han enviado a un usuario. |
| POST | `/recordatorio` | Envía el aviso de "tu evento es mañana". |
| DELETE | `/cancelar/{id}` | Detiene un envío si el evento se suspende. |

---

### 4.4 Diagramas de arquitectura de solución

#### Diagrama de Package

El diagrama ofrece una visión general de la arquitectura del sistema, mostrando cómo los módulos se organizan y se relacionan entre sí. Refleja un diseño modular que facilita la escalabilidad y la seguridad.

> _[Insertar imagen: diagrama de package]_

#### Diagrama de Microservicios

> _[Insertar imagen: diagrama de microservicios]_

#### Descripción de Componentes

1. Capa de clientes (portales por rol): Portal Comprador, Portal Organizador y Panel Administrador consumen una UI-Lib común para mantener consistencia.
2. API Gateway / Entrada única: aplica autenticación, rate limiting, trazabilidad y enrutamiento hacia BFF internos.
3. BFF por frente: adapta respuestas de microservicios al contexto de cada rol y minimiza acoplamiento frontend-backend.
4. Cluster Kubernetes: ejecuta microservicios desacoplados con escalamiento horizontal y tolerancia a fallos por zona.
5. Broker de eventos (RabbitMQ): desacopla procesos asincrónicos críticos y no críticos con retries y DLQ.
6. Capa de persistencia por dominio: modelo Database per Service para aislamiento transaccional y evolución independiente.
7. Servicios auxiliares y observabilidad: métricas, trazas y automatización CI/CD para operación confiable y auditable.

### 4.5 Diagrama de flujo de eventos (Core Logics)

Este bloque documenta cómo el sistema desacopla procesos críticos y no críticos durante la compra de entradas para mantener experiencia fluida en alta demanda.

#### Explicación técnica del comportamiento de colas

1. Flujo síncrono (capa de acceso): el comprador confirma checkout en Portal Comprador.
2. Flujo síncrono (capa de acceso): BFF-Comprador envía solicitud a MSCarrito para validar reserva y procesar cobro.
3. Flujo síncrono (capa de acceso): MSCarrito responde de forma inmediata con estado de operación al frontend.
4. Publicación de eventos (capa de mensajería): tras pago exitoso, MSCarrito publica `pago.aprobado.v1` en el Exchange `eventos.compra`.
5. Publicación de eventos (capa de mensajería): el Exchange enruta el evento hacia colas `cola.stock.confirmacion`, `cola.donacion.registro` y `cola.notificacion.compra`.
6. Consumo asíncrono (capa de dominios): MSEventos confirma stock y publica `stock.confirmado.v1`; MSDonaciones registra donación y publica `donacion.registrada.v1`.
7. Consumo asíncrono (capa de dominios): MSMensajeria consume eventos finales, genera QR/notificación y actualiza trazabilidad de entrega.

Resiliencia operacional: todos los consumidores aplican idempotencia por clave de negocio, retry exponencial y derivación a DLQ para reproceso controlado.

### 4.6 Arquitectura de red y alta disponibilidad (Multi-AZ)

La plataforma debe operar en una topología distribuida Multi-AZ para asegurar continuidad operacional ante fallos zonales sin interrupción del flujo crítico de compra.

#### Explicación del diseño de infraestructura

- Entrada controlada: balanceador L7 (Ingress Controller o Application Load Balancer) con health checks cada 10 segundos y failover automático entre zonas.
- Segmentación por capas: subred pública para entrada controlada y subredes privadas separadas para BFF/microservicios, broker y datos.
- Orquestación distribuida: cluster de Kubernetes en al menos 2 AZ, con `podAntiAffinity` para evitar réplicas del mismo servicio en un solo nodo o zona.
- Continuidad de servicios: despliegues de BFF y microservicios con mínimo 2 réplicas por servicio y HPA para escalar por CPU/memoria y latencia.
- Mensajería resiliente: RabbitMQ con colas tipo quorum replicadas entre nodos en distintas AZ, manteniendo consumo ante caída de un nodo.
- Persistencia resiliente: MySQL con réplica en zona alterna, backups completos diarios + binlogs incrementales y simulacros mensuales de restauración (objetivo RPO <= 15 min, RTO <= 60 min).

### 4.7 Estrategia de automatización: Pipeline CI/CD

El pipeline asegura calidad, trazabilidad y despliegue continuo sin degradar estabilidad.

#### Flujo del pipeline

1. Fase de build y pruebas unitarias: compilación con Maven/Gradle (backend) y NPM (frontend), ejecución de pruebas unitarias y generación de artefactos versionados por commit.
2. Fase de calidad y seguridad: análisis estático con SonarQube, verificación de dependencias vulnerables y control de umbrales de calidad antes de promover artefactos.
3. Fase de empaquetado y publicación: construcción de imágenes Docker por servicio, etiquetado semántico y publicación en Container Registry para trazabilidad de releases.
4. Fase de despliegue progresivo: actualización en Kubernetes mediante Rolling Update, health checks post-despliegue y rollback automático/manual si no se cumplen criterios de estabilidad.

## 5. Matriz de Herramientas y Justificación Técnica

### 5.1 Infraestructura y Orquestación

| Herramienta | Rol en la solución | Justificación técnica |
|-------------|--------------------|-----------------------|
| Docker | Contenedores de servicios | Docker permite empaquetar cada microservicio con sus dependencias exactas, eliminando diferencias entre desarrollo, pruebas y producción. Este aislamiento facilita despliegues repetibles, acelera rollback y reduce incidentes causados por deriva de entorno. |
| Kubernetes | Orquestación de microservicios | Kubernetes habilita escalamiento horizontal por demanda, autorecuperación de pods y despliegues progresivos sin interrupción relevante. Su modelo declarativo permite controlar alta disponibilidad, distribución por zonas y políticas de resiliencia coherentes con los RNF de continuidad. |
| API Gateway/BFF | Punto de entrada y agregación | La capa Gateway+BFF centraliza autenticación/autorización, observabilidad y control de tráfico, mientras adapta contratos por tipo de cliente para reducir acoplamiento. Esto mejora seguridad y rendimiento al disminuir llamadas innecesarias desde frontend hacia múltiples dominios backend. |

### 5.2 Desarrollo y Lenguajes

| Herramienta | Rol en la solución | Justificación técnica |
|-------------|--------------------|-----------------------|
| Java/JavaScript | Backend y frontend | La combinación Java/JavaScript ofrece un ecosistema robusto, con amplio soporte en librerías, frameworks y tooling para sistemas distribuidos. Permite separar responsabilidades por dominio sin perder interoperabilidad entre capas y equipos de desarrollo. |
| React | Interfaz web | React favorece una arquitectura de UI basada en componentes reutilizables, facilitando mantenibilidad, pruebas y evolución incremental de funcionalidades. Su adopción transversal reduce curva de aprendizaje y habilita una base común para los tres frentes de Ticketti. |
| React Bootstrap | Sistema de componentes visuales | React Bootstrap entrega componentes accesibles y responsivos listos para producción, alineados con patrones UI consistentes en todos los portales. Esto reduce esfuerzo de implementación visual, baja riesgo de inconsistencias y acelera entregas de frontend. |
| Vite | Build tool y dev server | Vite proporciona un pipeline de build ultrarrápido con recarga caliente (HMR) instantánea, optimizaciones de bundle automáticas y soporte nativo para ES módulos. Reduce significativamente tiempos de desarrollo y garantiza builds de producción livianos, mejorando experiencia de desarrollador y rendimiento en cliente. |
| React Router | Enrutamiento SPA | React Router habilita enrutamiento declarativo en el lado del cliente con patrones estándar de React v6+, proporcionando control explícito sobre navegación, parámetros de ruta y estado. Esta separación clara entre tooling (Vite) y enrutamiento (React Router) favorece mantenibilidad y permite evolucionar cada capa independientemente. |
| Maven/Gradle/NPM | Gestión de dependencias | Estas herramientas formalizan resolución de dependencias, versionado y scripts de build de forma reproducible. Además, facilitan integración con CI/CD al definir pasos automáticos verificables y auditables por release. |

### 5.3 Comunicación y Persistencia

| Herramienta | Rol en la solución | Justificación técnica |
|-------------|--------------------|-----------------------|
| MySQL (por servicio) | Persistencia transaccional | MySQL por dominio permite mantener consistencia fuerte local y autonomía evolutiva entre microservicios, evitando dependencias rígidas a nivel de esquema. Este enfoque se alinea con Database per Service y reduce impacto de cambios de modelo en dominios no relacionados. |
| RabbitMQ | Mensajería asíncrona | RabbitMQ habilita desacoplamiento temporal entre servicios, absorbe picos de carga y soporta patrones de retry/DLQ requeridos por procesos críticos de compra, stock y donación. Su modelo de enrutamiento por exchanges y colas facilita trazabilidad operativa de eventos de negocio. |
| Redis (opcional) | Cache/sesión | Redis permite optimizar tiempos de respuesta en lecturas frecuentes y gestionar estados efímeros de sesión o rate limiting con baja latencia. Su uso controlado mejora experiencia de usuario sin comprometer la fuente de verdad transaccional de cada dominio. |

### 5.4 Calidad y Observabilidad

| Herramienta | Rol en la solución | Justificación técnica |
|-------------|--------------------|-----------------------|
| SonarQube | Calidad de código | SonarQube impone puertas de calidad sobre mantenibilidad, cobertura, deuda técnica y vulnerabilidades, evitando que código de riesgo avance a producción. Esto fortalece gobernanza técnica y estandariza criterios objetivos en revisiones de merge y releases. |
| Prometheus/Grafana | Monitoreo y métricas | Prometheus recolecta métricas técnicas y de negocio, mientras Grafana habilita tableros y alertas accionables para operación diaria y gestión de SLO. Esta visibilidad permite detectar degradaciones tempranas y responder incidentes con evidencia cuantitativa. |
| Trazas distribuidas | Diagnóstico extremo a extremo | La trazabilidad distribuida conecta una solicitud desde frontend hasta microservicios y broker, reduciendo el tiempo para identificar cuellos de botella y fallos de integración. Es clave para depurar operaciones complejas como checkout y convergencia de estados interdominio. |
| OpenAPI/Swagger | Contratos y documentación de API | OpenAPI define contratos versionados consumibles por equipos frontend y backend, mientras Swagger UI facilita inspección y validación funcional de endpoints. Al tratarse de un artefacto de documentación técnica, se gestiona en la capa de APIs y no como componente de interfaz de usuario final. |

## 6. Evaluación Ética y Técnica del Diseño

La arquitectura de Ticketti no solo busca eficiencia técnica, sino que se fundamenta en principios de Software Responsable y Ética en Microservicios, asegurando un impacto positivo en el ecosistema digital de organizaciones benéficas y compuesto de ciudadanos conscientes.

### 6.1 Sostenibilidad Ambiental (Green Computing)

El diseño basado en Kubernetes y dimensionamiento dinámico permite una gestión inteligente de los recursos de cómputo:

● **Escalado Dinámico:** A diferencia de plataformas que mantienen servidores encendidos 24/7 "por si acaso", Ticketti consume energía solo cuando hay demanda real (picos de venta durante estrenos o campañas benéficas), reduciendo significativamente la huella de carbono de la infraestructura.

● **Eficiencia de Contenedores:** Al usar Docker, optimizamos el uso de CPU y memoria al compartir el kernel del sistema operativo, permitiendo una mayor densidad de servicios en menos hardware físico, disminuyendo el consumo energético total de la plataforma.

### 6.2 Privacidad y Protección de Datos (Privacy by Design)

Dado que gestionamos datos sensibles de compradores (tarjetas de crédito, direcciones) y de organizadores (información bancaria, datos de contacto):

● **Cifrado de PII:** Implementamos cifrado de Información de Identificación Personal (PII) mediante AES-256 en reposo y TLS 1.3 en tránsito, asegurándonos de que credenciales y datos de pago viajan encriptados.

● **Aislamiento de Dominios:** Al usar el patrón Database per Service, limitamos el radio de impacto. Si el servicio de catálogo se ve comprometido, los datos de transacciones financieras del servicio de pago permanecen aislados y seguros.

● **Tokenización (JWT):** Evitamos viajar con credenciales de usuario (passwords) en cada petición, utilizando tokens de sesión con tiempo de expiración limitado y alcance específico (scopes para Comprador, Organizador o Admin).

### 6.3 Equidad y Transparencia Algorítmica

En la descoberta y selección de eventos, el ranking puede generar sesgos si no se diseña correctamente:

● **Transparencia en el Ranking:** El algoritmo de recomendación de eventos utiliza reglas de negocio claras y auditables (categoría, fecha, objetivo social, disponibilidad) en lugar de favoritismos ocultos, evitando que ciertos organizadores sean privilegiados sistemáticamente.

● **Logs de Auditoría Inmutables:** Gracias al Sidecar de Logging en cada microservicio, cada cambio crítico (cambio de estado de evento, cancelación, reembolso) queda registrado con timestamp e identificación del actor, permitiendo resolver disputas de forma justa entre comprador, organizador y plataforma.

### 6.4 Inclusión y Accesibilidad Digital

La UI-Lib (Librería de Componentes React Bootstrap) no es solo estética, es una herramienta de inclusión social:

● **Estándares WCAG:** Todos los componentes frontales están diseñados para ser operables por personas con diversas capacidades (navegación por teclado, contraste de colores WCAG AA mínimo, compatibilidad con lectores de pantalla). Esto asegura que cualquier ciudadano, sin importar sus capacidades físicas, pueda descubrir eventos, comprar entradas o gestionar una organización benéfica en Ticketti.

● **Responsive y Bajo Ancho de Banda:** La plataforma funciona óptimamente en conexiones lentas (3G) y desde dispositivos de gama baja, reconociendo que el acceso digital para causas sociales no debe depender de infraestructura de punta. Esto amplía la inclusión geográfica y socioeconómica de participantes.
