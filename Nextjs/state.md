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
