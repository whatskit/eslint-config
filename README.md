<h1 align="center">eslint-config-whatskit</h1>

> 💅 🦋 Shareable ESLint config for keeping JavaScript consistent across all of whatskit's projects, built upon [JavaScript Standard Style](https://github.com/standard/standard).

This cat clearly forgot to lint her JavaScript before deployment:

Don't be like that cat.

**Table of Contents**

- [Usage](#usage)
  - [React](#react)
  - [Prettier](#prettier)
  - [Editor Plugins](#editor-plugins)
- [Rules](#rules)
- [Development](#development)
- [⬆️ Releases](#️-releases)
  - [Production](#production)
  - [Pre-Releases](#pre-releases)
- [Changelog](#changelog)
- [Contributing](#contributing)
- [🏛 License](#-license)

---

## Usage

For every project containing JavaScript, ESLint should be set up with this base setup.

```bash
npm install --save-dev eslint eslint-config-whatskit
```

Then, create a new file `.eslintrc` in the root of your project and fill with:

```json
{
  "extends": "whatskit"
}
```

### React

When using within a React project use this to get set up:

```bash
npm i -D eslint eslint-config-whatskit
```

And in your `.eslintrc`:

```json
{
  "extends": ["whatskit", "whatskit/react"]
}
```

### Prettier

Additionally, you should add [Prettier](https://prettier.io) to your project and work with it through ESLint:

```bash
npm i -D prettier eslint-config-prettier eslint-plugin-prettier
```

Then add a `.prettierrc` file to the root of your project with this content:

```json
{
  "semi": false,
  "singleQuote": true,
  "trailingComma": "none"
}
```

Finally, modify your `.eslintrc`:

```json
{
  "extends": ["whatskit", "prettier/standard", "plugin:prettier/recommended"],
  "plugins": ["prettier"]
}
```

### Editor Plugins

For maximum fun during coding, install an ESLint plugin in your favorite editor to get suggestions and autofixes as you type.

- VS Code: [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
- Atom: [linter-eslint](https://atom.io/packages/linter-eslint)
- PyCharm: [Installing, enabling, and configuring ESLint in PyCharm](https://www.jetbrains.com/help/pycharm/eslint.html)
- Sublime Text: [SublimeLinter-eslint](https://github.com/SublimeLinter/SublimeLinter-eslint)
- IntelliJ IDEA, RubyMine, WebStorm, PhpStorm, PyCharm, AppCode, Android Studio: [ESLint](https://plugins.jetbrains.com/plugin/7494-eslint)
- Vim, NeoVim: [ALE](https://github.com/w0rp/ale)

## Rules

We keep it simple and follow almost everything defined in the [JavaScript Standard Style](https://github.com/standard/standard). Only deviations are:

- indentation: **2**
- **no** space before function parenthesis
- **double quotes** for jsx attributes
- prefer destructuring from objects & arrays
- enforce spacing inside curly braces

## Development

Again, keeping it simple with 2 files for now:

- `index.js`: holds all the custom JavaScript linting rules
- `react.js`: holds all the custom React linting rules

For local development, clone this repo and install all dependencies:

```bash
git clone git@github.com:whatskit/eslint-config-whatskit.git
cd eslint-config-whatskit/

npm i
```

Linting is setup against the actual rules within this repo so for testing new rules against every js file in this repo, you can run:

```bash
npm test
```

## ⬆️ Releases

Releases are managed semi-automatically. They are always manually triggered from a developer's machine with release scripts.

### Production

From a clean `main` branch you can run the release task bumping the version accordingly based on semantic versioning:

```bash
npm run release
```

The task does the following:

- bumps the project version in `package.json`, `package-lock.json`
- auto-generates and updates the CHANGELOG.md file from commit messages
- creates a Git tag
- commits and pushes everything
- creates a GitHub release with commit messages as description
- Git tag push will trigger a GitHub Action workflow to do a npm release

### Pre-Releases

For pre-releases, this is required for the first one like `v0.18.0-next.0`:

```bash
./node_modules/.bin/release-it major|minor|patch --preRelease=next
```

Further releases afterwards can be done with `npm run release` again and selecting the appropriate next version, in this case `v0.18.0-next.1` and so on.
