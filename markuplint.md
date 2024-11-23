#js 

インストール
```terminal
$ npm i -D markuplint
$ npx markuplint --init
$ npm i -D @markuplint/react-spec @markuplint/jsx-parser
```

`.markuplintrc`
```text
  "extends": [
    "markuplint:recommended-react"
  ],
  "parser": {
    ".[jt]sx$": "@markuplint/jsx-parser"
  },
  "specs": {
    ".[jt]sx$": "@markuplint/react-spec"
  }
```

`package.json`
```JSON
  "scripts": {
    ...
    "markuplint": "markuplint \"./src/**/*.{jsx,tsx}\"",
    "markuplint:fix": "markuplint \"./src/**/*.{jsx,tsx}\" --fix"
```

