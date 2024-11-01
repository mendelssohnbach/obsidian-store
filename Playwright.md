#js 

```
$ npm init playwright@latest
```

`package.json`
```json
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint",
    "codegen": "playwright codegen http://localhost:3000",
    "test:ui": "playwright test --ui"
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

テストを行う
```terminal
// 不安定なテストを除外したすべてのテストを行う
$ npx playwright test --grep-invert @unsatisfactory
// 失敗したテストのみ実行
$ npx playwright test --last-failed
// 変更されたテストファイルのみ実行
$ npx playwright test --only-changed
// 2つのブランチを比較して異なるファイルを実行
$ npx playwright test --only-changed=main
// 同じテストを複数回実行
$ npx playwright test --repeat-each 100
// `test.only` が含まれている場合は失敗させる
$ npx playwright test --forbid-only
// UIモードと共にブラウザを開く
$ npx playwright test --ui --headed --workers 1
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

