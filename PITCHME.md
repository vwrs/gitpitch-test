# largeVis

---

## 背景
t-SNEの欠点:
- K近傍グラフの構築にvantage-point treeを使っており，計算コストが高い
- グラフの可視化ステップにおいてもデータ数に比例して効率が悪くなる
- 異なるデータに対する最適なパラメータが大きく異なる．パラメータに敏感
これらを主に改善したのがlargeVis. $O(N\log N)$

---

## contributions
- 数百万，数百次元のデータでも計算できる可視化手法の提案
- 高次元，大規模データに対する効率的なK近傍グラフの構築をした
- グラフの可視化のための確率モデルの提案．
  - 目的関数は非同期SGDで効率的に最適化できる．
  - 時間複雑度 $O(N)$，t-SNEは $O(N\log N)$
- 実データにおけるt-SNEとのパフォーマンス比較

---

## k-NN graphの構築
Random Projection tree(RP-tree)に基づくアルゴリズムを提案．

元のアルゴリズムより近傍の探索方法を工夫している．

グラフ構造の可視化:
- よくある次元削減の方法(PCAからt-SNEとか)
- force-directedな方法

うまく可視化できるのはforce-directedな方法だが，計算コストが高い．

+++
force-directedな手法一覧:
- 古典的なfruchterman-Reingo $O(N^2)$
- ForceAtlas  $O(N^2)$
- ForceAtlas2 $O(N\log N)$
- Openord $O(N\log N)$

---
## 余談

各種embeddingの手法を適用して100次元程度に落としてからlargeVisを適用するのもあり！

- [LINE: Large-scale information network embedding](https://github.com/tangjianpku/LINE):
  - 著者が以前提案したネットワークorグラフのembedding手法
- Skip-gram

---

おわり
