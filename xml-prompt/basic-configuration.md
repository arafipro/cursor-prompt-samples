# XML Prompt 基本構成

```xml
<project_setup>
  <instructions>
    <title>{{プロジェクト名}}</title>
    <purpose>{{目的}}</purpose>
    <description>{{全体の概要説明}}</description>

    <!-- 前提条件がある場合 -->
    <prerequisites>
      <requirement>{{必要な前提条件}}</requirement>
    </prerequisites>

    <!-- 使用する技術スタック -->
    <tech_stack>
      <technology>
        <name>{{技術名}}</name>
        <description>{{説明}}</description>
      </technology>
    </tech_stack>

    <!-- セットアップ手順 -->
    <steps>
      <step>
        <number>{{順番}}</number>
        <description>{{手順の説明}}</description>
        <action>
          <command>{{実行するコマンド}}</command>
        </action>
        <details>
          <item>{{補足説明項目}}</item>
        </details>
      </step>
    </steps>
  </instructions>

	<execution>
    <prompt>コードブロックを使ったモジュールアプローチを使用してください</prompt>
		<prompt>各ステップの説明は、必ず行なってください</prompt>
  </execution>
</project_setup>
```
