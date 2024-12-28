## 前提条件

Bunはインストール済み

## 技術スタック

- Bun
- TypeScript
- [React Native](https://reactnative.dev/docs/0.74/getting-started)
- [Expo](https://docs.expo.dev/)
- [NativeWind](https://www.nativewind.dev/)
  
## Steps

ステップを順番通りに進める

### Step 0: プロジェクト用ディレクトリを作成

プロジェクト用ディレクトリ名を聞いて、ターミナルで入力されるのを待つ
入力されたディレクトリ名で作成
作成したら、ディレクトリ内に移動

```sh
mkdir {{入力されたディレクトリ名}}
cd {{入力されたディレクトリ名}}
```

以降、`{{入力されたディレクトリ名}}`内で指示を実行する

### Step 1: プロジェクトを作成

#### Command:

```bash
bun create expo ./ --template blank-typescript
```

### Step 2: expo routerを導入

#### 依存関係のインストール    

```sh
npx expo install expo-router react-native-safe-area-context react-native-screens expo-linking expo-constants expo-status-bar
```

#### エントリーポイントの設定

`package.json`の`main`プロパティを`expo-router/entry`に設定

```json
{
  "main": "expo-router/entry"
}
```

#### プロジェクト設定の変更

`app.json`にディープリンク用の`scheme`を追加

```json
{
  "scheme": "your-app-scheme"
}
```

#### Babel設定の変更

`babel.config.js`で`babel-preset-expo`をプリセットとして使用

```javascript
module.exports = function (api) {
  api.cache(true);
  return {
    presets: ['babel-preset-expo'],
  };
};
```

`babel.config.js`が存在しない場合、以下のコマンドで作成

```sh
npx expo customize babel.config.js
```

#### `app/index.tsx`を作成

`app/index.tsx`を作成し、以下のコードを追加

```ts
import { StyleSheet, Text, View } from "react-native";

export default function Page() {
  return (
    <View style={styles.container}>
      <Text>Home</Text>;
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    backgroundColor: "skyblue",
  },
});
```

ルートディレクトリの`App.tsx`を必要ないので、削除

#### `app/_layout.tsx`を作成

`app/_layout.tsx`を作成し、以下のコードを追加

```ts
import { Slot } from 'expo-router';

export default function Layout() {
  return <Slot />;
}
```

### Step 3: NativeWindを導入

#### NativeWindのインストール

```sh
npx expo install nativewind tailwindcss react-native-reanimated react-native-safe-area-context
```

#### Tailwind CSSの設定

プロジェクトのルートディレクトリで以下のコマンドを実行し、`tailwind.config.js`ファイルを生成

```sh
npx tailwindcss init
```

#### `tailwind.config.js`を編集

コンテンツの設定を追加

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  // NOTE: Update this to include the paths to all of your component files.
  content: ["./app/**/*.{js,jsx,ts,tsx}"],
  presets: [require("nativewind/preset")],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

#### `global.css`ファイルを作成

ルートディレクトリに`global.css`ファイルを作成
Tailwindの基本スタイルをインポート

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

#### Babelプリセットの追加

`babel.config.js`ファイルを編集し、`nativewind/babel`プリセットを追加

```js
module.exports = function (api) {
  api.cache(true);
  return {
    presets: [
      ["babel-preset-expo", { jsxImportSource: "nativewind" }],
      "nativewind/babel",
    ]
  };
};
```

#### Metro設定の変更

`metro.config.js`を編集し、`withNativeWind`を使用して設定を拡張

```js
const { getDefaultConfig } = require("expo/metro-config");
const { withNativeWind } = require("nativewind/metro");

const config = getDefaultConfig(__dirname);

module.exports = withNativeWind(config, { input: "./global.css" });
```

#### CSSファイルのインポート

`app/_layout.tsx`で、`global.css`をインポート

```ts
import { Slot } from "expo-router";

// グローバルCSSファイルをインポート
import "../global.css";

export default function Layout() {
  return <Slot />;
}
```

#### TypeScriptの設定

ルートディレクトリに`nativewind-env.d.ts`を作成
以下のコードを追加

```ts
<reference types="nativewind/types" />
```

### Step 4: Tailwind CSSをコードに適用

`app/index.tsx`のコードを変更
Tailwind CSSのスタイルが適用されることを確認
以下を

```ts
<View style={styles.container}>
```

次のように書き換え

```ts
<View className="flex-1 justify-center items-center bg-sky-500">
```

また、以下のコードは不要なので削除

```ts
const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    backgroundColor: "skyblue",
  },
});
```

#### バンドラーキャッシュのクリア

Babel設定を更新した後、以下のコマンドでバンドラーのキャッシュをクリア

```sh
npx expo start -c
```
