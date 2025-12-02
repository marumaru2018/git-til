# Git コマンド

## Git の設定を確認

```
git config --list
```

## リモートブランチの一覧を確認

```
git branch -r
```

## 特定のブランチがリモートに存在するか確認

```
git ls-remote --heads origin 特定のブランチ名
```

## リモートの 特定ブランチをローカルに取得する

```
git fetch origin 特定ブランチ:特定ブランチ
```

または、よりシンプルな方法:

```
git checkout -b 特定ブランチ origin/特定ブランチ
```
