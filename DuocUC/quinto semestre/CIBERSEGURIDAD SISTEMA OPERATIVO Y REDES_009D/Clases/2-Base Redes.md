# Clase 2 – Fundamentos de Redes y Sistemas para Ciberseguridad

## Objetivo de la clase

Que los estudiantes comprendan cómo se comunican los sistemas, porque la mayoría de los ataques ocurren aprovechando esa comunicación.

## 1. Caso real de ciberespionaje en Chile

### Introducción a la noticia

Un informe de Google Threat Intelligence Group reveló que un grupo de ciberespionaje vinculado al gobierno chino ha estado realizando operaciones de intrusión en decenas de países, incluido Chile.

Este grupo, identificado como **UNC2814**, ha atacado principalmente:

- Gobiernos
- Telecomunicaciones
- Organizaciones estratégicas

Sus operaciones han afectado al menos **53 organizaciones en 42 países**.

Lo importante es que estas intrusiones **no comenzaron ahora**. Los investigadores han rastreado la actividad del grupo desde **al menos 2017**.

Es decir: La noticia aparece hoy… pero las operaciones llevan años ocurriendo.

### Qué hacía este grupo de espionaje

Este grupo no hacía ataques simples. Su objetivo era **ciberespionaje estratégico**.

Esto significa que buscaban:

- Robar información
- Obtener acceso persistente a redes
- Monitorear comunicaciones
- Recolectar inteligencia tecnológica o política

Una de las técnicas que usaban era bastante interesante.

Los atacantes utilizaban **aplicaciones SaaS legítimas como infraestructura de comando y control**, enviando tráfico malicioso que parecía tráfico normal.

Esto les permitía:

- Camuflar su actividad
- Evitar detecciones
- Permanecer infiltrados durante largos periodos

En otras palabras: **No es el típico hacker intentando entrar rápido. Son operaciones diseñadas para permanecer ocultas durante años.**

### Qué significa realmente "ciberespionaje"

Cuando pensamos en hacking muchas veces imaginamos:

- Ransomware
- Robo de dinero
- Ataques visibles

Pero existe otro tipo de operaciones: **ciberespionaje estatal**.

El objetivo **no es necesariamente causar daño inmediato**.

El objetivo es:

- Obtener información estratégica
- Vigilar comunicaciones
- Conocer decisiones políticas o tecnológicas
- Robar propiedad intelectual

### Por qué esto es importante para Chile

Chile no es una superpotencia tecnológica, pero sí tiene:

- Recursos naturales estratégicos
- Empresas mineras
- Telecomunicaciones
- Acuerdos internacionales
- Proyectos de infraestructura digital

Todo eso genera interés geopolítico.

Por eso los actores estatales muchas veces realizan operaciones de inteligencia en múltiples países al mismo tiempo.

### Algo muy importante para que entiendan

> "La noticia aparece hoy, pero los ataques comenzaron hace años."

Esto ocurre constantemente en ciberseguridad. Muchos incidentes se descubren **años después de que comenzaron**.

Esto pasa porque los atacantes más sofisticados buscan:

- Permanecer ocultos
- Evitar detecciones
- Mantener acceso persistente

## 2. Por qué redes y sistemas importan en seguridad

### Pregunta fundamental

"Si un atacante quiere hackear un sistema… ¿cómo creen que llega a ese sistema?"

Respuestas típicas:

- Internet
- Vulnerabilidades
- Redes
- Phishing
- Malware

### Concepto clave

> "La mayoría de los ataques informáticos ocurren porque los sistemas están conectados entre sí."

Si los sistemas no estuvieran conectados:

- No existirían ataques remotos
- No existiría internet
- La superficie de ataque sería mucho menor

### Ejemplo real

Imagina una empresa con:

- Un servidor web
- Una base de datos
- Una aplicación móvil
- Usuarios internos

Todos esos sistemas se comunican a través de una red.

Si un atacante logra entrar a uno de ellos, muchas veces puede moverse hacia otros sistemas dentro de la misma red.

Este concepto se conoce como **movimiento lateral**.

### Mensaje clave

> Para entender ciberseguridad primero debemos entender cómo funcionan los sistemas y las redes.

Si no entiendes cómo funciona la comunicación entre sistemas, no podrás entender:

- Cómo se produce un ataque
- Dónde están las vulnerabilidades
- Cómo defender un sistema

## 3. Qué es un sistema

### Concepto

En ciberseguridad no protegemos "computadores" de forma aislada.

Lo que realmente protegemos son **sistemas que cumplen funciones para una organización**.

Un sistema puede definirse como:

> Un conjunto de componentes que trabajan juntos para recibir información, procesarla y entregar un resultado.

Esto significa que un sistema no es solo un software o una máquina. Un sistema normalmente incluye **múltiples elementos trabajando juntos**.

### Flujo básico de un sistema

Todos los sistemas, desde los más simples hasta los más complejos, siguen una lógica similar.

Un sistema:

1. Recibe información
2. Procesa esa información
3. Entrega un resultado

Este proceso ocurre constantemente en todos los sistemas informáticos.

### Ejemplo simple: Un buscador web

1. **Recibe una solicitud**: El usuario escribe "restaurantes cerca"
2. **Procesa la información**: El sistema busca en su base de datos
3. **Entrega un resultado**: Devuelve una lista de resultados

### Ejemplo en una empresa: Sistema de gestión de clientes

**Entrada:**

- Datos del cliente
- Solicitudes
- Consultas

**Procesamiento:**

- Validación
- Almacenamiento
- Análisis

**Salida:**

- Información del cliente
- Reportes
- Actualizaciones

### Ejemplos de sistemas informáticos

**Servidor web**
Un sistema que entrega páginas web a los usuarios.
Cuando visitas una página en internet, el servidor web procesa la solicitud y devuelve la página.

**Aplicación móvil**
Una app del celular también es un sistema.

Ejemplo - App de banco:

- Recibe: Credenciales, solicitudes de transferencia
- Procesa: Validación, verificación de saldo
- Entrega: Confirmación de operación

**Base de datos**
Un sistema diseñado para almacenar y gestionar información.

Ejemplos:

- Clientes
- Productos
- Transacciones

Las bases de datos son uno de los **sistemas más críticos para una organización**.

**Router**
Un router también es un sistema. Recibe tráfico de red, lo procesa y decide a dónde enviarlo.

**Computador personal**
Incluso un computador es un sistema completo.

Tiene:

- Hardware
- Sistema operativo
- Aplicaciones
- Usuarios
- Datos

### Qué compone realmente un sistema

Cuando hablamos de sistemas en ciberseguridad debemos entender que no se trata solo de software.

Un sistema normalmente tiene varios componentes.

#### 1. Software

El software es lo que ejecuta las funciones del sistema.

Ejemplos:

- Sistema operativo
- Aplicaciones
- Servicios
- APIs

El software es donde muchas veces aparecen vulnerabilidades.

Por ejemplo:

- Errores de programación
- Validaciones incorrectas
- Fallas de seguridad

#### 2. Configuraciones

Los sistemas también dependen de configuraciones.

Las configuraciones determinan cómo se comporta el sistema.

Ejemplos:

- Permisos de acceso
- Servicios habilitados
- Reglas de firewall
- Configuraciones de autenticación

Muchas brechas de seguridad ocurren por **configuraciones incorrectas**, no por fallas en el software.

#### 3. Usuarios

Todo sistema tiene usuarios.

Los usuarios pueden ser:

- Personas
- Administradores
- Aplicaciones
- Servicios automáticos

Cada usuario tiene distintos niveles de privilegio. Si estos privilegios no se controlan bien, pueden producirse accesos indebidos.

#### 4. Datos

Los datos son normalmente lo más valioso de un sistema.

Ejemplos de datos:

- Información personal
- Información financiera
- Propiedad intelectual
- Credenciales de acceso

En la mayoría de los ataques, el objetivo final es **acceder a datos o manipularlos**.

### Conexión con ciberseguridad

Todo sistema puede tener problemas de seguridad.

**Errores**
Errores de programación.
Ejemplo: Un sistema que no valida correctamente la entrada de datos.

**Vulnerabilidades**
Debilidades técnicas que pueden ser explotadas.
Ejemplo: Un servidor con software desactualizado.

**Configuraciones incorrectas**
Muchos incidentes de seguridad ocurren por malas configuraciones.
Ejemplo: Una base de datos expuesta a internet sin autenticación.

### Mensaje clave

> En ciberseguridad no protegemos computadores. Protegemos sistemas que cumplen funciones críticas para una organización.

Por ejemplo: No es lo mismo que falle el sistema de impresión que falle el sistema de pagos de una empresa. El impacto es completamente distinto.

### Ejemplo completo: Sistema de pagos online

Este sistema recibe:

- Solicitudes de pago
- Información de clientes
- Datos de tarjetas

Procesa:

- Validación de pagos
- Verificación de saldo
- Autorización de transacciones

Entrega:

- Confirmación del pago
- Registro de la transacción

#### Qué pasa si este sistema tiene problemas de seguridad

**Robo de datos**
Un atacante podría obtener:

- Datos personales
- Información financiera
- Tarjetas de crédito

**Manipulación de pagos**
Un atacante podría alterar transacciones.
Ejemplo: Modificar montos o desviar pagos.

**Acceso no autorizado**
Un atacante podría acceder a cuentas de usuarios. Esto puede permitir:

- Fraude
- Robo de fondos
- Suplantación de identidad

## 4. Qué es una red

### Concepto

Una red es **un conjunto de sistemas conectados para**:

- Intercambiar información
- Compartir recursos
- Comunicarse

Ejemplos:

- Internet
- Red corporativa
- Red de una universidad
- Red de una casa

### Concepto clave: Direcciones IP

Cada dispositivo conectado tiene una **dirección IP**.

La IP funciona como una **dirección en una ciudad**.

Analogía:

- IP → dirección
- Red → ciudad
- Dispositivos → casas

### Conexión con ciberseguridad

La mayoría de los ataques existen porque:

- Los sistemas están conectados
- Están expuestos a internet

**Mensaje clave:**

> "La red es el camino que usa el atacante."

## 5. Modelo Cliente / Servidor

### Flujo de una solicitud

**Paso 1: El cliente envía una solicitud**

El navegador envía una solicitud HTTP al servidor.

Por ejemplo: `GET /index.html`

Esto significa: "Quiero ver la página principal."

**Paso 2: El servidor recibe la solicitud**

El servidor web recibe la petición. El servidor analiza:

- Qué página se pidió
- Si existe
- Si el usuario tiene acceso

**Paso 3: El servidor procesa la solicitud**

El servidor puede:

- Buscar información en una base de datos
- Ejecutar código
- Verificar autenticación

**Paso 4: El servidor responde**

El servidor envía la respuesta al cliente.

Puede incluir:

- Código HTML
- Imágenes
- Datos
- Mensajes de error

El navegador recibe la respuesta y muestra la página.

### Conexión con ciberseguridad

Este modelo es **extremadamente importante** para entender cómo funcionan los ataques.

En seguridad debemos entender algo fundamental:

> Un atacante también es un cliente. La diferencia es que no se comporta como un usuario normal.

#### Cómo se comporta un cliente normal

Un usuario normal:

- Sigue el flujo esperado
- Envía datos válidos
- Usa la aplicación correctamente

Ejemplo: Cuando alguien inicia sesión en una página web.

#### Cómo se comporta un atacante

Un atacante intenta **romper ese comportamiento esperado**.

Puede enviar solicitudes que el sistema no espera.

**Solicitudes mal formadas**
El atacante envía datos incorrectos o incompletos.

Ejemplo:

- Parámetros inválidos
- Datos corruptos
- Entradas inesperadas

Esto puede provocar errores en el servidor.

**Solicitudes manipuladas**
El atacante modifica los parámetros enviados.

Por ejemplo: Cambiar un identificador de usuario.

Ejemplo:

```
/account?id=123
```

podría cambiarse a

```
/account?id=124
```

Esto podría permitir acceder a la cuenta de otro usuario.

**Solicitudes repetidas**
El atacante puede enviar miles o millones de solicitudes.

Esto puede provocar:

- Sobrecarga del sistema
- Caídas del servicio

Este tipo de ataques se conocen como: **Denial of Service (DoS)**.

### Qué puede provocar esto

Si el sistema no está bien diseñado o protegido, estas solicitudes pueden provocar:

**Fallas**
Errores internos en el servidor.

**Acceso indebido**
Usuarios accediendo a información que no deberían ver.

**Fuga de información**
Datos sensibles expuestos.

Por ejemplo:

- Información personal
- Credenciales
- Registros internos

### Ejemplo concreto

Imagina una API de una tienda online.

**Solicitud normal:**

```
GET /orders?id=100
```

El servidor devuelve la orden del usuario.

Pero un atacante podría probar:

```
GET /orders?id=101
```

Si el sistema no valida correctamente los permisos, podría ver pedidos de otros usuarios.

Este tipo de falla se conoce como: **Broken Access Control (OWASP Top 10)**.

### Mensaje clave

> "Muchos ataques no consisten en romper sistemas complejos. Consisten en enviar solicitudes que el servidor no estaba preparado para manejar."

### Cierre de la sección

> "En ciberseguridad muchas veces no estamos hackeando computadoras, estamos interactuando con servidores de formas que los desarrolladores no anticiparon."

## 6. Puertos y servicios

Este es uno de los **conceptos más importantes para seguridad**.

### Pregunta fundamental

Hasta ahora hemos visto que los sistemas se comunican a través de redes y que existe un modelo cliente-servidor.

Pero surge una pregunta importante:

> Si un servidor puede ofrecer muchos servicios distintos al mismo tiempo, ¿cómo sabe el sistema a cuál servicio debe enviar una solicitud?

La respuesta está en los **puertos**.

Los puertos son un mecanismo que permite que un mismo computador pueda ejecutar muchos servicios simultáneamente, y que cada uno pueda recibir las solicitudes que le corresponden.

### Qué es un servicio

Un servicio es **un programa que se ejecuta en un sistema y que está diseñado para esperar solicitudes de otros sistemas**.

Cuando decimos que un servicio está "escuchando", significa que está **esperando conexiones entrantes**.

Ejemplos de servicios muy comunes:

- Servidor web
- Servidor de correo
- Servidor de base de datos
- Servidor de acceso remoto
- Servidor DNS

Cada uno de estos servicios realiza funciones diferentes.

Por ejemplo:

- Un servidor web se encarga de entregar páginas web
- Un servidor de correo gestiona correos electrónicos
- Un servidor SSH permite acceso remoto al sistema

### Qué es un puerto

Un puerto es **un número que identifica un servicio dentro de un sistema**.

Podemos imaginar que un computador es como una **gran central de comunicaciones**.

Cuando llega una solicitud desde la red, el sistema necesita saber a qué servicio entregarla.

Ahí es donde entran los puertos.

**Cada servicio escucha en un número de puerto específico.**

Esto permite que múltiples servicios funcionen al mismo tiempo sin interferir entre sí.

### Ejemplo sencillo

Imaginemos un servidor que tiene:

- Un servidor web
- Un servicio SSH
- Un servidor de correo

Cada uno utiliza un puerto distinto.

Por ejemplo:

| Puerto | Servicio |
|--------|----------|
| 80 | HTTP (páginas web) |
| 443 | HTTPS (web segura) |
| 22 | SSH (acceso remoto) |
| 21 | FTP (transferencia de archivos) |
| 25 | SMTP (correo electrónico) |

Esto significa que cuando llega una solicitud al puerto 80, el sistema sabe que debe enviarla al servidor web.

### Analogía del edificio

Una analogía muy útil es imaginar que un computador es como un **edificio**.

El edificio tiene muchas puertas. Cada puerta tiene un número. Cada puerta conduce a un departamento diferente.

El computador funciona de manera similar:

- El edificio → el computador
- Los departamentos → los servicios
- Los números de puerta → los puertos

Cuando alguien llega al edificio, debe saber a qué puerta ir. Si toca la puerta incorrecta, nadie responderá.

### Qué significa que un puerto esté abierto

Cuando decimos que un puerto está abierto, significa que **existe un servicio escuchando en ese puerto**.

Esto quiere decir que el sistema está preparado para aceptar conexiones entrantes.

Por ejemplo:

- Si el puerto 80 está abierto, significa que probablemente hay un servidor web funcionando
- Si el puerto 22 está abierto, significa que probablemente existe acceso SSH al servidor

### Puertos más comunes

| Puerto | Servicio | Uso |
|--------|----------|-----|
| 22 | SSH | Acceso remoto seguro |
| 80 | HTTP | Páginas web |
| 443 | HTTPS | Web segura |
| 21 | FTP | Transferencia de archivos |
| 25 | SMTP | Correo electrónico |
| 53 | DNS | Resolución de nombres |
| 3306 | MySQL | Base de datos |

### Conexión con ciberseguridad

Este concepto es **extremadamente importante** para entender cómo funcionan muchos ataques.

Un principio clave en ciberseguridad es:

> "Si un puerto está abierto, significa que existe una superficie potencial de ataque."

Cada servicio expuesto puede tener:

- Vulnerabilidades
- Configuraciones incorrectas
- Errores de implementación

Por eso, uno de los primeros pasos en hacking es **descubrir qué puertos están abiertos en un sistema**.

Esto se llama **escaneo de puertos**.

### Ejemplo real de cómo piensa un atacante

Supongamos que un atacante encuentra un servidor en internet.

Lo primero que hará es **escanear el sistema** para ver qué servicios están disponibles.

Por ejemplo, el resultado podría ser:

| Puerto | Servicio |
|--------|----------|
| 22 | SSH |
| 80 | Servidor web |
| 3306 | Base de datos |

Esto le dice al atacante que el servidor tiene varios servicios activos.

Ahora el atacante puede investigar cada uno.

### Superficie de ataque

El concepto de **superficie de ataque** se refiere a la cantidad de puntos por los cuales un sistema puede ser atacado.

Cuantos más servicios exponga un sistema, **mayor es su superficie de ataque**.

Por ejemplo:

**Servidor A**

- Puerto 80
- Puerto 443

**Servidor B**

- Puerto 21
- Puerto 22
- Puerto 80
- Puerto 443
- Puerto 3306
- Puerto 8080

El servidor B tiene una **superficie de ataque mucho mayor**.

### Ejemplo práctico

Imagina un servidor corporativo que tiene abiertos los siguientes servicios:

- SSH para administración remota
- Base de datos accesible desde la red
- Panel administrativo web

Esto puede ser **muy peligroso**.

Un atacante podría intentar:

- Atacar el servicio SSH con fuerza bruta
- Explotar vulnerabilidades en la base de datos
- Intentar acceder al panel administrativo

**Cada servicio representa un posible vector de ataque.**

### Buenas prácticas de seguridad

Por esta razón, una de las **primeras reglas de seguridad** es:

> "No expongas servicios que no necesitas."

Esto se conoce como **reducción de la superficie de ataque**.

Muchas organizaciones siguen el principio de: **cerrar todos los puertos innecesarios.**

Solo se mantienen abiertos los servicios que realmente se requieren.

## 7. TCP vs UDP

### TCP (Transmission Control Protocol)

**Características:**

- Conexión confiable
- Verifica entrega
- Más lento
- Garantiza que los datos llegan en orden

**Ejemplos de uso:**

- Web (HTTP/HTTPS)
- SSH
- Bases de datos
- Correo electrónico

**Cuándo usarlo:**
Cuando es crítico que los datos lleguen correctamente y en orden.

### UDP (User Datagram Protocol)

**Características:**

- No verifica entrega
- Más rápido
- Menos control
- No garantiza que los datos lleguen

**Ejemplos de uso:**

- Streaming de video
- DNS
- Videojuegos
- Llamadas de voz

**Cuándo usarlo:**
Cuando la velocidad es más importante que la confiabilidad.

### Conexión con seguridad

**TCP es más fácil de analizar.**

Esto significa que es más fácil detectar patrones maliciosos en conexiones TCP.

**UDP es más difícil de monitorear.**

Dado que UDP no requiere una conexión establecida, es más fácil enviar paquetes sin que el destino los espere.

**Muchos ataques de DDoS usan UDP.**

Los atacantes pueden enviar enormes cantidades de paquetes UDP a un servidor, saturándolo sin necesidad de establecer una conexión completa.
