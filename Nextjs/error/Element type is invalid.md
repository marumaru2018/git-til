Runtime Error

Element type is invalid: expected a string (for built-in components) or a class/function (for composite components) but got: undefined. You likely forgot to export your component from the file it's defined in, or you might have mixed up default and named imports.

Check the render method of `StorePage`.

src\app\store\page.tsx (8:7) @ StorePage

6 | <div>
7 | <h1>Store Page</h1>

> 8 | <GetStore />

     |       ^

9 | <SetStore />
10 | </div>
11 | );
Call Stack
16

Show 15 ignore-listed frame(s)
StorePage
src\app\store\page.tsx (8:7)

## 原因と対応

GetStore と SetStore コンポーネントが存在しないか、正しくエクスポートされていない可能性があります。
今回の場合
コンポーネントは存在しますが、GetStore に"use client"ディレクティブがありません。Zustand のストアを使用するコンポーネントはクライアントコンポーネントである必要があります。
