# React で CSS を使用する

## タグに直接スタイルを記述する

css の定義をキャメルケースで記述する

```
<h1 style={{fontFamily:'Meiryo', fontSize:'20px'}}>Hello World</h1>
```

## Material-UI

sx={{***}}という記述でスタイルを指定

```
<Button variant="contained" sx={{fontWeight:'bold'}}>ボタン</Button>
```

## CSS ライブラリ

- Emotion
  CSS ライブラリの一つに Emotion がある

```
npm install @emotion/css
```

Emotion のインストール完了後プロジェクトルートにある tsconfig.json ファイルを開き
compilerOptions の設定として以下を追記し保存します。

```
"compilerOptions": {
    (省略)
    "jsxImportSource": "@emotion/react",　// 追加
    "types": ["@emotion/react/types/css-prop"],　//　追加
  },
```

Emotion を使用する事で CSS 定義をファイルとしてまとめる事が可能です。
スタイル定義を画面コンポーネントとは別ファイルで管理することで画面やコンポーネントのサイズが肥大化する事を避ける事ができます。

使用する際は @emotion/react から css を import して
CSS を定義したオブジェクトを右のように作成します。

export を付ける事で他の画面やコンポーネントから
CSS 定義を読み込めるようにします。

CSS の定義方法が２種類あり
１つ目の css()で指定する方法の場合、CSS 定義はキャメルケースで行います。予測変換などが使用可能です。

２つ目の css``（バッククォート）で指定する場合は、キャメルケースではなく通常の記述方法で OK です。

```
import { css } from "@emotion/react";

export const styles = {
  Title: css({
    fontFamily: 'メイリオ',
    color: 'red',
  }),
  Button: css`
    background:darkblue;
    color:#FFF;
    width:120px;
    height:40px;
    font-weight:bold;
    margin:5px;
  `,
};
```
