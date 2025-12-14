# uv

## uv のインストール

uvx は uv パッケージに含まれるコマンドです。
Python が入ったら以下を実行してください:

windows

```
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/0.9.17/install.ps1 | iex"
```

Linux

```
https://docs.astral.sh/uv/getting-started/installation/#installation-methods
curl -LsSf https://astral.sh/uv/install.sh | sh
```

インストール後、以下で確認できます:
uvx --version
