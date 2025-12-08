# state とは

コンポーネントごとに保持・管理される値

# useState

useState の set 関数を呼び出すと関数コンポーネント自体も呼び出される

# state 内の配列の更新

公式
https://ja.react.dev/learn/updating-arrays-in-state

b13o
https://b13o.com/books/simple-memo-app/5.implement-memo-creation-form

React は、state に格納する配列やオブジェクトを、イミュータブル（immutable, 不変性, 書き換え不能）なものとして扱う
なので、、リストや、オブジェクトの中身の値を、直接変更してはいけない
もし、変更されても、再レンダリングは起きない
元の配列を変更するのではなく、新しい配列を作成するアプローチで、状態を変化させる

```
// 直感的な操作
setState(list.push(item));

// React での操作
setState([item, ...list]);
```

## state 使用上の注意

下記+ボタン押した場合、コンソールログには 0 が表示され、画面上の現在のカウント数には 1 が表示される
setCount はステートの値を更新してくださいと指示を出すだけで、関数コンポーネントの実行が完了、サイレンダリングされるときに反映される。
要するに setXX は非同期で行われる。関数コンポーネントの実行が完了、サイレンダリングされるときに反映される。

```
const Example = () => {
  const [count, setCount] = useState(0);
  const handlerIncrement = () => {
    // setCount((prevCount) => prevCount + 1);
    setCount(count + 1);
    setCount(count + 1);
    console.log(count);
  };
  const handlerDecrement = () => {
    setCount((prevCount) => prevCount - 1);
  };
  return (
    <>
      <p>現在のカウント数: {count}回</p>
      <button onClick={() => handlerIncrement()}>+</button>
      <button onClick={() => handlerDecrement()}>-</button>
    </>
  );
};
```

ただし、前回更新した値を取得することができる関数がある
名前はなんでもよく setXX に関数を渡す。prevstate
下記+ボタン押した場合、コンソールログには 0 が表示され、画面上の現在のカウント数には 3 が表示される

```
  const handlerIncrement = () => {
    // setCount(count + 1);
    // setCount(count + 1);

    setCount(count + 1);
    setCount((prevstate) => {
      return prevstate + 1;
    });
    // 省略形
    setCount((prevstate) => prevstate + 1);
    console.log(count);
  };
```

最終形

```
  const hanldeIncrement = () => {
    // setCount((prevCount) => prevCount + 1);
    setCount((prevCount) => prevCount + 1);
  };
  const hanldeDecrement = () => {
    // setCount((prevCount) => prevCount - 1);
    setCount((prevCount) => prevCount - 1);
  };
```

## state 使用上の注意 オブジェクト型

オブジェクト型の state の場合、更新する際は、
オブジェクトの構造と同じ構造で更新する必要がある

```
const Example = () => {
  const personObj = { name: "Tom", age: 18 };
  const [person, setPerson] = useState(personObj);

  const handlerNameChange = (e) => {
    setPerson({
      name: e.target.value,  // ←★画面入力値をセット
      age: person.age,  // ←★もとの値をセット
    });
  };

  const handleReset = () => {
    setPerson({
      name: "",
      age: "",
    });
  };

  return (
    <>
      {person.name} - {person.age}
      <input type="text" value={person.name} onChange={handlerNameChange} />
      <input type="text" value={person.age} />
      <button onClick={handleReset}>リセット</button>
    </>
  );
};
```

## state 使用上の注意 オブジェクト型 さらに

オブジェクト型の state を更新する場合は、新しいオブジェクトを渡す必要がある
元設定していたものと別のオブジェクト

上記の書き方だとプロパティが多い場合、大変。
その場合、スプレット演算子を使う

元のオブジェクトが展開されて、新しいオブジェクトを作ってくれる
スレッド演算子で展開された値を上書きする場合、
スレッド演算子の後に、カンマで区切ってプロパティと値を記述

```
  const handlerNameChange = (e) => {
    //     setPerson({
    //       name: e.target.value,
    //       age: person.age,
    //     });
    setPerson({...person, name: e.target.value});
  };
```

## state 使用上の注意 オブジェクト型 さらに

このままでもいいが
元の値を使う場合はコールバック関数を使うとよりよいとか、、

コールバック関数で書き換えた実装

```
const Example = () => {
  const orderObj = { item: "apple", count: 10 };
  const [order, setOrder] = useState(orderObj);
  const changeItem = (e) => {
    // setOrder({ ...order, item: e.target.value });
    setOrder((order) => ({ ...order, item: e.target.value }));
  };
  const countUp = () => {
    // setOrder({ ...order, count: order.count + 1 });
    setOrder((order) => ({ ...order, count: order.count + 1 }));
  };
  const countDown = () => {
    // setOrder({ ...order, count: order.count - 1 });
    setOrder((order) => ({ ...order, count: order.count - 1 }));
  };
```

**()をつける理由**
setOrder((order) => **(**{ ...order, count: order.count - 1 }**)**);

javascript のエンジンがオブジェクトリテラルの波括弧なのかアロー関数の波括弧なのかわからないなので、
**オブジェクトを返す場合は、()括弧をつける**
