## 前提条件

Bunはインストール済み

## 技術スタック

- Bun
- TypeScript
- [React Native](https://reactnative.dev/docs/0.74/getting-started)
- [Expo](https://docs.expo.dev/)
- [NativeWind](https://www.nativewind.dev/)
- [Clerk](https://clerk.com/docs/quickstarts/expo)

## Steps

ステップを順番通りに進める

### Step 1: @clerk/clerk-expo をインストール

```sh
bun add @clerk/clerk-expo
```

### Step 2: @clerk/types をインストール

```sh
bun add @clerk/types
```

### Step 3: プロジェクト用ディレクトリを作成

`app/_layout.tsx`に`<ClerkProvider>`を追加

```ts
import { ClerkLoaded, ClerkProvider } from "@clerk/clerk-expo";
import { Slot } from "expo-router";
import "../global.css";

export default function RootLayout() {
  const publishableKey = process.env.EXPO_PUBLIC_CLERK_PUBLISHABLE_KEY!;

  if (!publishableKey) {
    throw new Error("Add EXPO_PUBLIC_CLERK_PUBLISHABLE_KEY to your .env file");
  }

  return (
    <ClerkProvider publishableKey={publishableKey}>
      <ClerkLoaded>
        <Slot />
      </ClerkLoaded>
    </ClerkProvider>
  );
}
```

### Step 4: トークンキャッシュの設定

#### ライブラリをインストール

```sh
bun add expo-secure-store
```

#### ルートディレクトリに`cache.ts`を作成

ルートディレクトリに`cache.ts`を作成して、以下のコードを追加

```ts
import * as SecureStore from "expo-secure-store";
import { Platform } from "react-native";
import { TokenCache } from "@clerk/clerk-expo/dist/cache";

const createTokenCache = (): TokenCache => {
  return {
    getToken: async (key: string) => {
      try {
        const item = await SecureStore.getItemAsync(key);
        if (item) {
          console.log(`${key} was used 🔐 \n`);
        } else {
          console.log("No values stored under key: " + key);
        }
        return item;
      } catch (error) {
        console.error("secure store get item error: ", error);
        await SecureStore.deleteItemAsync(key);
        return null;
      }
    },
    saveToken: (key: string, token: string) => {
      return SecureStore.setItemAsync(key, token);
    },
  };
};

// SecureStore is not supported on the web
export const tokenCache =
  Platform.OS !== "web" ? createTokenCache() : undefined;
```

#### `app/_layout.tsx`にコードを追加

```ts
import { tokenCache } from "@/cache";
```

`<ClerkProvider>`に`tokenCache`を追加して、`tokenCache`を指定

```ts
<ClerkProvider tokenCache={tokenCache} publishableKey={publishableKey}>
```

### Step 5: `app/(auth)/_layout.tsx`を作成

`app/(auth)/_layout.tsx`を作成して、以下のコードを追加

```ts
import { useAuth } from "@clerk/clerk-expo";
import { Redirect, Stack } from "expo-router";

export default function AuthRoutesLayout() {
  const { isSignedIn } = useAuth();

  if (isSignedIn) {
    return <Redirect href={"/"} />;
  }

  return <Stack screenOptions={{ headerShown: false }} />;
}
```

### Step 6: `(home)`グループを作成

#### `app/(home)/_layout.tsx`を作成

`app/(home)/_layout.tsx`を作成して、以下のコードを追加

```ts
import { Stack } from "expo-router/stack";

export default function Layout() {
  return <Stack screenOptions={{ headerShown: false }} />;
}
```

#### `app/(home)/index.tsx`を作成

`app/(home)/index.tsx`を作成して、以下のコードを追加

```ts
import {
  SignedIn,
  SignedOut,
  useAuth,
  useOAuth,
  useUser,
} from "@clerk/clerk-expo";
import { Ionicons } from "@expo/vector-icons";
import { Text, TouchableOpacity, View } from "react-native";

export default function Page() {
  const { signOut } = useAuth();
  const { user } = useUser();
  const { startOAuthFlow } = useOAuth({
    strategy: "oauth_github",
  });

  const handleGitHubLogin = async () => {
    try {
      const { createdSessionId, setActive } = await startOAuthFlow();

      if (createdSessionId) {
        setActive!({ session: createdSessionId });
      }
    } catch (err) {
      console.error("OAuth error", err);
    }
  };

  const handleSignOut = async () => {
    try {
      await signOut();
    } catch (err) {
      console.error("Error signing out:", err);
    }
  };

  return (
    <View className="flex-1 items-center justify-center gap-4">
      <SignedIn>
        <Text className="mt-2">ユーザーID: {user?.fullName}</Text>
        <TouchableOpacity
          onPress={handleSignOut}
          className="bg-red-500 px-4 py-2 rounded-lg"
        >
          <Text className="text-white font-semibold">ログアウト</Text>
        </TouchableOpacity>
      </SignedIn>
      <SignedOut>
        <TouchableOpacity
          onPress={handleGitHubLogin}
          className="flex-row items-center gap-2 border border-gray-300 px-4 py-2 rounded-lg"
        >
          <Ionicons name="logo-github" size={24} />
          <Text className="font-semibold">GitHubでログイン</Text>
        </TouchableOpacity>
      </SignedOut>
    </View>
  );
}
```
