#css

環境設定
```terminal
$ npm install -D tailwindcss postcss autoprefixer
$ npx tailwindcss init -p
```

`tailwind.config.js`
```javaScript
content: ['./index.html', './src/**/*.{js,ts,jsx,tsx}'],
```

`./src/index.css`
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

`src/App.jsx`
```JavaScript
function App() {
  return <h1 className="text-3xl font-bold underline">Hello world!</h1>;
}

export default App;
```

