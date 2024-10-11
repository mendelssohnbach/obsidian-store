#js 

インストール
```terminal
$ npm init @eslint/config@latest
```

`eslint.config.mjs`
```javascript
import globals from "globals";
import pluginJs from "@eslint/js";


  export default [
  {
    files: ['**/*.{js,mjs,cjs,ts,jsx,tsx}'],
    rules: {
      'no-eval': ['error'],
    },
  },
  { languageOptions: { parserOptions: { ecmaFeatures: { jsx: true } } } },
  { languageOptions: { globals: globals.browser } },
  pluginJs.configs.recommended,
  ...
];

// 最後に追加するパターン
  pluginReact.configs.flat.recommended,
  {
    rules: {
      "no-eval": ["error"]
    }
  }
];
```

`package.json`
```json
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "lint": "eslint src/**/*.js"
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

