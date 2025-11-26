# イベント操作

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
