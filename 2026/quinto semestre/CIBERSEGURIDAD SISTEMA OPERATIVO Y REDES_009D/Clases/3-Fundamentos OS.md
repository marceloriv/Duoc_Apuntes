# Clase 3 – Sistemas Operativos y Seguridad

**Tema:** Sistemas operativos para seguridad (Linux, Windows, usuarios, privilegios y superficie de ataque)

**Objetivo de la clase:**

Que los estudiantes comprendan:

- Qué hace realmente un sistema operativo
- Por qué es un componente crítico de seguridad
- Cómo funcionan usuarios y privilegios
- Qué significa superficie de ataque en un sistema

---

## 1. Qué es realmente un sistema operativo

### Introducción

> "Antes de hablar de seguridad en sistemas, quiero partir con algo muy básico. ¿Alguien me puede decir qué es un sistema operativo?"

Lo más probable es que los estudiantes respondan cosas como:

- Windows
- Linux
- macOS
- Android

"Todas esas respuestas están bien… pero en realidad esas son **ejemplos de sistemas operativos**, no la definición de lo que es un sistema operativo."

### Definición

Un sistema operativo es **el software fundamental que gestiona todos los recursos de un computador**.

Es el programa principal que se encarga de coordinar todo lo que ocurre dentro del sistema.

Su función principal es **actuar como intermediario entre tres elementos:**

#### Hardware

Los componentes físicos del computador.

Ejemplos:

- Procesador (CPU)
- Memoria RAM
- Disco duro o SSD
- Tarjeta de red
- Teclado
- Pantalla

El hardware por sí solo no sabe ejecutar programas ni tomar decisiones. Necesita software que lo controle.

#### Aplicaciones

Las aplicaciones son los programas que utilizan los usuarios.

Ejemplos:

- Navegadores web
- Aplicaciones móviles
- Bases de datos
- Programas de oficina
- Servidores web
- Videojuegos

Las aplicaciones **no interactúan directamente con el hardware**. En cambio, le piden al sistema operativo que realice acciones por ellas.

Por ejemplo:

- Guardar archivos
- Usar memoria
- Conectarse a la red
- Acceder al disco

#### Usuarios

Los usuarios son las personas que utilizan el sistema.

Ejemplos:

- Un estudiante usando su notebook
- Un empleado trabajando en un computador corporativo
- Un administrador gestionando servidores

El sistema operativo controla **qué usuarios pueden hacer qué cosas dentro del sistema**.

> "El sistema operativo es el administrador central del computador. Todo pasa a través de él."

### Qué gestiona un sistema operativo

Un sistema operativo controla varios aspectos críticos del funcionamiento de un computador.

#### Procesos

Un proceso es simplemente un programa que se está ejecutando en el sistema.

Cada vez que abrimos una aplicación, el sistema operativo crea uno o más procesos.

Ejemplos de procesos:

- Un navegador web
- Un editor de texto
- Un reproductor de música
- Un servidor web
- Una base de datos

**Ejemplo práctico:**
Cuando un estudiante abre Chrome:

1. El sistema operativo carga el programa en memoria
2. Asigna recursos de CPU
3. Gestiona el uso de memoria
4. Controla su ejecución

Además, el sistema operativo permite que muchos procesos se ejecuten al mismo tiempo. Esto se llama **multitarea**.

Por ejemplo, un computador puede estar ejecutando simultáneamente:

- Navegador
- Spotify
- Antivirus
- Actualizaciones del sistema
- Servicios de red

El sistema operativo decide cuándo y cómo se ejecuta cada proceso.

#### Memoria

La memoria RAM es el espacio donde los programas se ejecutan mientras el computador está encendido.

La RAM es un recurso limitado. Por ejemplo, un computador puede tener:

- 8 GB
- 16 GB
- 32 GB de RAM

El sistema operativo decide:

- Qué procesos pueden usar memoria
- Cuánta memoria puede usar cada uno
- Qué ocurre cuando la memoria se llena

**Ejemplo simple:**
Si un computador tiene abiertos:

- Un navegador con muchas pestañas
- Word
- Spotify
- Una aplicación de videollamada

Todos esos programas están usando memoria al mismo tiempo. El sistema operativo se encarga de administrar ese uso de memoria para que el sistema no colapse.

#### Archivos

El sistema operativo también controla el sistema de archivos, que es la forma en que los datos se almacenan en el disco.

Esto incluye:

- Documentos
- Imágenes
- Programas
- Bases de datos
- Configuraciones del sistema

**Qué hace el sistema operativo con los archivos:**

El sistema operativo decide:

- Dónde se guardan los archivos en el disco
- Quién puede acceder a ellos
- Quién puede modificarlos
- Quién puede ejecutarlos

**Ejemplo:**
Cuando guardas un documento en tu computador, el sistema operativo:

1. Decide en qué parte del disco guardarlo
2. Registra su ubicación
3. Asigna permisos de acceso

#### Dispositivos

El sistema operativo también controla los dispositivos de hardware conectados al computador.

Ejemplos de dispositivos:

- Discos duros
- Tarjetas de red
- Teclados
- Impresoras
- Dispositivos USB
- Cámaras

**Qué hace el sistema operativo:**

Gestiona la comunicación entre los programas y el hardware.

Por ejemplo, cuando un navegador descarga un archivo desde internet:

1. Usa la tarjeta de red
2. Guarda datos en el disco
3. Muestra información en la pantalla

Todo eso ocurre gracias al sistema operativo.

#### Usuarios

El sistema operativo también gestiona las identidades dentro del sistema.

Esto significa que controla:

- Quién puede acceder al sistema
- Qué acciones puede realizar cada usuario

Cada usuario tiene:

- Un nombre
- Credenciales (como contraseña)
- Permisos específicos

**Ejemplo:**
En un computador pueden existir varios tipos de usuarios:

- Administrador
- Usuario estándar
- Usuario invitado

Cada uno tiene permisos distintos. Por ejemplo, un usuario normal puede usar aplicaciones, pero no debería poder modificar configuraciones críticas del sistema.

### Conexión con ciberseguridad

"Todo lo que hemos visto hasta ahora muestra que el sistema operativo **controla prácticamente todo dentro del computador**."

Esto significa que **el sistema operativo es el controlador principal de seguridad del sistema**.

Si el sistema operativo es comprometido por un atacante, pueden ocurrir varias cosas graves.

El atacante podría:

- Acceder a todos los archivos
- Controlar los programas que se ejecutan
- Instalar malware
- Interceptar comunicaciones
- Modificar configuraciones del sistema

En ese momento el atacante tiene **control total del sistema**.

### Por qué muchos ataques buscan escalar privilegios

Muchos ataques informáticos siguen un patrón similar.

Primero el atacante obtiene **acceso limitado**. Por ejemplo:

- Compromete una aplicación web
- Roba credenciales de un usuario
- Explota una vulnerabilidad

Pero ese acceso inicial suele ser limitado.

Entonces el atacante intenta algo llamado: **escalación de privilegios**.

Esto significa intentar pasar de:

- Usuario limitado → Administrador del sistema

Si lo logra, el atacante puede **controlar completamente el sistema operativo**.

Y cuando alguien controla el sistema operativo: **controla todo el sistema**.

> "En ciberseguridad muchas veces no se trata solo de proteger aplicaciones. Se trata de proteger el sistema operativo que controla todo."

---

## 2. Linux vs Windows en seguridad

> "Ahora que entendemos qué es un sistema operativo, hay algo muy importante que deben saber en ciberseguridad: No todos los sistemas operativos se usan en los mismos contextos."

En el mundo real existen muchos sistemas operativos, pero dos dominan prácticamente toda la infraestructura tecnológica:

- **Windows**
- **Linux**

Cada uno domina distintos entornos tecnológicos, y eso tiene implicancias directas en ciberseguridad.

### Windows

Windows domina principalmente en **entornos de usuario final y entornos corporativos**.

Esto significa que es el sistema operativo más común en:

- Computadores personales
- Notebooks de empresas
- Estaciones de trabajo
- Redes corporativas
- Entornos de oficina

Si entran a cualquier empresa grande, lo más probable es que encuentren:

- Computadores con Windows
- Servidores Windows
- Infraestructura basada en Active Directory

#### Active Directory

Uno de los componentes más importantes de Windows en empresas es **Active Directory**.

Active Directory es un sistema que permite **administrar centralmente:**

- Usuarios
- Contraseñas
- Permisos
- Computadores
- Servidores
- Políticas de seguridad

Por ejemplo, en una empresa con 2000 empleados: no sería práctico crear usuarios manualmente en cada computador.

En cambio, se usa Active Directory para:

- Crear cuentas de usuario
- Asignar permisos
- Controlar accesos
- Aplicar políticas de seguridad

**Ejemplo práctico:**
Cuando un empleado inicia sesión en su computador corporativo:

1. Ingresa su usuario y contraseña
2. El computador consulta a Active Directory
3. Active Directory valida la identidad
4. El usuario obtiene acceso a recursos de la empresa

Es decir, Active Directory controla gran parte de la seguridad de la red corporativa.

#### Importancia para ciberseguridad

Debido a que Windows domina los entornos corporativos, **muchos ataques reales se enfocan en comprometer sistemas Windows**.

Por ejemplo:

- Robo de credenciales de usuarios
- Abuso de Active Directory
- Movimiento lateral dentro de la red

**Ejemplo real de ataques:**
En muchos ataques de ransomware el objetivo final del atacante es: **comprometer el Domain Controller de Active Directory**.

El Domain Controller es el servidor que controla toda la autenticación de la empresa.

Si el atacante compromete ese servidor: **puede controlar toda la red corporativa**.

### Linux

Linux domina en **infraestructura tecnológica crítica**.

Aunque muchos estudiantes no lo sepan, **gran parte de internet funciona sobre Linux**.

Linux domina en:

- Servidores
- Infraestructura cloud
- Centros de datos
- Dispositivos de red
- Supercomputadores
- Plataformas backend

#### Ejemplos reales

La mayoría de:

- Servidores web
- Plataformas cloud
- Bases de datos
- Sistemas backend
- Plataformas de streaming

Funcionan sobre Linux.

Empresas como:

- Google
- Amazon
- Facebook
- Netflix

Utilizan principalmente **Linux en sus infraestructuras**.

#### Cloud computing

Las plataformas cloud más grandes del mundo utilizan Linux masivamente.

Por ejemplo:

- AWS
- Azure
- Google Cloud

Ofrecen principalmente servidores Linux. Esto significa que muchos servicios modernos funcionan sobre este sistema operativo.

#### Contenedores

Otro elemento importante donde Linux domina es en contenedores.

Tecnologías como:

- Docker
- Kubernetes

Se basan principalmente en Linux.

Los contenedores permiten ejecutar aplicaciones de forma aislada y escalable.

### Diferencias relevantes para seguridad

#### Windows

Windows está diseñado principalmente para **entornos corporativos integrados**.

Esto significa que muchas funcionalidades están profundamente conectadas entre sí.

Por ejemplo:

- Active Directory
- Autenticación
- Gestión de políticas
- Administración de usuarios

Esta integración facilita la administración de redes corporativas.

Pero también significa que: **si un atacante compromete ciertos componentes, puede moverse fácilmente dentro de la red**.

**Superficie de ataque grande:**
Windows suele tener una superficie de ataque grande debido a:

- Muchos servicios integrados
- Compatibilidad con software antiguo
- Entornos complejos

Por ejemplo, en redes corporativas es común encontrar:

- SMB
- RDP
- Servicios de dominio
- Herramientas administrativas

Cada uno de esos componentes puede ser un posible vector de ataque.

#### Linux

Linux tiene un enfoque diferente. Es un **sistema operativo más modular**.

Esto significa que puede instalarse solo con los componentes necesarios.

Por ejemplo, un servidor Linux puede ejecutar únicamente:

- Servidor web
- SSH
- Base de datos

Sin instalar componentes innecesarios.

**Control de permisos:**
Linux también tiene un **sistema de permisos muy estructurado**.

Los archivos y procesos tienen permisos específicos como:

- Lectura
- Escritura
- Ejecución

Esto permite controlar con precisión qué usuarios pueden hacer ciertas acciones.

**Uso en servidores:**
Linux es muy utilizado en servidores porque:

- Es estable
- Consume pocos recursos
- Puede configurarse de forma muy específica

Esto lo hace ideal para infraestructura crítica.

### Mensaje clave

"Aunque Linux y Windows son diferentes, hay algo muy importante que deben entender para ciberseguridad."

La **mayoría de los ataques reales terminan interactuando con el sistema operativo**.

Esto significa que los atacantes muchas veces buscan:

- Robar credenciales
- Escalar privilegios
- Ejecutar código malicioso
- Instalar malware
- Moverse dentro de la red

**Ejemplo real de ataque:**
Un ataque típico puede funcionar así:

1. El atacante compromete una aplicación web
2. Obtiene acceso al servidor
3. Obtiene acceso a una shell del sistema operativo
4. Intenta escalar privilegios
5. Toma control del sistema

En ese momento el atacante está interactuando directamente con el sistema operativo.

> "En ciberseguridad no basta con entender aplicaciones o redes. Hay que entender cómo funcionan los sistemas operativos."

Porque al final:

- Los ataques ocurren dentro del sistema
- Las defensas se implementan en el sistema
- Y el control final del atacante ocurre en el sistema operativo

---

## 3. Usuarios y autenticación

> "Ahora vamos a hablar de uno de los conceptos más importantes en seguridad: las identidades dentro de un sistema."

En casi todos los sistemas informáticos existe el concepto de usuario.

Esto permite que el sistema operativo controle **quién puede acceder al sistema y qué puede hacer cada persona dentro de él**.

### Concepto de usuario

Un sistema operativo funciona con usuarios.

Un usuario **representa una identidad dentro del sistema**.

Esto significa que el sistema operativo necesita saber quién está usando el sistema en cada momento.

Cada usuario tiene normalmente tres elementos principales:

- Nombre de usuario
- Contraseña u otro mecanismo de autenticación
- Permisos dentro del sistema

#### Nombre de usuario

El nombre de usuario es la forma en que el sistema identifica a una persona.

Ejemplos:

- diego
- admin
- juan.perez
- estudiante01

Este nombre permite al sistema saber qué identidad está intentando acceder.

#### Contraseña

La contraseña sirve para verificar que la persona que intenta acceder es realmente el usuario legítimo.

Este proceso se llama: **autenticación**

Autenticación significa simplemente: **comprobar que una identidad es quien dice ser**.

#### Permisos

Los permisos determinan qué puede hacer ese usuario dentro del sistema.

Por ejemplo, un usuario puede tener permiso para:

- Leer archivos
- Crear archivos
- Ejecutar programas

Pero no necesariamente puede:

- Instalar software
- Modificar configuraciones del sistema
- Cambiar otros usuarios

### Tipos de usuarios

En la mayoría de los sistemas operativos existen diferentes tipos de usuarios con distintos niveles de privilegio.

Los dos tipos más comunes son:

- Usuario normal
- Usuario administrador

#### Usuario normal

Un usuario normal es un usuario con **permisos limitados**.

Puede usar el sistema, pero no puede modificar partes críticas del mismo.

Normalmente puede:

- Ejecutar aplicaciones
- Crear y modificar sus propios archivos
- Navegar por internet
- Usar programas instalados

Pero normalmente no puede:

- Instalar software para todo el sistema
- Modificar configuraciones críticas
- Cambiar permisos de otros usuarios
- Acceder a archivos del sistema

**Por qué existen usuarios normales:**

Esto existe por un principio muy importante en seguridad llamado: **principio de mínimo privilegio**.

Este principio dice que: **un usuario debería tener solo los permisos necesarios para realizar su trabajo**.

Esto reduce el impacto de errores o ataques.

**Ejemplo práctico:**
En una empresa, un empleado de marketing necesita:

- Acceso a documentos
- Acceso a correo
- Acceso a herramientas de trabajo

Pero no necesita:

- Modificar servidores
- Instalar software del sistema
- Administrar usuarios

Por lo tanto, se le asigna una cuenta de usuario normal.

#### Usuario administrador

Un usuario administrador tiene **control completo sobre el sistema**.

Esto significa que puede realizar prácticamente cualquier acción.

Por ejemplo, puede:

- Instalar software
- Modificar configuraciones del sistema
- Cambiar permisos de archivos
- Crear o eliminar usuarios
- Administrar servicios del sistema

**Por qué existen administradores:**

Los administradores son necesarios porque alguien debe poder:

- Instalar programas
- Mantener el sistema
- Realizar tareas técnicas
- Resolver problemas

Pero por razones de seguridad **el número de administradores debe ser limitado**.

**Riesgo de seguridad:**

Si una cuenta de administrador es comprometida por un atacante: el atacante puede:

- Instalar malware
- Robar información
- Modificar el sistema
- Crear nuevas cuentas

En ese momento el atacante tiene **control total del sistema**.

#### Ejemplo en Linux

En Linux existen usuarios normales y un usuario especial llamado: **root**

El usuario root es el administrador del sistema. Tiene permisos para realizar cualquier acción dentro del sistema operativo.

Por ejemplo, root puede:

- Modificar archivos del sistema
- Instalar software
- Eliminar cualquier archivo
- Cambiar permisos de otros usuarios

**Importancia del usuario root:**

El usuario root tiene tanto poder que muchas distribuciones Linux restringen su uso directo.

En cambio, se utilizan mecanismos como: **sudo**

Esto permite ejecutar comandos administrativos solo cuando es necesario.

Esto reduce el riesgo de cometer errores o ejecutar malware con privilegios altos.

#### Ejemplo en Windows

En Windows el sistema de privilegios funciona de manera similar, pero con una estructura diferente.

Windows utiliza **grupos de usuarios**.

Uno de los grupos más importantes es: **Administrators**

Los usuarios que pertenecen a este grupo tienen **privilegios elevados**.

Esto significa que pueden:

- Instalar software
- Modificar configuraciones del sistema
- Gestionar usuarios
- Administrar servicios

**Usuarios estándar:**

Los usuarios normales en Windows se llaman: **Standard Users**

Estos usuarios tienen permisos limitados y no pueden modificar el sistema.

**UAC (User Account Control):**

Windows también utiliza un mecanismo llamado: **UAC – User Account Control**

Cuando un usuario intenta realizar una acción administrativa, Windows solicita confirmación.

Esto ayuda a evitar que programas maliciosos obtengan privilegios elevados sin permiso.

### Conexión con ciberseguridad

"Muchos ataques informáticos no comienzan hackeando sistemas complejos. Comienzan simplemente comprometiendo una cuenta de usuario."

#### Cómo se comprometen cuentas de usuario

Los atacantes pueden obtener acceso a cuentas de usuario mediante diferentes técnicas.

Por ejemplo:

**Phishing:**
Correos electrónicos falsos que engañan al usuario para que entregue su contraseña.

Ejemplo: Un correo que parece provenir de la empresa o de un servicio confiable.

**Robo de credenciales:**
Malware o ataques que capturan contraseñas almacenadas en el sistema.

Por ejemplo:

- Keyloggers
- Malware que roba cookies o tokens

**Malware:**
Un usuario descarga o ejecuta un programa malicioso.

Ese programa puede robar credenciales o abrir acceso al sistema.

#### Qué ocurre después del acceso inicial

Una vez que un atacante obtiene acceso a una cuenta de usuario, normalmente intenta algo llamado: **escalación de privilegios**.

Esto significa intentar pasar de:

- Usuario normal → Administrador del sistema

**Ejemplo típico de ataque:**
Un ataque puede seguir estos pasos:

1. El atacante roba credenciales de un usuario
2. Accede al sistema con permisos limitados
3. Busca vulnerabilidades en el sistema
4. Explota una vulnerabilidad para obtener privilegios de administrador

Una vez que logra eso, el atacante puede **controlar completamente el sistema**.

### Mensaje clave

> "Muchas veces la seguridad de un sistema no se rompe por una falla técnica extremadamente compleja, sino porque un atacante logra comprometer una cuenta de usuario."

Por eso la seguridad moderna se enfoca mucho en:

- Proteger identidades
- Proteger credenciales
- Controlar privilegios

---

## 4. Privilegios y control de acceso

> "En la sección anterior vimos que los sistemas operativos funcionan con usuarios. Pero ahora aparece una pregunta muy importante para la seguridad: ¿qué puede hacer cada usuario dentro del sistema?"

La respuesta a esa pregunta está en los **privilegios**.

### Qué son los privilegios

Los privilegios **determinan qué acciones puede realizar un usuario dentro de un sistema**.

Es decir, los privilegios **definen los límites de lo que una cuenta puede hacer**.

En otras palabras: **los privilegios determinan el nivel de poder que tiene un usuario dentro del sistema**.

#### Ejemplo básico

Un usuario puede tener permiso para:

- Leer archivos
- Escribir archivos
- Ejecutar programas

Pero puede no tener permiso para:

- Modificar archivos del sistema
- Instalar software
- Cambiar configuraciones críticas

#### Ejemplo práctico

Supongamos que un usuario abre un archivo en su computador.

- Si tiene **permiso de lectura**, puede abrirlo
- Si tiene **permiso de escritura**, puede modificarlo
- Si tiene **permiso de ejecución**, puede ejecutar ese archivo como un programa

Estos permisos son gestionados por el sistema operativo.

#### Ejemplo en Linux

En Linux los permisos clásicos son:

- **r** (read) → Leer
- **w** (write) → Escribir
- **x** (execute) → Ejecutar

Estos permisos pueden aplicarse a:

- El propietario del archivo
- El grupo
- Otros usuarios

Esto permite controlar con precisión quién puede hacer qué.

### Principio de mínimo privilegio

"Uno de los principios más importantes de la ciberseguridad es el **principio de mínimo privilegio**."

Este principio establece que:

> Cada usuario debe tener solo los permisos estrictamente necesarios para realizar su trabajo. Ni más. Ni menos.

#### Por qué es importante

Esto reduce enormemente el impacto de:

- Errores humanos
- Malware
- Ataques informáticos

Si un usuario tiene permisos muy limitados, incluso si su cuenta es comprometida, el atacante también tendrá permisos limitados.

#### Ejemplo sencillo

Imaginemos un empleado del área de marketing.

Su trabajo requiere acceso a:

- Documentos de marketing
- Campañas publicitarias
- Material gráfico

Pero no necesita acceso a:

- Base de datos financiera
- Registros de clientes
- Configuraciones de servidores

Por lo tanto, siguiendo el principio de mínimo privilegio, el sistema debería permitirle acceder solo a los recursos necesarios para su trabajo.

#### Qué ocurre si no se aplica este principio

Si todos los empleados tienen acceso a todo:

- Aumenta el riesgo de filtraciones de información
- Aumenta el impacto de errores
- Aumenta el impacto de ataques

Por ejemplo, si un empleado descarga malware, ese malware podría acceder a toda la información de la empresa.

### Qué ocurre cuando esto falla

En muchos incidentes de seguridad el problema **no es una vulnerabilidad técnica extremadamente compleja**.

El problema es **una mala gestión de privilegios**.

Si los privilegios están mal configurados pueden ocurrir cosas como:

- Usuarios con acceso innecesario a información sensible
- Cuentas con privilegios excesivos
- Servicios ejecutándose con permisos administrativos
- Malware ejecutándose con privilegios elevados

#### Ejemplo realista

Imagina que en una empresa **todos los usuarios tienen privilegios de administrador**.

Esto significa que cualquier usuario puede:

- Instalar software
- Modificar configuraciones del sistema
- Ejecutar programas con privilegios altos

Si un usuario abre un archivo malicioso, ese programa se ejecutará con privilegios de administrador.

Esto facilita que el malware:

- Instale otros programas maliciosos
- Modifique el sistema
- Desactive controles de seguridad

### Escalación de privilegios

"Muchos ataques informáticos no comienzan con acceso total al sistema. Comienzan con acceso limitado."

Por ejemplo:

- Comprometiendo un usuario normal
- Explotando una aplicación vulnerable
- Obteniendo acceso a un servicio

Pero ese acceso inicial suele ser limitado.

Entonces el atacante intenta algo llamado: **escalación de privilegios**.

#### Qué es escalación de privilegios

La escalación de privilegios consiste en **aumentar el nivel de acceso dentro del sistema**.

Es decir: **pasar de un nivel bajo de permisos a un nivel alto**.

Por ejemplo: **Usuario normal → Administrador**

#### Ejemplo típico de ataque

Muchos ataques siguen un patrón similar:

1. El atacante compromete un usuario normal
2. Obtiene acceso limitado al sistema
3. Busca vulnerabilidades dentro del sistema operativo
4. Explota una vulnerabilidad
5. Obtiene privilegios de administrador

Este proceso se conoce como: **privilege escalation**.

#### Qué puede hacer el atacante después

Si el atacante logra escalar privilegios puede:

- Instalar malware persistente
- Robar información sensible
- Crear nuevas cuentas administrativas
- Desactivar sistemas de seguridad
- Moverse a otros sistemas dentro de la red

En ese momento el atacante tiene **control total del sistema**.

#### Ejemplo real de la industria

Muchos ataques de ransomware siguen exactamente esta lógica.

Primero:

- Comprometen un usuario mediante phishing

Luego:

- Escalan privilegios

Después:

- Toman control de servidores

Finalmente:

- Cifran sistemas completos

### Mensaje clave

> "En seguridad no basta con proteger el acceso inicial. También es fundamental controlar los privilegios dentro del sistema."

Porque si un atacante entra con permisos bajos, pero puede escalar fácilmente, el sistema sigue siendo vulnerable.

---

## 5. Superficie de ataque del sistema operativo

> "Si ustedes fueran atacantes y quisieran comprometer un sistema, ¿por dónde intentarían entrar?"

Probablemente dirán cosas como:

- Por internet
- Por una vulnerabilidad
- Por un programa
- Por una contraseña

> "Exactamente. Y todos esos puntos posibles forman lo que llamamos **superficie de ataque**."

### Concepto

La **superficie de ataque es el conjunto de todos los puntos por donde un sistema puede ser atacado**.

Es decir, **todos los lugares donde un atacante podría interactuar con el sistema**.

Mientras más componentes tenga un sistema, **más posibilidades existen de que algo falle o tenga una vulnerabilidad**.

En un sistema operativo, la superficie de ataque incluye elementos como:

- Servicios que están ejecutándose
- Puertos abiertos en la red
- Aplicaciones instaladas
- Cuentas de usuario
- Configuraciones del sistema

Cada uno de estos componentes puede convertirse en un **punto de entrada para un atacante**.

### Ejemplo de superficie de ataque

Imaginemos un servidor que tiene instalados varios servicios.

Por ejemplo:

- Servidor web
- Servicio SSH
- Base de datos
- Panel administrativo

Cada uno de estos servicios permite que alguien interactúe con el sistema.

Por ejemplo:

- El servidor web permite que usuarios accedan a una página
- SSH permite que administradores se conecten remotamente
- La base de datos gestiona información
- El panel administrativo permite gestionar la aplicación

#### Desde la perspectiva de seguridad

Cada uno de estos componentes representa un **posible punto de ataque**.

Un atacante podría intentar:

- Explotar una vulnerabilidad en el servidor web
- Atacar el servicio SSH con fuerza bruta
- Explotar vulnerabilidades en la base de datos
- Comprometer el panel administrativo

Es decir, **cada componente adicional aumenta el número de posibles ataques**.

### Analogía simple

Imagina que un sistema es como un **edificio**.

Cada puerta o ventana representa un **posible punto de entrada**.

Si el edificio tiene:

- Una puerta
- Dos ventanas

Hay pocos lugares por donde entrar.

Pero si tiene:

- Diez puertas
- Veinte ventanas
- Varias entradas traseras

Entonces existen muchos más puntos por donde alguien podría entrar.

Esto es exactamente lo que ocurre con los sistemas informáticos.

### Otros elementos de superficie de ataque

La superficie de ataque no se limita solo a servicios visibles en la red. También incluye muchos otros factores internos del sistema.

#### Servicios innecesarios

Los sistemas operativos pueden ejecutar múltiples servicios en segundo plano.

Un servicio es un programa que se ejecuta continuamente para ofrecer una función.

Por ejemplo:

- Servidor web
- Servicio de impresión
- Servidor FTP
- Servicios de red
- Servicios administrativos

**Problema de seguridad:**

Muchas veces los sistemas tienen servicios activados que **no son necesarios**.

Por ejemplo, un servidor web que también tiene activado:

- Servicio FTP
- Servicio de impresión
- Servicio de escritorio remoto

Si esos servicios no son necesarios, simplemente **aumentan la superficie de ataque**.

Cada servicio adicional es una oportunidad más para que exista una vulnerabilidad.

#### Software desactualizado

Otro factor muy importante es el **software desactualizado**.

Muchos programas contienen vulnerabilidades conocidas. Cuando se descubren estas vulnerabilidades, normalmente se publican **parches de seguridad para corregirlas**.

Pero si el software no se actualiza, esas vulnerabilidades siguen existiendo.

**Ejemplo real:**
Un servidor puede estar ejecutando:

- Una versión antigua de Apache
- Una versión vulnerable de OpenSSH
- Una base de datos desactualizada

Un atacante puede buscar estas versiones vulnerables y explotarlas. Esto ocurre constantemente en internet.

#### Usuarios con privilegios excesivos

Otro elemento de superficie de ataque son las cuentas de usuario.

Mientras más cuentas existan en un sistema, **mayor es el riesgo de que alguna sea comprometida**.

Esto se vuelve especialmente peligroso cuando existen usuarios con privilegios elevados.

**Ejemplo:**
Si una empresa tiene muchos usuarios con privilegios de administrador:

Cualquier cuenta comprometida puede convertirse en una puerta de entrada para controlar el sistema.

Por ejemplo:

- Una contraseña débil
- Un ataque de phishing
- Malware que roba credenciales

Si esa cuenta tiene privilegios elevados, el atacante obtiene mucho poder dentro del sistema.

#### Configuraciones incorrectas

Las configuraciones también forman parte de la superficie de ataque.

Un sistema puede ser vulnerable **no por el software que utiliza, sino por cómo está configurado**.

Ejemplos comunes de malas configuraciones:

- Permisos de archivos incorrectos
- Servicios expuestos innecesariamente
- Contraseñas débiles
- Acceso remoto abierto a internet
- Bases de datos accesibles públicamente

**Ejemplo realista:**
Una base de datos que debería estar accesible solo desde la red interna podría estar **expuesta directamente a internet**.

Esto permitiría que cualquier persona en internet intente conectarse.

En muchos incidentes de seguridad, los problemas **no son vulnerabilidades sofisticadas**. Son simplemente **malas configuraciones**.

### Mensaje clave

> "Cuantos más componentes tenga un sistema, mayor es su superficie de ataque."

Esto significa que un sistema con:

- Muchos servicios
- Muchas aplicaciones
- Muchas cuentas de usuario
- Muchas configuraciones complejas

Tiene **más posibilidades de tener errores o vulnerabilidades**.

### Principio de seguridad

Por esta razón, una de las prácticas más importantes en seguridad es:

> **Reducir la superficie de ataque.**

Esto se logra mediante acciones como:

- Deshabilitar servicios innecesarios
- Cerrar puertos no utilizados
- Eliminar cuentas innecesarias
- Actualizar software
- Aplicar configuraciones seguras

### Cierre de la sección

> "Un buen administrador de sistemas no solo instala software y servicios. También se preocupa de reducir al máximo los puntos por donde un atacante podría entrar."

---

## 6. Ataque WannaCry – 2017: Un caso real

> "Para cerrar la clase quiero mostrarles un ejemplo real de cómo una vulnerabilidad en un sistema operativo puede generar un impacto global."

En **mayo de 2017**, uno de los **ataques informáticos más grandes de la historia** afectó a miles de organizaciones en todo el mundo.

Este ataque fue conocido como **WannaCry**.

### Qué ocurrió

WannaCry era un **ransomware**, es decir, un malware que **cifra los archivos de un computador** y luego exige un pago para recuperarlos.

El ataque explotaba una **vulnerabilidad en Microsoft Windows**.

Esta vulnerabilidad estaba en un componente del sistema operativo llamado **SMB (Server Message Block)** puertos 139 y 445.

**SMB es un protocolo utilizado por Windows para compartir archivos dentro de redes**.

### La vulnerabilidad

La vulnerabilidad explotada se conocía como **EternalBlue**.

Permitía que un atacante pudiera:

- Enviar paquetes especialmente diseñados al sistema
- Ejecutar código remoto
- Tomar control del computador

Lo más grave es que **este ataque podía realizarse sin autenticación**, es decir, **sin necesidad de usuario o contraseña**.

Esto se conoce como **Remote Code Execution (RCE)**.

### Cómo se propagó el ataque

Una vez que un computador era infectado, el malware **buscaba otros computadores en la red con la misma vulnerabilidad**.

Luego intentaba **infectarlos automáticamente**.

Esto convirtió el ataque en algo similar a un **gusano informático (worm)**.

Es decir, el malware **podía propagarse por sí solo dentro de una red**.

### Impacto global

El ataque se propagó **extremadamente rápido**.

En pocas horas afectó a:

- Más de 150 países
- Más de 200.000 computadores

Muchas organizaciones importantes fueron afectadas.

#### Ejemplo: NHS del Reino Unido

Uno de los casos más graves ocurrió en el **National Health Service (NHS) del Reino Unido**, el sistema de salud público.

Muchos hospitales utilizaban computadores con **versiones antiguas de Windows que no habían sido actualizadas**.

Cuando el ransomware se propagó:

- Los sistemas de hospitales quedaron inutilizables
- Los médicos no podían acceder a historiales médicos
- Se cancelaron cirugías
- Ambulancias tuvieron que redirigirse a otros hospitales

> Esto demuestra algo muy importante: **un problema de seguridad informática puede afectar directamente servicios críticos para la sociedad**.

### Por qué ocurrió el ataque

El ataque fue posible por varias razones relacionadas con lo que vimos hoy en clase.

#### Software desactualizado

Muchos sistemas estaban ejecutando **versiones antiguas de Windows**.

Microsoft ya había publicado un **parche de seguridad**, pero muchas organizaciones no lo habían aplicado.

#### Servicios expuestos

El servicio **SMB estaba accesible dentro de muchas redes corporativas**.

Esto permitió que el malware se propagara rápidamente.

#### Superficie de ataque grande

Muchos sistemas tenían:

- Configuraciones inseguras
- Servicios innecesarios activos
- Sistemas antiguos

Esto **aumentó la superficie de ataque**.

### Conexión con lo visto en clase

Este caso ilustra varios conceptos que vimos hoy.

#### Sistema operativo

La vulnerabilidad estaba en el **sistema operativo Windows**. No era una aplicación. Era un componente central del sistema.

#### Superficie de ataque

El servicio SMB expuesto era parte de la **superficie de ataque del sistema**.

#### Privilegios

Una vez ejecutado el exploit, el malware podía ejecutar código con **privilegios altos**.

Esto permitía instalar ransomware en el sistema.

### Lección clave

> "Muchas veces cuando hablamos de ciberseguridad pensamos en hackers sofisticados o ataques muy complejos."

Pero en este caso el problema fue simplemente:

- Sistemas sin actualizar
- Servicios expuestos
- Vulnerabilidades conocidas

---

## Cierre de la clase

### Mensaje final

> "Hoy vimos que el sistema operativo controla procesos, memoria, archivos, usuarios y privilegios."

Si el sistema operativo tiene una vulnerabilidad o está mal configurado, **todo el sistema puede verse comprometido**.

Y como vimos con WannaCry, esto puede afectar:

- Empresas
- Hospitales
- Gobiernos
- Países completos

### Mensaje de cierre

> "El sistema operativo es el corazón de cualquier sistema."

Si un atacante logra comprometer el sistema operativo: **puede controlar todo lo demás**.

Por eso entender cómo funcionan:

- Usuarios
- Privilegios
- Servicios

Es **fundamental para la ciberseguridad**.
