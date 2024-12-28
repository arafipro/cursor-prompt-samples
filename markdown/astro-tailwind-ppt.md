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

### Step 3: Tailwind CSSをコードに適用
`index.astro`のコードを変更して、Tailwind CSSのスタイルが適用されることを確認します。

変更内容:
以下を変更します:
```html
<h1>Astro</h1>
```
次のように書き換えます:
```html
<h1 class="text-3xl font-bold underline">Hello world!</h1>
```

---

### Step 4: Tailwind CSSが反映されたかを確認
開発サーバーを起動し、変更が反映されているかを確認します。

Command:
```bash
bun run dev
```
