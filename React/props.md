# コンポーネント間でデータを渡すには Props を使用

## 使い方

### 渡す側

JSX の属性値の記法

```
<Welcome name="太郎" age={25} />
```

### 受け取り側

```
// Propsの型を定義する
type Props = {
  name: string,
  age: number
};
// 第一引数でオブジェクトとしてPropsを受け取る
export const Welcome = ({name, age}: Props) => {
  return <h1>私の名前は {name} です。 年齢は{age.toString()}歳です。</h1>;
}
```

Props が増えすぎると処理が複雑になりコードの可読性も低下します。
また、コンポーネント間の依存度が高くなりコンポーネント単体でのテスト実施が難しくなります。
取得したデータを表示するようなパターンであれば、まずは親コンポーネントで取得した
データを子コンポーネントに渡すのではなく、子コンポーネント側でデータを取得する形にして
Props を使用しない形で対応できないかを検討しましょう。
どうしても親コンポーネント側でデータを管理する必要がある場合のみ
Props でデータを渡すようにするのが望ましいです。

## 名前を変える

```
// const Child = (props: ChildProps) => {
const Child = ({ color: c = "green" }: ChildProps) => {
  // const { color } = props;
  return (
    <div className="component">
      {/* <h3>Hello Component color={color}</h3> */}
      <h3>Hello Component color={c}</h3>
    </div>
  );
};
```

# props ではすべてのデータ型を渡せる

親

```
  const fn = (arg) => {
    return `hogehoge${arg}`;
  };

  return (
    <>
      <Child
        color="red"
        num={10}
        fn={fn("props")}
        bool
        obj={{ name: "John", age: 30 }}
      />
```

子

```
type ChildProps = {
  color: String;
  num: number;
  fn: String;
  bool: boolean;
  obj: { name: string; age: number };
};

// const Child = (props: ChildProps) => {
const Child = ({ color: c = "green", num, fn, bool, obj }: ChildProps) => {
  // const { color } = props;
  console.log(c, num, fn, bool, obj);
  return (
    <div className="component">
      {/* <h3>Hello Component color={color}</h3> */}
      <h3>Hello Component color={c}</h3>
      <p>Number: {num}</p>
      <p>Function result: {fn}</p>
      <p>Boolean: {bool}</p>
      <p>
        Name: {obj?.name}, Age: {obj?.age}
      </p>
    </div>
  );
};
```

## 以下の書き方でオブジェクトを展開できる(スプレッド演算子)

itemobj のようにオブジェクトに値が入っていて、わざわざ分けて props に渡すのがめんどくさい場合など以下のようにかける

```
  const fn = (arg) => {
    return `hogehoge${arg}`;
  };
  const itemobj = { color: "pink", num: 10000 };

  return (
    <>
      <Child
        // color="red"
        // num={10}
        {...itemobj}
        fn={fn("props")}
        bool
        obj={{ name: "John", age: 30 }}
      />
```

## props の重要なルール

- props の流れは一方通行（親 ⇒ 子）
  コンポーネント間で共通の変数を使用する場合は親コンポーネントに定義する

- props は読み取り専用
  props は読み取り専用のオブジェクトなので値を書き換えることはできない
