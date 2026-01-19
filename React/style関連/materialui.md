# Material-UIのデフォルトブレークポイント:

xs = 0px～ (スマホ)
sm = 600px～ (タブレット)
md = 900px～ (小型PC)
lg = 1200px～ (デスクトップ)
xl = 1536px～ (大型ディスプレイ)

- 実装例

```
flexDirection={{ xs: "column", sm: "row" }}
```

- 意味
  画面サイズによってFlexboxの配置方向を変更します:

xs: "column" - 小さい画面（スマホ）では縦方向に要素を並べる
sm: "row" - 中サイズ以上の画面（タブレット・PC）では横方向に要素を並べる
