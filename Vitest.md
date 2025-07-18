#js

## 最小限の環境
インストール
```
$ npm i -D vitest @vitest/coverage-v8 @types/node
```

関数ファイル内にテストを書く
```
export function add(a: number, b: number): number {
  return a + b;
}

// *** Test ***
import { expect, test } from 'vitest';
if (process.env.NODE_ENV === 'test') {
  test('1+1=2', () => {
    expect(add(1, 1)).toBe(2);
  });
}
```
## vite + TypeScript + SWC
[Vitest導入ガイド](https://sakublog.tech/tips/vitest-react-setup/)
インストール
```terminal
$ npm create vite@latest
$ cd <PROJECT_DIR>
$ npm i
$ npm install -D @testing-library/jest-dom @testing-library/react @testing-library/user-event @vitest/coverage-v8 happy-dom vitest vite-tsconfig-paths @vitest/eslint-plugin
```

ブラウザモード
```terminal
$ npx vitest init browser
```

`vitest-setup.ts`
```typescript
import "@testing-library/jest-dom/vitest";
import { cleanup } from "@testing-library/react";
import { afterEach } from "vitest";

afterEach(() => {
  cleanup();
});
```

`vite.config.ts`
```typescript
/// <reference types="vitest" />
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react-swc";
import tsconfigPaths from "vite-tsconfig-paths";

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react(), tsconfigPaths()],
  test: {
    globals: true,
    environment: "happy-dom",
    setupFiles: ["./vitest-setup.ts"],
    // テストパターン
    include: ['src/**/*.test.ts', 'src/**/*.test.tsx'],
  },
}); 
```

`eslint.config.ts`
```typescript
import js from '@eslint/js';
import vitest from '@vitest/eslint-plugin';
import reactHooks from 'eslint-plugin-react-hooks';
import reactRefresh from 'eslint-plugin-react-refresh';
import globals from 'globals';
import tseslint from 'typescript-eslint';

export default tseslint.config(
  { ignores: ['dist'] },
  {
    extends: [js.configs.recommended, ...tseslint.configs.recommended],
    files: ['**/*.{ts,tsx}'],
    languageOptions: {
      ecmaVersion: 2020,
      globals: globals.browser,
    },
    plugins: {
      'react-hooks': reactHooks,
      'react-refresh': reactRefresh,
      vitest,
    },
    rules: {
      ...reactHooks.configs.recommended.rules,
      ...vitest.configs.recommended.rules,
      'react-refresh/only-export-components': ['warn', { allowConstantExport: true }],
    },
  }
);
```

`tsconfig.app.json`
```json
{
  "compilerOptions": {
    "composite": true,
    "tsBuildInfoFile":          "./node_modules/.tmp/tsconfig.app.tsbuildinfo",
    "target": "ES2020",
    "useDefineForClassFields": true,
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "module": "ESNext",
    "skipLibCheck": true,
    "types": ["vitest/globals", "vitest", "@testing-library/jest-dom"],// 追記1
    "baseUrl": "./",// 追記2
    "paths": {
      "@/*": ["src/*"],
    },

    /* Bundler mode */
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "moduleDetection": "force",
    "noEmit": true,
    "jsx": "react-jsx",

    /* Linting */
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true
  },
  "include": ["src","vitest-setup.ts"]// 追記3
} 
```

`package.json`
```json
  "scripts": {
    "dev": "vite",
    "build": "tsc -b && vite build",
    "lint": "eslint . --config ./eslint.config.js --report-unused-disable-directives --max-warnings 0",
    "preview": "vite preview",
    "test": "vitest",
    "coverage": "vitest run --coverage",
    "typecheck": "vitest --typecheck",
    "test:browser": "vitest --workspace=vitest.workspace.ts"
  }, 
```

`vitest.workspace.ts`
```typescript
import { defineWorkspace } from 'vitest/config';

export default defineWorkspace([
  // If you want to keep running your existing tests in Node.js, uncomment the next line.
  // 'vite.config.ts',
  {
    extends: 'vite.config.ts',
    test: {
      include: ['src/**/*.browser.test.tsx'],
      browser: {
        enabled: true,
        name: 'chrome',
        provider: 'preview',
      },
    },
  },
]);
```

テストファイル雛形
```TypeScript
import { render, screen } from '@testing-library/react';
import { expect, test } from 'vitest';
```