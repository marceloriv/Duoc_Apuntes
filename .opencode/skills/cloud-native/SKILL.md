---
name: cloud-native
description: Guía el proyecto de Cloud Native I (Duoc UC): MVP de la primera evaluación (Frontend + API Manager + BFF), versionado de API, CORS, políticas por rol y entregables de la semana 5. Usar cuando se trabaje sobre Proyectos/Cloud Native, se diseñe o revise el API Manager, el BFF o los microservicios del proyecto, o se mencionen "Cloud Native I", "API Manager", "MVP E1" o "reportes ciudadanos".
compatibility: opencode
metadata:
  domain: cloud-native
  role: project-guide
  scope: Proyectos/Cloud Native
---

# Cloud Native I — Guía de proyecto

Apoyo para el proyecto del ramo **Cloud Native I** (sexto semestre, Duoc UC). El foco del ramo es construir el **API Manager**, no los microservicios.

## Arquitectura objetivo

```
Frontend (por rol)
   │
   ▼
API Manager (punto único: auth, policies, rate limit, CORS, versionado, logging)
   │
   ▼
BFF (patrón de arquitectura, agregación por rol)
   ├── user-service
   ├── report-service
   ├── department-service
   └── notification-service
```

## Criterios de aprobación (primera evaluación = MVP)

Según `2026/sexto semestre/Cloud Native I/Semana 1/2.md`:

- El MVP es **Frontend + API Manager + BFF** (BFF como patrón de arquitectura).
- Se puede comenzar ya por **Frontend** y **BFF**.
- **Versionado de API**: se versiona por URL cuando cambia compatibilidad, seguridad, tipos de solicitud, políticas o headers de solicitud.
- **CORS**: API pública permite `*`; API propia restringe a la URL del consumidor.
- La idea debe mostrar roles/permisos naturales, políticas distintas por consumidor y al menos un caso real de versionado.

## Entregables semana 5

- **Frontend**: 1 pantalla real por rol (ej. ciudadano + funcionario) consumiendo solo el API Manager.
- **API Manager**: autenticación JWT, autorización por rol, rate limiting, CORS y ≥1 política por consumidor.
- **BFF**: 1 endpoint de agregación (ej. `GET /api/v1/citizens/dashboard`) combinando 2-3 microservicios.
- **Microservicios**: 2-3 de dominio (mínimo viable, no son el foco).
- **Versionado**: usar `/v1` y documentar el caso de cambio a `/v2`.

## Checklist: cómo lucirse en el API Manager

Reutilizar lo resuelto y auditado en `Proyectos/Ticketti.md` (Spring Cloud Gateway, JWT, BFF NestJS):

- [ ] Autenticación JWT en el gateway y validación de `iss`/`aud`.
- [ ] Autorización por rol (ej. `PATCH /status` solo técnicos/funcionarios): demostrar que no es solo routing.
- [ ] Rate limits distintos por endpoint/consumidor (ej. `POST` estricto, `GET` laxo).
- [ ] CORS: API pública `*` vs. ruta interna restringida a la URL del frontend.
- [ ] Versionado por URL (`/v1`, `/v2`) documentado en OpenAPI.
- [ ] Propagación de headers `X-Usuario`, `X-Usuario-Id`, `X-Rol-Usuario-Id` al BFF.
- [ ] Logging/trazabilidad con `X-Request-Id` por request.
- [ ] Circuit breaker / timeouts (Resilience4j) para evitar cascadas hacia el BFF.

## Referencias locales

- Idea elegida y alternativas: `Proyectos/Cloud Native/ideas.md`
- Notas del ramo: `2026/sexto semestre/Cloud Native I/Semana 1/1.md` y `2.md`
- Experiencia previa (stack y patrones): `Proyectos/Ticketti.md`, `Proyectos/Ticketti-Audit.md`
- Fechas de evaluación: `2026/sexto semestre/Gestion de proyectos de Software/Semana 1/2.md`

## Reglas de trabajo

- Solo tocar los archivos solicitados (edición quirúrgica).
- Verificar lógica no trivial con una prueba o assertion.
- Documentación en español, bullet-driven y concisa.
