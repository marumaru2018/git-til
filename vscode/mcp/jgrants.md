# J グランツ MCP サーバーを VS Code に導入してみた

## 概要

デジタル庁が運用する補助金電子申請システム「[J グランツ](https://www.jgrants-portal.go.jp/)」の MCP サーバーを VS Code で使えるようにしました。

- 公式記事: https://digital-gov.note.jp/n/n09dfb9fa4e8e
- GitHub: https://github.com/digital-go-jp/jgrants-mcp-server

### できること

- 自然言語で補助金の検索
- 補助金情報の詳細参照
- 申請ガイドライン等のファイルのダウンロードと閲覧

公式では Claude Desktop での利用方法のみ記載されていましたが、VS Code でも同様に利用できます。

## 導入手順

### 1. 環境の準備

**前提条件:**

- Python 3.11 以上
- VS Code
- GitHub Copilot (Chat パネルで利用可能)

### 2. リポジトリのクローンと依存パッケージのインストール

```powershell
# リポジトリのクローン
git clone https://github.com/digital-go-jp/jgrants-mcp-server.git
cd jgrants-mcp-server

# Python仮想環境の作成
python -m venv venv

# 仮想環境の有効化
venv\Scripts\activate

# 依存パッケージのインストール
pip install -r requirements.txt
```

### 3. MCP サーバーの起動

```powershell
# HTTPサーバーを起動（デフォルト: localhost:8000）
python -m jgrants_mcp_server.core

# ホストとポートを指定する場合
python -m jgrants_mcp_server.core --host 127.0.0.1 --port 8000
```

サーバー起動後、以下のエンドポイントが利用可能になります：

- **MCP エンドポイント**: `http://localhost:8000/mcp` または `http://127.0.0.1:8000/mcp`

### 4. VS Code の設定

VS Code の settings.json に MCP サーバーの設定を追加します。

**設定ファイルの場所:**

~~- Windows: `%APPDATA%\Code\User\settings.json`~~
~~- または VS Code で `Ctrl + ,` → 右上の「設定を開く」アイコン → settings.json~~

**設定ファイルの場所（Windows）**
`~\AppData\Roaming\Code\User\mcp.json`

**※私の場合は、上記ファイルに書きました。正しい配置場所は公式サイト等を確認ください。**

> **注意:** 設定ファイルについては setting.json に書く方法などもあるようですが、今回は mcp.json を使用しました。

```json
{
  "servers": {
    "jgrants": {
      "command": "uvx",
      "args": ["fastmcp", "run", "http://localhost:8000/mcp"]
    }
  }
}
```

**注意事項:**

- `uvx` は `uv` のコマンドラインツール実行機能です
- `uv` がインストールされていない場合は、先に `pip install uv` を実行してください
- localhost でうまくいかない場合は `127.0.0.1` に変更してください

### 5. VS Code の再起動

設定を反映させるため、VS Code を再起動します。

### 6. 動作確認

1. VS Code の GitHub Copilot Chat を開く
2. MCP サーバーが接続されていることを確認
3. 以下のような質問で動作確認：

```
IT関連の補助金を検索して
```

## 使用例

### 補助金の検索

```
東京都で申請できるDX関連の補助金を教えて
```

### 補助金の詳細取得

```
補助金ID: a0WJ200000CDR9HMAX の詳細を教えて
```

### 申請ガイドラインの確認

補助金詳細を取得すると、申請ガイドラインなどの PDF ファイルが自動的にダウンロードされ、内容を確認できます。

## トラブルシューティング

### サーバーが起動しない場合

- Python のバージョンを確認（3.11 以上必要）
- 依存パッケージが正しくインストールされているか確認
- ポートが他のプロセスで使用されていないか確認

### VS Code で認識されない場合

- settings.json の記述が正しいか確認
- VS Code を完全に再起動
- `uvx` または `fastmcp` が正しくインストールされているか確認

### MCP エンドポイントに接続できない場合

- MCP サーバーが起動しているか確認
- `localhost` を `127.0.0.1` に変更してみる
- ファイアウォールの設定を確認

## 参考リンク

- [J グランツポータル](https://www.jgrants-portal.go.jp/)
- [デジタル庁公式記事](https://digital-gov.note.jp/n/n09dfb9fa4e8e)
- [GitHub リポジトリ](https://github.com/digital-go-jp/jgrants-mcp-server)
- [J グランツ API ドキュメント](https://developers.digital.go.jp/documents/jgrants/api/)

## 注意事項

- 取得した補助金情報を公開する際は、「J グランツ（jGrants）からの出典」である旨を明記してください
- 正式な申請前には必ず公式サイトで最新情報を確認してください
- API への過度な連続アクセスは避けてください
