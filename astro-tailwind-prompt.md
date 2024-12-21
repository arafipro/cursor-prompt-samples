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
        <description>Tailwind CSSをコードに適用</description>
        <action>
					index.astroの`<h1>Astro</h1>`を`<h1 class="text-3xl font-bold underline">Hello world!</h1>`に変更
        </action>
      </step>
      <step>
        <number>4</number>
        <description>Tailwind CSSが反映されたかを確認</description>
        <action>
          <command>cd astro-project && bun run dev</command>
        </action>
      </step>
    </steps>
  </instructions>
  <execution>
    <prompt>コードブロックを使ったモジュールアプローチを使用してください</prompt>
    <prompt>各ステップの説明は、必ず行なってください</prompt>
  </execution>
</project_setup>
