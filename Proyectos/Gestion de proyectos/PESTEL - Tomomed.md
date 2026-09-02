# Analisis PESTEL - Aplicacion Movil Tomomed

> **Caso:** Laboratorio Clinico Tomomed — red de 12 centros de toma de muestras en RM y Valparaiso. Desarrollo de app movil (iOS/Android) + app para personal de salud + panel web logistico para solicitar examenes clinicos a domicilio.
> **Fuente:** [[Proyectos/Gestion de proyectos/7.- Aplicacion Movil para solicitar examenes a domicilio.docx|Caso 7 - Tomomed]]

---

## P - Politico

| Factor                                                                                                                           | Impacto en el software                                                                                                                                                                                                                                                                                                                                            |
| -------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **[Ley 21.541 (2023)](https://www.bcn.cl/leychile/navegar?idNorma=1190336)** — autoriza atenciones de salud digital/telemedicina | La plataforma debe cumplir con los requisitos de autorizacion sanitaria para prestadores de salud digital. Implica ficha clinica electronica, estandares de seguridad de la informacion clinica y trazabilidad de atenciones.                                                                                                                                     |
| **Ley 21.668 (2024)** — interoperabilidad de fichas clinicas                                                                     | Requiere que el sistema soporte estandares de intercambio de datos clinicos (HL7/FHIR) para integrarse con el LIS existente y otras plataformas del ecosistema de salud.                                                                                                                                                                                          |
| **ClaveUnica como autenticacion estatal**                                                                                        | Solo el 21% de adultos mayores sabe usar ClaveUnica [(BCN, Informe 34-25, 2025)](https://obtienearchivo.bcn.cl/obtienearchivo?id=repositorio%2F10221%2F37647%2F1%2FInforme_34_25_Alfabetismo_digital_en_Chile.pdf). El software no puede depender exclusivamente de ClaveUnica para registro/auth — necesita mecanismos alternativos (RUT + contrasena, SMS OTP). |
| **Programa Nacional de Telesalud (Res. 342/2018)**                                                                               | El software se enmarca en la estrategia de teleasistencia del MINSAL, lo que facilita la aprobacion regulatoria pero impone estandares de calidad asistencial.                                                                                                                                                                                                    |

**Requerimientos derivados:**

- Ficha clinica electronica con registro de atenciones a distancia (R1)
- Integracion HL7/FHIR con LIS (R2)
- Auth flexible que no dependa de ClaveUnica (R3)
- Cumplimiento con estandares de autorizacion sanitaria MINSAL (R4)

---

## E - Economico

| Factor                                                                                                                                         | Impacto en el software                                                                                                                                                                                                                                                                                 |
| ---------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Fonasa (80% afiliados) + Isapres (18%)**                                                                                                     | El 90% de la poblacion rural es Fonasa [(Superintendencia de Salud, 2022)](https://www.superdesalud.gob.cl/wp-content/uploads/2023/07/Caracterizaci%C3%B3n-2022.pdf). El software debe integrarse con bono electronico (Imed/Medipass) y calcular copagos en tiempo real segun prevision del paciente. |
| **30.7M conexiones moviles (155% de la poblacion)** [(DataReportal, Digital 2025: Chile)](https://datareportal.com/reports/digital-2025-chile) | Alta penetracion movil valida el modelo app-first. Sin embargo, el gap de smartphones en 60+ (~50%) requiere canales alternativos.                                                                                                                                                                     |
| **Gasto en salud ~9% PIB, crecimiento sostenido**                                                                                              | Viabilidad economica del servicio a domicilio depende de escala. El software debe soportar 500+ agendamientos simultaneos (ya en requisitos) para absorber demanda en temporadas altas.                                                                                                                |
| **Pasarela de pago: Webpay Plus + Mercado Pago**                                                                                               | Integracion obligatoria con multiples medios de pago para cubrir segmentos (debito, credito, billeteras digitales).                                                                                                                                                                                    |

**Requerimientos derivados:**

- Modulo de integracion con bonos Fonasa (Imed/Medipass) (R5)
- Calculo de copago en tiempo real por prevision (R6)
- Pasarela de pagos Webpay Plus + Mercado Pago (R7)
- Boleta/factura electronica automatica (R8)
- Capacidad de 500 agendamientos simultaneos (R9)

---

## S - Social

| Factor                                                                                                                     | Impacto en el software                                                                                                                                      |
| -------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Brecha digital adultos mayores** — solo 50% tiene smartphone, 42% usa internet activamente (UC-Confuturo, 2024)          | La UI debe cumplir WCAG 2.1 AA (ya en requisitos). Se requieren canales alternativos: telefono, WhatsApp, formulario web simplificado.                      |
| **Envejecimiento poblacional** — 1 de cada 3 chilenos sera adulto mayor en 2050 (Worldpanel, 2026)                         | Crecimiento del target. Enfermedades cronicas (diabetes, hipertension) requieren controles periodicos — funcionalidad "Repetir Solicitud" es critica.       |
| **Disparidades RM vs Valparaiso** — RM concentra 59.7% de especialistas, Valparaiso 8.2% (Superintendencia de Salud, 2022) | La logica de asignacion debe diferenciar cobertura geografica. Zonas semi-rurales de Valparaiso (11 comunas rurales) requieren gestion de rutas extendidas. |
| **Brecha digital rural** — solo 5% de adultos mayores ha recibido capacitacion digital formal (Conecta Mayor UC)           | El software debe ser extremadamente simple para el paciente. Flujo de agendamiento en maximo 3-4 pasos.                                                     |

**Requerimientos derivados:**

- UI accesible WCAG 2.1 AA con fuente Grande y contraste alto (R10)
- Canales alternativos de agendamiento (telefono/WhatsApp) (R11)
- Funcionalidad "Repetir Solicitud" con un clic (R12)
- Modo offline para个人 de salud en zonas rurales (R13)
- Logica de cobertura geografica diferenciada por comuna/zona (R14)

---

## T - Tecnologico

| Factor                                                                                                                                                         | Impacto en el software                                                                                                                                               |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Cobertura 4G/5G** — universal en areas urbanas RM/Valparaiso, parcheada en semi-rural (Subtel)                                                               | Requiere modo offline sincronizable para个人 de salud en sectores con baja cobertura (ya en requisitos).                                                             |
| **HL7 v2 historico, FHIR en adopcion** — Norma Tecnica N237 (2025)                                                                                             | Arquitectura orientada a APIs REST estandarizadas, preparada para migracion a FHIR.                                                                                  |
| **No existe API publica Fonasa/Isapre** — integracion B2B contractual via Imed/Medipass                                                                        | Modulo de integracion con plataformas de bonos electronicos. Sin bus nacional unificado (estilo X-Road), el control vertical del flujo completo es el diferenciador. |
| **Ecosistema de competencia** — apps de telemedicina existentes (Reservo, etc.) pero pocos servicios de toma de muestras a domicilio con trazabilidad completa | El diferenciador tecnologico es la trazabilidad de custody de muestras (codigo de barras + monitoreo de temperatura).                                                |

**Requerimientos derivados:**

- Arquitectura hibrida offline/online con sincronizacion diferida (R15)
- APIs REST estandarizadas, preparadas para FHIR (R16)
- Modulo de integracion Imed/Medipass para bonos electronicos (R17)
- Trazabilidad completa: codigo de barras + monitoreo de temperatura (R18)

---

## E - Ecologico

| Factor                                                                                                            | Impacto en el software                                                                                                     |
| ----------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| **DS 148/2014 — transporte de muestras biologicas** — cadena de frio 2-8C, tiempo maximo 3 horas desde extraccion | Modulo de monitoreo de temperatura en tiempo real con alertas automaticas al laboratorio si se supera el limite.           |
| **Huella de carbono del transporte** — vehiculos propios y locomocion                                             | Algoritmo de optimizacion de rutas para minimizar km recorridos y emisiones. Reduce costos operativos simultaneamente.     |
| **Normativa MINSAL para residuos biologicos** — registro de manipulacion y transporte                             | Registro de cadena de custodia con codigo de barras vinculado a paciente,profesional y trazabilidad completa del trayecto. |

**Requerimientos derivados:**

- Sensores/modulo de monitoreo de temperatura en tiempo real (R19)
- Alerta automatica si contenedor excede 3 horas o temperatura fuera de rango (R20)
- Algoritmo de optimizacion de rutas (R21)
- Registro de cadena de custodia digital (R22)

---

## L - Legal

| Factor                                                                              | Impacto en el software                                                                                                                                                                                                                                                                                       |
| ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Ley 20.584 + Ley 21.541** — derechos y deberes de pacientes, atencion a distancia | Consentimiento informado digital antes de cada atencion. Registro de atenciones con fecha, hora y profesional. Ficha clinica electronica accesible al paciente.                                                                                                                                              |
| **Ley 21.719 (vigente dic 2026)** — proteccion de datos personales                  | Datos de salud = datos sensibles. Consentimiento expreso por cada finalidad. Derechos ARCO (acceso, rectificacion, cancelacion, oposicion). Sanciones hasta 20.000 UTM. Obliga a: cifrado AES-256 en reposo, TLS 1.3 en transito, log de auditoria inmutable, modulo de gestion de consentimientos por capa. |
| **Menores (<14) y adolescentes (14-16)** — Art. 16 quater Ley 19.628/21.719         | Consentimiento parental/legal para datos sensibles de menores de 16. Flujo de registro diferenciado segun edad del paciente.                                                                                                                                                                                 |
| **Ley 19.496 — Proteccion al Consumidor**                                           | Terminos y condiciones claros. Mecanismo de reclamos dentro de la app. Derecho de arrepentimiento en compras online (15 dias).                                                                                                                                                                               |
| **SII — Boleta/Factura electronica**                                                | Integracion con SII para emision automatica de documentos tributarios electronicos.                                                                                                                                                                                                                          |
| **Ley 21.668 — Interoperabilidad fichas clinicas**                                  | El sistema debe permitir exportar/recibir fichas clinicas en formatos estandarizados.                                                                                                                                                                                                                        |

**Requerimientos derivados:**

- Modulo de gestion de consentimientos informados por capa (R23)
- Cifrado AES-256 en reposo, TLS 1.3 en transito (R24)
- Log de auditoria inmutable (RUT, fecha, hora, accion) (R25)
- Flujo diferenciado de registro para menores/adolescentes (R26)
- Mecanismo de reclamos y terminos condiciones integrados (R27)
- Integracion con SII para facturacion electronica (R28)
- Exportacion de fichas clinicas en formato estandarizado (R29)

---

## Resumen de Requerimientos Clave por Factor PESTEL

| Factor      | Requerimientos criticos                                                                    |
| ----------- | ------------------------------------------------------------------------------------------ |
| Politico    | Ficha clinica electronica, HL7/FHIR, auth flexible, autorizacion sanitaria                 |
| Economico   | Integracion Fonasa/Isapre, pasarela de pagos, facturacion electronica, escalabilidad       |
| Social      | WCAG 2.1 AA, canales alternativos, "Repetir Solicitud", modo offline, cobertura geografica |
| Tecnologico | Arquitectura hibrida offline/online, APIs REST, integracion Imed/Medipass, trazabilidad    |
| Ecologico   | Monitoreo de temperatura, alertas de tiempo, optimizacion de rutas, cadena de custodia     |
| Legal       | Consentimientos por capa, cifrado AES-256/TLS 1.3, auditoria inmutable, menores, SII       |
