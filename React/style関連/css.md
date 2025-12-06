# CSS フレームワーク

## Tailwind CSS

事前に定義されたコンポーネントを活用するのではなく、
flex、pt-4、text-center、rotate-90 などのような、低レベルのユーティリティクラスが提供されています。

これにより、マークアップで、柔軟に任意のデザインを記述できます。

### Tailwind CSS 公式

https://tailwindcss.com/docs/installation/using-vite

### インストール

```
npm install tailwindcss @tailwindcss/vite
```

### vite.config.js ファイルに、プラグインを追加

```
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react-swc";
import tailwindcss from "@tailwindcss/vite";

// https://vite.dev/config/
export default defineConfig({
  plugins: [react(), tailwindcss()],
});
```

### ./src/index.css ファイルに、Tailwind CSS をインポートする

```
@import "tailwindcss";
```

## 適用例

```
<h1 className="text-5xl text-blue-500">Vite + React</h1>
```
