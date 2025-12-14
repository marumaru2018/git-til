# ステートの受け渡し

Example コンポーネント内で現在のカウントの値を管理する state を一つ定義
カウントの更新（CountUpdate）と表示（CountResult）を別のコンポーネントに分離する

```
import { useState } from "react";

const Example = () => {
  const [count, setCount] = useState(0);
  return (
    <>
      <h3>練習問題</h3>
      {/* このコメントアウトを外して利用！
        <CountResult title="カウント" />
        <CountUpdate />
      */}
      <CountResult title="カウント" count={count} />
      <CountUpdate setCount={setCount} />
    </>
  );
};
const CountResult = ({ title, count } /* propsを定義 */) => (
  <h3>
    {title}:{count}
    {/* propsのtitleとcountの値を表示 */}
  </h3>
);

const CountUpdate = ({ setCount } /* propsを定義 */) => {
  const countUp = () => {
    /* countに1追加 */
    setCount((prevCount) => prevCount + 1);
  };
  const countDown = () => {
    /* countから1マイナス */
    setCount((prevCount) => prevCount - 1);
  };
  return (
    <>
      <button onClick={countUp}>+</button>
      <button onClick={countDown}>-</button>
    </>
  );
};

export default Example;
```
