#js 

インストール
```terminal
$ mkdir DIR && cd $_
$ npm init -y
$ npm i typescript ts-node nodemon @types/node -D
$ npx tsc -v
Version 5.6.3
$ npx tsc --init --rootDir src --outDir dist --esModuleInterop --resolveJsonModule --lib es6,dom --module commonjs
? strict true ?
$ mkdir src
$ touch src/index.ts
```

`package.json`
```json
"scripts": {
    "start": "npm run build:live",
    "build": "tsc -p .",
    "build:live": "nodemon --watch 'src/**/*.ts' --exec \"ts-node\" src/*.ts",
    "check": "tsc --noEmit",
    "check:live": "tsc --noEmit --watch"
  },
```

トランスパイル
```terminal
$ npm run start
$ npm run build // build js file
```

Node.jsによる実験的サポート
```terminal
実験的サポート
$ node --experimental-strip-types example.ts
実験的サポート with enum
$ node --experimental-strip-types --experimental-transform-types another-example.ts
```

