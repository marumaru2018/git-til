# GitHub Pages へのデプロイ手順

公式
https://ja.vite.dev/guide/static-deploy.html#github-pages

## 事前設定

### vite.config.js 設定ファイルに、base URL の設定を追記します

```
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react-swc";
import tailwindcss from "@tailwindcss/vite";

// https://vite.dev/config/
export default defineConfig({
  base: process.env.GITHUB_PAGES ? "REPOSITORY_NAME" : "./",
  plugins: [react(), tailwindcss()],
});

```

### GitHub Actions のワークフローを記述する

.github\workflows\deploy-gh-pages.yml を作成する

```
# 静的コンテンツを GitHub Pages にデプロイするためのシンプルなワークフロー
name: Deploy static content to Pages

on:
  # デフォルトブランチを対象としたプッシュ時にで実行されます
  push:
    branches: ["main"]

  # Actions タブから手動でワークフローを実行できるようにしますgit remote add origin
  workflow_dispatch:

# GITHUB_TOKEN のパーミッションを設定し、GitHub Pages へのデプロイを許可します
permissions:
  contents: read
  pages: write
  id-token: write

# 1 つの同時デプロイメントを可能にする
concurrency:
  group: "pages"
  cancel-in-progress: true

jobs:
  # デプロイするだけなので、単一のデプロイジョブ
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Set up Node
        uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: "npm"
      - name: Install dependencies
        run: npm ci
      - name: Build
        run: npm run build
      - name: Setup Pages
        uses: actions/configure-pages@v4
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          # dist フォルダーのアップロード
          path: "./dist"
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

## デプロイ

通常通り、コミットまで実施。
リモートリポジトリに対して push まで行う

※GitHub 上のリポジトリは公開で作成。
また、Pages の設定を有効にする。
「settings」→「Pages」→「Build and deployment」を GitHub Actions に設定

## 補足

public ディレクトリ内の画像を、相対パスで指定した場合、
デプロイ先によっては、本番環境の URL が、自動で画像パスに適用されない場合があります。
その場合は、以下の公式ガイドに従い、本番環境時の URL を、設定する必要があります

1. src/constants/index.js ファイル内に、定数として URL を定義しておきます

```
export const BASE_URL =
  import.meta.env.MODE === "production" ? "あなたのデプロイ先のURL" : "";
```

使用箇所
本番環境では、デプロイ先の URL を指定

```
          <img
            src={`${BASE_URL}/camp-coffee.jpg`} // 追加
            alt="Camp Coffee"
            className="rounded-lg shadow-md"
          />

```
