#js 

レガシースタイル
```terminal
$ npm init @eslint/config@latest
```

インストール
```terminal
$ $ npm i -D eslint@8.57.0 eslint-config-next eslint-config-prettier eslint-plugin-tailwindcss eslint-plugin-unused-imports @typescript-eslint/parser
$ npm i -D prettier @ianvs/prettier-plugin-sort-imports prettier-plugin-tailwindcss
```

`.eslintrc.json`
```json
{
  "parser": "@typescript-eslint/parser","env
  "parserOptions": {
    "ecmaVersion": 2021,
    "sourceType": "module",
    "ecmaFeatures": {
      "jsx": true
    }
  },
  "plugins": ["tailwindcss", "unused-imports"],
  "root": true,
  "extends": [
    "next/core-web-vitals",
    "next/typescript",
    "prettier",
    "plugin:tailwindcss/recommended"
  ],
  "rules": {
    "tailwindcss/no-custom-classname": "off",
    "unused-imports/no-unused-imports": "warn",
    "unused-imports/no-unused-vars": "warn",
    "@typescript-eslint/no-unused-vars": "warn",
    "react/jsx-uses-react": "off",
    "react/react-in-jsx-scope": "off",
  },
  "settings": {
    "tailwindcss": {
      "callees": ["cn"],
      "config": "./tailwind.config.ts"
    },
    "next": {
      "rootDir": ["./src/"]
    }
  },
  "ignorePatterns": ["node_modules/", ".next/", "assets/", "public/"]
}
```

`.prettierrc.json`
```json
{
  "arrowParens": "always",
  "bracketSameLine": false,
  "bracketSpacing": true,
  "embeddedLanguageFormatting": "auto",
  "htmlWhitespaceSensitivity": "css",
  "insertPragma": false,
  "jsxSingleQuote": false,
  "printWidth": 100,
  "proseWrap": "preserve",
  "quoteProps": "as-needed",
  "requirePragma": false,
  "semi": true,
  "singleAttributePerLine": true,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5",
  "useTabs": false,
  "tailwindConfig": "./tailwind.config.ts",
  "plugins": ["@ianvs/prettier-plugin-sort-imports", "prettier-plugin-tailwindcss"]
}
```

`package.json`
```json
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint",
    "format": "prettier --write './src/**/*.{ts,tsx}'",
    "lint:fix": "next lint --fix && format"
  },
```

a11y

```terminal
$ npm install eslint-plugin-jsx-a11y --save-dev
```

`eslint.config.js`
```javascript
...
import jsxA11y from 'eslint-plugin-jsx-a11y';


export default [
  {
    files: ['**/*.{js,mjs,cjs,ts,jsx,tsx}'],
    settings: {
      react: {
        version: 'detect',
      },
    },
  },
  { languageOptions: { parserOptions: { ecmaFeatures: { jsx: true } } } },
  { languageOptions: { globals: globals.browser } },
  ...
  jsxA11y.flatConfigs.recommended,
];
```

json/markdown
インストール
```terminal
$ npm install @eslint/json -D
$ npm install @eslint/markdown -D
```

`eslint.config.mjs`
```JavaScript
import json from "@eslint/json";
import markdown from "@eslint/markdown";

export default [
  {  // lint JSON files
    files: ["**/*.json"],
    language: "json/json",
    ...json.configs.recommended,
  },

  { // lint Markdown files
    files: ["**/*.md"],
    plugins: {
      markdown
    },
    language: "markdown/gmf",
    rules: {
      "markdown/no-html": "error"
    }
  },
  ...markdown.configs.recommended,
];
```

## ルール: utf-8

`eslint.config.js`
**fs.readFile** の **encoding** 引数にて `utf8` 表記を **Error** として扱う
```
  {
    rules: {
      'no-restricted-syntax': [
        'error', // 'error' または 'warn' に設定
        {
          selector: `CallExpression[callee.object.name='fs'][callee.property.name='readFile'] > ObjectExpression > Property[key.name='encoding'][value.value='utf8']`,
          message: "Use 'utf-8' instead of 'utf8' for fs.readFile encoding.",
        },
      ],
    },
  },
```