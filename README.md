# Basic structure

# Start with yarn

yarn create vite

# Add package

Plugin eslint and prettier

```bash
yarn add eslint prettier @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint-config-prettier eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react eslint-plugin-prettier prettier-plugin-tailwindcss eslint-plugin-react-hooks -D
```

Tailwindcss

```bash
yarn add -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

Add package `@types/node` to use nodejs in ts file

```bash
yarn add -D @types/node
```

# Details

## ESLint and Prettier

- ESLint: Main code rule check

- Prettier: Main code formatter

- @typescript-eslint/eslint-plugin: ESLint plugin provide rule for Typescript

- @typescript-eslint/parser: Parser allow ESLint Typescript check rule.

- eslint-config-prettier: ESLint config to disable ESLint rules that conflict with Prettier.

- eslint-plugin-import: Help ESLint hcan understand `import...` systax insource code.

- eslint-plugin-jsx-a11y: Check for issues related to accessiblity

- eslint-plugin-react: ESLint rule for React

- eslint-plugin-prettier: Prettier rule for ESLint

- prettier-plugin-tailwindcss: Sorting class tailwindcss

- eslint-plugin-react-hooks: ESLint for React hook

Run command below to install

```bash
yarn add eslint prettier @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint-config-prettier eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react eslint-plugin-prettier prettier-plugin-tailwindcss eslint-plugin-react-hooks -D
```

ESLint Config

Create file `.eslintrc.cjs`

```js
/* eslint-disable @typescript-eslint/no-var-requires */
const path = require("path");

module.exports = {
  extends: [
    // Default plugin rule from package
    "eslint:recommended",
    "plugin:react/recommended",
    "plugin:react-hooks/recommended",
    "plugin:import/recommended",
    "plugin:import/typescript",
    "plugin:jsx-a11y/recommended",
    "plugin:@typescript-eslint/recommended",
    // Disable rules conflict with prettier.
    // Should add at the bottom to override rules above
    "eslint-config-prettier",
    "prettier",
  ],
  plugins: ["prettier"],
  settings: {
    react: {
      // eslint-plugin-react automatically know React version.
      version: "detect",
    },
    // ESLint handle import
    "import/resolver": {
      node: {
        paths: [path.resolve(__dirname, "")],
        extensions: [".js", ".jsx", ".ts", ".tsx"],
      },
    },
  },
  env: {
    node: true,
  },
  rules: {
    // Disable import React in file jsx
    "react/react-in-jsx-scope": "off",
    // Warning tag <a target='_blank'> without rel="noreferrer"
    "react/jsx-no-target-blank": "warn",
    // Add some prettier rule (copy từ file .prettierrc qua)
    "prettier/prettier": [
      "warn",
      {
        arrowParens: "always",
        semi: false,
        trailingComma: "none",
        tabWidth: 2,
        endOfLine: "auto",
        useTabs: false,
        singleQuote: true,
        printWidth: 120,
        jsxSingleQuote: true,
      },
    ],
  },
};
```

Create file `.eslintignore`

```json
node_modules/
dist/
```

Create file `.prettierrc`

```json
{
  "arrowParens": "always",
  "semi": false,
  "trailingComma": "none",
  "tabWidth": 2,
  "endOfLine": "auto",
  "useTabs": false,
  "singleQuote": true,
  "printWidth": 120,
  "jsxSingleQuote": true
}
```

Create file `.prettierignore`

```json
node_modules/
dist/
```

Add new script to `package.json`

```json
  "scripts": {
    ...
    "lint": "eslint --ext ts,tsx src/",
    "lint:fix": "eslint --fix --ext ts,tsx src/",
    "prettier": "prettier --check \"src/**/(*.tsx|*.ts|*.css|*.scss)\"",
    "prettier:fix": "prettier --write \"src/**/(*.tsx|*.ts|*.css|*.scss)\""
  },
```

### Install editorconfig

Create file `.editorconfig`

```EditorConfig
[*]
indent_size = 2
indent_style = space
```

### Config tsconfig.json

Set `"target": "ES2015"` và `"baseUrl": "."` trong `compilerOptions`

### Install tailwindcss

Reference [https://tailwindcss.com/docs/guides/vite](https://tailwindcss.com/docs/guides/vite)

```bash
yarn add -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

Cấu hình file config

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

Add into file `src/index.css`

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### Vite config

Add package `@types/node` to use nodejs in ts file

```bash
yarn add -D @types/node
```

file `vite.config.ts`

```ts
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import path from "path";

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  server: {
    port: 3000,
  },
  css: {
    devSourcemap: true,
  },
  resolve: {
    alias: {
      src: path.resolve(__dirname, "./src"),
    },
  },
});
```

### Cài extension và setup VS Code

Các Extension should add

- ESLint

- Prettier - Code formatter

- Tailwindcss

- EditorConfig for VS Code

VS Code `settings.json` config

- Turn on Format On Save
- Default Formatter is Prettier

## Code note

Remote special symbol on keyboard code

```ts
export const removeSpecialCharacter = (str: string) =>
  // eslint-disable-next-line no-useless-escape
  str.replace(
    /!|@|%|\^|\*|\(|\)|\+|\=|\<|\>|\?|\/|,|\.|\:|\;|\'|\"|\&|\#|\[|\]|~|\$|_|`|-|{|}|\||\\/g,
    ""
  );
```

Fix Tailwindcss Extension not suggest

Add code into `settings.json` on VS Code

```json
{
  //...
  "tailwindCSS.experimental.classRegex": ["[a-zA-Z]*class[a-zA-Z]*='([^']+)'"]
}
```
