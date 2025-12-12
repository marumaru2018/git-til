# useQuery

## 通常のフェッチ

const fetchUserData = async () => {
const res = await fetch(`/users/${userId}`);
return res.json();
};

## useQuery を使用した実装

@tanstack/react-query から useQuery をインポート
useQuery フックでユーザー情報を取得（queryKey と queryFn を定義）
取得したデータ（userData）をフォームの初期値に設定
データ読み込み中の状態（isLoading）も取得可能
この実装により、React Query のキャッシュ機能や自動再取得などの恩恵を受けられます。

```
  const { data: userData, isLoading } = useQuery({
    queryKey: ["user", userId],
    queryFn: async () => {
      const res = await fetch(`/users/${userId}`);
      return res.json();
    },
  });
```

queryKey は React Query でクエリを識別するためのユニークなキーです。

主な役割：

キャッシュ管理 - 同じ queryKey でデータをキャッシュし、再利用します
自動再取得 - 同じキーのクエリが複数の場所で使われても、1 回だけフェッチされます
無効化・更新 - queryKey を指定してキャッシュを無効化し、データを再取得できます

React Query が適切なタイミングで管理してくれます。これが従来の useEffect 内での手動フェッチと比べた大きな利点です。
