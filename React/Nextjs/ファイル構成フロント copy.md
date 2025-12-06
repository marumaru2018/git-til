# Next.js ファイル構成

## ファイル構成

- ページは app フォルダに格納する

- アプリケーションのホームページ
  src/app/page.tsx

- ページ間共通のレイアウト
  src/app/layout.tsx

- 通常ページ
  app/about/page.tsx ファイルを作成すると、/about という URL でアクセスできる

## ページ間の遷移

- `<Link>`を使用

```
      <Link href="/about">
        Aboutページへ
      </Link>
```

**普通の HTML の`<a>`タグとの違いは、Link コンポーネントを使うことで、ページ遷移時にページの再読み込みが発生しない**
