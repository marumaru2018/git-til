AWS MCP Server を導入してみる

その前に AWS MCP Server を使う場合、２つの利用方法があるとか

- 簡単に使いたい / AWS がホストするサーバーに接続したい → mcp-proxy-for-aws
- 閉域環境やローカルでサーバーを立ち上げたい → @modelcontextprotocol/server-aws

---

## 違い

| パッケージ                             | 役割                                                                                                                                                                          | 利用シーン                                                                                     |
| -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| **`mcp-proxy-for-aws`**                | MCP クライアント（VS Code Copilot, Cursor など）と AWS が提供する **マネージド MCP Server** をつなぐプロキシ。サーバーを自分で立てずに AWS の公式エンドポイントへ接続できる。 | 「簡単に試したい」「AWS がホストする MCP Server をそのまま使いたい」場合。導入が最もシンプル。 |
| **`@modelcontextprotocol/server-aws`** | AWS MCP Server の公式実装。ローカル環境や閉域ネットワークで MCP Server を直接立ち上げる。                                                                                     | セキュリティ要件が厳しく「自前でサーバーを管理したい」場合。Docker や npx で起動可能。         |

今回は **`mcp-proxy-for-aws`** → AWS が提供するマネージド MCP Server に接続する方式を選択

---

以下、導入手順は、Copilot の回答をもとに検証する形で進める。

## 🛠️ 導入手順（`mcp-proxy-for-aws` 利用）

### 1. 前提条件

- **AWS CLI** が設定済み（`aws configure` で認証情報を登録）
- **Node.js** と **uvx** が利用可能
- **MCP 対応クライアント**（VS Code Copilot, Cursor, Kiro CLI など）

---

### 2. 設定ファイルに MCP Server を登録

VS Code Copilot の場合は `~/.copilot/mcp.json` に以下を追加します。

⇒ 自分の環境は、~\AppData\Roaming\Code\User\mcp.json

~~Cursor の場合は `~/.cursor/mcp.json` に同様の設定を記述します。~~

```json
{
  "mcpServers": {
  "Servers": {　←自分の場合は、これ
    "aws-mcp": {
      "command": "uvx",
      "args": [
        "mcp-proxy-for-aws@latest",
        "https://aws-mcp.us-east-1.api.aws/mcp",
        "--metadata",
        "AWS_REGION=ap-northeast-1"
      ],
      "env": {
        "AWS_PROFILE": "default"
      }
    }
  }
}
```

- **command**: `uvx` を指定
- **args**: `mcp-proxy-for-aws@latest` と AWS MCP Server のエンドポイント
- **AWS_REGION**: 東京なら `ap-northeast-1`
- **AWS_PROFILE**: 利用する認証情報を設定

---

### 3. 動作確認

1. VS Code / Cursor を再起動
2. Copilot チャットで自然言語で AWS 操作を依頼  
   例:
   ```
   AWSに新しいS3バケットを作成して。名前はproject-logsで東京リージョンに。
   ```
   → MCP Server が API 呼び出しに変換し、S3 バケットを作成

---

### 4. 注意点

- **CloudTrail に必ず記録**されるため、IAM 権限は最小限に設計
- **プレビュー版**なのでリージョンや機能に制約あり
- MCP Server 自体は無料ですが、作成した AWS リソースには通常の料金が発生

---

📌 **まとめ**

- **`mcp-proxy-for-aws`** → AWS がホストする MCP Server に接続するためのプロキシ。導入が最も簡単。
- **`@modelcontextprotocol/server-aws`** → ローカルで MCP Server を立ち上げたい場合に利用。

Masashi さんが今回は選んだ **`mcp-proxy-for-aws`** なら、設定ファイルに登録するだけで VS Code Copilot から自然言語で AWS を操作できるようになります。

---

👉 次は、Masashi さんのプロジェクトに合わせて **「Next.js 16 ホスティング環境を Copilot チャットから自動構築するプロンプト例」**を整理しましょうか？
