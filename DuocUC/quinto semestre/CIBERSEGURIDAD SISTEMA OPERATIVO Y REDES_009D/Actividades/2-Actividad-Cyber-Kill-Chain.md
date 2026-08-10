# Actividad - Analisis de Incidente (Cyber Kill Chain)

## Instrucciones

Trabajen individualmente o en parejas. Lean cada caso y completen cada seccion.
El objetivo es reconstruir el ataque utilizando el modelo Cyber Kill Chain y proponer medidas de defensa.

---

## Caso N.1 (Beginner Friendly)

### Contexto del caso

Una empresa detecta actividad sospechosa en su red.
Un empleado recibio un correo con un archivo adjunto.
Luego de abrirlo, se registro un login exitoso desde otro pais.
Posteriormente, se detecto la instalacion de software no autorizado.
Horas despues, se observo trafico hacia una IP externa y extraccion de datos.

### 1. Reconstruccion del ataque (Cyber Kill Chain)

**Reconnaissance:**
El atacante recopila informacion publica de la empresa y sus colaboradores (cargos, correos, funciones) para identificar una victima con acceso util.

**Weaponization:**
Prepara un archivo malicioso (por ejemplo, documento con macro o ejecutable disfrazado) orientado al perfil de la victima.

**Delivery:**
Envia un correo de phishing con el archivo adjunto para inducir al colaborador a abrirlo.

**Exploitation:**
Cuando el usuario abre el adjunto, se ejecuta el codigo malicioso y se compromete el equipo/cuenta.

**Installation:**
Se instala software no autorizado para persistencia y ejecucion continua en el endpoint.

**Command & Control:**
El equipo infectado establece comunicacion con infraestructura externa del atacante (por ejemplo, HTTP/DNS) para recibir instrucciones.

**Actions on Objectives:**
El atacante realiza exfiltracion de datos hacia una IP externa, cumpliendo su objetivo de robo de informacion.

### 2. Punto de quiebre del ataque

**Fases donde pudo haberse detenido:**

- Delivery: filtro antiphishing y bloqueo de adjuntos maliciosos.
- Exploitation: antivirus/EDR y bloqueo de macros o ejecucion no confiable.
- Installation: control de aplicaciones y privilegios minimos.
- Command & Control: bloqueo de conexiones salientes sospechosas y monitoreo DNS/HTTP.

El punto critico inicial fue la apertura del adjunto malicioso, pero existieron oportunidades posteriores para contener el incidente.

### 3. Controles recomendados

**Preventivos:**

- MFA para todos los accesos corporativos.
- Filtro de correo antiphishing y sandbox de adjuntos.
- Politicas de seguridad y minimo privilegio.
- Actualizacion y parchado continuo de sistemas.
- Segmentacion de red y restriccion de salida a internet.

**Detectivos:**

- SIEM con correlacion de eventos de login anomalo.
- EDR/antivirus con alertas de ejecucion sospechosa.
- Monitoreo de trafico saliente y deteccion de exfiltracion.
- Honeypots o cuentas canario para deteccion temprana.

**Correctivos:**

- Plan de respuesta a incidentes con runbooks.
- Aislamiento de equipos comprometidos.
- Reseteo de credenciales y revocacion de sesiones.
- Backups diarios y pruebas de restauracion.
- Analisis forense y lecciones aprendidas.

### 4. Conclusion

El ataque siguio una cadena tipica: phishing, ejecucion del adjunto, persistencia y exfiltracion.
La principal debilidad fue la combinacion de error humano con controles de deteccion y respuesta insuficientes para reaccionar a tiempo.

---

## Caso N.2 (Real World Scenario)

### Contexto organizacional

La empresa FinSecure S.A. es una organizacion del sector financiero en Latinoamerica que ofrece:

- Servicios de pagos digitales
- Gestion de cuentas empresariales
- APIs para integracion con terceros

Cuenta con:

- Infraestructura hibrida (on-premise + cloud)
- Active Directory para gestion de identidades
- Acceso remoto via VPN
- Multiples proveedores externos

### Estructura relevante

- Empleados internos (~800)
- Proveedores externos con acceso limitado
- Equipo de TI centralizado
- SOC basico (monitoreo parcial)

### Contexto tecnico

- Autenticacion con usuario/contrasena (MFA solo en algunos sistemas)
- Logs centralizados parcialmente (no todo integrado al SIEM)
- Segmentacion de red limitada
- Acceso a sistemas criticos desde red interna

### Situacion detectada

**Dia 1:**

- Multiples intentos fallidos de login en cuentas corporativas desde IP extranjeras.

**Dia 2:**

- Login exitoso en cuenta de empleado del area financiera.
- Acceso fuera de horario laboral.
- No se genera alerta critica.

**Dia 3:**

- Creacion de un nuevo usuario en sistema interno con privilegios elevados.
- Accion no registrada en procesos formales.

**Dia 4:**

- Ejecucion de scripts en servidores internos.
- Actividad inusual en bases de datos.
- Aumento de trafico interno entre servidores.

**Dia 5:**

- Trafico saliente periodico hacia IP desconocida.
- Volumen de datos superior al normal.
- Deteccion tardia por parte del equipo.

### Observaciones adicionales

- La cuenta comprometida no tenia MFA habilitado.
- El usuario afectado habia recibido correos sospechosos dias antes.
- No se aplicaron parches recientes en algunos servidores.
- El monitoreo SIEM no cubre todos los sistemas.
- Los accesos de proveedores no estan completamente restringidos.

### Impacto preliminar

- Posible acceso no autorizado a sistemas criticos.
- Posible exfiltracion de informacion financiera.
- Riesgo de compromiso de multiples cuentas.
- Exposicion de datos sensibles.

### 1. Reconstruccion del ataque (Cyber Kill Chain)

**Reconnaissance:**
El atacante recolecta informacion de empleados, sistemas expuestos y patrones de acceso de la organizacion.

**Weaponization:**
Prepara una campana de phishing dirigida y posibles scripts/herramientas para post-explotacion y elevacion de privilegios.

**Delivery:**
Envia correos sospechosos al personal (incluyendo area financiera), buscando robo de credenciales o ejecucion de contenido malicioso.

**Exploitation:**
Tras varios intentos fallidos (Dia 1), logra un login valido en una cuenta sin MFA (Dia 2), posiblemente por credenciales robadas.

**Installation:**
Establece persistencia mediante creacion de usuario interno con privilegios elevados (Dia 3) y prepara ejecucion de scripts en servidores (Dia 4).

**Command & Control:**
Mantiene comunicaciones periodicas con IP externa desconocida (Dia 5), usando ese canal para control remoto y coordinacion del ataque.

**Actions on Objectives:**
Realiza movimiento lateral, acceso a bases de datos y exfiltracion de informacion financiera sensible (Dias 4-5).

### 2. Punto de quiebre del ataque

**Fases donde pudo haberse detenido:**

- Reconnaissance/Delivery: capacitacion anti-phishing y protecciones de correo.
- Exploitation: MFA obligatorio y politicas de acceso condicional.
- Installation: control estricto de creacion de cuentas privilegiadas.
- Lateral movement: segmentacion de red y control de privilegios.
- Command & Control: deteccion de beaconing y bloqueo de IP/dominio malicioso.

**Momento mas claro de quiebre:**
El Dia 2, cuando se detecto el login fuera de horario desde contexto anomalo sin generar alerta critica ni respuesta inmediata.

### 3. Controles recomendados

**Preventivos:**

- MFA obligatorio en todos los sistemas criticos y accesos remotos.
- Acceso condicional por riesgo (horario, geolocalizacion, reputacion IP, dispositivo).
- Segmentacion de red y modelo Zero Trust.
- Gestion de parches priorizada por criticidad.
- Control de accesos de terceros con minimo privilegio y ventanas acotadas.

**Detectivos:**

- SIEM con cobertura total de logs (AD, VPN, endpoints, servidores, bases de datos, cloud).
- Casos de uso para detectar: login anomalo, creacion de cuentas privilegiadas, ejecucion de scripts, exfiltracion.
- EDR en endpoints y servidores criticos.
- UEBA para detectar comportamiento anomalo de usuarios.
- Alertamiento con severidad y SLA de atencion.

**Correctivos:**

- Plan formal de respuesta a incidentes probado con simulacros.
- Contencion inmediata de cuentas comprometidas y aislamiento de equipos.
- Rotacion de credenciales y revisiones de privilegios.
- Restauracion segura desde backups verificados.
- Post-mortem tecnico y plan de remediacion con responsables y fechas.

### 4. Conclusion

El incidente muestra un ataque progresivo: intento de acceso, compromiso de cuenta sin MFA, escalamiento de privilegios, movimiento lateral y exfiltracion.
La principal debilidad de la organizacion fue la baja madurez operativa en monitoreo y respuesta, junto con brechas de controles basicos (MFA no universal, SIEM parcial, segmentacion limitada y parchado incompleto).

---

## Cierre general

En ambos casos, el modelo Cyber Kill Chain permite entender en que etapa fallo la defensa y donde instalar controles de quiebre.
La leccion clave es que la seguridad efectiva depende de capas coordinadas: prevencion, deteccion temprana y respuesta rapida.
