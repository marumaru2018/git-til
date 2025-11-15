# Next.js エラー集

## Failed to construct 'URL': Invalid URL

```
app\page.tsx (56:15) @ <anonymous>

  54 |           return (
  55 |             <Link href={`/item/read/${item.id}`} key={item.id}>
> 56 |               <Image
     |               ^
  57 |                 src={item.image}
```

## 原因と対応

データベースから取得した item.image の値が相対パス（例：img3.jpg）になっているようです。
Next.js の Image コンポーネントでは、相対パスの画像は/で始まる必要があります。
