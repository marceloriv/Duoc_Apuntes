# Especificación de Requisitos de Software

**Proyecto:** Ticketti  
**Versión:** 1.4  
**Fecha:** 24/03/2026  
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
  - [1. Introducción](#1-introducción)
    - [1.1 Propósito](#11-propósito)
    - [1.2 Ámbito del Sistema](#12-ámbito-del-sistema)
      - [Lo que el Sistema Hará](#lo-que-el-sistema-hará)
      - [Lo que el Sistema NO Hará](#lo-que-el-sistema-no-hará)
      - [Beneficios, Objetivos y/o Metas](#beneficios-objetivos-yo-metas)
  - [2. Descripción General](#2-descripción-general)
    - [2.1 Perspectiva del Producto](#21-perspectiva-del-producto)
    - [2.2 Funciones del Producto](#22-funciones-del-producto)
    - [2.3 Características de los Usuarios](#23-características-de-los-usuarios)
    - [2.4 Restricciones](#24-restricciones)
    - [2.5 Suposiciones y Dependencias](#25-suposiciones-y-dependencias)
    - [2.6 Requisitos Futuros](#26-requisitos-futuros)
  - [3. Requisitos Específicos](#3-requisitos-específicos)
    - [3.1 Requisitos comunes de las interfaces](#31-requisitos-comunes-de-las-interfaces)
      - [3.1.1 Interfaces de usuario](#311-interfaces-de-usuario)
      - [3.1.2 Interfaces de hardware](#312-interfaces-de-hardware)
      - [3.1.3 Interfaces de software](#313-interfaces-de-software)
    - [3.2 Requisitos Funcionales (RF)](#32-requisitos-funcionales-rf)
      - [RF-1 Gestión de usuarios y acceso (MSUsuarios)](#rf-1-gestión-de-usuarios-y-acceso-msusuarios)
      - [RF-2 Gestión de eventos (MSEventos)](#rf-2-gestión-de-eventos-mseventos)
      - [RF-3 Carrito y compra de entradas (MSCarrito)](#rf-3-carrito-y-compra-de-entradas-mscarrito)
      - [RF-4 Donaciones e impacto social (MSDonaciones)](#rf-4-donaciones-e-impacto-social-msdonaciones)
      - [RF-5 Notificaciones y comunicación (MSMensajeria)](#rf-5-notificaciones-y-comunicación-msmensajeria)
    - [3.3 Requisitos no Funcionales](#33-requisitos-no-funcionales)
    - [3.4 Otros Requisitos](#34-otros-requisitos)
  - [4. Arquitectura de Software y Ecosistema Front](#4-arquitectura-de-software-y-ecosistema-front)
    - [4.1 Ecosistema Frontend](#41-ecosistema-frontend)
    - [4.2 Capa de Agregación (BFF)](#42-capa-de-agregación-bff)
    - [4.3 Capa de Backend y Microservicios](#43-capa-de-backend-y-microservicios)
      - [A. Microservicio de Usuarios (MSUsuarios)](#a-microservicio-de-usuarios-msusuarios)
      - [B. Microservicio de Eventos (MSEventos)](#b-microservicio-de-eventos-mseventos)
      - [C. Microservicio de Carrito de Compras (MSCarrito)](#c-microservicio-de-carrito-de-compras-mscarrito)
      - [D. Microservicio de Donaciones (MSDonaciones)](#d-microservicio-de-donaciones-msdonaciones)
      - [E. Microservicio de Mensajería (MSMensajeria)](#e-microservicio-de-mensajería-msmensajeria)
    - [4.4 Diagramas de arquitectura de solución](#44-diagramas-de-arquitectura-de-solución)
      - [Diagrama de Package](#diagrama-de-package)
      - [Diagrama de Microservicios](#diagrama-de-microservicios)
  - [Notas y puntos abiertos del equipo](#notas-y-puntos-abiertos-del-equipo)

---

## Control de Versiones

| Fecha | Revisión | Autor | Modificación |
|-------|----------|-------|--------------|
| 19/03/2026 | 1.0 | Marcelo Rivera, Ingrid Núñez | Inicio de construcción de ERS. |
| 21–22/03/2026 | 1.1 | Meritxell Arroyo | Requisitos funcionales y no funcionales. |
| 22/03/2026 | 1.2 | Pamela Alvarez | Completados 1.2, 2.1, 2.4, 2.5, 2.6, 3.1.1, 3.1.2, 3.1.3, 3.4. RNF con valores de industria. 3.2 pasado a tabla. |
| 24/03/2026 | 1.3 | Ingrid Núñez | Integración de sistema de notificaciones como RF. Inicio del desarrollo de 4.1, 4.2, 4.3. |
| 24/03/2026 | 1.4 | Pamela Alvarez | 3.2: reestructuración de requisitos, separados por módulos. |
| 26/03/2026 | 1.5 | Pamela Alvarez | 3.2: ajuste de requisitos a los microservicios finales. |
| 26/03/2026 | 1.6 | Ingrid Núñez | Desarrollo del diagrama de Package. |

---

## 1. Introducción

### 1.1 Propósito

Detallar los requerimientos necesarios para construir un software de gestión de eventos que permite visualizar eventos por categoría, comprar tickets de forma rápida y segura, recibir notificaciones y destinar un porcentaje de cada venta a organizaciones sin fines de lucro. Este documento está dirigido principalmente al equipo de desarrolladores, para garantizar una comprensión clara del sistema y asegurar su correcta funcionalidad. El desarrollo será entregado al cliente para su evaluación.

### 1.2 Ámbito del Sistema

**Nombre del sistema:** Ticketti

#### Lo que el Sistema Hará

- Permitir la visualización y búsqueda de eventos disponibles, organizados por categoría, fecha y ubicación.
- Gestionar la compra de entradas de forma rápida y segura, con control de stock para evitar sobreventas.
- Enviar notificaciones automáticas al usuario ante acciones relevantes, tales como la confirmación de compra, devoluciones aprobadas y recomendaciones personalizadas.
- Destinar automáticamente un porcentaje configurable de cada venta a organizaciones sin fines de lucro registradas en la plataforma.
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

## 2. Descripción General

### 2.1 Perspectiva del Producto

Ticketti es un sistema independiente de gestión de venta de entradas a eventos con impacto social, diseñado para operar como plataforma digital de uso público. El sistema no reemplaza pasarelas de pago externas, sino que se integra con ellas para completar las transacciones de forma segura. Internamente, la plataforma cuenta con una interfaz web accesible desde distintos dispositivos y un conjunto de servicios backend orientados a la escalabilidad y la disponibilidad. Adicionalmente, el sistema se integra con un servicio de notificaciones para la comunicación con los usuarios y gestiona la persistencia de datos mediante una base de datos relacional.

### 2.2 Funciones del Producto

| Nombre de la Función | Descripción de la Función |
|----------------------|--------------------------|
| Gestión de cuentas | Registro e inicio de sesión de usuario mediante credenciales, eliminación de cuenta de usuario, soporte para administrador, comprador y organizador. |
| Gestión de eventos | Creación, edición, publicación y cancelación de eventos por parte de organizadores. |
| Compra de entradas | Permite al usuario comprar entradas del evento de su preferencia. |
| Gestión de inventario | Control de stock por tipo de entrada con cupo límite para evitar sobreventas en compras simultáneas. |
| Sistema de Notificaciones | Envío de alertas sobre compras, devoluciones y recomendaciones a los usuarios. |
| Devolución de entradas | Procesamiento de reembolsos según política de devolución del evento, con notificación al comprador. |
| Filtros y categoría | Permite buscar eventos según filtros y categorías, ubicación o fecha. |
| Visualización de estadísticas de compras | Permitir visualizar las estadísticas de los movimientos obtenidos en tiempo real tras cada compra del usuario comprador. |
| Apoyo a causas sociales | Permite al usuario comprador seleccionar durante la compra una organización sin fines de lucro a la cual se destinará un porcentaje de su transacción. |

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

## 3. Requisitos Específicos

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

#### RF-1 Gestión de usuarios y acceso (MSUsuarios)

Los requerimientos de este dominio contemplan el ciclo de vida completo de la identidad del usuario en la plataforma.

- **RF-1.1 Registrar usuario con aceptación de términos por rol:** El sistema debe permitir registrar usuarios diferenciando el flujo según rol: el comprador acepta términos de compra y política de privacidad (Ley N°21.719); el organizador acepta además los términos de publicación de eventos. El sistema registra fecha, hora e IP de cada aceptación mediante `registrarAceptacionTerminos()`.

- **RF-1.2 Inicio de sesión por rol:** El sistema debe autenticar usuarios mediante correo y contraseña, redirigiendo según su rol (Comprador, Organizador, Administrador). Bloquea temporalmente la cuenta tras 3 intentos fallidos consecutivos.

- **RF-1.3 Eliminar cuenta y datos personales:** El sistema debe permitir solicitar la eliminación definitiva de la cuenta con un periodo de recuperación de 30 días, tras el cual se suprimen permanentemente todos los datos personales conforme al derecho de supresión de la Ley N°21.719.

- **RF-1.4 Exportar datos personales:** El sistema debe permitir al usuario descargar todos sus datos personales almacenados en formato JSON o PDF, conforme al derecho de portabilidad de la Ley N°21.719. La solicitud queda registrada con fecha y hora para auditoría.

- **RF-1.5 Revocar consentimientos opcionales:** El sistema debe permitir revocar consentimientos opcionales (notificaciones, recomendaciones) desde la sección de privacidad, sin afectar el acceso a las funciones principales de la plataforma.

- **RF-1.6 Gestión de usuarios (Administrador):** El sistema debe permitir al administrador consultar, activar, suspender y cambiar el rol de usuarios registrados, sin acceso a sus contraseñas. Toda acción queda registrada con fecha, hora y actor responsable.

#### RF-2 Gestión de eventos (MSEventos)

- **RF-2.1 Crear y publicar evento:** El sistema debe permitir al organizador crear eventos definiendo nombre, descripción, categoría (`asignarCategorias`), ubicación (`definirLocacion`) y capacidad máxima por tipo de entrada (`definirCapacidad`). La capacidad queda registrada en MSEventos y es consultada por MSCarrito para validar disponibilidad.

- **RF-2.2 Editar evento y gestionar estado:** El sistema debe permitir al organizador editar un evento en estado borrador y publicarlo. Una vez publicado, solo el administrador puede cancelarlo, con registro obligatorio del motivo. Los cambios de capacidad no están permitidos si ya existen ventas activas.

- **RF-2.3 Listar y visualizar detalle de evento:** El sistema debe permitir a cualquier usuario, incluyendo invitados sin sesión, listar eventos disponibles y visualizar su detalle completo: nombre, descripción, fecha, locación, disponibilidad de entradas, precios, restricciones de edad y causas sociales activas.

- **RF-2.4 Buscar y filtrar eventos:** El sistema debe permitir buscar eventos por nombre, artista, comuna, región y categoría, con resultados ordenados por relevancia o fecha próxima. Garantiza igual visibilidad entre eventos de organizadores grandes y pequeños dentro de cada categoría.

#### RF-3 Carrito y compra de entradas (MSCarrito)

- **RF-3.1 Seleccionar entradas con validación de límite:** El sistema debe permitir al comprador autenticado seleccionar entradas para un evento, aplicando la regla de negocio de máximo 4 entradas por compra (`ReglaLimiteEntradas`). Para verificar disponibilidad, MSCarrito consulta la capacidad registrada en MSEventos.

- **RF-3.2 Gestionar carrito y calcular total:** El sistema debe permitir agregar, modificar y eliminar entradas del carrito, recalculando en tiempo real el subtotal de la compra (`calcularTotal`) más el 10% de donación (`integrarDonacion`). El resumen debe mostrar el desglose entre precio de entradas y monto donado antes de confirmar.

- **RF-3.3 Confirmar compra y procesar pago:** Al confirmar la compra, MSCarrito debe validar el stock final con MSEventos, procesar el pago mediante la pasarela externa y registrar la compra. En caso de fallo en el pago, la selección se mantiene en carrito. Si el pago es exitoso, se actualiza la disponibilidad en MSEventos y se disparan los eventos hacia MSDonaciones y MSMensajeria.

- **RF-3.4 Solicitar devolución de entradas:** El sistema debe permitir al comprador solicitar devolución de una entrada con reembolso del 85% del valor total pagado (incluyendo el 10% de donación ya procesado), siempre que el evento no haya ocurrido y la solicitud esté dentro del plazo establecido.

- **RF-3.5 Consultar historial de compras:** El sistema debe permitir al comprador visualizar el historial completo de sus pedidos con estado actual (confirmado, pendiente, devuelto), detalle de entradas, monto pagado y monto donado por cada transacción.

#### RF-4 Donaciones e impacto social (MSDonaciones)

Los requerimientos de este dominio contemplan la gestión del porcentaje solidario integrado en cada transacción.

- **RF-4.1 Calcular donación fija del 10%:** El sistema debe calcular automáticamente el monto de donación como el 10% fijo del total de la compra de entradas, sin posibilidad de modificación por parte del usuario ni del administrador. Este porcentaje es una regla de negocio invariable del sistema.

- **RF-4.2 Seleccionar y asociar causa social:** Durante el proceso de compra, el sistema debe mostrar las causas sociales activas disponibles para que el usuario seleccione a cuál destinar el 10% de su compra (`asociarCausa`). Si no hay causas activas, se informa al usuario y la compra puede continuar destinando el monto a un fondo general.

- **RF-4.3 Registrar y persistir donación:** Al confirmarse una compra, MSDonaciones debe persistir la donación (`persistirDonacion`) vinculada al ID de transacción, causa seleccionada y monto correspondiente. El registro queda disponible para auditoría y para el comprobante que envía MSMensajeria.

- **RF-4.4 Administrar causas sociales:** El administrador debe poder crear, activar y desactivar causas sociales disponibles en la plataforma. Una causa desactivada no aparece en nuevas compras, pero las donaciones históricas vinculadas a ella se conservan íntegras en la base de datos.

#### RF-5 Notificaciones y comunicación (MSMensajeria)

Los requerimientos de este dominio contemplan la comunicación automatizada con los usuarios a través de múltiples canales.

- **RF-5.1 Enviar QR de entrada al comprador:** Al confirmarse una compra, MSMensajeria debe generar y enviar un código QR único por entrada (`generarQR`) que sirva como credencial de acceso al evento. El QR queda vinculado al ID de compra y al usuario comprador.

- **RF-5.2 Enviar confirmación de compra con detalle de donación:** El sistema debe enviar al comprador una confirmación (`construirMensajeConfirmacion`) con el detalle de la compra: entradas, evento, fecha, precio total y monto destinado al 10% de donación con el nombre de la causa beneficiada.

- **RF-5.3 Enviar notificación de devolución:** Al resolverse una solicitud de devolución, MSMensajeria debe enviar la notificación correspondiente (`construirMensajeDevolucion`) informando el resultado, el monto reembolsado (85% del total pagado) y el plazo estimado de acreditación.

- **RF-5.4 Enviar recomendaciones opcionales:** El sistema debe permitir enviar recomendaciones de eventos personalizadas al usuario (`construirRecomendaciones`) únicamente si éste otorgó consentimiento para ello. Si el consentimiento fue revocado (RF-1.5), este envío queda bloqueado automáticamente.

---

### 3.3 Requisitos no Funcionales

Atributos de Calidad según ISO 25010 (10 unidades):

| Id. | Nombre Corto | Descripción | Atributo de Calidad |
|-----|-------------|-------------|---------------------|
| RNF01 | Cantidad de usuarios | El sistema debe soportar como mínimo 100 usuarios durante la compra de entradas. | Rendimiento |
| RNF02 | Tiempo de respuesta | El sistema debe responder en menos de 3 segundos al cargar la página de inicio. | Rendimiento |
| RNF03 | Cálculo de precio | El sistema debe mostrar el cálculo del precio en el total de la compra, como también el porcentaje a la causa social apoyada. | Funcionalidad |
| RNF04 | Accesibilidad de navegadores | El sistema debe ser accesible desde al menos un navegador web (Chrome, Edge, etc). | Compatibilidad |
| RNF05 | Recuperación de datos de compra | El sistema debe recuperar el estado de la compra en caso de fallo repentino. | Fiabilidad |
| RNF06 | Disponibilidad del sistema | El sistema debe disponibilizar el servicio un 99% del tiempo. | Fiabilidad |
| RNF07 | Validación de datos del usuario | El sistema debe validar los datos ingresados por el usuario para la prevención de información inválida o maligna. | Seguridad |
| RNF08 | Corrección de errores | El sistema debe permitir la corrección de errores oportuna sin afectar el resto de su funcionamiento. | Mantenibilidad |
| RNF09 | Responsividad en distintos dispositivos | El sistema debe permitir la visualización desde distintos dispositivos (celulares, tablets, computadoras). | Portabilidad |
| RNF10 | Estructura del sistema | El sistema debe estar estructurado con una arquitectura estratégica para facilitar futuras actualizaciones. | Mantenibilidad |

### 3.4 Otros Requisitos

- El sistema deberá cumplir con la Ley N°21.719 sobre Protección y Tratamiento de los Datos Personales, vigente en Chile desde el 13 de diciembre de 2024, aplicando los principios de consentimiento explícito, minimización de datos, privacidad por diseño y notificación de brechas de seguridad.
- El porcentaje destinado a organizaciones sin fines de lucro será configurable por el administrador, con un mínimo del 1% por transacción completada.

---

## 4. Arquitectura de Software y Ecosistema Front

Para garantizar una solución escalable y centrada en el usuario, Ticketti adopta una arquitectura de microservicios desacoplados. Esta estructura permite que cada componente sea independiente en su despliegue y escalabilidad, gestionando su propia lógica de negocio y persistencia de datos (MySQL), comunicándose entre sí mediante protocolos REST y mensajería en formato JSON.

### 4.1 Ecosistema Frontend

Para este proyecto se han diseñado interfaces especializadas según el rol y el contexto de uso.

| Componente | Tecnología | Función / Propósito |
|------------|-----------|---------------------|
| Sales Web | React (Node.js) | Creación de vistas rápidas y modernas para Clientes, Admins y Organizadores. |
| Diseño y Estilo | Bootstrap / CSS | Garantizar que el sistema sea responsive y se vea bien en celulares. |
| Comunicación | JSON | Formato de mensajería para mostrar la información del servidor en pantallas. |
| Documentación de flujo | Swagger | Guía visual para que los desarrolladores sepan qué datos mostrar en cada vista. |
| Calidad de Interfaz | Docker | Asegurar que la interfaz cargue y funcione exactamente igual en cualquier navegador o servidor. |

### 4.2 Capa de Agregación (BFF)

> **[PENDIENTE]** — Definir responsabilidades del BFF. Considerar: autenticación JWT, agregación de llamadas a microservicios, transformación de respuestas para el frontend.

### 4.3 Capa de Backend y Microservicios

La arquitectura del software Ticketti se fundamenta en un modelo de microservicios desacoplados. Esta estructura permite que cada componente sea independiente en su despliegue y escalabilidad, gestionando su propia lógica de negocio y persistencia de datos (MySQL), comunicándose entre sí mediante protocolos REST y mensajería en formato JSON.

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
| DELETE | `/{id}` | Eliminación o baja del sistema mediante su identificador. |

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
| DELETE | `/{id}` | Eliminar un evento del sistema. |

---

#### C. Microservicio de Carrito de Compras (MSCarrito)

**Responsabilidad:** Gestión de la compra de entradas: agregado, eliminación y confirmación.

> **[DECISIÓN PENDIENTE]** — Evaluar si el carrito se implementa como microservicio con persistencia propia o como estado temporal en el frontend (hooks/localStorage). La opción de microservicio permite recuperación ante fallos (RNF05) y auditoría, pero agrega complejidad operacional.

**Base URL:** `/api/v1/Carrito`

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| POST | `/crearVentaCarrito` | Realiza una compra de entrada(s). |
| GET | `/listarVentasCarrito` | Muestra el registro de todas las ventas efectuadas. |
| GET | `/ventas/{id}` | Obtiene una venta específica por id. |
| DELETE | `/vaciarCarrito/{id}` | Elimina por completo la venta de entrada del usuario, por id. |
| PUT | `/actualizarVentaCarrito/{id}` | Actualiza la cantidad o tipo de entradas en el carrito. |

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

---

## Notas y puntos abiertos del equipo

> Esta sección consolida los puntos pendientes identificados en el documento para facilitar su resolución en próximas revisiones.

1. **BFF (4.2):** Definir responsabilidades concretas: ¿JWT aquí o en cada MS? ¿Agrega llamadas o solo enruta?
2. **MSCarrito — decisión de arquitectura:** Microservicio con BD propia vs. estado en frontend. Impacta RNF05 (recuperación ante fallos).
3. **MSCarrito — endpoint PUT:** Definir qué campos son actualizables (¿cantidad de entradas?, ¿tipo?).
4. **Consistencia entre bases de datos:** Dado que cada microservicio gestiona su propia BD (MySQL), definir el mecanismo de consistencia eventual. Opciones a evaluar: eventos de dominio vía broker de mensajes (RabbitMQ/Kafka), Saga pattern, o llamadas síncronas con compensación.
5. **Nombre del proyecto:** Confirmar "Ticketti" vs "Tikití" (aparece ambiguo en el documento original).
