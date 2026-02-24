# devブランチから新たにprodブランチを作成する

最新取得:

```
git fetch origin
```

devへ移動:

```
git switch dev（古いGitなら git checkout dev）
```

devを最新化:

```
git pull origin dev
```

prodを作成して移動:

```
git switch -c prod
```

リモートへ作成＆追跡設定:

```
git push -u origin prod
```

確認:

```
git branch -a と git status
```

補足:
もしローカルにdevが無い場合は git switch -c dev origin/dev の後に同じ流れでOKです。
既にprodが存在する場合は作成せず、git switch prod を使ってください。
