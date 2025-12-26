## Error Type

Runtime Error

## Error Message

Event handlers cannot be passed to Client Component props.
<... onClick={function handleButtonClick} label=...>
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
If you need interactivity, consider converting part of this to a Client Component.

    at stringify (<anonymous>:1:18)
    at stringify (<anonymous>:1:18)

Next.js version: 16.1.1 (Turbopack)

## 原因

ClickButton コンポーネントがクライアントコンポーネントの指定がないため、サーバーコンポーネントとして扱われています。

解決方法：ClickButton コンポーネントに 'use client' を追加

Next.js App Router のルール：

デフォルトでは全てのコンポーネントがサーバーコンポーネント
onClick などのイベントハンドラーやブラウザ API を使う場合は 'use client' が必要
サーバーコンポーネントからクライアントコンポーネントにはシリアライズ可能な props（文字列、数値など）のみ渡せる
これでエラーが解消されるはずです。
