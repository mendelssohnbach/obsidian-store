#js 

`package.json`
```json
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint",
    "codegen": "npx playwright codegen http://localhost:3000",
    "test:ui": "npx playwright test --ui"
  },
```

eslint-plugin
```terminal
$ npm install -D eslint-plugin-playwright
```

`.eslintrc.json`
```json
{
  "extends": ["next/core-web-vitals", "next/typescript"],
  "overrides": [
    {
      "files": "tests/**",
      "extends": "plugin:playwright/recommended"
    }
  ],
  "playwright/no-raw-locators": [
    "error",
    {
      "allowed": ["iframe", "[aria-busy='false']"]
    }
  ]
}
```

不安定なテストを除外したすべてのテストを行う
```terminal
$ npx playwright test --grep-invert @unsatisfactory
```

`@unsatisfactory` をコードに追加する必要がある
```typescript
import { test, expect } from '@playwright/test';

test('flakey test', {
  tag: '@unsatisfactory',
}, async ({ page }) => {
  // ...
});

test('solid test', async ({ page }) => {
  // ...
});
```

