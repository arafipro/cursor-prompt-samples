# XML Prompt 基本構成

```xml
<project_setup>
  <instructions>
    <title>{{プロジェクト名/目的}}</title>
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

    <!-- 設定が必要な場合 -->
    <configuration>
      <question>{{設定項目の質問}}</question>
      <answer>{{設定値}}</answer>
    </configuration>

    <!-- ベストプラクティス -->
    <best_practices>
      <category>{{カテゴリ名}}</category>
      <items>
        <item>{{推奨事項}}</item>
      </items>
    </best_practices>
  </instructions>
</project_setup>
```
