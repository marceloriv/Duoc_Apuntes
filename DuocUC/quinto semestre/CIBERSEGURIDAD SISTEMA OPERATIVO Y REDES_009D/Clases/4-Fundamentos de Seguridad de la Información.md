# Clase 4 – Fundamentos de Seguridad de la Información

**Temas:**

- Triada CIA
- Activos
- Amenazas
- Vulnerabilidades
- Riesgos

**Objetivo de la clase:**

Que los estudiantes comprendan cómo se analiza la seguridad de un sistema desde una perspectiva estructurada y cómo se relacionan entre sí los conceptos fundamentales de seguridad de la información.

---

## Bloque 1 – Introducción a seguridad de la información

> "Cuando hablamos de ciberseguridad, ¿qué creen que estamos protegiendo realmente?"

Respuestas típicas de estudiantes:

- Computadores
- Servidores
- Redes
- Sistemas

**Pero la realidad es diferente:**

> "La ciberseguridad en realidad no se trata de proteger computadores. Se trata de proteger información."

En realidad, lo que protegemos **no son los computadores**. Lo que protegemos es **la información**.

"Todas esas cosas son parte de la infraestructura… pero lo que realmente tiene valor es la información que contienen."

### Diferencia importante: Ciberseguridad vs Seguridad de la Información

Es importante aclarar dos conceptos que muchas veces se confunden.

**Ciberseguridad:**
Se enfoca en **proteger sistemas tecnológicos**.

Ejemplos:

- Servidores
- Redes
- Aplicaciones
- Infraestructura tecnológica

**Seguridad de la Información:**
Se enfoca en **proteger la información sin importar dónde esté almacenada o cómo se procese**.

Por ejemplo, la información puede estar en:

- Una base de datos
- Un documento digital
- Un correo electrónico
- Un archivo en un computador
- Un documento impreso

> "Un documento impreso también es información. Si alguien roba ese documento, sigue siendo un problema de seguridad de la información."

---

## Bloque 2 – Triada CIA

Uno de los modelos más importantes de seguridad de la información es la **triada CIA**.

**CIA significa:**

- **C**onfidentiality (Confidencialidad)
- **I**ntegrity (Integridad)
- **A**vailability (Disponibilidad)

Estos tres principios **describen los objetivos fundamentales de la seguridad de la información**.

### 1. Confidencialidad

**Definición:**
La confidencialidad significa que **solo las personas autorizadas pueden acceder a la información**.

**Ejemplos de información que requiere confidencialidad:**

- Historiales médicos
- Datos bancarios
- Información personal de clientes
- Secretos industriales
- Datos de investigación

**Ejemplo simple:**
Si un atacante roba la base de datos de clientes de una empresa, se rompe la confidencialidad.

Si desbloqueas tu celular con contraseña o huella digital, ese mecanismo está **protegiendo la confidencialidad** de tu información personal.

**Controles que ayudan a proteger la confidencialidad:**

- Autenticación
- Control de acceso
- Cifrado
- Gestión de identidades

**Ejemplo real: Incidente de Equifax (2017)**

Uno de los casos más conocidos de pérdida de confidencialidad fue el incidente de Equifax en 2017.

Equifax es una empresa que gestiona información crediticia en Estados Unidos.

Un atacante explotó una vulnerabilidad en un servidor web y logró acceder a una enorme base de datos.

**Se filtraron datos de aproximadamente 147 millones de personas.**

Entre los datos filtrados había:

- Nombres
- Direcciones
- Números de seguridad social
- Fechas de nacimiento

> Este incidente es un ejemplo claro de pérdida de confidencialidad.

### 2. Integridad

**Definición:**
La integridad significa que **la información no debe ser alterada sin autorización**. La información debe mantenerse correcta, completa y confiable.

**Ejemplo claro:**
En un banco, si alguien modifica el saldo de una cuenta sin autorización, se rompe la integridad de la información.

**Otros ejemplos de problemas de integridad:**

- Modificación de notas de estudiantes
- Alteración de registros contables
- Manipulación de datos en una base de datos

**Controles utilizados para proteger la integridad:**

- Firmas digitales
- Hashes criptográficos
- Controles de cambios
- Registros de auditoría

### 3. Disponibilidad

**Definición:**
La disponibilidad significa que **la información y los sistemas deben estar accesibles cuando se necesitan**.

Si un sistema no está disponible, la organización no puede operar normalmente.

**Ejemplo claro:**
Si un hospital no puede acceder al sistema donde están los registros de pacientes, se rompe la disponibilidad.

**Ejemplos comunes de incidentes que afectan disponibilidad:**

- Ataques DDoS
- Fallas de infraestructura
- Ataques ransomware
- Fallas de sistemas críticos

**Ejemplo en hospitales:**
En hospitales la disponibilidad es **crítica**.

Si un médico no puede acceder al historial de un paciente porque el sistema está caído, puede afectar directamente la atención médica.

### Resumen de la Triada CIA

| Principio | Significado | Ejemplo |
|-----------|------------|---------|
| **Confidencialidad** | Solo personas autorizadas acceden a la información | Proteger contraseñas |
| **Integridad** | Información correcta y sin modificaciones no autorizadas | No alterar registros |
| **Disponibilidad** | Información accesible cuando se necesita | Sistemas en línea 24/7 |

### Algo muy importante para estudiantes

> "Muchos incidentes de seguridad afectan más de uno de estos pilares al mismo tiempo."

Por ejemplo:

- Un **ransomware** puede afectar:
  - Disponibilidad (porque los sistemas quedan cifrados)
  - Integridad (porque los datos se modifican)

- Una **filtración de datos** afecta principalmente:
  - Confidencialidad

---

## Bloque 3 – Activos de Información

### Concepto de Activo

En seguridad de la información usamos el concepto de **activo**.

**Definición sencilla:**

> Un activo es cualquier recurso que tiene valor para una organización y que debe ser protegido.

**Algo muy importante:**

> "En seguridad no protegemos todo por igual. Protegemos especialmente aquello que tiene valor."

### Ejemplos de activos

- Bases de datos
- Sistemas críticos
- Servidores
- Aplicaciones
- Propiedad intelectual
- Información de clientes
- Infraestructura tecnológica

### Importancia relativa de los activos

Un punto importante que deben entender los estudiantes es que **no todos los activos tienen el mismo valor**.

Algunos activos son más críticos que otros.

**Ejemplo en una empresa:**

- El **sistema de pagos** puede ser un activo **extremadamente crítico**
- El **sistema de impresión** puede ser menos crítico

Esto significa que los **controles de seguridad deben priorizar los activos más importantes**.

### Tipos de activos

Las organizaciones tienen muchos tipos de activos que van más allá de computadores.

#### 1. Información

La información suele ser el **activo más importante** de una organización.

Ejemplos:

- Bases de datos de clientes
- Registros financieros
- Propiedad intelectual
- Documentos estratégicos
- Datos personales

**Ejemplo práctico:**
Una empresa de comercio electrónico tiene una base de datos con:

- Millones de clientes
- Direcciones
- Historial de compras

Ese conjunto de datos es un **activo extremadamente valioso**.

#### 2. Sistemas

Los sistemas informáticos también son activos.

Ejemplos:

- Sistemas de pago
- Plataformas web
- Sistemas internos de gestión
- Sistemas de producción

**Ejemplo:**
El sistema de pagos de una empresa. Si ese sistema deja de funcionar, la empresa no puede operar.

#### 3. Infraestructura tecnológica

La infraestructura tecnológica incluye elementos como:

- Servidores
- Redes
- Centros de datos
- Infraestructura cloud

**Ejemplos:**

- Servidores en AWS
- Redes corporativas
- Infraestructura de virtualización

Todo esto también forma parte de los **activos de la organización**.

#### 4. Personas

Esto suele sorprender a los estudiantes, pero **las personas también son activos**.

Ejemplos:

- Empleados
- Administradores de sistemas
- Desarrolladores
- Ejecutivos

Las personas tienen acceso a:

- Información
- Sistemas
- Decisiones

Por eso **muchas campañas de ataque apuntan directamente a las personas**.

**Ejemplo:**
Ataques de phishing.

#### 5. Procesos

Las organizaciones también tienen **procesos críticos**.

Ejemplos:

- Proceso de pago a proveedores
- Proceso de atención a clientes
- Procesos de producción

Si estos procesos se interrumpen, la organización puede sufrir **pérdidas importantes**.

---

## Bloque 4 – Amenazas y Vulnerabilidades

Aquí introducimos dos conceptos que muchas veces se confunden.

### Amenaza

**Definición:**

> Una amenaza es cualquier evento o actor que puede causar daño a un activo.

Las amenazas pueden ser:

- Atacantes externos
- Empleados maliciosos
- Errores humanos
- Desastres naturales
- Fallas tecnológicas

#### Tipos de amenazas

**Amenaza humana maliciosa:**

- Hackers
- Grupos criminales
- Espionaje estatal

**Amenaza humana no intencional:**

- Errores de empleados
- Configuraciones incorrectas

**Amenaza tecnológica:**

- Fallas de software
- Fallas de hardware

**Amenaza física:**

- Incendios
- Terremotos
- Cortes de energía

### Vulnerabilidad

**Definición:**

> Una vulnerabilidad es una debilidad que puede ser explotada por una amenaza.

**Ejemplos de vulnerabilidades:**

- Software sin actualizar
- Contraseñas débiles
- Mala configuración de sistemas
- Permisos incorrectos
- Falta de controles de seguridad

**Ejemplo simple para explicar:**

- **Activo:** Servidor web
- **Amenaza:** Atacante externo
- **Vulnerabilidad:** Software desactualizado

En este caso, el atacante podría explotar la vulnerabilidad para comprometer el servidor.

#### Ejemplos de vulnerabilidades comunes

**Software desactualizado:**
Un servidor que no ha sido actualizado puede tener vulnerabilidades conocidas.

**Contraseñas débiles:**
Si un sistema utiliza contraseñas simples, un atacante podría adivinarlas.

**Configuraciones incorrectas:**
Un servidor mal configurado puede exponer información sensible.

**Errores de programación:**
Un bug en una aplicación puede permitir ejecutar código malicioso.

---

## Bloque 5 – Riesgo en Seguridad

Aquí conectamos todos los conceptos anteriores.

### Definición de Riesgo

> Un riesgo aparece cuando una amenaza puede explotar una vulnerabilidad y afectar un activo.

**Fórmula conceptual sencilla:**

$$\text{Riesgo} = \text{Amenaza} + \text{Vulnerabilidad} + \text{Impacto}$$

**Ejemplo completo:**

- **Activo:** Sistema de pagos
- **Amenaza:** Atacante externo
- **Vulnerabilidad:** Software sin parches
- **Impacto:** Fraude o interrupción del servicio

En este caso existe un **riesgo significativo** para la organización.

### Ejemplo 1 – Servidor web vulnerable

**Escenario:**
Una empresa tiene un sitio web corporativo que está alojado en un servidor conectado a Internet.

Ese servidor utiliza una versión antigua de un software web que tiene vulnerabilidades conocidas.

**Análisis paso a paso:**

**Pregunta 1:** "¿Cuál sería el activo en este caso?"

- **Activo:** Servidor web o aplicación web

**Pregunta 2:** "¿Cuál sería la amenaza?"

- **Amenaza:** Atacante externo
- Podría ser:
  - Un hacker individual
  - Un grupo criminal
  - Un bot automatizado buscando vulnerabilidades

**Pregunta 3:** "¿Cuál es la vulnerabilidad?"

- **Vulnerabilidad:** Software desactualizado con fallas conocidas

> Algo importante: "Los atacantes no necesitan descubrir vulnerabilidades nuevas. Muchas veces explotan vulnerabilidades públicas que ya existen."

De hecho, **la mayoría de los ataques reales utilizan vulnerabilidades conocidas**.

**Pregunta 4:** "¿Cuál sería el impacto?"
Posibles respuestas:

- Acceso no autorizado al servidor
- Robo de información
- Modificación del sitio web
- Instalación de malware

### Ejemplo 2 – Robo de credenciales mediante phishing

**Escenario:**
Un empleado de una empresa recibe un correo electrónico que parece provenir del departamento de TI.

El correo le pide que ingrese sus credenciales en un enlace para "verificar su cuenta".

El empleado introduce su usuario y contraseña en una página falsa.

**Análisis:**

**Pregunta 1:** "¿Cuál sería el activo?"

- **Activo:** Cuenta del usuario o acceso al sistema corporativo
- También podrían ser activos:
  - Información interna
  - Sistemas corporativos

**Pregunta 2:** "¿Cuál es la amenaza?"

- **Amenaza:** Atacante que realiza phishing

> Nota: El phishing es uno de los **ataques más comunes en el mundo**. Muchos incidentes importantes comienzan con robo de credenciales.

**Pregunta 3:** "¿Cuál es la vulnerabilidad?"

- **Vulnerabilidad:** Falta de concientización del usuario o autenticación débil
- También podría ser:
  - Ausencia de autenticación multifactor

**Pregunta 4:** "¿Cuál sería el impacto?"
Posibles respuestas:

- Acceso a sistemas internos
- Robo de información
- Movimiento lateral dentro de la red
- Instalación de malware

### Ejemplo 3 – Ransomware

**Escenario:**
Una empresa tiene múltiples computadores conectados a su red interna.

Uno de los usuarios descarga un archivo malicioso desde un correo electrónico.

Ese archivo instala ransomware que comienza a cifrar archivos en los sistemas.

**Análisis:**

**Pregunta 1:** "¿Cuál sería el activo?"
Posibles respuestas:

- Datos de la empresa
- Servidores
- Sistemas corporativos

**Pregunta 2:** "¿Cuál sería la amenaza?"

- **Amenaza:** Grupo criminal que distribuye ransomware

> Nota: Muchos ataques de ransomware son realizados por **organizaciones criminales especializadas**.

**Pregunta 3:** "¿Cuál sería la vulnerabilidad?"
Posibles respuestas:

- Usuario abre archivo malicioso
- Software sin parches
- Falta de controles de seguridad

**Pregunta 4:** "¿Cuál sería el impacto?"
Respuestas posibles:

- Sistemas cifrados
- Interrupción del negocio
- Pérdida de datos
- Pago de rescate

---

## Bloque 6 – Gestión de Riesgos

### Idea clave de la práctica profesional

Una idea muy importante del mundo profesional:

> "En la práctica profesional de la ciberseguridad, el objetivo no es eliminar todos los riesgos."

Esto es **imposible**.

**Todas las organizaciones tienen riesgos.**

Lo que se hace realmente es:

- Identificar riesgos
- Evaluarlos
- Priorizarlos
- Reducirlos

Esto se llama: **Gestión de riesgos**

### Conexión con los roles profesionales en ciberseguridad

Los conceptos que vimos hoy se aplican en todos los roles de ciberseguridad.

**Red Team:**

- Busca vulnerabilidades antes que los atacantes
- Identifica amenazas potenciales

**Blue Team:**

- Detecta y responde a ataques
- Implementa controles para mitigar riesgos

**GRC (Governance, Risk and Compliance):**

- Analiza y gestiona los riesgos de seguridad
- Prioriza activos
- Define políticas de protección

**CTI (Cyber Threat Intelligence):**

- Estudia a los adversarios y sus tácticas
- Identifica amenazas específicas

> "Todas estas áreas utilizan los conceptos que vimos hoy."

### Reflexión final

> "Antes de implementar herramientas o tecnologías, lo primero es entender qué estamos protegiendo y contra qué riesgos."

En ciberseguridad, el análisis estructurado de:

- Activos
- Amenazas
- Vulnerabilidades
- Riesgos

Es fundamental para tomar decisiones correctas sobre seguridad.
