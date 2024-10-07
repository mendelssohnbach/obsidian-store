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
  { languageOptions: { globals: globals.browser } },
  pluginJs.configs.recommended,

  {
    rules: {
      "no-eval": ["error"],
    },
  },
];
```

`package.json`
```json
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "lint": "eslint src/**/*.js"
  },
```

