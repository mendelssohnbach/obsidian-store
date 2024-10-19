#js
## vite + TypeScript + SWC
[Vitest導入ガイド](https://sakublog.tech/tips/vitest-react-setup/)
インストール
```typescript
$ npm create vite@latest
$ cd <PROJECT_DIR>
$ npm i
$ npm install -D @testing-library/jest-dom @testing-library/react @testing-library/user-event @vitest/coverage-v8 happy-dom vitest vite-tsconfig-paths
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
    environment: "happy-dom",
    setupFiles: ["./vitest-setup.ts"],
    globals: true,
  },
}); 
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
    "types": ["vitest/globals"],// 追記1
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
    "lint": "eslint . --ext ts,tsx --report-unused-disable-directives --max-warnings 0",
    "preview": "vite preview",
    "test": "vitest",
    "coverage": "vitest run --coverage"
  }, 
```