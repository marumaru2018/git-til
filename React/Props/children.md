## Props応用

children props
コンポーネントのタグの間に記述された内容を受け取る、特別な props
以下のようなコードであれば
<Layout>

<h1>ようこそ</h1>
<p>ポートフォリオサイトです</p>
</Layout>

**Layoutの間に書かれたタグをまとめてchildrenというpropsで引き取れる**

childrenというpropsを使用して、コンポーネントに子コンポーネントを埋め込むことができる。

```
// レイアウトコンポーネント
function Layout({ children }) {
    return (
        <div className="layout">
            <Header />
            <main className="content">{children}</main>
            <Footer />
        </div>
    );
}
```

```
// 使用例
function App() {
    return (
        <Layout>
            <h1>ようこそ</h1>
            <p>ポートフォリオサイトです</p>
        </Layout>
    );
}
```
