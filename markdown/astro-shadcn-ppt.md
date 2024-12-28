# Astro Project Setup

## Purpose
Astroプロジェクトを作成し、フロントエンドを構築します。

## Description
Astroを使ってコンテンツ重視のウェブサイトを作成します。

## Prerequisites
- Requirement: Bunはインストール済みであること。

## Tech Stack

### Bun
- Description: 高速なJavaScriptランタイムで、開発環境を迅速にセットアップ可能。

### Astro
- Description: コンテンツ重視のウェブサイトを構築するためのモダンなフレームワーク。

### TypeScript
- Description: 型安全なJavaScript開発を可能にするプログラミング言語。

### Tailwind
- Description: ユーティリティファーストのCSSフレームワークで効率的なデザイン構築を支援。

### shadcn/ui
- Description: 高品質で再利用可能なReactコンポーネントライブラリで、洗練されたUIを迅速に構築可能。

---

## Steps

### Step 1: Astroプロジェクトを作成
Astroプロジェクトをセットアップします。

Command:
```bash
bunx create-astro@latest ./ --template minimal --install --git --yes
```

---

### Step 2: Tailwind CSSを導入
Tailwind CSSをプロジェクトに追加します。

Command:
```bash
npx astro add tailwind --yes --yes --yes
```

---

### Step 3: Reactを導入
Reactをプロジェクトに追加します。

Command:
```bash
bunx --bun astro add react --yes --yes --yes
```

---

### Step 4: `styles/globals.css`を作成
`src/styles/globals.css`を作成し、以下の内容を追加します。

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

---

### Step 5: `globals.css`ファイルをインポート
`src/pages/index.astro`に以下を追加して、CSSをインポートします。

```javascript
import "../styles/globals.css";
```

---

### Step 6: `astro.config.mjs`に設定を追加
以下の設定を`astro.config.mjs`に追加します。

```javascript
export default defineConfig({
  integrations: [
    tailwind({
      applyBaseStyles: false,
    }),
  ],
});
```

---

### Step 7: `tsconfig.json`ファイルを編集する
以下の設定を`tsconfig.json`に追加します。

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": [
        "./src/*"
      ]
    }
  }
}
```

---

### Step 8: shadcnを初期化する
shadcnを初期化します。

Command:
```bash
bunx --bun shadcn@latest init --defaults
```

---

### Step 9: Buttonコンポーネントをインストールする
shadcn/uiのButtonコンポーネントをインストールします。

Command:
```bash
bunx --bun shadcn add button
```

---

### Step 10: Buttonコンポーネントを追加
`src/pages/index.astro`を以下のように編集します。

```html
---
import { Button } from "@/components/ui/button";
---
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="icon" type="image/svg+xml" href="/favicon.svg" />
    <meta name="viewport" content="width=device-width" />
    <meta name="generator" content={Astro.generator} />
    <title>Astro</title>
  </head>
  <body>
    <h1 class="text-3xl font-bold underline">Hello world!</h1>
    <Button variant="destructive">Hello World</Button>
  </body>
</html>
```

---

### Step 11: shadcn/uiが反映されたかを確認
開発サーバーを起動して、変更が反映されているか確認します。

Command:
```bash
bun run dev
```
