## 補足: VS Code の MCP 設定方法

VS Code の MCP 設定には 2 つの方法があります：

settings.json 方式（現在使用中）

settings.json 内の mcpServers セクションで設定

### 1. settings.json 方式（現在使用中）

- `settings.json` 内の `mcpServers` セクションで設定
- VS Code の標準的な設定方法
- 現在この方法を使用しています

### 2. mcp.json 方式（古い方法）

- 独立した `mcp.json` ファイルで設定
- 以前のバージョンや特定の環境で使用

### 設定ファイルの使い分け

#### settings.json の場合

**ユーザー設定**

- VS Code 全体のグローバルな設定として MCP サーバーを登録
- どのプロジェクトを開いても同じサーバー設定が利用可能
- `Ctrl + Shift + P` → "Preferences: Open User Settings (JSON)" で開く

**ワークスペース設定 (.vscode/settings.json)**

- 特定のプロジェクト内でのみ有効な設定として MCP サーバーを登録

#### .vscode/mcp.json の場合

- VS Code の「MCP: サーバーを追加」コマンドで「ワークスペース設定」を選択すると作成される
- プロジェクトのルートディレクトリ直下の `.vscode` フォルダ内に `mcp.json` が作成される
- ワークスペース設定の糖衣構文（シンタックスシュガー）のようなもの
- MCP サーバーの設定のみを独立して管理したい場合に便利

### 結論

どちらのファイルも設定に使用できますが、以下の基準で選ぶのが一般的です：

- **mcp.json**: プロジェクト固有の MCP サーバー設定を、他の VS Code 設定と分けてシンプルに管理したい場合
- **settings.json**: グローバルまたはプロジェクトの `settings.json` 内で他の設定と一緒に一元管理したい場合

参考
microsoft 公式
https://learn.microsoft.com/ja-jp/visualstudio/ide/mcp-servers?view=visualstudio
