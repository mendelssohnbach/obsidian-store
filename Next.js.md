#js 

プロジェクトを作成
```terminal
$ npx create-next-app@latest
```

## 型

**React.ReactNode**
用途: `children` や柔軟に描画できる中身を受け取る
```TypeScript
type Props = {
  children: React.ReactNode;
};

export default function Layout({ children }: Props) {
  return <main>{children}</main>;
};
```

**React.JSX.Element**
用途: 1つの要素を返すことが確定しているとき
```
const Page = (): React.JSX.Element => {
  return <div>Hello World</div>
};
```

**React.FC**
用途: `children` を暗黙的に含む
```TypeScript
const Card: React.FC<{ title: string }> = ({ title, children }) => (
  <div>
    <h2>{title}</h2>
    {children}
  </div>
);
```

**React.ComponentProps**
用途: 既存コンポーネントやHTMLタグの `props型` を取得
```TypeScript
type ButtonProps = React.ComponentProps<'button'>;

const MyButton = (props: ButtonProps) => <button {...props} />;
```

**React.ComponentPropsWithoutRef
用途: `ref` を除いた `props型` を取得
```TypeScript
type InputWithRefProps = React.ComponentPropsWithRef<"input">;

const InputWithRef = React.forwardRef<HTMLInputElement, InputWithRefPfops>(
  (props, ref) => <input ref{ref} {...props} />
);
```

**React.FormEvent**
用途: フォーム送信などのフォーム全体のイベント型
```TypeScript
const handleSubmit = (e: React.FormEvent<HTMLFormElement>) => {
  e.preventDefault();
  console.log('送信);
};
```

**React.KeyboardEvent**
用途: キーボード操作のイベント型
```TypeScript
const handleKeyDown = (e: React.KeybordEvent<HTMLInputElement>) => {
  (e.key === 'Enter) {
    console.log('Enterが押された');
  };
};
```