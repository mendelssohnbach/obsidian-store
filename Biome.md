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
    "lint": "biome lint --write ./src/",
    "format": "biome format ./src/",
    "check": "biome check --write ./src/"
  },
```

`biome.json`
```json
{
  "$schema": "https://biomejs.dev/schemas/1.9.3/schema.json",
  "vcs": {
    "enabled": false,
    "clientKind": "git",
    "useIgnoreFile": false
  },
  "files": {
    "include": ["./*.js", "./*.mjs", "./*.ts", "./*.tsx", "./*.json"],
    "ignoreUnknown": false,
    "ignore": ["node_modules", "public", ".next"]
  },
  "formatter": {
    "enabled": true,
    "indentStyle": "space"
  },
  "organizeImports": {
    "enabled": true
  },
  "linter": {
    "enabled": true,
    "rules": {
      "recommended": true
    }
  },
  "javascript": {
    "formatter": {
      "quoteStyle": "single"
    }
  }
}
```



