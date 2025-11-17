Runtime Error

Invalid hook call. Hooks can only be called inside of the body of a function component. This could happen for one of the following reasons:

1. You might have mismatching versions of React and the renderer (such as React DOM)
2. You might be breaking the Rules of Hooks
3. You might have more than one copy of React in the same app
   See https://react.dev/link/invalid-hook-call for tips about how to debug and fix this problem.
   app/item/update/[id]/page.tsx (49:29) @ handleSubmit

47 | const handleSubmit = async (e: React.FormEvent) => {
48 | e.preventDefault();

> 49 | const router = useRouter();

     |                             ^

50 | try {
51 | const params = await context.params;
52 | const id = params.id;
Call Stack
12

Show 11 ignore-listed frame(s)
handleSubmit
app/item/update/[id]/page.tsx (49:29)

## 訳

フック呼び出しが無効です。フックは関数コンポーネントの本体内でのみ呼び出すことができます。これは、次のいずれかの理由で発生する可能性があります。1. React とレンダラー（React DOM など）のバージョンが一致していない可能性があります。2. フックのルールに違反している可能性があります。3. 同じアプリ内に React のコピーが複数存在する可能性があります。https をご覧ください。

## 原因と対応

フックは関数コンポーネントでないと使えない
