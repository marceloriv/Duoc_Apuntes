# Evaluacion N.1 - Analisis de Ciberseguridad

## Contexto del informe

- Empresa analizada: AgroAndes S.A.
- Rubro: produccion y exportacion de alimentos
- Fecha: 08-04-2026
- Enfoque: analisis aplicado al negocio, no definiciones teoricas

---

## 1) Identificacion de activos criticos

Se identifican 8 activos criticos (minimo solicitado: 6):

| Activo | Que es | Por que es critico para el negocio |
|---|---|---|
| ERP legacy (finanzas, inventario, operaciones) | Plataforma central transaccional para costos, compras, stock y procesos operativos | Si falla o se altera, impacta produccion, facturacion, costos y cumplimiento de compromisos de exportacion |
| Sistema de logistica y trazabilidad | Sistema que registra estado de envios, lotes y trazabilidad de productos | La trazabilidad es clave para exportacion, auditorias y respuesta ante reclamos o retiros de producto |
| Datos de clientes y contratos (CRM + documentos comerciales) | Informacion comercial, historicos de ventas, condiciones y acuerdos con clientes internacionales | Su perdida o filtracion afecta ingresos, ventaja cokmpetitiva y confianza comercial |
| Identidades corporativas (AD + cuentas cloud + VPN) | Cuentas y privilegios que habilitan acceso a sistemas internos y cloud | Es el "llavero" de toda la empresa; una cuenta comprometida permite movimiento lateral y escalamiento |
| Infraestructura de red interna (segmentos admin, operaciones, IoT) | Conectividad entre sedes, plantas, sistemas corporativos y dispositivos operativos | La continuidad operativa depende de la red; ademas, segmentacion incompleta aumenta riesgo de propagacion |
| APIs internas/externas de integracion | Servicios que conectan ERP, CRM, portal y partners | Si se comprometen, se altera el flujo de datos entre procesos criticos y terceros |
| Portal web externo para clientes | Plataforma web para consulta de pedidos y estado comercial | Punto de contacto directo con clientes; una caida afecta servicio e imagen de marca |
| Backups y repositorios de recuperacion | Copias de seguridad de sistemas y datos criticos | Son esenciales para continuidad ante ransomware, error humano o falla de infraestructura |

Lectura de criticidad de negocio:

- AgroAndes depende de continuidad operativa y trazabilidad para vender/exportar.
- El mayor impacto esperado no es solo tecnico: afecta ingresos, cumplimiento contractual y reputacion internacional.

---

## 2) Analisis de impacto CIA (Confidencialidad, Integridad, Disponibilidad)

Se analizan 4 activos criticos (minimo solicitado: 3):

### Activo A: ERP legacy

- Confidencialidad (alto): expone costos, margenes y datos financieros; esto favorece fraude y espionaje comercial.
- Integridad (alto): cambios no autorizados en inventario o compras pueden generar despachos errados, quiebres de stock y reportes financieros incorrectos.
- Disponibilidad (alto): una interrupcion detiene procesos transversales (operacion, finanzas, logistica), con impacto directo en compromisos de exportacion.

### Activo B: Sistema de logistica y trazabilidad

- Confidencialidad (medio): incluye rutas, volumenes y condiciones comerciales; su exposicion aumenta riesgo de fraude o abuso competitivo.
- Integridad (alto): si se altera trazabilidad de lotes/envios, se compromete cumplimiento regulatorio y capacidad de respuesta ante incidentes sanitarios.
- Disponibilidad (alto): sin sistema de seguimiento, la operacion no puede planificar ni validar entregas en tiempo.

### Activo C: Identidades (AD, cloud, VPN)

- Confidencialidad (alto): robo de credenciales habilita acceso a datos sensibles de multiples sistemas.
- Integridad (alto): una identidad privilegiada comprometida puede modificar politicas, crear cuentas y alterar configuraciones criticas.
- Disponibilidad (alto): abuso de privilegios puede bloquear cuentas o servicios, degradando la operacion completa.

### Activo D: APIs internas y externas

- Confidencialidad (alto): APIs pueden exponer datos de clientes, pedidos e integraciones con partners.
- Integridad (alto): manipulacion de payloads o transacciones puede desalinear procesos entre sistemas (ERP-CRM-logistica).
- Disponibilidad (medio/alto): una degradacion de APIs rompe integraciones y retrasa procesos clave de negocio.

Conclusion CIA:

- Los activos analizados tienen impacto predominantemente alto en integridad y disponibilidad, coherente con una empresa de operacion distribuida y exportacion regulada.

---

## 3) Amenazas y vulnerabilidades

### 3.1 Amenazas relevantes (minimo solicitado: 5)

1. Ransomware dirigido a entorno hibrido (on-prem + cloud).
2. Robo de credenciales por phishing/spear phishing.
3. Movimiento lateral interno desde red menos protegida hacia sistemas criticos.
4. Fraude interno o abuso de privilegios por cuentas compartidas/roles amplios.
5. Exfiltracion de datos comerciales y financieros (espionaje).
6. Compromiso de APIs por autenticacion debil o mala exposicion.

### 3.2 Vulnerabilidades presentes (minimo solicitado: 5)

1. MFA parcial (solo admin y VPN).
2. Cuentas compartidas en operaciones.
3. Accesos heredados no revisados periodicamente.
4. Segmentacion interna incompleta (sistemas accesibles desde multiples redes).
5. Hardening inconsistente en sistemas.
6. Sistemas legacy con parcheo infrecuente.
7. Servicios internos expuestos sin autenticacion robusta.
8. SIEM y logging con cobertura parcial/logs incompletos.
9. Falta de proceso formal maduro de respuesta a incidentes.

### 3.3 Relacion amenaza-vulnerabilidad (ejemplos clave)

| Amenaza | Vulnerabilidad que la facilita | Justificacion contextual |
|---|---|---|
| Robo de credenciales | MFA parcial + accesos fuera de horario no contenidos | Ya se observaron accesos anomalos; una sola credencial valida puede abrir varios sistemas |
| Ransomware | Segmentacion incompleta + parcheo legacy debil | Facilita propagacion lateral y explotacion de vulnerabilidades conocidas |
| Exfiltracion de datos | Servicios internos mal autenticados + logs incompletos | Permite acceso y salida de datos con baja trazabilidad |
| Fraude interno | Cuentas compartidas + roles amplios | Reduce no repudio y control de segregacion de funciones |
| Ataques a APIs | Hardening inconsistente + controles de acceso debiles | Afecta integraciones criticas con partners/clientes |

---

## 4) Analisis de riesgos

Se construyen 4 riesgos (minimo solicitado: 3):

### Riesgo 1: Secuestro de operaciones por ransomware

- Activo: ERP + red interna + servidores on-prem.
- Amenaza: ransomware.
- Vulnerabilidad: segmentacion incompleta + sistemas legacy sin parcheo frecuente.
- Escenario: un endpoint comprometido en operaciones permite movimiento lateral y cifrado de servidores de negocio.
- Impacto: alto.
- Probabilidad: alta.
- Justificacion: entorno distribuido, debilidades de segmentacion y legado; impacto directo en continuidad y exportaciones.

### Riesgo 2: Compromiso de cuentas y escalamiento de privilegios

- Activo: AD, identidades cloud, VPN.
- Amenaza: robo de credenciales y abuso de cuentas.
- Vulnerabilidad: MFA parcial + cuentas compartidas + revision de accesos no periodica.
- Escenario: atacante usa credenciales validas y luego escala por roles amplios/accesos heredados.
- Impacto: alto.
- Probabilidad: alta.
- Justificacion: hay evidencias de accesos fuera de horario y modelo IAM con controles incompletos.

### Riesgo 3: Perdida de trazabilidad y problemas regulatorios

- Activo: sistema de logistica/trazabilidad.
- Amenaza: manipulacion de datos o falla de disponibilidad.
- Vulnerabilidad: servicios internos expuestos sin autenticacion robusta + monitoreo parcial.
- Escenario: alteracion de registros de lote/envio sin deteccion temprana.
- Impacto: alto.
- Probabilidad: media.
- Justificacion: trazabilidad es requisito de negocio y compliance; no todos los eventos estan bien registrados.

### Riesgo 4: Exfiltracion silenciosa de informacion sensible

- Activo: CRM, documentos comerciales, datos financieros.
- Amenaza: espionaje comercial / fuga de datos.
- Vulnerabilidad: logs incompletos + SIEM parcial + controles internos no maduros.
- Escenario: actor interno/externo extrae datos por periodos prolongados sin contencion oportuna.
- Impacto: alto.
- Probabilidad: media/alta.
- Justificacion: operacion internacional y valor estrategico de datos comerciales aumentan incentivo atacante.

Prioridad sugerida (matriz simple):

- Prioridad 1: Riesgo 1 y Riesgo 2.
- Prioridad 2: Riesgo 4.
- Prioridad 3: Riesgo 3.

---

## 5) Superficie de ataque

### 5.1 Exposicion externa

Puntos de entrada posibles:

- Portal web externo para clientes.
- VPN de acceso remoto.
- APIs expuestas para integraciones.
- Correo corporativo (vector de phishing).

Sistemas expuestos:

- Frontend web y servicios API en cloud.
- Perimetro de autenticacion remota (VPN).

Accesos relevantes:

- Usuarios administrativos y remotos.
- Integraciones con terceros/partners.

### 5.2 Exposicion interna

Entradas posibles:

- Estaciones de trabajo comprometidas mediante phishing, adjuntos maliciosos o robo de credenciales.
- Dispositivos IoT o de operacion conectados a la red corporativa.
- Servicios internos con autenticacion debil o mal configurada.
- Acceso remoto interno desde equipos de administracion o soporte.

Sistemas expuestos:

- Directorio activo y servicios de identidad.
- ERP y sistemas de gestion interna.
- Servidores de archivos y repositorios compartidos.
- Servidores backend Linux y bases de datos.
- Equipos de operacion y dispositivos IoT integrados a la red corporativa.

Accesos relevantes:

- Cuentas de administracion de TI y soporte.
- Usuarios de operaciones con acceso a sistemas productivos.
- Cuentas de servicio e integraciones internas entre aplicaciones.
- Accesos heredados o amplios sobre recursos compartidos y bases de datos.

Lectura de riesgo de superficie:

- El mayor riesgo esta en la frontera interna (post-compromiso), no solo en el perimetro externo.
- Segmentacion parcial y credenciales debiles aumentan probabilidad de movimiento lateral.

---

## 6) Analisis de usuarios, accesos y privilegios

### 6.1 Debilidades de autenticacion (Authn)

- MFA no universal: solo admin y VPN; usuarios de negocio quedan mas expuestos.
- Dependencia en usuario + contrasena para varios sistemas.
- Evidencia de accesos fuera de horario laboral sin respuesta oportuna.

### 6.2 Debilidades de autorizacion (Authz)

- RBAC basico con roles amplios en algunos sistemas.
- Accesos heredados no revisados periodicamente.
- Posible exceso de privilegios y falta de segregacion de funciones.

### 6.3 Problemas de gestion de identidades

- Uso de cuentas compartidas en operaciones (rompe trazabilidad y no repudio).
- Integracion parcial AD-cloud (riesgo de inconsistencias de ciclo de vida de cuentas).
- Falta de proceso robusto para recertificacion de accesos.

Riesgo principal IAM:

- Compromiso de una identidad valida + controles de autorizacion debiles = escalamiento rapido y alto impacto transversal.

---

## 7) Evaluacion de controles de seguridad

### 7.1 Clasificacion de controles existentes

| Control existente | Clasificacion |
|---|---|
| Firewall perimetral | Preventivo |
| Antivirus endpoints | Preventivo / Detectivo |
| SIEM (cobertura parcial) | Detectivo |
| VPN acceso remoto | Preventivo |
| Backups diarios | Correctivo |
| Politicas de seguridad documentadas | Preventivo (gobierno) |

### 7.2 Debilidades de implementacion/operacion (minimo solicitado: 3)

1. SIEM con cobertura parcial y sin monitoreo operativo continuo.

- Relacion con clases: un control detectivo solo funciona con logs completos, reglas utiles y respuesta oportuna.
- Efecto en AgroAndes: aumenta el dwell time del atacante y retrasa la contencion en fases de Installation y C2.

1. Segmentacion interna incompleta entre oficinas, operaciones e IoT.

- Relacion con clases: debilita la defensa en profundidad y permite que un fallo en una capa impacte otras.
- Efecto en AgroAndes: facilita movimiento lateral hacia AD, ERP y servidores criticos tras un acceso inicial.

1. Hardening y parchado inconsistente en entornos legacy.

- Relacion con clases: hardening y patching son controles preventivos base; cuando no se puede parchear, se requieren controles compensatorios.
- Efecto en AgroAndes: mantiene superficies explotables conocidas y eleva probabilidad de escalamiento de privilegios.

1. Brecha entre controles documentados y controles efectivamente operados.

- Relacion con clases: confirma el problema de gobierno; la seguridad falla por procesos y responsabilidades, no solo por falta de herramientas.
- Efecto en AgroAndes: existen controles en papel, pero su ejecucion irregular reduce su efectividad real.

1. Ausencia de proceso formal y probado de respuesta a incidentes.

- Relacion con clases: respuesta y recuperacion son parte esencial de los controles correctivos y del ciclo operacional.
- Efecto en AgroAndes: contencion ad hoc, mayor impacto operativo y recuperacion mas lenta ante ransomware o exfiltracion.

---

## 8) Hardening y mejora tecnica

Se proponen 8 medidas concretas (minimo solicitado: 5):

| Medida (que hacer) | Problema que soluciona |
|---|---|
| 1. Extender MFA a todos los usuarios y aplicaciones criticas (incluye SSO cloud) | Reduce exito de phishing y abuso de credenciales |
| 2. Implementar recertificacion trimestral de accesos y eliminar cuentas compartidas | Corrige exceso de privilegios y mejora trazabilidad |
| 3. Segmentar red por zonas de confianza (admin, operaciones, IoT, servidores criticos) + ACL estrictas | Disminuye movimiento lateral y alcance de incidentes |
| 4. Programa de parchado basado en riesgo para legacy (con controles compensatorios donde no se pueda parchear) | Reduce exposicion a CVE conocidas |
| 5. Hardening estandar por baseline (Windows, Linux, AD, servicios web) y control de cambios | Elimina configuraciones inseguras e inconsistentes |
| 6. Fortalecer APIs con autenticacion fuerte, autorizacion por alcance, rate limit y validacion de entradas | Reduce abuso de APIs y manipulacion de datos |
| 7. Completar cobertura de logs en SIEM (AD, VPN, ERP, APIs, servidores, cloud) y casos de uso prioritarios | Mejora deteccion temprana y capacidad de investigacion |
| 8. Definir e implementar plan formal de respuesta a incidentes con runbooks y simulacros semestrales | Acelera contencion y recuperacion, reduciendo impacto de negocio |

Orden de ejecucion recomendado (90 dias):

- Fase 1 (0-30 dias): MFA masivo, eliminacion de cuentas compartidas, casos de uso SIEM de alto riesgo.
- Fase 2 (31-60 dias): segmentacion priorizada, recertificacion de accesos, hardening baseline.
- Fase 3 (61-90 dias): parchado legacy + controles compensatorios, simulacro IR, maduracion de monitoreo.

---

## 9) Analisis del ataque (Cyber Kill Chain)

Escenario plausible: compromiso de cuenta comercial por phishing, escalamiento interno y exfiltracion de datos, con intento final de ransomware para presion/extorsion.

1. Reconocimiento

- El atacante recopila correos, cargos y estructura de areas (comercial, finanzas, operaciones) mediante fuentes abiertas y patron de dominios.

1. Weaponization

- Prepara campana de spear phishing con pagina de login falsa y malware ligero para persistencia.

1. Delivery

- Envia correo dirigido a usuario de area comercial con enlace a portal falso y adjunto de seguimiento logistico.

1. Explotacion

- El usuario entrega credenciales; como MFA no es universal, el atacante logra acceso a aplicaciones internas.

1. Instalacion / acceso

- Crea persistencia en endpoint y usa credenciales para explorar red interna; aprovecha roles amplios/accesos heredados.

1. Command & Control

- Establece canal C2 cifrado desde host comprometido hacia infraestructura externa.

1. Accion final

- Exfiltra datos de clientes/contratos y luego ejecuta cifrado parcial (ransomware) en servidores de alto impacto para interrumpir operacion.

Coherencia con el contexto:

- Se alinea con amenazas declaradas (ransomware, robo de credenciales, espionaje) y debilidades observadas (MFA parcial, logs incompletos, segmentacion parcial).

---

## 10) Punto de deteccion y contencion

### 10.1 Fases donde pudo detectarse

- Delivery/Explotacion:
  - Señales: correo sospechoso, login fuera de horario o desde ubicacion inusual.
  - Control disponible: SIEM parcial + registros VPN/AD.
  - Limitacion real: monitoreo no centralizado y revision no constante.

- Instalacion:
  - Señales: creacion de nuevas cuentas, cambios de privilegios, ejecucion anomala en endpoints/servidores.
  - Control disponible: antivirus y logs de sistemas.

- C2/Accion final:
  - Señales: trafico inusual, volumen de datos atipico, accesos internos no habituales.
  - Control disponible: firewall perimetral + SIEM (si existiera cobertura completa).

### 10.2 Fase donde pudo detenerse con mayor probabilidad

- Fase de Explotacion (mejor punto de quiebre):
  - Si MFA fuese obligatorio para todos los accesos criticos, el robo de contrasena no habria sido suficiente.

- Fase de Instalacion (segundo mejor punto):
  - Con control estricto de privilegios, cuentas no compartidas y segmentacion efectiva, el atacante habria tenido menor capacidad de escalar.

Justificacion:

- Los controles actuales existen, pero su operacion parcial reduce capacidad de detener ataques tempranamente.

---

## 11) Conclusion ejecutiva (orientada a gerencia)

AgroAndes presenta un nivel de riesgo general medio-alto: dispone de controles base importantes, pero con brechas de operacion y gobierno que incrementan la probabilidad de incidentes con impacto de negocio relevante.

Las debilidades mas criticas son la gestion de identidades (MFA parcial, cuentas compartidas, accesos no recertificados), la segmentacion interna incompleta y una capacidad detectiva todavia parcial (SIEM y logs no totalmente integrados). En este contexto, un ataque por credenciales robadas puede evolucionar rapidamente a movimiento lateral, exfiltracion de informacion comercial/financiera e interrupcion operativa.

El impacto potencial para el negocio incluye:

- interrupcion de procesos de produccion, logistica y exportacion,
- incumplimientos contractuales y regulatorios vinculados a trazabilidad,
- dano reputacional frente a clientes internacionales,
- y costos directos de recuperacion y continuidad.

La postura de seguridad no es critica, pero tampoco madura: la organizacion cuenta con fundamentos, aunque requiere cerrar brechas de ejecucion para pasar de una seguridad "implementada en partes" a una seguridad "operada de forma consistente".

Prioridad ejecutiva recomendada:

1. Fortalecer identidad y acceso (MFA total + recertificacion + fin de cuentas compartidas).
2. Reducir superficie y propagacion interna (segmentacion + hardening + parchado por riesgo).
3. Aumentar deteccion y respuesta efectiva (cobertura SIEM completa + proceso formal de incidentes).

Con estas acciones, AgroAndes puede reducir rapidamente su exposicion a los escenarios de mayor impacto y mejorar su resiliencia operacional y comercial.
