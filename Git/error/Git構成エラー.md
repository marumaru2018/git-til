# エラー

Git の"user.name"と"user.email"を構成していることを確認してください。

## 原因

Git の設定でユーザー名とメールアドレスが設定されていないために発生しています。

## 対処

以下のコマンドをターミナルで実行して、Git の設定を行う

```bash
git config --global user.name "あなたの名前"
git config --global user.email "your.email@example.com"
```

※AWS CodeCommit の場合のユーザ名確認方法
aws iam get-user --query 'User.UserName' --output text

尚、特定のプロジェクトだけに設定したい場合は、以下のように--local を使用する
git config --local user.name "あなたの名前"
git config --local user.email "your.email@example.com"

補足
**ローカル設定は.git/config に保存される**

例:

## 設定が正しく行われたか確認する方法

```bash
git config --global user.name
git config --global user.email
```

## 他

関連コマンド

```
git config --global --list
git config --system --list
```
