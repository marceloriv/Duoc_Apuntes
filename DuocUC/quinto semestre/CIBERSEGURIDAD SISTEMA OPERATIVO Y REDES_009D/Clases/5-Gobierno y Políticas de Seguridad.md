# Clase 5 – Gobierno y Políticas de Seguridad

> Esta clase es nivel **semi-profesional (GRC real)**, alineada con cómo operan empresas

**Objetivo de la clase:**

Que los estudiantes entiendan:

- Cómo se gestiona la seguridad a nivel organizacional
- Cómo se traducen los riesgos en reglas
- Cómo se implementa seguridad en la práctica
- Cómo trabajan las empresas (no solo hackers)

---

## Bloque 1 – Seguridad no es solo técnica

> "Hasta ahora hemos hablado de sistemas, ataques, vulnerabilidades… Pero les voy a hacer una pregunta importante."

> "¿Se puede tener buena seguridad solo con herramientas?"

**La respuesta es: No.**

> "Porque la seguridad en el mundo real no falla por falta de herramientas… falla por falta de organización."

### Ejemplo real

"Las empresas hoy tienen tecnología avanzada:

- Firewalls
- EDR
- SIEM
- Inteligencia artificial

Y aun así siguen siendo comprometidas."

¿Por qué?

Porque:

- Nadie revisa alertas
- No hay responsables
- No hay procedimientos

**Resultado:** El ataque pasa igual

### La seguridad se basa en 3 pilares

1. **Personas**
2. **Procesos**
3. **Tecnología**

#### Personas

Las personas son el **componente más débil… y más importante**.

Ejemplos:

- Usuarios que hacen clic en phishing
- Administradores que configuran mal sistemas
- Equipos que no siguen procedimientos

> "Puedes tener el mejor sistema del mundo… pero si una persona hace clic en un correo malicioso, todo falla."

#### Procesos

Los procesos son **cómo se hacen las cosas**.

Ejemplos:

- Cómo se responde a un incidente
- Cómo se gestionan accesos
- Cómo se aplican parches

> "Si no hay procesos, todo depende de improvisación. Y la improvisación en seguridad es igual a fallar."

#### Tecnología

La tecnología son **las herramientas**.

**Firewall:**

- Controla el tráfico de red
- Permite o bloquea conexiones según reglas
- Bloquea conexiones no autorizadas
- Segmenta redes

> "El firewall no ve lo que pasa dentro del sistema."

Ejemplos: Palo Alto Networks, Fortinet, Cisco (ASA / Firepower)

**Antivirus:**

- Detecta y elimina malware
- Analiza archivos
- Bloquea programas maliciosos

> "El antivirus muchas veces detecta solo lo conocido."

Ejemplos: Microsoft Defender, Kaspersky, Bitdefender

**SIEM (Security Information and Event Management):**

- Recopila y analiza logs de múltiples sistemas
- Centraliza logs
- Correlaciona eventos
- Genera alertas

Detecta:

- Login sospechoso
- Múltiples intentos fallidos
- Actividad anómala

Ejemplos: Splunk, IBM QRadar, Microsoft Sentinel

**EDR (Endpoint Detection and Response):**

- Monitorea lo que ocurre dentro de los equipos (endpoints)
- Detecta comportamiento malicioso
- Analiza procesos
- Permite respuesta rápida

Detecta:

- Ejecución de malware
- Movimientos laterales
- Escalación de privilegios

> **Diferencia clave:** Antivirus → detecta malware conocido | EDR → detecta comportamiento sospechoso

Ejemplos: CrowdStrike, SentinelOne, Microsoft Defender for Endpoint

**WAF (Web Application Firewall):**

- Protege aplicaciones web
- Filtra tráfico HTTP malicioso
- Analiza solicitudes HTTP
- Bloquea ataques comunes

Protege contra:

- SQL Injection
- XSS (Cross-Site Scripting)
- Ataques automatizados

Ejemplos: Cloudflare, Akamai, F5

> "La tecnología ayuda… pero no toma decisiones por sí sola."

### Ejemplo más profundo: El problema real

"Esto pasa mucho en empresas grandes."

**Escenario:**

- Detectan actividad sospechosa
- El equipo recibe alertas
- Pero nadie sabe quién debe responder
- Pasan horas
- El atacante sigue avanzando

> "La tecnología es solo una parte. Si las personas y procesos fallan, la seguridad falla igual."

### Mensaje clave

> "La seguridad no es un software. Es una capacidad organizacional."

---

## Bloque 2 – Gobierno de seguridad

### Introducción

> "Si una empresa quiere ser segura, necesita organizar la seguridad."

### Definición

> **Gobierno de seguridad es cómo una organización dirige y controla la ciberseguridad.**

### Qué incluye el gobierno de seguridad

#### Quién toma decisiones

> "En seguridad siempre hay decisiones difíciles."

Ejemplos de decisiones que se deben tomar:

- ¿Parchar ahora o después?
- ¿Detener un sistema crítico o mantenerlo funcionando?
- ¿Invertir en seguridad o en negocio?

> "Si no está claro quién decide, nadie decide… o todos deciden mal."

#### Quién es responsable

"Debe haber claridad sobre responsabilidades."

Ejemplo:

- Si ocurre un incidente, ¿quién lo investiga?
- ¿Quién responde a alertas?
- ¿Quién tiene autoridad para tomar decisiones críticas?

#### Qué se prioriza

"En una organización con muchos riesgos, ¿cuál se atiende primero?"

Requiere:

- Evaluación de riesgos
- Priorización clara
- Recursos asignados

#### Cómo se gestionan riesgos

"El gobierno define el proceso de gestión de riesgos formalmente."

Incluye:

- Identificación
- Evaluación
- Mitigación
- Seguimiento

### Estructura típica de gobierno

```
┌─────────────────────────────────────┐
│          Gerencia / Negocio         │
│   Define riesgo aceptable           │
│   Aprueba inversión                 │
└──────────────┬──────────────────────┘
               │
     ┌─────────┴──────────┐
     │                    │
┌────▼──────────────┐ ┌──▼──────────────┐
│ CISO              │ │ Equipo de TI    │
│ Estrategia        │ │ Operación       │
│ Ejecución         │ │ Mantenimiento   │
│ Respuesta         │ │ Infraestructura │
└──────────────────┘ └─────────────────┘
     │
┌────▼──────────────────┐
│ Equipo de Seguridad   │
│ Monitoreo             │
│ Análisis              │
│ Respuesta a incidentes│
│ Implementación        │
└───────────────────────┘
```

#### CISO (Chief Information Security Officer)

**Responsabilidad:** Estrategia de seguridad

**Funciones:**

- Define prioridades
- Reporta a gerencia
- Toma decisiones de alto nivel
- Comunica riesgos

#### Equipo de seguridad

**Responsabilidad:** Ejecución

**Funciones:**

- Monitoreo 24/7
- Análisis de alertas
- Respuesta a incidentes
- Implementación de controles

#### TI (Tecnología)

**Responsabilidad:** Operación

**Funciones:**

- Mantiene servidores
- Gestiona redes
- Administra infraestructura
- Aplica parches

#### Gerencia / Negocio

**Responsabilidad:** Dirección estratégica

**Funciones:**

- Define nivel de riesgo aceptable
- Aprueba presupuesto
- Toma decisiones de negocio vs seguridad

### Ejemplo práctico: Incidente crítico

> "¿Qué pasa cuando ocurre un incidente crítico? ¿Quién decide qué hacer?"

**Sin gobierno:**

- Caos total
- Decisiones improvisadas
- Nadie sabe quién manda
- Respuesta lenta

**Con gobierno:**

- Roles claros
- Escalación definida
- Respuesta rápida
- Autoridades claras

### Problema común en empresas

> "Muchas empresas tienen tecnología… pero no tienen gobierno."

**Resultado:**

- Nadie se hace responsable
- No hay prioridades
- Todo es reactivo
- Crisis constantemente

### Mensaje clave

> "Sin gobierno, la seguridad no escala."

---

## Bloque 3 – Políticas de seguridad

### Introducción

> "Ya vimos que una organización necesita gobierno de seguridad… pero ahora aparece una pregunta clave."

> "¿Cómo se traduce ese gobierno en acciones concretas?"

### Concepto: Las reglas son necesarias

"Una organización necesita reglas claras para funcionar."

**Ejemplos fuera de ciberseguridad:**

- Reglas de tránsito
- Reglas en una empresa
- Reglas en una universidad

"En ciberseguridad, esas reglas se llaman **políticas**."

> "No es una recomendación. Es una obligación."

### Definición

> **Una política de seguridad es una regla formal que define cómo se debe actuar.**

### Ejemplos de políticas comunes

| Política | Define |
|----------|--------|
| **Contraseñas** | Longitud, complejidad, cambio, MFA |
| **Accesos** | Quién puede acceder a qué, roles, revisiones |
| **Uso aceptable** | Qué puede hacer un usuario en equipos corporativos |
| **Backups** | Frecuencia, almacenamiento, pruebas |
| **Actualizaciones** | Cuándo y cómo se aplican parches |
| **Respuesta a incidentes** | Cómo se reportan y se manejan |

### Ejemplos detallados de políticas

#### Política de contraseñas

**Define:**

- Longitud mínima (ej: 12 caracteres)
- Complejidad (mayúsculas, números, símbolos)
- Uso obligatorio de MFA
- Cambio periódico (ej: 90 días)
- No reutilización (no se pueden usar últimas 5 contraseñas)

**Ejemplo real:**
"Las contraseñas deben tener mínimo 12 caracteres, incluir mayúsculas, números y símbolos. MFA obligatorio. Cambio cada 90 días."

#### Política de accesos

**Define:**

- Quién puede acceder a qué sistemas
- Niveles de privilegio por rol
- Revisión anual de accesos
- Solicitud formal de acceso
- Revocación inmediata al cambio de rol

#### Política de uso aceptable

**Define:**

- Qué puede hacer un usuario en equipos corporativos
- Qué no puede hacer

**Ejemplos de lo que está prohibido:**

- No instalar software no autorizado
- No usar equipos corporativos para minería de criptomonedas
- No descargar contenido personal

#### Política de backups

**Define:**

- Frecuencia de respaldo (diaria, horaria)
- Dónde se almacenan (geografía, redundancia)
- Pruebas de recuperación (mensual, trimestral)
- Tiempo de recuperación objetivo (RTO)

### Lo más importante: Política vs Implementación

> "Las políticas no son técnicas."

**Pausa.**

> "Son reglas de negocio."

#### Diferencia clave

Las políticas:

- **NO son:** comandos, configuraciones, herramientas
- **SÍ son:** decisiones organizacionales, reglas de negocio, obligaciones

### Problema crítico: Políticas que no se cumplen

> "El mayor problema no es no tener políticas… es tenerlas y no aplicarlas."

#### Caso real típico

**Empresa tiene política:**

- Prohíbe compartir contraseñas
- Prohíbe dejar computadores desbloqueados

**Pero en la práctica:**

- Todos comparten cuentas
- Escritorios abiertos todo el día
- Nadie revisa

**Resultado:** Política inútil

#### Por qué fallan las políticas

1. No se comunican bien
2. No se supervisan
3. No hay consecuencias para quien las incumple
4. No hay controles técnicos que las respalden
5. Están desconectadas de la realidad

### Mensaje clave

> "Una política solo sirve si se implementa y se controla."

---

## Bloque 4 – Controles de seguridad

### Introducción

> "Las políticas dicen qué hacer. Los controles hacen que eso realmente ocurra."

### Definición

> **Un control es una medida para reducir un riesgo.**

### Tipos de controles: El triángulo

Existen tres tipos de controles basados en **cuándo actúan**:

1. **Preventivos** – Evitan el ataque
2. **Detectivos** – Detectan que ocurre un ataque
3. **Correctivos** – Responden después del ataque

### 1. Controles preventivos

**Definición:** Intentan **evitar que el ataque ocurra**

**Ejemplos:**

- Autenticación multifactor (MFA)
- Firewall
- Control de acceso
- Hardening de sistemas
- Validación de entrada
- Cifrado

**Explicación:**
"Intentan bloquear al atacante antes de que entre."

**Ejemplo práctico:**

- **Ataque:** Robo de credenciales
- **Control preventivo:** MFA
- **Resultado:** Aunque el atacante tenga la contraseña, no puede entrar sin el segundo factor

### 2. Controles detectivos

**Definición:** Permiten **detectar que algo está ocurriendo**

**Ejemplos:**

- Logs y auditoría
- SIEM
- Alertas
- Monitoreo continuo
- Análisis de comportamiento

**Explicación:**
"No evitan el ataque… pero permiten darte cuenta a tiempo."

**Ejemplo práctico:**

- **Ataque:** Un atacante entra al sistema
- **Control detectivo:** SIEM detecta:
  - Login desde otro país
  - Actividad anómala
  - Múltiples fallos
- **Resultado:** Se notifica al equipo en minutos, no en semanas

### 3. Controles correctivos

**Definición:** **Responden después de que el ataque ocurre**

**Ejemplos:**

- Backups y recuperación
- Parches de seguridad
- Respuesta a incidentes
- Aislamiento de sistemas comprometidos
- Notificación a usuarios

**Explicación:**
"Asumen que el ataque ya ocurrió… y buscan minimizar el impacto."

**Ejemplo práctico:**

- **Ataque:** Ransomware cifra datos
- **Control correctivo:** Restaurar desde backup reciente
- **Resultado:** Se pierde 1 día de datos, no todo

**Insight importante:**
> "No puedes evitar todos los ataques… pero puedes recuperarte rápido."

### Ejemplo completo: Defensa multicapa

**Riesgo:** Robo de cuenta

**Control Preventivo:**

- MFA obliga segundo factor

**Control Detectivo:**

- Alerta de login desde ubicación nueva

**Control Correctivo:**

- Reset de credenciales
- Auditoría de acciones realizadas

### Error común en empresas

> "Pensar que instalar una herramienta resuelve el problema."

Ejemplo:

- Compran un firewall → Seguridad "resuelta"
- Pero no auditan logs
- No tienen respuesta a incidentes
- No hacen hardening

**Resultado:** Falsa sensación de seguridad

### Insight importante

> "No existe seguridad con un solo control."

La seguridad real es **capas de controles**:

- Preventivos al frente
- Detectivos en el medio
- Correctivos de emergencia

### Mensaje clave

> "La seguridad real se construye con controles bien implementados."

---

## Bloque 5 – Hardening

### Introducción

> "Ahora vamos a algo muy práctico."

### Definición

> **Hardening es reducir la superficie de ataque de un sistema.**

### Principio simple

**Menos cosas expuestas = Menos riesgo**

### Ejemplo básico

**Servidor original:**

- SSH (puerto 22)
- FTP (puerto 21)
- Web (puerto 80)
- Base de datos (puerto 3306)

**Después de hardening:**

- SSH solo desde red interna
- FTP eliminado completamente
- Web actualizado a HTTPS
- Base de datos no expuesta a internet

**Resultado:** Superficie de ataque mucho menor

### Acciones de hardening comunes

1. **Eliminar servicios innecesarios**
   - FTP → SFTP
   - Telnet → SSH
   - HTTP → HTTPS

2. **Cerrar puertos**
   - Solo abrir los necesarios
   - Usar firewall para restringir

3. **Actualizar software**
   - Aplicar todos los parches
   - Usar versiones modernas

4. **Restringir accesos**
   - Cambiar puertos estándar
   - Usar IP whitelisting
   - Autenticación fuerte

5. **Aplicar configuraciones seguras**
   - Deshabilitar funciones peligrosas
   - Usar estándares de hardening
   - Probar regularmente

### Ejemplo real

Muchos ataques ocurren porque:

- **Servicios innecesarios están activos**
  - FTP abierto innecesariamente
  - Telnet expuesto
  - Puertos de administración visibles

- **Sistemas no están parchados**
  - Versiones antiguas conocidas
  - Vulnerabilidades públicas
  - Exploit known

### Mensaje clave

> "El mejor sistema es el que tiene menos cosas expuestas."

### Insight profesional

> "El hardening es una de las medidas más costo-efectivas en seguridad."

**¿Por qué?**

- No requiere herramientas costosas
- Se hace una sola vez
- Reduce significativamente el riesgo
- Mejora performance

### Error común en industria

> "Las empresas compran herramientas… pero no hacen hardening."

**Resultado:**

- Sistemas sobrecargados
- Superficie de ataque grande
- Falsos positivos en detectores
- Desempeño pobre

---

## Bloque 6 – Estándares (ISO / NIST)

### Introducción

> "Hasta ahora hemos visto muchas cosas: gobierno, políticas, controles, hardening…"

> "Pero ahora aparece una pregunta importante."

> "¿Las empresas inventan todo esto desde cero?"

**La respuesta es: No.**

> "Las empresas usan estándares. Porque la seguridad ya está estudiada, estructurada y probada."

---

### ISO 27001

#### Qué es

> **ISO 27001 es un estándar internacional de seguridad de la información.**

> "Es usado por empresas de todo el mundo."

#### Qué hace

"Define cómo gestionar la seguridad de la información de manera formal y estructurada."

#### Qué incluye

ISO 27001 cubre (conectado con lo visto):

- **Políticas** – Define cómo deben ser
- **Controles** – Establece controles mínimos necesarios
- **Gestión de riesgos** – Proceso formal de riesgos
- **Roles y responsabilidades** – Qué hace cada uno
- **Auditoría** – Cómo se verifica

#### Insight clave

> "ISO no te dice cómo hackear… te dice cómo organizar la seguridad."

#### Ejemplo práctico

Una empresa que sigue ISO 27001:

- Tiene **políticas definidas** y documentadas
- Tiene **controles implementados** y medidos
- **Gestiona riesgos** formalmente
- Tiene **roles claros** y responsables
- Se **audita regularmente**

#### Ventaja: Certificación

> "ISO también permite certificarse."

Esto significa:

- Auditorías externas independientes
- Validación formal de seguridad
- Confianza para clientes
- Cumplimiento regulatorio

#### Ejemplo real

> "Muchas empresas grandes exigen ISO 27001 a sus proveedores."

Pregunta: ¿Sin certificación, ¿Cómo confías?" → ISO lo valida

---

### NIST Framework

#### Qué es

> **NIST es otro framework muy importante, especialmente en Estados Unidos.**

Desarrollado por el National Institute of Standards and Technology (NIST).

#### Diferencia clave entre ISO y NIST

| Aspecto | ISO 27001 | NIST |
|---------|-----------|------|
| **Enfoque** | Formal y certificable | Práctico y operativo |
| **Uso** | Certificación, cumplimiento | Mejora continua |
| **Origen** | Internacional | USA (especialmente gobiernos) |
| **Flexibilidad** | Más rígido | Más flexible |

#### Los 5 pilares de NIST

NIST organiza la seguridad en 5 funciones:

**1. Identify (Identificar)**
> "Saber qué tienes."

Incluye:

- Identificar activos
- Mapear sistemas
- Entender riesgos
- Establecer línea base

**2. Protect (Proteger)**
> "Implementar controles."

Incluye:

- Control de acceso
- Protección de sistemas
- Implementación de políticas
- Hardening

**3. Detect (Detectar)**
> "Detectar ataques."

Incluye:

- Logs y monitoreo
- SIEM
- Análisis de vulnerabilidades
- Detección de anomalías

**4. Respond (Responder)**
> "Responder al incidente."

Incluye:

- Contención del ataque
- Análisis del incidente
- Acciones correctivas
- Comunicación

**5. Recover (Recuperar)**
> "Recuperarse después del ataque."

Incluye:

- Restaurar sistemas
- Volver a operar
- Análisis post-incidente
- Mejora

#### Ejemplo: Empresa madura siguiendo NIST

Una empresa madura:

1. **Identifica** todos sus activos y riesgos
2. **Protege** sistemas con controles implementados
3. **Detecta** ataques automáticamente
4. **Responde** en minutos, no horas
5. **Se recupera** rápidamente y mejora

**Resultado:** Resiliencia contra ataques

#### Importancia

- Ordena la seguridad de forma estructurada
- Permite auditorías objetivas
- Mejora madurez de seguridad
- Crea cultura de mejora continua

---

## Cierre Final

### Reflexión

> "Hoy dimos un paso importante."

> "Pasamos de ver ataques… a entender cómo se organiza la seguridad en una empresa."

### La diferencia clave

- **Los hackers** explotan vulnerabilidades
- **Las empresas que fallan,** fallan por no tener control

### Lo que vimos hoy

- **Gobierno:** Roles y decisiones claras
- **Políticas:** Reglas formales
- **Controles:** Medidas preventivas, detectivas, correctivas
- **Hardening:** Reducción de superficie de ataque
- **Estándares:** Marcos de referencia probados

### Resultado esperado después de esta clase

Los estudiantes ahora:

- Entienden **GRC (Governance, Risk, Compliance)**
- Entienden **cómo operan empresas reales**
- **Dejan de ver seguridad solo como hacking**
- Comprenden que seguridad es **organización, procesos y tecnología**

### Mensaje final

> "La seguridad moderna no se trata de tener las mejores herramientas."

> "Se trata de tener organizaciones bien estructuradas que manejen la seguridad como una capacidad estratégica."
