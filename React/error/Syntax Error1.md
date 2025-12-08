# エラー

[plugin:vite:react-swc] × Expected ',', got ':'
╭─[C:/dev/learn/React/react-guide-material/05_state_and_event/src/060_state_object/start/Example.jsx:13:1]
10 │ name: e.target.value,
11 │ age: person.age,
12 │ });
13 │ setPerson(...person, name: e.target.value);
· ─
14 │ };
15 │
16 │ const handleReset = () => {
╰────

Caused by:
Syntax Error
C:/dev/learn/React/react-guide-material/05_state_and_event/src/060_state_object/start/Example.jsx

## 対処

修正前コード

```
  const handlerNameChange = (e) => {
    // person.name = e.target.value;
    setPerson({
      name: e.target.value,
      age: person.age,
    });
    setPerson(...person, name: e.target.value);

  };
```

修正後コード
オブジェクト形式になっていなかった

```
//    setPerson(...person, name: e.target.value);
    setPerson({ ...person, name: e.target.value });
```
