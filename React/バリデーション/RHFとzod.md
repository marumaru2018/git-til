# React Hook Form と ZOD を使ったバリデーション

FormContainer は react-hook-form-mui というライブラリのコンポーネントです。
react-hook-form-mui は、React Hook Form と Material UI を統合するためのラッパーライブラリで、
FormContainer はフォームのコンテキストを提供し、バリデーションやフォーム送信を簡単に扱えるようにするコンポーネントです。

login./page.tsx

```
"use client";
import { z } from "zod";
import { useForm } from "react-hook-form";
import { FormContainer, TextFieldElement } from "react-hook-form-mui";
import { useMutation } from "@tanstack/react-query";
import { zodResolver } from "@hookform/resolvers/zod/dist/zod.js";
import { Stack, Box, Button, FormHelperText } from "@mui/material";
import { UserInfo } from "@/types/userType";
import { schema } from "@/schema/login.schema";
import { styles } from "../../../public/css/common";
// import { useRouter } from "next/router";
import { useRouter } from "next/navigation";
import { useUserStore } from "@/stores/userUserStore";
import React from "react";

/**
 * ログイン画面
 */
export default function LoginPage() {
  const router = useRouter();
  const setUserInfo = useUserStore((state) => state.setUserInfo);

  // ①Formを定義して、zodスキーマと紐づけする
  type FormValues = z.infer<typeof schema>;
  const formContext = useForm<FormValues>({
    resolver: zodResolver(schema),
    defaultValues: { userId: "", passwd: "" },
  });

  // ログインAPI定義
  const mutation = useMutation({
    mutationFn: async (data: FormValues): Promise<UserInfo> => {
      const res = await fetch("/authenticate", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(data),
      });
      return res.json();
    },
    onSuccess: (data: UserInfo) => {
      // ユーザー情報の保存
      setUserInfo(data);

      // トップ画面への遷移
      router.push("/home");
    },
    onError: (error) => {
      console.log(JSON.stringify(error));
    },
  });

  // ログインボタン押下
  const onSubmit = (data: FormValues) => {
    mutation.mutate({
      userId: data.userId,
      passwd: data.passwd,
    });
  };

  return (
    // ②定義したFormValuesをformに配置
    // ※FormContainerは、react-hook-form-mui というライブラリのコンポーネント
    <FormContainer formContext={formContext} onSuccess={onSubmit}>
      <Box sx={styles.Container}>
        <Stack spacing={1} sx={{ width: "200px" }}>
          <TextFieldElement size="small" name="userId" label="ユーザーID" />
          <TextFieldElement
            size="small"
            name="passwd"
            label="パスワード"
            type="password"
          />
          <Button variant="contained" type="submit" sx={styles.ButtonBase}>
            ログイン
          </Button>
          {mutation.isError && (
            <div>
              <FormHelperText error>{mutation.error.message}</FormHelperText>
            </div>
          )}
        </Stack>
      </Box>
    </FormContainer>
  );
}

```

このコードのバリデーションの動きを解説します:

## バリデーション成功時の流れ

1. **フォーム送信時** - ユーザーがログインボタンをクリック
2. **クライアント側バリデーション** - `zodResolver(schema)` が `login.schema.ts` のルールに基づいて入力値を検証
3. **成功時** - `FormContainer` の `onSuccess` プロップで指定された `onSubmit` 関数が呼ばれる（54 行目）
4. **API 呼び出し** - `mutation.mutate()` でログイン API に POST リクエスト送信（47-50 行目）
5. **API 成功時** - `onSuccess` コールバック（35-38 行目）が実行され、ユーザー情報を受け取る

## バリデーションエラー時の流れ

### クライアント側バリデーションエラー

- Zod スキーマ（`login.schema.ts`）の条件を満たさない場合
- `FormContainer` が自動的にエラーを処理し、フォーム送信をブロック
- `TextFieldElement` 配下に自動でエラーメッセージが表示される
- `onSubmit` 関数は**呼ばれない**

### API 呼び出し時のエラー

- `onError` コールバック（39-41 行目）が実行される
- `mutation.isError` が `true` になる
- 71-75 行目の条件分岐により、`mutation.error.message` がフォーム下部に赤文字で表示される

```tsx
{
  mutation.isError && (
    <div>
      <FormHelperText error>{mutation.error.message}</FormHelperText>
    </div>
  );
}
```
