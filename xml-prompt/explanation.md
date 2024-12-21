# XML Promptの解説

## 基本構造

```xml
<project_setup>
  <instructions>
    <title>プロジェクト名/目的</title>
    <description>全体の概要説明</description>

    <!-- 前提条件がある場合 -->
    <prerequisites>
      <requirement>必要な前提条件</requirement>
    </prerequisites>

    <!-- 使用する技術スタック -->
    <tech_stack>
      <technology>
        <name>技術名</name>
        <description>説明</description>
      </technology>
    </tech_stack>

    <!-- セットアップ手順 -->
    <steps>
      <step>
        <number>順番</number>
        <description>手順の説明</description>
        <action>
          <command>実行するコマンド</command>
        </action>
        <details>
          <item>補足説明項目</item>
        </details>
      </step>
    </steps>

    <!-- 設定が必要な場合 -->
    <configuration>
      <question>設定項目の質問</question>
      <answer>設定値</answer>
    </configuration>

    <!-- ベストプラクティス -->
    <best_practices>
      <category>カテゴリ名</category>
      <items>
        <item>推奨事項</item>
      </items>
    </best_practices>
  </instructions>
</project_setup>
```

## 構造化のルール

1. ドキュメントルール

   - プロジェクト固有の名前を持つルート要素を使用
   - `<instructions>` に全体の手順を含める
   - 論理的な階層構造を維持

2. 必須セクション

   - `<title>`: プロジェクトの目的
   - `<description>`: 全体の概要
   - `<steps>`: セットアップ手順

3. ステップの記述ルール

   - 番号による順序付け
   - 明確な説明
   - 具体的なコマンド
   - 必要に応じた補足説明

4. コマンド記述ルール

   - `<command>` タグ内に完全なコマンドを記載
   - バックスラッシュやオプションを明確に区別
   - 一行につき1つのコマンド

5. 設定オプションルール
   - 対話型設定は `<configuration>` で定義
   - 質問と回答のペアで記述
   - 選択肢がある場合はすべて記載

## 使用上の注意点

1. 一貫性

   - 同じ種類の情報は同じタグで記述
   - 階層レベルを統一
   - 命名規則の統一

2. 明確性

   - 各ステップの目的を明示
   - コマンドの効果を説明
   - エラー発生時の対処方法を含める

3. 完全性

   - 必要な情報をすべて含める
   - 省略や略記を避ける
   - 前提条件を明確に記述

4. 保守性
   - バージョン情報の明記
   - 更新履歴の管理
   - 依存関係の明確化

このフォーマットを使用することで、以下の利点が得られます：

- セットアップ手順の標準化
- 説明の一貫性確保
- エラーの防止
- ドキュメントの保守性向上
