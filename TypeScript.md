#js 

インストール
```terminal
$ mkdir DIR && cd $_
$ npm init -y
$ npm i typescript -D
$ npx tsc
Version 5.6.3
tsc: The TypeScript Compiler - Version 5.6.3
$ npx tsc --init --rootDir src --outDir dist --esModuleInterop --resolveJsonModule --lib es6,dom --module commonjs
```

コンパイル
```terminal
$ npx tsc index.ts
$ node index.js
```
