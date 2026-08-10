# Controles de Seguridad

## 1. Que es un control de seguridad

Un control de seguridad es una medida tecnica, administrativa o fisica que se usa para reducir riesgos, proteger activos y mejorar la capacidad de prevenir, detectar, responder y recuperar frente a incidentes.

En ciberseguridad, los controles no funcionan solos: se combinan para crear defensa en profundidad.

---

## 2. Clasificacion principal de los controles

### Preventivos

Evitan que ocurra un incidente o reducen la probabilidad de que suceda.

Ejemplos:

- MFA
- Firewall
- Politicas de contraseñas
- Control de acceso
- Hardening
- Segmentacion de red
- Cifrado
- Parches de seguridad

### Detectivos

Detectan eventos anormales, intentos de ataque o incidentes ya en curso.

Ejemplos:

- SIEM
- IDS
- EDR con deteccion
- Monitoreo de logs
- Alertas de seguridad
- Auditorias

### Correctivos

Ayudan a contener, recuperar o restaurar servicios despues de un incidente.

Ejemplos:

- Backups
- Plan de respuesta a incidentes
- Restauracion de sistemas
- Aislamiento de equipos comprometidos
- Reinstalacion o limpieza de malware

### Compensatorios

Se usan cuando no es posible aplicar el control ideal, pero se necesita reducir el riesgo.

Ejemplos:

- Aislar un servidor legacy
- Restringir acceso por VPN a un sistema antiguo
- Monitoreo reforzado sobre un sistema que no puede parchearse

---

## 3. Controles tecnicos mas comunes

| Control | Descripcion breve | Tipo principal |
|---|---|---|
| Antivirus | Detecta y bloquea malware conocido. | Preventivo / Detectivo |
| EDR | Monitorea endpoints y responde ante comportamiento sospechoso. | Detectivo / Correctivo |
| MFA | Exige mas de un factor para autenticar. | Preventivo |
| Firewall | Filtra trafico segun reglas. | Preventivo |
| IDS | Detecta patrones de intrusiones o trafico anomalo. | Detectivo |
| IPS | Detecta y bloquea trafico malicioso. | Preventivo / Detectivo |
| SIEM | Centraliza logs y genera alertas. | Detectivo |
| VPN | Crea un canal seguro para acceso remoto. | Preventivo |
| Cifrado | Protege datos en reposo o en transito. | Preventivo |
| Backups | Permiten recuperar informacion o servicios. | Correctivo |
| DLP | Evita fugas de informacion sensible. | Preventivo / Detectivo |
| NAC | Controla que equipos pueden conectarse a la red. | Preventivo |
| WAF | Protege aplicaciones web frente a ataques comunes. | Preventivo |
| Hardening | Reduce superficie de ataque mediante configuracion segura. | Preventivo |
| Patching | Corrige vulnerabilidades conocidas. | Preventivo |

---

## 4. Controles de acceso e identidad

### MFA

Agrega una segunda verificacion aparte de la contrasena. Puede ser:

- Algo que sabes: contrasena o PIN
- Algo que tienes: token, app autenticadora, llave fisica
- Algo que eres: biometria

Beneficio: reduce mucho el impacto del robo de contraseñas.

### Politicas de contraseñas

Definen longitud minima, complejidad, rotacion cuando aplique y bloqueo por intentos fallidos.

### RBAC

Control de acceso basado en roles. Cada usuario recibe solo los permisos necesarios para su funcion.

### PAM

Privileged Access Management. Protege cuentas administrativas y privilegios elevados.

### Revision periodica de accesos

Permite detectar permisos excesivos, cuentas inactivas y accesos que ya no corresponden al cargo.

---

## 5. Controles de red

### Firewall

Filtra el trafico entre redes o equipos segun reglas.

Usos comunes:

- Bloquear puertos innecesarios
- Limitar acceso entre segmentos
- Permitir solo servicios autorizados

### Segmentacion de red

Divide la red en zonas para reducir movimiento lateral.

Ejemplos:

- Usuarios separados de servidores
- Sistemas criticos en una VLAN aislada
- Zona DMZ para servicios expuestos

### VPN

Protege el acceso remoto creando un tunel cifrado.

Buenas practicas:

- MFA obligatorio
- Restricciones por dispositivo o ubicacion
- Registro de sesiones

### IDS / IPS

- IDS: detecta
- IPS: detecta y bloquea

Sirven para observar trafico sospechoso, firmas de ataque y patrones anormales.

---

## 6. Controles en endpoints y servidores

### Antivirus

Busca malware conocido por firmas o heuristicas basicas.

Limitacion: no siempre detecta ataques nuevos o tecnicas muy sofisticadas.

### EDR

Vigila procesos, conexiones, comportamiento y persistencia.

Ventaja: ayuda a responder rapido ante compromisos reales.

### Hardening

Consiste en endurecer sistemas:

- Deshabilitar servicios innecesarios
- Cerrar puertos no usados
- Quitar permisos excesivos
- Configurar politicas seguras

### Parches y actualizaciones

Corrigen vulnerabilidades que ya son conocidas y explotables.

### Control de aplicaciones

Permite ejecutar solo software autorizado.

### Cifrado de disco

Protege la informacion si un equipo es robado o perdido.

---

## 7. Controles de monitoreo y deteccion

### Logs

Los registros guardan eventos de autenticacion, accesos, errores, cambios y acciones administrativas.

### SIEM

Centraliza los logs, correlaciona eventos y emite alertas.

Sirve para:

- Detectar accesos anormales
- Ver patrones de ataque
- Apoyar investigacion forense

### Monitoreo continuo

Supervisa sistemas y servicios para detectar incidentes lo antes posible.

### Alertas y casos de uso

Un control detectivo solo funciona bien si hay reglas utiles, prioridades claras y respuesta oportuna.

---

## 8. Controles de respaldo y recuperacion

### Backups

Permiten restaurar informacion o sistemas despues de:

- Ransomware
- Error humano
- Falla de hardware
- Corrupcion de datos

Buenas practicas:

- Regla 3-2-1: tres copias, dos medios, una fuera del sitio
- Pruebas de restauracion periodicas
- Copias inmutables o protegidas

### Plan de respuesta a incidentes

Define:

- Deteccion
- Contencion
- Erradicacion
- Recuperacion
- Lecciones aprendidas

### Continuidad operativa

Busca que el negocio siga funcionando o recupere servicios criticos en tiempos aceptables.

---

## 9. Controles administrativos y de gobierno

### Politicas y normas

Establecen reglas formales sobre:

- Uso aceptable
- Contraseñas
- Clasificacion de informacion
- Accesos
- Dispositivos

### Procedimientos

Indican como ejecutar tareas de forma segura y repetible.

### Concientizacion y capacitacion

Reduce errores humanos como phishing, contrasenas debiles o uso incorrecto de informacion.

### Gestion de riesgos

Prioriza controles segun impacto y probabilidad.

### Auditorias y revisiones

Verifican si los controles se cumplen y si siguen siendo efectivos.

---

## 10. Controles fisicos

### Control de acceso a instalaciones

- Tarjetas
- Cerraduras
- Guardias
- Biometria

### Proteccion del equipamiento

- Racks cerrados
- UPS
- Sensores ambientales
- Control de incendio

### Limpieza de escritorio y pantallas

Reduce el riesgo de fuga de informacion visible o impresa.

---

## 11. Mapa rapido para estudiar

| Categoria | Ejemplos |
|---|---|
| Preventivos | MFA, firewall, hardening, parches, segmentacion, RBAC |
| Detectivos | SIEM, logs, IDS, EDR, auditorias |
| Correctivos | backups, restauracion, respuesta a incidentes |
| Compensatorios | aislamiento de legacy, monitoreo reforzado |

---

## 12. Ejemplo de defensa en capas

Si un atacante roba una contrasena:

1. MFA puede bloquear el acceso.
2. El firewall o la VPN pueden limitar desde donde entra.
3. El SIEM puede detectar un inicio de sesion raro.
4. El EDR puede alertar sobre actividad maliciosa en el equipo.
5. El equipo de seguridad puede contener y recuperar el servicio.

La idea central es que un solo control no basta.

---

## 13. Resumen corto

- Los controles de seguridad reducen riesgos.
- Se agrupan en preventivos, detectivos, correctivos y compensatorios.
- MFA, firewall, hardening y parches son controles preventivos.
- SIEM, logs, IDS y EDR ayudan a detectar incidentes.
- Backups y respuesta a incidentes permiten recuperacion.
- La seguridad real se construye por capas.
