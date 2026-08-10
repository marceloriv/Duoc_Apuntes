# Resumen Prueba 1

## 1. Glosario de terminos clave

| Termino | Descripcion |
|---|---|
| Ciberseguridad | Disciplina que protege sistemas, redes, datos, servicios digitales y personas frente a ataques o accesos no autorizados. |
| Sistema operativo | Software fundamental que gestiona todos los recursos del computador. Es el administrador central del sistema. |
| UAC (User Account Control) | Funcion de Windows que solicita elevacion de permisos para cambios administrativos. |
| Active Directory (AD) | Servicio de Microsoft para administrar usuarios, equipos, roles y politicas en entornos corporativos. |
| Activo | Recurso con valor para la organizacion que debe protegerse (informacion, sistemas, infraestructura, personas y procesos). |
| Amenaza | Evento, actor o condicion capaz de causar dano a un activo. |
| Vulnerabilidad | Debilidad que puede ser explotada por una amenaza. |
| Backdoor | Mecanismo oculto de acceso remoto persistente en un sistema comprometido. |
| Ataque de cadena de suministro | Compromiso de proveedor/componente externo para llegar al objetivo principal. |
| Zero Trust (confianza cero) | Modelo que asume que nada es confiable por defecto; aplica minimo privilegio y verificacion continua. |
| EternalBlue | Vulnerabilidad critica de Windows sobre SMBv1, explotada en ataques como WannaCry. |
| C2 (Command and Control) | Canal de comunicacion entre equipo comprometido e infraestructura del atacante. |
| MFA | Verificacion con dos o mas factores (algo que sabes, tienes o eres). |
| Triada CIA | Confidencialidad, Integridad y Disponibilidad. Nucleo de seguridad de la informacion. |
| CVE | Identificador publico y estandar de vulnerabilidades conocidas. |
| NVD | Base de datos publica de vulnerabilidades mantenida por NIST. |
| CVSS v3 | Sistema de puntuacion para medir severidad de vulnerabilidades. |
| GRC | Gobierno, gestion de riesgos y cumplimiento normativo. |
| CTI | Analisis de actores, campanas, TTPs e indicadores para anticipar amenazas. |
| DDoS | Saturacion distribuida de un servicio para dejarlo fuera de linea. |
| EDR | Monitorea endpoints para detectar comportamiento malicioso y responder. |
| SIEM | Centraliza logs, correlaciona eventos y genera alertas de seguridad. |
| Kill Chain | Modelo por fases de un ataque: desde reconocimiento hasta objetivo final. |
| NIST CSF | Framework con 5 funciones: Identify, Protect, Detect, Respond, Recover. |
| RCE | Ejecucion remota de codigo. |
| CISO | Responsable de la estrategia de seguridad de la organizacion. |

---

## 2. Red y modelo cliente-servidor

### La red

- Es infraestructura para intercambio de informacion.
- En seguridad, tambien es el camino fisico y logico que recorre un atacante para llegar al objetivo.
- Cada dispositivo tiene direccion IP (analogia: direccion de una casa).

### Modelo cliente-servidor

1. El cliente envia solicitud.
2. El servidor recibe y procesa.
3. El servidor responde.

Clave: un atacante tambien es un cliente, pero envia solicitudes maliciosas o inesperadas.

---

## 3. Puertos y servicios

- Los puertos son puertas logicas del sistema.
- Mas puertos/servicios expuestos = mayor superficie de ataque.

### Puertos comunes

- HTTP: 80
- HTTPS: 443
- FTP: 21
- SSH: 22
- MySQL: 3306
- DNS: 53
- SMTP: 25

### TCP vs UDP

- TCP: mas confiable y ordenado; mas lento.
- UDP: mas rapido; sin garantia de entrega.

Ejemplos TCP: web, bases de datos, SSH.
Ejemplos UDP: DNS, streaming, juegos.

---

## 4. Sistemas operativos y seguridad

- El sistema operativo controla procesos, memoria, archivos, dispositivos, usuarios y permisos.
- Si se compromete, el atacante puede controlar gran parte del entorno.
- Movimiento lateral: desplazamiento del atacante dentro de la red tras acceso inicial.

### Puertos relevantes en Windows

- 139: SMB sobre NetBIOS.
- 445: SMB directo sobre TCP.
- 3389: RDP (acceso remoto).

Nota: 445 es SMB, no RDP.

### Recomendaciones practicas

- No dejar servicios innecesarios expuestos.
- Mantener software y parches al dia.
- Evitar privilegios administrativos innecesarios.
- No exponer bases de datos a internet sin controles.

---

## 5. Clase 4: triada CIA, activos y riesgo

### Triada CIA

- Confidencialidad: acceso solo autorizado.
- Integridad: datos correctos, sin cambios no autorizados.
- Disponibilidad: acceso cuando se necesita.

### Activos de informacion

5 activos comunes en empresa:

- Informacion
- Sistemas
- Infraestructura
- Personas
- Procesos

### Amenaza, vulnerabilidad y riesgo

- Amenaza: quien/que puede causar dano.
- Vulnerabilidad: debilidad explotable.
- Riesgo = Amenaza + Vulnerabilidad + Impacto.

Insight clave: muchos atacantes no inventan fallas nuevas; explotan vulnerabilidades publicas conocidas y sin parche.

---

## 6. Equipos y roles

- Red Team: busca y explota vulnerabilidades en pruebas controladas.
- Blue Team: protege activos y detecta/responde incidentes.
- CTI: estudia amenazas y patrones de adversarios.
- GRC: alinea seguridad con gobierno, riesgo y cumplimiento.

---

## 7. Clase 5: gobierno, controles y defensa en capas

Problema frecuente: los incidentes no ocurren solo por falta de herramientas, sino por falla organizacional.

Ejemplos:

- Nadie revisa alertas
- No hay responsables claros
- No hay procedimientos

### Gobierno de seguridad

- CISO: define estrategia, prioridades y comunica riesgos.
- Equipo de seguridad: monitoreo 24/7, analisis, respuesta e implementacion de controles.
- TI: operacion, redes, infraestructura y parches.
- Gerencia/negocio: define riesgo aceptable y presupuesto.

### Controles

- Preventivos: evitan (MFA, hardening, control de acceso).
- Detectivos: detectan (SIEM, monitoreo, alertas).
- Correctivos: recuperan/contienen (reset cuentas, restauracion, respuesta a incidentes).

### Defensa en profundidad (caso rapido)

1. Atacante roba contrasena.
2. MFA bloquea acceso total (preventivo).
3. SIEM detecta login anomalo (detectivo).
4. Equipo reinicia cuenta y contiene incidente (correctivo).

Conclusion: no existe seguridad con un solo control; se necesita seguridad por capas.

---

## 8. Resumen para memorizar

- CIA = Confidencialidad, Integridad, Disponibilidad.
- Activo, amenaza y vulnerabilidad explican el riesgo.
- Riesgo = Amenaza + Vulnerabilidad + Impacto.
- AD centraliza identidades; UAC controla elevacion de permisos.
- Zero Trust aplica minimo privilegio y verificacion continua.
- SMB usa 139/445; RDP usa 3389.
- CVE identifica fallas, NVD las publica, CVSS v3 mide severidad.
- Seguridad real = personas + procesos + tecnologia + controles por capas.
