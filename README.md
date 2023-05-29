# Vue config environment 

Vite is a build tool developed by Evan You, the author of Vue. It uses native ES Module imports to provide a fast running development environment with no bundling required. Vue3, React and Preact are also supported.

We'll build a Vue3 project environment using Vite, Typescript, ESLint and Prettier. Later we'll add some tests.

Vite requires Node.js version 14.18+, 16+. However, some templates require a higher Node.js version to work, please upgrade if your package manager warns about it.

```sh
npm create vite@latest my-app -- --template=vue-ts
```

## Introducing ESLint

The first thing we will do is install ESLint.

```sh
npm i -D eslint eslint-plugin-vue @vue/eslint-config-typescript @typescript-eslint/parser @typescript-eslint/eslint-plugin
```

Create the file **.eslintrc** with the following:

```sh
{
  "root": true,
  "env": {
      "browser": true,
      "es2021": true,
      "node": true
  },
  "extends": [
    "plugin:vue/vue3-recommended",
    "eslint:recommended",
    "@vue/typescript/recommended"
  ],
  "parserOptions": {
      "ecmaVersion": 2021
  },
  "plugins": [
  ],
  "rules": {
  }
}

```

## Configuring husky and lint-staged

Before committing, let's run a static check to make sure you can't commit the error code.

```sh
npm i -D husky lint-staged
```

Add the following to **package.json**:

```sh
{
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  },
  "lint-staged": {
    "*.{ts,vue}": "eslint --fix"
  }
}

```

## Configuring Prettier

Let Prettier do the formatting for your entire project

```sh
npm i -D prettier eslint-plugin-prettier @vue/eslint-config-prettier
```

Create the file **.prettierrc** with the following:

```sh
{
  "singleQuote": true,
  "semi": true,
  "vueIndentScriptAndStyle": true
}
```

When ESLint and Prettier are used together, we need to fix the .eslintrc to avoid duplicate rules.

```sh
{
  "extends": [
    "plugin:vue/vue3-recommended",
    "eslint:recommended",
    "@vue/typescript/recommended",
    "@vue/prettier" // Add this line
  ]
}
```

For VSCode users, install the [ESLint Plugin](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) and you can format the code automatically with the following settings.

```sh
{
  "[typescript]": {
    "editor.formatOnSave": false,
    "editor.codeActionsOnSave": [
      "source.addMissingImports",
      "source.fixAll.eslint"
    ]
  },
  "[vue]": {
    "editor.formatOnSave": false,
    "editor.codeActionsOnSave": [
      "source.addMissingImports",
      "source.fixAll.eslint"
    ]
  },
  "editor.defaultFormatter": "dbaeumer.vscode-eslint"
}
```

## Configuring Stylelint

Let's make the style a target for linting as well.

```sh
npm i -D stylelint stylelint-config-recommended stylelint-config-standard
```

Create the file **.stylelintrc** with the following:

```sh
{
  "extends": ["stylelint-config-recommended", "stylelint-config-standard"]
}
```

We need a extension. You can download it from [here](https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint).

## Adding Testing Libraries

Cooming soon.