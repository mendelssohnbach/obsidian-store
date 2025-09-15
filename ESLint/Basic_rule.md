#ESLint

`Enum` と `namespace` を禁止する

インストール
```Terminal
$ npm install --save-dev eslint @typescript-eslint/eslint-plugin @typescript-eslint/parser
```

`eslint.config.js`
```JavaScript
// eslint.config.js (Flat Config)
import js from '@eslint/js';
import tsEslintPlugin from '@typescript-eslint/eslint-plugin';
import tsParser from '@typescript-eslint/parser';

export default [
  js.configs.recommended,
  {
    files: ['**/*.ts', '**/*.tsx'],
    plugins: {
      '@typescript-eslint': tsEslintPlugin,
    },
    languageOptions: {
      parser: tsParser,
      parserOptions: {
        project: './tsconfig.json',
      },
    },
    rules: {
      'no-restricted-syntax': [
        'error',
        {
          // Enum の使用を禁止する
          selector: 'TSEnumDeclaration',
          message: 'Enums are not allowed. Use union types instead.',
        },
        {
          // namespace の使用を禁止するnp
          selector: 'TSModuleDeclaration',
          message: 'Namespaces are not allowed. Use ES Modules instead.',
        },
      ],
    },
  },
];
```