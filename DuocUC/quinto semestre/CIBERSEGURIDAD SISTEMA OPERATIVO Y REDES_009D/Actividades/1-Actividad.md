# Actividad 1 - Evaluacion de Controles de Seguridad (FinCorp)

## Contexto

La empresa FinCorp Servicios Financieros es una organizacion mediana con operaciones en varios paises de Latinoamerica. Ofrece servicios de pagos digitales, gestion de cuentas y procesamiento de transacciones para clientes corporativos.

La empresa cuenta con la siguiente infraestructura y practicas de seguridad:

- Autenticacion mediante usuario y contrasena para todos los sistemas corporativos.
- MFA habilitado unicamente para accesos administrativos y VPN.
- Uso de firewall perimetral para controlar trafico entrante y saliente.
- Antivirus instalado en estaciones de trabajo y servidores.
- SIEM implementado, pero solo recibe logs de algunos sistemas criticos (no incluye aplicaciones internas ni algunos servidores legacy).
- Backups diarios automatizados de bases de datos criticas.
- Acceso remoto permitido mediante VPN, sin restriccion por geolocalizacion.
- Politicas de seguridad documentadas (contrasenas, accesos, uso aceptable).
- No existe un proceso formal de revision periodica de accesos.
- Algunos usuarios comparten cuentas en sistemas operativos de uso comun.
- Existen servidores con sistemas operativos desactualizados por compatibilidad con aplicaciones antiguas.
- No hay un proceso definido ni probado de respuesta a incidentes.
- Alertas del SIEM son revisadas de forma manual y no siempre de manera oportuna.

Durante una revision interna, se identifico que un usuario del area financiera accedio fuera de horario laboral desde una ubicacion inusual, sin que se generara una respuesta inmediata por parte del equipo de seguridad.

## Preguntas

1. Identificacion de controles
 Enumere los controles de seguridad que actualmente existen en la organizacion segun el contexto descrito.

2. Clasificacion de controles
 Para cada control identificado, indique si corresponde a:

- Preventivo
- Detectivo
- Correctivo

1. Evaluacion de efectividad
 Para cada uno de los controles identificados:

- Indique si esta correctamente implementado o presenta debilidades.
- Explique brevemente cual es la principal falencia o limitacion.

1. Identificacion de brechas de seguridad
 Identifique al menos cuatro problemas relevantes en la implementacion u operacion de los controles que puedan impactar la postura de seguridad de la organizacion.

2. Propuesta de mejoras
 Proponga al menos cinco medidas concretas para mejorar la postura de seguridad, indicando:

- Que control se debe mejorar o implementar.
- Que problema especifico soluciona.

## 1. Identificacion de controles existentes

Los controles actualmente presentes en FinCorp son:

1. Autenticacion con usuario y contrasena para sistemas corporativos.
2. MFA habilitado para accesos administrativos y VPN.
3. Firewall perimetral para trafico entrante y saliente.
4. Antivirus en estaciones de trabajo y servidores.
5. SIEM implementado (con cobertura parcial de logs).
6. Backups diarios automatizados de bases de datos criticas.
7. VPN para acceso remoto.
8. Politicas documentadas (contrasenas, accesos, uso aceptable).

Tambien se observan practicas que impactan negativamente la seguridad:

1. No hay revision periodica formal de accesos.
2. Hay cuentas compartidas en sistemas operativos de uso comun.
3. Hay servidores con sistemas operativos desactualizados.
4. No existe proceso definido ni probado de respuesta a incidentes.
5. Revision manual y no oportuna de alertas SIEM.

## 2. Clasificacion de controles

| Control | Tipo principal |
|---|---|
| Autenticacion usuario + contrasena | Preventivo |
| MFA (admin y VPN) | Preventivo |
| Firewall perimetral | Preventivo |
| Antivirus | Preventivo y Detectivo |
| SIEM | Detectivo |
| Backups diarios | Correctivo |
| VPN acceso remoto | Preventivo |
| Politicas documentadas | Preventivo (gobierno) |

Nota: algunos controles pueden cumplir mas de una funcion, pero se clasifican por su objetivo principal.

## 3. Evaluacion de efectividad por control

| Control | Estado | Principal limitacion o falencia |
|---|---|---|
| Autenticacion usuario + contrasena | Parcial / Debil | Sin MFA generalizado, mayor riesgo de compromiso por phishing o robo de credenciales. |
| MFA (admin y VPN) | Parcial | No cubre a todos los usuarios ni todos los sistemas criticos. |
| Firewall perimetral | Aceptable con limites | No protege por si solo amenazas internas, movimientos laterales o abuso de credenciales validas. |
| Antivirus | Parcial | Mayor eficacia frente a malware conocido; visibilidad limitada frente a tecnicas avanzadas o comportamiento anomalo. |
| SIEM | Debil | Cobertura incompleta de logs y revision manual no oportuna; aumenta tiempo de deteccion y respuesta. |
| Backups diarios | Bueno pero incompleto | No se evidencia prueba periodica de restauracion ni cobertura explicitada para todos los activos criticos. |
| VPN remoto | Parcial / Debil | Sin restriccion geográfica ni controles adicionales de riesgo de inicio de sesion. |
| Politicas documentadas | Parcial / Debil | Existen en papel, pero hay incumplimientos (cuentas compartidas) y falta de procesos de control (revision de accesos). |

## 4. Brechas de seguridad relevantes

Al menos cuatro brechas criticas identificadas:

1. Cobertura incompleta de monitoreo en SIEM.

- Impacto: actividad maliciosa puede no ser detectada o detectarse tarde.

1. Ausencia de proceso formal y probado de respuesta a incidentes.

- Impacto: demoras, decisiones improvisadas y mayor dano durante incidentes.

1. Falta de revision periodica de accesos y existencia de cuentas compartidas.

- Impacto: perdida de trazabilidad, exceso de privilegios y dificultad para atribucion.

1. Sistemas operativos desactualizados en servidores legacy.

- Impacto: exposicion a vulnerabilidades conocidas y mayor probabilidad de compromiso.

1. MFA no extendido a toda la organizacion.

- Impacto: mayor superficie para ataques de phishing y credential stuffing.

1. Acceso remoto por VPN sin controles adaptativos (geolocalizacion, riesgo, horario).

- Impacto: accesos anomalos pueden ocurrir sin bloqueo preventivo ni escalamiento oportuno.

## 5. Propuesta de mejoras concretas

Se proponen las siguientes medidas para mejorar la postura de seguridad:

| Medida propuesta | Control a mejorar o implementar | Problema que soluciona |
|---|---|---|
| Extender MFA a todos los usuarios y aplicaciones criticas (prioridad alta). | Autenticacion / Control de acceso | Reduce riesgo de compromiso por robo de credenciales y phishing. |
| Completar ingesta de logs en SIEM (incluyendo apps internas y servidores legacy) y definir casos de uso minimos. | Monitoreo detectivo (SIEM) | Elimina puntos ciegos y mejora deteccion temprana. |
| Implementar SOC operativo basico: alertas priorizadas, runbooks, SLA de atencion, escalamiento 24/7 o guardias. | Operacion detectiva y respuesta | Disminuye tiempo de respuesta ante eventos criticos. |
| Disenar y probar plan de respuesta a incidentes (IRP): roles, comunicacion, contencion, recuperacion y lecciones aprendidas. | Control correctivo / Proceso de incidentes | Evita improvisacion y reduce impacto de incidentes reales. |
| Ejecutar recertificacion periodica de accesos (trimestral/semestral) y eliminar cuentas compartidas. | Gobierno de acceso (IAM) | Reduce privilegios excesivos y mejora trazabilidad y cumplimiento. |
| Implementar plan de gestion de parches para legacy (parchado, aislamiento, compensating controls). | Hardening / Vulnerability management | Mitiga exposicion de sistemas desactualizados. |
| Fortalecer acceso VPN con politicas de acceso condicional (geolocalizacion, horario, reputacion IP, dispositivo confiable). | Control preventivo de acceso remoto | Bloquea o desafia accesos inusuales como el caso detectado. |
| Validar backups con pruebas de restauracion periodicas y definir RTO/RPO por activo critico. | Control correctivo (continuidad) | Asegura recuperacion real frente a ransomware o falla operativa. |

## Cierre ejecutivo

FinCorp cuenta con una base de controles relevante, pero su principal debilidad esta en la madurez operativa: monitoreo incompleto, respuesta tardia y gobierno de accesos insuficiente. La prioridad debe ser combinar controles preventivos (MFA total, acceso condicional, hardening) con capacidad detectiva y correctiva efectiva (SIEM completo, SOC operativo, respuesta a incidentes probada).
