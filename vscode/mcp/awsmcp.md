# AWS MCP Server を導入してみる

## 概要

AWS MCP Server を使う場合、2 つの利用方法があるようです：

- **簡単に使いたい / AWS がホストするサーバーに接続したい** → `mcp-proxy-for-aws`
- **閉域環境やローカルでサーバーを立ち上げたい** → `@modelcontextprotocol/server-aws`

## 違い

| パッケージ                             | 役割                                                                                                                                                                          | 利用シーン                                                                                     |
| -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| **`mcp-proxy-for-aws`**                | MCP クライアント（VS Code Copilot, Cursor など）と AWS が提供する **マネージド MCP Server** をつなぐプロキシ。サーバーを自分で立てずに AWS の公式エンドポイントへ接続できる。 | 「簡単に試したい」「AWS がホストする MCP Server をそのまま使いたい」場合。導入が最もシンプル。 |
| **`@modelcontextprotocol/server-aws`** | AWS MCP Server の公式実装。ローカル環境や閉域ネットワークで MCP Server を直接立ち上げる。                                                                                     | セキュリティ要件が厳しく「自前でサーバーを管理したい」場合。Docker や npx で起動可能。         |

今回は **`mcp-proxy-for-aws`** → AWS が提供するマネージド MCP Server に接続する方式を選択しました。

以下、導入手順は Copilot の回答をもとに検証する形で進めます（Windows 環境）。

## 導入手順（`mcp-proxy-for-aws` 利用）

### 1. 前提条件

- **AWS CLI** が設定済み（`aws configure` で認証情報を登録）
- **Node.js** と **uvx** が利用可能
- **MCP 対応クライアント**（VS Code Copilot, Cursor, Kiro CLI など）

### 2. 設定ファイルに MCP Server を登録

VS Code Copilot の場合は設定ファイルに以下を追加します。

**設定ファイルの場所（Windows）**
`~\AppData\Roaming\Code\User\mcp.json`

**※私の場合は、上記ファイルに書きました。正しい配置場所は公式サイト等を確認ください。**

> **注意:** 設定ファイルについては setting.json に書く方法などもあるようですが、今回は mcp.json を使用しました。

```json
{
  "servers": {
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

**設定のポイント**

- **command**: `uvx` を指定
- **args**: `mcp-proxy-for-aws@latest` と AWS MCP Server のエンドポイント
- **AWS_REGION**: 東京リージョンの場合は `ap-northeast-1`
- **AWS_PROFILE**: 利用する AWS 認証情報を設定

### 3. 動作確認

1. VS Code / Cursor を再起動
2. Copilot チャットで自然言語で AWS 操作を依頼

**例：**

```
AWSに新しいS3バケットを作成して。名前はproject-logsで東京リージョンに。
```

→ MCP Server が API 呼び出しに変換し、S3 バケットを作成します。

### 4. 注意点

- **CloudTrail に必ず記録される**ため、IAM 権限は最小限に設計すること
- MCP Server 自体は無料だが、作成した AWS リソースには通常の料金が発生する

## まとめ

- **`mcp-proxy-for-aws`** → AWS がホストする MCP Server に接続するためのプロキシ。導入が最も簡単
- **`@modelcontextprotocol/server-aws`** → ローカルで MCP Server を立ち上げたい場合に利用

## 参考

- [AWS MCP Server リリース情報](https://aws.amazon.com/jp/about-aws/whats-new/2025/11/aws-mcp-server/)
- [iret.media の解説記事](https://iret.media/178469)
