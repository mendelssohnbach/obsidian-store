#js 

インストール
```terminal
$ npm i --save-dev --save-exact @biomejs/biome
$ npx @biomejs/biome init
```

`package.json`
```json
  "scripts": {
    "dev": "vite",
    "build": "tsc -b && vite build",
    "preview": "vite preview",
    "format-check": "biome format ./src",
    "format": "biome format --write ./src",
    "lint-check": "biome lint ./src",
    "lint": "biome lint --write ./src",
    "biome:all": "npm run format && npm run lint"
  },
```

