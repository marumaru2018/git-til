# イベント操作

## イベントリスナとは

イベントが発生した際に実行したい関数を登録しておく場所のこと
クリック、値変更など

## クリックイベント

React で、ボタンクリックイベントなどを扱うために、onClick や onChange のように、まずキャメルケースでイベントの種類を指定する。

```
export function ProfileCard({
  name,
  nickname,
  bio,
  avatarUrl,
}: {
  name: string;
  nickname: string;
  bio?: string;
  avatarUrl: string;
}) {
  const handler = (name: string): void => {
    alert(`私の名前は${name}です。`);
  };
  return (
    // ボタンに関数を紐付けてください
    <button className="profile-card" onClick={() => handler({ name })}>

```

### メモ

以下の書き方だと JSX 作成時に実行され、クリックしなくても表示される
()があると関数自体が実行されてしまう

```
      <button onClick={clickHandler()}>Click me</button>
```

クリックした時に実行させるには

```
      <button onClick={clickHandler}>Click me</button>
```

もしくは、

```
      <button onClick={() => clickHandler()}>Click me</button>
```

↓ これは省略しない場合、以下のように書く。

```
      <button onClick={() => {clickHandler()}}>Click me</button>
```

## 入力値取得

```
import { useState } from "react";
const Example = () => {
  const [text, setText] = useState("");

        <label>
          入力値を取得：
          <input type="text"
          onChange={(e) => {
          setText(e.target.value);
          }}
          />
        </label>
```

以下の部分は、分割代入が使われている
const [text, setText] = useState("");

本来は、以下のよう書く
const valArry = useState("");

配列の 0 番目に参照用の値が渡ってくる
0 番目：参照用の値
1 番目：更新用の関数

参照する場合、以下のように書く
{valArry[0]}
