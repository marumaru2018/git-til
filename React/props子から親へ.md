# 子から親へ値を受け渡す

親コンポーネント側でテキストボックスの入力値を管理するステートを定義します
次にステートに値をセットする関数を作り子コンポーネントに props で渡します
子コンポーネント側ではこの関数を受け取ってテキストボックスの onChange イベントで実行します
親コンポーネントで定義したステートを更新する関数を子コンポーネント側で呼び出す事で子コンポーネントで入力した値を親コンポーネントのステートで管理できます

子

```
import { Button } from "@mui/material";
import { TextField } from "@mui/material";
import React, { useState } from "react";
type ChildComponentProps = {
  updText: (text: string) => void;
};
const ChildComponent = ({ updText }: ChildComponentProps) => {
  //   const [text, setText] = useState<string>("");
  // //   const handleOnChange = (e: React.ChangeEvent<HTMLInputElement>) => {
  //     console.log(e.target.value);
  //     setText(e.target.value);
  //   };

  return (
    <>
      <div>ChildComponent</div>
      <TextField onChange={(e) => updText(e.target.value)}></TextField>
      {/* <Button onClick={() => handleClick(text)}></Button> */}
    </>
  );
};
export default ChildComponent;
```

親

```
"use client";
import { Button } from "@mui/material";
import React, { useState } from "react";
import ChildComponent from "../_components/child";

const ParentPage = () => {
  const [parent, setParent] = useState<string>("");
  const updText = (text: string) => {
    setParent(text);
  };
  return (
    <>
      <div>ParentPage</div>
      <p>{parent}</p>
      <ChildComponent updText={updText} />
    </>
  );
};
export default ParentPage;
```
