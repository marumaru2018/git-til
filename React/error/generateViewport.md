エラー

## Error Type

Runtime Error

## Error Message

Attempted to call generateViewport() from the server but generateViewport is on the client. It's not possible to invoke a client function from the server, it can only be rendered as a Component or passed to props of a Client Component.

Next.js version: 15.5.9 (Webpack)

対応
コンポーネントの export default が抜けている場合に
発生する。
export default StorePage;

修正方法：
以下を追加
export default StorePage;
