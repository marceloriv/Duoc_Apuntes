# 1-Introducción a la Ciberseguridad

## 1. Inicio de la clase

La ciberseguridad hoy es uno de los campos más críticos y con mayor crecimiento en tecnología.

Todas las organizaciones del mundo hoy dependen de sistemas digitales:

- Bancos
- Hospitales
- Gobiernos
- Universidades
- Empresas de retail
- Fintech
- Startups

Y cada uno de esos sistemas puede ser atacado.

Durante este semestre vamos a estudiar algo muy particular:

- Cómo funcionan los sistemas desde el punto de vista de la seguridad
- Cómo se protegen
- Cómo se atacan
- Cómo se defienden

## 2. Objetivo del curso

El objetivo del curso **no es que memoricen conceptos**.

El objetivo es que **aprendan a pensar en seguridad**.

Que entiendan:

- Cómo funcionan los sistemas
- Dónde están los riesgos
- Cómo piensa un atacante
- Cómo se defiende una organización

## 3. Qué aprenderán durante el semestre

Durante el curso verán varias áreas:

### Fundamentos de ciberseguridad

- Activos
- Amenazas
- Vulnerabilidades
- Riesgos

### Red Team

- Cómo atacan los adversarios
- Ethical hacking
- Vulnerabilidades

### Blue Team

- Detección de ataques
- Monitoreo
- Respuesta a incidentes

### Cyber Threat Intelligence

- Entender quién ataca
- Por qué atacan
- Cómo operan

## 4. Evaluaciones

- Evaluación teórica de fundamentos
- Práctica de Red Team
- Evaluación de Blue Team y CTI
- Examen final integrador

## 5. Qué es realmente la ciberseguridad

> "La ciberseguridad es la disciplina que busca proteger sistemas, redes, datos y servicios digitales contra ataques o accesos no autorizados."

Pero la realidad es más amplia. La ciberseguridad protege:

- Información
- Servicios
- Operaciones de negocio

### Ejemplo simple: Un banco

Si un atacante logra:

- Robar datos
- Modificar transferencias
- Detener el sistema de pagos

El impacto puede ser enorme.

¿Y qué pasa si ataca un hospital?

### Mensaje clave

> La ciberseguridad no protege computadores. Protege negocios, organizaciones y personas.

## 6. Panorama actual de amenazas

### Tipos de ataques actuales

Los más comunes hoy:

- Ransomware
- Phishing
- Robo de credenciales
- Explotación de vulnerabilidades
- Ataques a la cadena de suministro
- Infostealers

## 7. Caso Real: Colonial Pipeline (2021)

### Contexto

Colonial Pipeline es una empresa que opera uno de los oleoductos más grandes de Estados Unidos.

Ese oleoducto transporta combustible —principalmente gasolina y diésel— desde Texas hasta la costa este del país.

Para dimensionarlo:

- Tiene más de 8.800 kilómetros de extensión
- Transporta aproximadamente 45% del combustible consumido en la costa este de Estados Unidos

Es decir, si ese sistema deja de funcionar, millones de personas se quedan sin combustible.

### El ataque

En mayo de 2021, la empresa sufrió un ataque de **ransomware**.

El ransomware es un tipo de malware que:

- Cifra archivos
- Bloquea sistemas
- Exige un pago para recuperar el acceso

El grupo responsable fue **DarkSide**, una organización criminal especializada en ransomware.

### Cómo comenzó el ataque

Según investigaciones posteriores, el ataque comenzó por algo aparentemente simple:

Los atacantes obtuvieron **credenciales válidas de acceso remoto** a la red de la empresa.

Esas credenciales probablemente provenían de:

- Filtraciones previas
- Contraseñas reutilizadas
- Accesos VPN antiguos

Con esas credenciales lograron entrar a la red corporativa.

### Movimiento dentro de la red

Una vez dentro de la red, los atacantes:

- Exploraron sistemas internos
- Identificaron servidores críticos
- Extrajeron información

Este paso se llama **movimiento lateral**.

En muchos ataques modernos los atacantes no solo cifran sistemas, también roban información antes de hacerlo. Esto se conoce como **doble extorsión**.

### El ransomware

Cuando los atacantes tuvieron acceso suficiente, desplegaron el ransomware.

Este malware comenzó a cifrar sistemas corporativos, incluyendo:

- Servidores
- Sistemas de gestión
- Infraestructura administrativa

Aunque el ataque no afectó directamente el sistema industrial del oleoducto, la empresa tomó una decisión crítica.

### La decisión de apagar el sistema

Para evitar que el ataque se propagara hacia sistemas operacionales, la empresa decidió **detener completamente el oleoducto**.

Esto significa que un ataque informático contra sistemas corporativos terminó afectando infraestructura física real.

### Consecuencias inmediatas

El impacto fue enorme.

Durante varios días:

- Estaciones de servicio en varios estados se quedaron sin combustible
- Se generaron filas masivas en gasolineras
- Los precios del combustible aumentaron

Algunas estimaciones indican que:

- Millones de personas se vieron afectadas
- Se produjo una interrupción importante en la cadena de suministro

### Pago del rescate

La empresa finalmente decidió pagar el rescate: aproximadamente **4,4 millones de dólares en Bitcoin** a los atacantes.

Posteriormente el FBI logró recuperar una parte del dinero, pero el daño ya estaba hecho.

### Impacto económico y político

El incidente fue tan grave que el gobierno de Estados Unidos:

- Declaró estado de emergencia energética en varios estados
- Inició investigaciones federales
- Emitió nuevas regulaciones de ciberseguridad para infraestructura crítica

### Lecciones de seguridad

1. Un ataque puede comenzar con algo pequeño: El punto de entrada fue una cuenta comprometida. No fue una vulnerabilidad compleja.

2. Los sistemas corporativos también son críticos: Aunque el ransomware no atacó directamente los sistemas industriales, el impacto fue igual de grave.

3. El impacto de un ciberataque puede ser físico: No solo afecta datos. Puede afectar:
   - Transporte
   - Energía
   - Hospitales
   - Economía

### Conclusión del caso

> Este caso demuestra algo muy importante: la ciberseguridad no se trata solo de proteger computadores. Se trata de proteger infraestructura, servicios y la vida cotidiana de las personas.

## 8. Caso Real: Equifax (2017)

### Introducción

Equifax es una empresa estadounidense que se dedica a algo muy sensible: recolectar y analizar información financiera de personas.

Su negocio principal es generar informes de crédito, que utilizan bancos y empresas para decidir cosas como:

- Si te dan un crédito
- Si te aprueban una tarjeta
- Si puedes obtener un préstamo

Es decir, Equifax maneja información extremadamente sensible de millones de personas.

### El problema

En 2017 se descubrió que atacantes habían logrado acceder a los sistemas de la empresa y robar datos personales de aproximadamente **147 millones de personas**.

Para dimensionarlo, eso corresponde a casi la mitad de la población adulta de Estados Unidos.

### Qué información fue robada

Los atacantes obtuvieron datos altamente sensibles, como:

- Nombres completos
- Números de seguridad social
- Fechas de nacimiento
- Direcciones
- Algunos números de licencia de conducir
- Información financiera

Este tipo de información es extremadamente valiosa para:

- Robo de identidad
- Fraudes financieros
- Creación de cuentas falsas
- Ataques dirigidos

### Cómo ocurrió el ataque

El ataque comenzó debido a una **vulnerabilidad en Apache Struts**.

Apache Struts es un framework utilizado para desarrollar aplicaciones web empresariales.

En ese momento se había publicado una vulnerabilidad crítica identificada como: **CVE-2017-5638**

Esta vulnerabilidad permitía a un atacante:

- Ejecutar comandos en el servidor
- Acceder a archivos
- Moverse dentro del sistema

### El problema clave: falta de actualización

El problema **no fue que existiera la vulnerabilidad**. El problema fue que **Equifax no aplicó el parche de seguridad a tiempo**.

El parche ya había sido publicado por los desarrolladores del software, pero el sistema vulnerable seguía expuesto en producción.

Esto significa que el atacante pudo aprovechar una falla que ya era conocida públicamente.

### Qué hicieron los atacantes

Una vez dentro del sistema, los atacantes:

- Accedieron a servidores internos
- Exploraron bases de datos
- Extrajeron información durante semanas

Lo más preocupante es que el acceso se mantuvo por un período prolongado sin ser detectado.

Esto indica fallas en:

- Monitoreo
- Detección de actividad anómala
- Gestión de seguridad interna

### Cómo se descubrió el ataque

La brecha fue descubierta **meses después** de que comenzara la intrusión.

Para ese momento los atacantes ya habían extraído enormes cantidades de datos.

Este retraso en la detección es un problema muy común en incidentes de seguridad. Muchas organizaciones descubren los ataques meses después de que ocurrieron.

### Consecuencias para Equifax

#### Impacto económico

Equifax tuvo que pagar cientos de millones de dólares en:

- Multas regulatorias
- Compensaciones a usuarios
- Costos legales

En total, el impacto financiero superó los **700 millones de dólares**.

#### Demandas legales

Miles de personas demandaron a la empresa debido al robo de información personal.

Esto generó uno de los casos legales más grandes relacionados con seguridad de datos.

#### Impacto reputacional

La reputación de la empresa sufrió un daño enorme. Muchas personas perdieron la confianza en la capacidad de la empresa para proteger datos sensibles.

Incluso ejecutivos de la empresa enfrentaron investigaciones y renuncias.

### Lecciones de seguridad

1. La gestión de parches es crítica: Una vulnerabilidad conocida y parchada puede convertirse en un desastre si no se actualizan los sistemas.

2. No basta con tener seguridad en papel: Las organizaciones pueden tener políticas de seguridad, pero si no se aplican en la práctica, el riesgo sigue existiendo.

3. El monitoreo es clave: Los atacantes permanecieron dentro de los sistemas durante semanas sin ser detectados. Esto indica problemas en monitoreo, alertas y respuesta a incidentes.

4. Los datos personales son extremadamente sensibles: Cuando se comprometen datos como números de identificación, información financiera y direcciones, el impacto puede durar años para las víctimas.

### Conclusión del caso

> El caso de Equifax demuestra que un problema aparentemente técnico —como no aplicar un parche— puede terminar afectando a millones de personas.

> En ciberseguridad muchas veces los incidentes más graves no ocurren por ataques extremadamente sofisticados, sino por errores básicos que no se gestionaron correctamente.

## 9. Mensaje clave sobre ataques actuales

> Los ataques actuales no buscan solo hackear. Buscan dinero, acceso o poder.

## 10. Roles profesionales en ciberseguridad

No existe un solo tipo de trabajo en ciberseguridad. La industria se divide en distintos equipos que cumplen funciones muy diferentes:

- Algunos atacan sistemas para encontrar fallas
- Otros los defienden
- Otros analizan amenazas
- Otros gestionan riesgos y cumplimiento

Las cuatro áreas más comunes son:

- **Red Team** (seguridad ofensiva)
- **Blue Team** (defensa y monitoreo)
- **Cyber Threat Intelligence – CTI** (análisis de amenazas)
- **GRC** – Governance, Risk & Compliance (gobierno y riesgos)

### 1. Red Team (Seguridad ofensiva)

El Red Team es el equipo que **simula ataques reales contra una organización** para identificar debilidades antes de que lo hagan los atacantes.

Su objetivo es pensar y actuar como un adversario para probar la seguridad de los sistemas.

> El Red Team básicamente intenta comprometer los sistemas de una empresa, pero de manera controlada y autorizada.

Esto puede incluir:

- Aplicaciones web
- Redes corporativas
- Infraestructura cloud
- Sistemas de autenticación
- Ingeniería social

Las actividades típicas incluyen penetration testing, explotación de vulnerabilidades y simulaciones de adversarios.

#### Puestos comunes en Red Team

**Pentester / Penetration Tester**

- Analiza sistemas para encontrar vulnerabilidades
- Intenta explotarlas de forma controlada
- Demuestra el impacto de un ataque
- Genera informes con evidencias y mitigaciones

*Ejemplo*: Analizar un sitio web de un banco, encontrar una vulnerabilidad de autenticación y demostrar cómo un atacante podría acceder a cuentas de usuarios.

**Red Team Operator**

- Simula ataques complejos y persistentes
- Replica tácticas de grupos APT
- Evasión de controles de seguridad
- Prueba si los equipos defensivos pueden detectar el ataque

Este tipo de ejercicios se llaman **adversary emulation**.

**Security Consultant / Offensive Security Consultant**

- Lidera evaluaciones de seguridad
- Define el alcance de pruebas ofensivas
- Explica riesgos a clientes
- Propone mejoras de arquitectura

### 2. Blue Team (Defensa de sistemas)

El Blue Team es el equipo encargado de **proteger la infraestructura de una organización**.

> Si el Red Team intenta entrar al sistema, el Blue Team es el equipo que intenta detectarlo y detenerlo.

Su trabajo incluye:

- Monitorear sistemas
- Detectar ataques
- Responder incidentes
- Mejorar controles de seguridad

Los Blue Teams suelen operar en entornos como **SOC (Security Operations Center)** donde se analizan alertas y eventos de seguridad.

#### Puestos comunes en Blue Team

**SOC Analyst (Security Operations Center Analyst)**

Uno de los roles más comunes de entrada.

Qué hace:

- Monitorea alertas de seguridad
- Analiza logs
- Investiga comportamientos sospechosos
- Determina si se trata de un ataque o un falso positivo

*Ejemplo*: Si el sistema detecta múltiples intentos de login desde distintos países, el SOC analyst investiga si es un ataque.

**Incident Responder**

Especialista en manejar incidentes de seguridad.

Qué hace:

- Investiga ataques en curso
- Contiene al atacante
- Elimina malware
- Recupera sistemas comprometidos

*Ejemplo*: Si una empresa sufre ransomware, el incident responder coordina la contención del incidente.

**Security Engineer**

Rol más enfocado en implementar controles de seguridad.

Qué hace:

- Configurar firewalls
- Implementar EDR o SIEM
- Diseñar arquitectura segura
- Aplicar hardening en sistemas

**Threat Hunter**

Rol más avanzado dentro del Blue Team.

Qué hace:

- Busca amenazas que no han sido detectadas automáticamente
- Analiza patrones de comportamiento
- Investiga actividad sospechosa en sistemas

### 3. Cyber Threat Intelligence (CTI)

CTI se enfoca en **entender a los atacantes y sus métodos**.

> Mientras el Red Team simula ataques y el Blue Team los detecta, CTI intenta entender quién está atacando y cómo lo hace.

Esto incluye analizar:

- Grupos de cibercriminales
- Campañas de ransomware
- Malware
- Infraestructura utilizada por atacantes

CTI analiza **tácticas, técnicas y procedimientos (TTPs)** para comprender el comportamiento de los adversarios.

#### Puestos comunes en CTI

**Threat Intelligence Analyst**

Rol principal del área.

Qué hace:

- Investiga amenazas emergentes
- Analiza campañas de ataque
- Estudia grupos APT
- Produce reportes de inteligencia

*Ejemplo*: Investigar cómo opera un grupo de ransomware que está atacando empresas del sector financiero.

**Threat Researcher**

Más enfocado en investigación profunda.

Qué hace:

- Estudiar malware
- Analizar infraestructura de atacantes
- Identificar patrones de ataque

**Malware Analyst**

Rol técnico especializado.

Qué hace:

- Analizar malware
- Entender cómo funciona
- Identificar indicadores de compromiso

### 4. GRC (Governance, Risk and Compliance)

GRC es el área que se encarga de **gestionar la seguridad desde el punto de vista organizacional y estratégico**.

> Muchas personas creen que la ciberseguridad es solo técnica, pero en realidad gran parte del trabajo consiste en gestionar riesgos y políticas de seguridad.

GRC se enfoca en:

- Políticas de seguridad
- Gestión de riesgos
- Cumplimiento regulatorio
- Auditorías

#### Puestos comunes en GRC

**Security Risk Analyst**

Qué hace:

- Identifica riesgos de seguridad
- Evalúa impacto en el negocio
- Propone controles de mitigación

**Compliance Analyst**

Qué hace:

- Verifica cumplimiento de normas como:
  - ISO 27001
  - NIST
  - PCI-DSS

**CISO (Chief Information Security Officer)**

Rol ejecutivo.

Qué hace:

- Liderar la estrategia de seguridad
- Definir políticas
- Comunicar riesgos a la dirección
- Gestionar el programa de seguridad de la empresa

## 11. Cómo funciona la industria

### Tipos de organizaciones que necesitan ciberseguridad

**Empresas de seguridad (Consultoras)**

Hacen:

- Pentesting
- Auditorías
- Respuesta a incidentes

**Equipos internos**

Grandes empresas tienen:

- SOC
- Red Team
- Equipos de cloud security

**Gobierno**

También existe seguridad en:

- Defensa
- Inteligencia
- Infraestructura crítica

## 12. Conclusión

> La ciberseguridad es un campo enorme. Durante este semestre vamos a explorar cómo funcionan los sistemas desde el punto de vista de la seguridad. Cómo se atacan. Cómo se defienden. Y cómo se analizan las amenazas.
