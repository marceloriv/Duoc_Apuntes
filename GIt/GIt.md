La estructura de un mensaje de commit siguiendo la especificación sería la siguiente:

```shell
<tipo>[scope opcional]: <descripción del commit>

[cuerpo del mensaje, opcional]

[footer(s), opcionales]

```

### Tipos de commits

Los tipos de commits son los siguientes:

- **feat**: Una nueva característica o funcionalidad. Tendría correlación con una versión MINOR siguiendo _SemVer_.
- **fix**: Un error corregido. Tendría correlación con una versión PATCH siguiendo _SemVer_.
- **BREAKING CHANGE**: Un cambio que contenga esta palabra en el `footer` del mensaje o un signo `!` despues del tipo o scope, rompe la compatibilidad con versiones anteriores. Tendría correlación con una versión MAJOR siguiendo _SemVer_.

Se permiten también los siguientes tipos:

- **build**: Cambios que afectan el sistema de compilación o dependencias externas (ej. cambios en el `package.json`).
- **ci**: Cambios en nuestros archivos y scripts de configuración de integración continua.
- **docs**: Cambios en la documentación.
- **chore**: Otros cambios que no afectan el código fuente.
- **perf**: Un cambio de código que mejora el rendimiento.
- **refactor**: Un cambio de código que no corrige un error ni agrega una característica.
- **style**: Cambios que no afectan el significado del código (espacios en blanco, formato, puntos y comas faltantes, etc).
- **test**: Agregar pruebas faltantes o corregir pruebas existentes.

### Scope

El scope es opcional, y sirve para especificar el alcance del commit. Por ejemplo, si estamos trabajando en un proyecto monorepo, podemos especificar el paquete que estamos modificando.

### Ejemplos

Veamos algunos ejemplos de mensajes de commit siguiento la especificación:

**Commit que añade una nueva característica, sin un scope en concreto**.

```shell
feat: add support for TypeScript
```

**Commit que arregla un bug, dentro del paquete `ui` de nuestro proyecto**.

```shell
fix(ui): bugfix on Button component
```

**Commit que rompe la compatibilidad con versiones anteriores, aunque no añade características nuevas ni corrige bugs**.

```shell
chore!: drop support for Node 6

BREAKING CHANGE: use JavaScript features not available in Node 6.
```

**Commit que agrega pruebas faltantes**

```shell
test(ui): add missing tests for Button component
```

**Commit que agrega una tarea para el sistema de integración/despliegue continuo**.

```shell
ci: add GitHub Actions workflow
```

**Commit con un mensaje descriptivo largo y varios footers o pie de página**.

```shell
fix(api): prevent duplicate users from being created

This commit fixes a bug where the API would allow duplicate users to be created
with the same email address. This commit also adds a new `unique` constraint to
the `users` table to prevent this from happening in the future.

Paired with: X
Fixes #123

```

## ¿Por qué usar Conventional Commits?

- Permite la generación automática del fichero CHANGELOG.
- Determina automáticamente los cambios de versión siguiendo SemVer (basado en los tipos de commits utilizados).
- Comunican la naturaleza de los cambios a los demás integrantes del equipo o cualquier persona interesada.
- Activa los procesos de build y despliegue o publicación.
- Hacer más fácil a otras personas contribuir al proyecto al permitirles explorar el historial de commits de una forma más estructurada.

## Herramientas para usar Conventional Commits

### Plugin de VSCode

La primera que utilizo es la extensión o plugin de VSCode, [Conventional Commit](https://marketplace.visualstudio.com/items?itemName=vivaxy.vscode-conventional-commits) . Me ayuda a elegir el tipo de commit, el scope, escribir el mensaje,... todo a base de ventanas de dialogo.

### Gitemoji

Para darle más colorido a nuestros commits, podemos usar la convención [Gitemoji](https://gitmoji.dev/) . Es una convención en la que los emojis representan el tipo de commit. Por ejemplo, el emoji 🐛 representa un bugfix, ✨ un nuevo feature, etc... Así de un vistazo rápido puedes ver que tipo de cambio se ha realizado.

### Commitlint

[Commitlint](https://commitlint.js.org/#/)  es una herramienta que nos permite configurar reglas para validar los mensajes de commit. Igual que usamos un linter para comprobar si seguimos ciertas reglas de estilo en nuestro código, lo podemos usar para los mensajes de commit.

Para ello necesitas instalar la librería `@commitlint/cli` y `@commitlint/config-conventional` en tu proyecto.

```shell
npm install --save-dev @commitlint/cli @commitlint/config-conventional
```

Una vez instaladas, debes crear un fichero de configuración llamado `commitlint.config.js` en la raíz de tu proyecto con el siguiente contenido:

```js
module.exports = {
  extends: ["@commitlint/config-conventional"],
};
```

### Husky

Ya vimos [para que servía Husky en un post anterior](https://carlosazaustre.es/husky-lintstaged). Ahora vamos a añadirle una nueva regla al hook `pre-commit` para que verifique y valide si el mensaje de commit cumple las reglas de la convención Conventional Commits.

Si ya tienes [configurado Husky](https://carlosazaustre.es/husky-lintstaged) lo único que has de hacer es ejecutar el siguiente comando en la raíz de tu proyecto para que añada el comando al hook `commit-msg`:

```shell
npx husky add .husky/commit-msg  'npx --no -- commitlint --edit ${1}'
```

Y listo, cada vez que hagas un commit, verificará que sigue las reglas.

### CHANGELOG

Por último, también es interesante poder generar automáticamente el fichero CHANGELOG a partir de los mensajes de commit. Para ello hay diversas herramientas, una de ellas es [Conventional Changelog](https://github.com/conventional-changelog/conventional-changelog)