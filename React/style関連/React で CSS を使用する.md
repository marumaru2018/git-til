# React で CSS を使用する

## タグに直接スタイルを記述する

css の定義をキャメルケースで記述する

```
<h1 style={{fontFamily:'Meiryo', fontSize:'20px'}}>Hello World</h1>
```

## class タグを使用する

従来は class タグだが、React の場合 className とする。
通常の css ファイルは以下のようにインポートして使用する。

```
import "./Example.css";

const Example = () => {
  return (
    <div className="component">
      <h3>Hello Component</h3>
    </div>
  );
};

export default Example;
```

- クラスの定義
  Example.css
  ※従来通りの書き方

```
.component {
  padding: 1rem;
  color: black;
  border: 5px solid green;
}

```
