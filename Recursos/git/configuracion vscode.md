# Configuracion de VSCODE

> [!note]
> Estas configuraciones van en el `settings.json` de VS Code, no en `.vscode/settings.json` de la boveda (esa se versiona aparte).

> [!info]
> Estas configuraciones van en el `settings.json` **de usuario** de VS Code (`%APPDATA%\Code\User\settings.json` o `Cmd/Ctrl+Shift+P` -> "Preferences: Open User Settings (JSON)"). No en `.vscode/settings.json` de la boveda: las configuraciones de usuario son `git.*` (comportamiento personal de Git) y no se deben versionar en el repo.

## Configuracion recomendada

```json
{
  "git.autofetch": true,
  "git.enableSmartCommit": true,
  "git.confirmSync": false,
  "git.autoStash": true,
  "git.fetchOnPull": true,
  "git.postCommitCommand": "push"
}
```

## Descripcion de cada configuracion

| Configuracion | Valor | Que hace |
| --- | --- | --- |
| `git.autofetch` | `true` | Busca cambios del remoto (origin) automaticamente cada 3 minutos y muestra cuantos commits hay de diferencia. No descarga los cambios, solo los detecta. |
| `git.enableSmartCommit` | `true` | Deja commitear todos los cambios con `git commit` en el mismo cuadro, sin pasar por el boton "+". |
| `git.confirmSync` | `false` | Omite el dialogo de confirmacion antes de sincronizar (pull + push). |
| `git.autoStash` | `true` | Guarda temporalmente cambios locales no commiteados antes de un pull, evita que el pull falle o pise trabajo, y luego los restaura. |
| `git.fetchOnPull` | `true` | Ejecuta fetch antes del pull para que los indicadores de rama queden siempre al dia. |
| `git.postCommitCommand` | `"push"` | Pushea automaticamente despues de cada commit. Evita acumular commits locales sin subir (util en boveda sincronizada por Git). |

## Decision de configuracion (usuario vs workspace)

- **`settings.json` de usuario:** todo lo `git.*` de esta nota va aca. Aplica a todos tus repositorios.
- **`.vscode/settings.json` de la boveda:** solo config especifica del proyecto (vease el que ya existe en la raiz). No replicar aca lo que corresponde al usuario.
- Configs mixtas (ambos archivos valen): `files.eol`, `files.exclude`, `editor.*`.

## Notas para bovedas Obsidian sincronizadas con Git

- `git.autoStash: true` es clave: Obsidian reescribe archivos constantemente (frontmatter, link cache) y un pull puede chocar con esos cambios no commiteados; el autostash protege el trabajo local.
- `git.postCommitCommand: "push"` cierra el ciclo automatico: commit -> push, sin tocar la Terminal. Al combinar con `git.autofetch`, siempre sabras si estas al dia con el remoto.
- Si el remoto de alguna boveda se pushea manualmente (GitHub Desktop, LocalSend), conviene dejar `git.postCommitCommand` en `"none"` para no pisar ese flujo.

## Como abrir el settings.json

1. `Cmd/Ctrl+Shift+P` -> "Preferences: Open User Settings (JSON)".
2. Agregar las claves del bloque recomendado.
3. `Cmd/Ctrl+Shift+P` -> "Preferences: Open User Settings" para ver la UI y confirmar que quedaron activas.
