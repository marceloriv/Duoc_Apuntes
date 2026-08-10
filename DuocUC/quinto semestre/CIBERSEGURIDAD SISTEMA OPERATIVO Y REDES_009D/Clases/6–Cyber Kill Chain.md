# Clase 6 - Cyber Kill Chain

>[!NOTE]
>
> Esta clase conecta el ataque completo de principio a fin, con enfoque realista para Red Team, Blue Team y CTI.

**Objetivo de la clase:**

Que los estudiantes:

- Entiendan el flujo completo de un ataque real
- Dejen de pensar en "hacks aislados"
- Comprendan cómo se conectan todas las fases
- Preparen su mentalidad para Red Team, Blue Team y CTI

---

## Bloque 1 - Introduccion: el ataque como proceso

### Mensaje clave

> "Un ataque no es un evento, es un proceso."

### Apertura

"Un ataque real no es instantaneo."

"No es: clic -> hackeado."

"Un ataque es una secuencia de pasos, donde cada paso prepara el siguiente."

### Ejemplo simple

"Imaginen que alguien quiere robar en una casa."

Preguntas para la clase:

- Entra directamente?
- O primero observa?

Desglose:

1. Observa la casa
2. Identifica entradas
3. Busca horarios
4. Elige momento
5. Entra
6. Roba

"Eso es exactamente lo mismo que hace un atacante."

### Error comun

"Muchos piensan que el hacking es:"

- Ejecutar herramientas
- Encontrar vulnerabilidad
- Listo

Correccion:

- Un ataque tiene multiples fases
- Si una fase falla, el ataque se puede detener

### Conexión con lo aprendido

"Todo lo que vimos antes ahora se conecta:"

- Activos: lo que quieren atacar
- Vulnerabilidades: lo que explotan
- Controles: lo que los detiene
- Hardening: reduce oportunidades

"Para entender este proceso necesitamos un modelo."

---

## Bloque 2 - Que es la Cyber Kill Chain

"La Kill Chain describe las fases de un ataque real, desde no tener acceso hasta lograr el objetivo final."

"No es solo teoria: esta basada en ataques observados en la vida real."

### Fases del modelo

1. **Reconnaissance** - El atacante investiga
2. **Weaponization** - Prepara el ataque
3. **Delivery** - Entrega el ataque
4. **Exploitation** - Aprovecha una debilidad
5. **Installation** - Se instala en el sistema
6. **Command and Control (C2)** - Toma control remoto
7. **Actions on Objectives** - Cumple su objetivo

> "No necesitan memorizar los nombres todavia. Lo importante es entender el flujo."

### Mensaje clave

> "Si entiendes este modelo, entiendes como atacan en la vida real."

---

## Bloque 3 - Explicacion profunda de cada fase

### 1) Reconnaissance

**Definicion:** El atacante investiga el objetivo antes de atacar.

Que hace:

- Busca informacion publica
- Identifica sistemas y personas
- Entiende como funciona la organizacion

Ejemplos:

- Dominios
- Correos electronicos
- Tecnologias usadas
- Redes sociales

Insight:

> "Un buen ataque comienza con buena informacion."

### 2) Weaponization

**Definicion:** El atacante prepara el ataque para ese objetivo.

Que hace:

- Crea o adapta malware
- Prepara archivos maliciosos
- Diseña payloads segun el contexto

Ejemplos:

- PDF malicioso
- Documento con macro
- Payload especifico

Insight:

> "Mientras mas personalizado el ataque, mas efectivo."

### 3) Delivery

**Definicion:** El atacante entrega el vector de ataque.

Formas comunes:

- Phishing
- Enlaces
- Archivos
- Sitios web comprometidos

Pregunta para la clase:

- Que pasa si el usuario no hace clic?

Respuesta esperada:

- El ataque falla en esta fase

Insight:

> "Si no llega el ataque, no hay ataque."

### 4) Exploitation

**Definicion:** Se aprovecha una debilidad para ejecutar codigo o ganar acceso.

Puede ser:

- Vulnerabilidad tecnica
- Credenciales robadas
- Error humano

Insight:

> "No siempre es un exploit tecnico; muchas veces es un error humano."

### 5) Installation

**Definicion:** El atacante instala mecanismos para mantenerse dentro.

Busca:

- Persistencia
- Acceso estable

Ejemplos:

- Backdoor
- Malware residente
- Tareas programadas maliciosas

Insight:

> "Entrar no es suficiente: el atacante quiere quedarse."

### 6) Command and Control (C2)

**Definicion:** El sistema comprometido se comunica con la infraestructura del atacante.

Que ocurre:

- Recepcion de comandos
- Envio de informacion robada
- Coordinacion remota

Insight:

> "Sin C2, el atacante pierde control."

### 7) Actions on Objectives

**Definicion:** El atacante ejecuta su objetivo final.

Ejemplos:

- Robo de datos
- Ransomware
- Espionaje
- Fraude

Insight:

> "Todo lo anterior fue preparacion; aqui se materializa el impacto."

### Mensaje clave del bloque

> "El exploit es solo una parte pequena del ataque completo."

Secuencia completa simplificada:

1. Investiga empresa
2. Prepara ataque
3. Envia phishing
4. Usuario cae
5. Se instala malware
6. Controla sistema
7. Roba datos

---

## Bloque 4 - Caso real: ataque a Target (2013)

### Contexto

"En 2013, Target sufrio un ciberataque masivo."

Impacto reportado:

- Mas de 40 millones de tarjetas comprometidas
- Datos de mas de 70 millones de clientes
- Perdidas millonarias
- Gran dano reputacional

Objetivo del atacante:

- Robar datos de tarjetas de credito

### Mapeo del caso a la Kill Chain

1. **Reconnaissance**

- Investigaron proveedores, accesos externos y relaciones de confianza
- Insight: atacaron el eslabon mas debil, no el objetivo principal de forma directa

1. **Weaponization**

- Prepararon malware especializado para captura de datos de tarjetas

1. **Delivery**

- Entrada por proveedor externo (climatizacion)
- Phishing y robo de credenciales

1. **Exploitation**

- Usaron credenciales validas del proveedor
- No fue necesario un bug sofisticado

1. **Installation**

- Malware desplegado en sistemas POS
- Objetivo: capturar datos en tiempo real

1. **Command and Control (C2)**

- Exfiltracion hacia servidores externos
- Control remoto del malware

1. **Actions on Objectives**

- Robo masivo y sostenido de datos

### Reflexion para la clase

Pregunta:

- Cual fue la vulnerabilidad principal?

Respuestas esperadas:

- Acceso de terceros
- Falta de segmentacion
- Falta de monitoreo

Mensaje:

> "Los ataques mas peligrosos no siempre son directos; muchas veces son indirectos."

---

## Bloque 5 - Conexion con todo el curso

### Relacion con roles

- **Red Team:** ejecuta/simula fases de la Kill Chain para descubrir brechas
- **Blue Team:** detecta y responde durante distintas fases
- **CTI (Cyber Threat Intelligence):** estudia atacantes, tacticas y patrones

Mensaje clave:

> "Gran parte de la ciberseguridad operativa gira en torno a entender y romper esta cadena."

---

## Bloque 6 - Como detener la Kill Chain

"La mayoria piensa que hay que detener todo el ataque."

"No es necesario."

Principio central:

> El atacante necesita completar todas las fases. El defensor solo necesita bloquear una.

### Defensas por fase

1. **Reconnaissance**

- Reducir informacion publica
- Limitar exposicion de datos sensibles

1. **Weaponization**

- Fase con bajo control directo (ocurre fuera de tu entorno)

1. **Delivery**

- Filtros de correo
- Bloqueo de adjuntos peligrosos
- Concientizacion de usuarios

1. **Exploitation**

- Parches
- Configuraciones seguras
- MFA

1. **Installation**

- Antivirus/EDR
- Control de ejecucion de binarios/scripts

1. **Command and Control (C2)**

- Monitoreo de red
- Bloqueo de trafico sospechoso y dominios maliciosos

1. **Actions on Objectives**

- Segmentacion de red
- Control de acceso
- Monitoreo continuo

### Mini ejemplo de ruptura de cadena

Ataque de phishing:

- Recon: ok
- Delivery: llega correo
- Exploitation: usuario hace clic
- **Pero MFA bloquea el acceso**

Resultado:

- La cadena se rompe y el ataque no logra su objetivo

---

## Bloque 7 - Actividad en clase

### Actividad sugerida (15-20 min)

1. Dividir curso en grupos
2. Entregar un mini caso de ataque
3. Pedir que cada grupo:

- Identifique las 7 fases
- Proponga al menos 1 control defensivo por fase
- Defina en que fase el ataque pudo ser detenido antes

### Cierre de actividad

Pregunta final:

- En que fase es mas barato detener un ataque?

Respuesta esperada:

- Mientras mas temprano, menor costo e impacto

---

## Cierre de la clase

Mensaje final:

> "Mientras mas tarde detectas un ataque, mas caro y mas grave se vuelve."

Al terminar esta clase, los estudiantes:

- Entienden ataques completos, no eventos aislados
- Pueden analizar incidentes usando un modelo estructurado
- Quedan mejor preparados para mentalidad Red Team, Blue Team y CTI
