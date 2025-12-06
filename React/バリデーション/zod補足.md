```
export const schema = z.object({
  dept: z.string().optional(),
  section: z.string().optional(),
  username: z
    .string()
    .regex(/^[^ -~｡-ﾟ]*$/, "全角で入力してください")
    .max(10, "10文字以内で入力してください"),
  email: z.string().optional(),
});
```

## 上記コードの解説

email: z.string().optional() は Zod のバリデーションスキーマで、以下の意味を持ちます:

z.string(): 値が文字列型であることを要求
.optional(): このフィールドは省略可能（未入力でも OK）
つまり、email フィールドは:

入力された場合は文字列でなければならない
入力されなくても（空でも）エラーにならない
undefined の値を許容する
もし何も制約をつけない場合、フィールドは必須となり、空の状態でフォーム送信するとエラーになります。.optional() をつけることで、任意入力のフィールドとして扱われます。

この順序により:

まず文字列型のバリデーションルール（regex, max）を定義
最後に .optional() で「このフィールド全体が省略可能」と指定
こうすることで、値が入力された場合のみバリデーションが実行され、未入力の場合はバリデーションをスキップします。

username: z
.string()
.regex(/^[^ -~｡-ﾟ]\*$/, "全角で入力してください")
.max(10, "10 文字以内で入力してください")
.optional(),

## バリデーションのタイミングを変える

上記のコードは、ユーザーフィールドに文字入力するだけでバリデーションが動いています。これはなぜですか？

React Hook Form のデフォルト動作により、最初のフォーム送信後は入力中（onChange イベント）にリアルタイムでバリデーションが実行されます。

**onSubmit の時だけバリデーションを動かすには**

React Hook Form のデフォルト動作により、**最初のフォーム送信後**は入力中（`onChange`イベント）にリアルタイムでバリデーションが実行されます。

具体的な動作:

1. **初回（送信前）**: 入力中はバリデーションされない
2. **検索ボタンを一度押す**: フォーム送信時にバリデーション実行
3. **送信後**: 入力するたびにリアルタイムでバリデーションが実行される

これは `useForm` の `mode` オプションのデフォルト設定によるものです。現在は暗黙的に以下の設定になっています:

```typescript
const formContext = useForm<FormValues>({
  mode: "onSubmit", // デフォルト: 初回は送信時のみ
  reValidateMode: "onChange", // デフォルト: 送信後は入力時に再検証
  resolver: zodResolver(schema),
  // ...
});
```

**常に入力時にバリデーションしたい場合**:

```typescript
mode: "onChange"; // 常に入力時
```

**送信時のみバリデーションしたい場合**:

```typescript
mode: "onSubmit",
reValidateMode: "onSubmit"  // 送信後も送信時のみ
```

```
// Form 定義
type FormValues = z.infer<typeof schema>;
const formContext = useForm<FormValues>({
resolver: zodResolver(schema),
defaultValues: {
dept: "",
section: "",
username: "",
email: "",
},
// ↓ 送信時のみバリデーションしたい場合
mode: "onSubmit",
reValidateMode: "onSubmit", // 送信後も送信時のみ
// ↑ 送信時のみバリデーションしたい場合
});
```
