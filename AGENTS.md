# AGENTS.md

**Para el agente que trabaje en esta bóveda:**

- Sin emojis en notas, commits ni output — salvo los que ya usa Obsidian en callouts/frontmatter (`sticker: emoji//...`) o los que pida el usuario puntualmente.
- Esto es una bóveda Obsidian de apuntes académicos (Duoc UC), no un proyecto de software. No aplicar patrones de desarrollo genéricos (stack, tests, linters, deploy) salvo dentro de `Proyectos/`, donde se documentan proyectos de software reales que viven en otros repos.
- Este archivo es la fuente de verdad para este repo. Claude Code no lo carga solo (carga `CLAUDE.md`, no `AGENTS.md`) — decisión deliberada del usuario de no tener `CLAUDE.md` local, así que hay que leer/mencionar este archivo a mano cuando haga falta. No "arreglarlo" agregando un `CLAUDE.md` de import salvo que el usuario lo pida de nuevo explícitamente. El global del usuario (`~/.claude/CLAUDE.md`) sigue aplicando aparte y cubre estilo de respuesta (caveman), disciplina anti-sobreingeniería (ponytail), uso de codegraph y context-tools; no se repite acá.

## 0. Jerarquía de reglas

1. Seguridad y corrección — nunca se sacrifican por ninguna otra regla.
2. Convenciones de la bóveda (estructura, frontmatter, estilo de notas) — se siguen salvo instrucción explícita en contrario.
3. Minimalismo (Ponytail, ya activo por config global del usuario) — se aplica solo después de satisfacer 1 y 2.

## 1. Resumen del proyecto

Bóveda Obsidian personal de apuntes universitarios de Duoc UC (marceloriv). Contiene notas por semestre/asignatura, mapas de contenido (MOCs) y documentación de proyectos de software externos (ej. Ticketti, Cloud Native). Uso individual, sincronizada vía Git.

## 2. Herramientas

- Editor: Obsidian (plugins en `.obsidian/`, no versionados salvo config explícita).
- Sincronización/backup: Git + LocalSend.
- Formato de contenido: Markdown con extensiones de Obsidian (`[[wikilinks]]`, callouts `> [!tipo]`, embeds `![[nota]]`, Mermaid, frontmatter YAML).

## 3. Estructura de la bóveda

```text
2026/                  # apuntes por año/semestre/asignatura
  quinto semestre/     # CIBERSEGURIDAD SISTEMA OPERATIVO Y REDES, DESARROLLO FULLSTACK III, DevOps, EVALUACION DE PROYECTOS DE SOFTWARE
  sexto semestre/      # CIBERSEGURIDAD EN DESARROLLO, Cloud Native I, Gestion de proyectos de Software, Seguridad y calidad del Software
MOCs/                  # mapas de contenido: Académico.md, Proyectos.md, Recursos.md — índices de enlaces, no contenido propio
Proyectos/             # documentación de proyectos de software externos (código real vive en otro repo/carpeta)
Recursos/              # material de apoyo no atado a una asignatura (CIT, Curso de Pirata Ético, opencode.md)
.github/               # copilot-instructions.md + hooks/
.vscode/               # settings.json, mcp.json
.opencode/             # config de OpenCode
.codegraph/            # índice de codegraph
```

Archivos raíz: `AGENTS.md`, `Bienvenido.md`, `README.md`, `TODO.md`, `cambios.md`, `Despliegue.md`, `opencode.json`, `.gitignore`

## 4. Comandos

```powershell
# ver estado de la bóveda
git status
# ver historial reciente
git log --oneline -20
```

No hay build/test/deploy — es contenido markdown, no código ejecutable (excepto snippets de ejemplo dentro de las notas mismas).

## 5. Estilo de notas

- Frontmatter YAML opcional al inicio (`sticker:`, `tags:`, etc.) — no inventar campos que Obsidian no usa.
- Enlaces internos con `[[Nota]]` o `[[Nota#Sección]]`, nunca rutas relativas markdown (`[texto](../ruta.md)`) salvo enlace a archivo fuera de la bóveda.
- Callouts (`> [!info]`, `> [!warning]`, `> [!tip]`, etc.) para contexto adicional, no para contenido central de la nota.
- Jerarquía de encabezados lógica (no saltar de H2 a H4).
- Ver `Bienvenido.md` como referencia completa de sintaxis Obsidian/Markdown usada en la bóveda.

## 6. Mapas de Contenido (MOCs)

`MOCs/*.md` son índices, no contenido: solo enlaces `[[...]]` agrupados. Al agregar una nota nueva bajo `2026/` o `Proyectos/`, enlazarla desde el MOC correspondiente si aplica — no dejar notas huérfanas sin entrada en ningún MOC ni nota relacionada.

## 7. Proyectos (`Proyectos/`)

Estas notas documentan software real (arquitectura, decisiones, bitácoras de cambios) cuyo código vive en otro repo/carpeta (ej. rutas `file:///.../Desktop/Kari/...` referenciadas en las notas). Al editar estas notas:

- No asumir que el código está en esta bóveda — no intentar `Read`/`Edit` sobre rutas de código ahí referenciadas salvo que el usuario lo pida explícitamente y la ruta exista.
- Mantener las bitácoras (ej. `cambios.md`) como registro histórico: no reescribir entradas pasadas, solo añadir.

## 8. Seguridad

- No pegar credenciales, tokens ni claves reales en las notas, ni siquiera como "ejemplo" — si una nota documenta config de un proyecto externo, usar placeholders o confirmar con el usuario si el dato es sensible antes de commitear.
- Si una nota ya contiene un secreto real, avisar al usuario antes de commitear/pushear en vez de commitear en silencio.

## 9. Commits y PR

Formato: Conventional Commits (`docs:`, `feat:`, `refactor:`, `chore:`), en español, ámbito en minúsculas según carpeta/tema (`docs(cloud):`, `docs(seguridad):`, `docs(mocs):`). Sin Gitmoji — no es la convención vigente en este repo (commits recientes lo abandonaron).

Sujeto en imperativo, minúsculas tras los dos puntos, sin punto final. Rama no aplica (trabajo directo en `main`, bóveda personal) salvo que el usuario indique lo contrario.

Nunca agregar trailers/firmas de autoría de agente/IA (`Co-Authored-By: <agente>`, "Generated with…", enlaces de sesión) salvo pedido explícito del usuario para ese commit puntual.

## 10. Límites del agente

**Siempre** (sin pedir permiso): crear/editar notas markdown, actualizar MOCs, crear commits locales.

**Preguntar primero**: force-push, `git reset --hard`/`clean`, mover o borrar notas existentes en bloque, tocar config de `.obsidian/`/`.space/`/`.makemd/`.

**Nunca sin aprobación explícita**: push a remoto, editar código fuente de proyectos externos referenciados desde `Proyectos/`.

## 11. Mantenimiento

Tratar como código. Añadir una sección cuando el agente falle repetidamente en algo concreto de esta bóveda, eliminar una cuando la convención cambie.
