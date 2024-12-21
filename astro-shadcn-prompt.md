<project_setup>
  <instructions>
    <title>astro-project</title>
    <purpose>astroプロジェクトを作成</purpose>
    <description>astroを使ったフロントエンドを作成</description>
    <prerequisites>
      <requirement>bunはインストール済み</requirement>
    </prerequisites>
    <tech_stack>
      <technology>
        <name>bun</name>
        <description>高速なJavaScriptランタイムで、開発環境を迅速にセットアップ可能</description>
      </technology>
      <technology>
        <name>Astro</name>
        <description>コンテンツ重視のウェブサイトを構築するためのモダンなフレームワーク</description>
      </technology>
      <technology>
        <name>TypeScript</name>
        <description>型安全なJavaScript開発を可能にするプログラミング言語</description>
      </technology>
      <technology>
        <name>Tailwind</name>
        <description>ユーティリティファーストのCSSフレームワークで効率的なデザイン構築を支援</description>
      </technology>
    </tech_stack>
    <steps>
      <step>
        <number>1</number>
        <description>Astroプロジェクトを作成</description>
        <action>
          <command>bunx create-astro@latest ./ --template minimal --install --git --yes</command>
        </action>
      </step>
      <step>
        <number>2</number>
        <description>Tailwind CSSを導入</description>
        <action>
          <command>npx astro add tailwind --yes --yes --yes</command>
        </action>
      </step>
      <step>
        <number>3</number>
        <description>Reactを導入</description>
        <action>
          <command>bunx --bun astro add react --yes --yes --yes</command>
        </action>
      </step>
      <step>
        <number>4</number>
        <description>styles/globals.cssを作成</description>
        <action>
          srcディレクトリ内にstyles/globals.cssを作成
					@tailwind base;
					@tailwind components;
					@tailwind utilities;
        </action>
      </step>
      <step>
        <number>5</number>
        <description>globals.cssファイルをインポート</description>
        <action>
          src/pages/index.astroに`import "../styles/globals.css"`を追加
        </action>
      </step>
      <step>
        <number>6</number>
        <description>astro.config.mjsに設定を追加</description>
        <action>
					```
					export default defineConfig({
						integrations: [
							tailwind({
								applyBaseStyles: false,
							}),
						],
					})
					```
        </action>
      </step>
      <step>
        <number>7</number>
        <description>tsconfig.jsonファイルを編集する</description>
        <action>
					```
					{
					  "compilerOptions": {
					    // ...
					    "baseUrl": ".",
					    "paths": {
					      "@/*": [
					        "./src/*"
					      ]
					    }
					    // ...
					  }
					}
					```
        </action>
      </step>
      <step>
        <number>8</number>
        <description>shadcnを初期化する</description>
        <action>
          <command>bunx --bun shadcn@latest init --defaults</command>
        </action>
      </step>
      <step>
        <number>9</number>
        <description>Buttonコンポーネントをインストールする</description>
        <action>
          <command>bunx --bun shadcn add button</command>
        </action>
      </step>
      <step>
        <number>10</number>
        <description>Buttonコンポーネントを追加</description>
        <action>
          ```
          ---
					import { Button } from "@/components/ui/button"
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
        </action>
      </step>
      <step>
        <number>11</number>
        <description>shadcn/uiが反映されたかを確認</description>
        <action>
          <command>bun run dev</command>
        </action>
      </step>
    </steps>
  </instructions>
  <execution>
    <prompt>コードブロックを使ったモジュールアプローチを使用してください</prompt>
    <prompt>各ステップの説明は、必ず行なってください</prompt>
  </execution>
</project_setup>
