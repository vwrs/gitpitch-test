# LargeVis
Visualizing Large-scale and High-dimensional Data

- 大規模，高次元データに対する効率的な可視化，次元削減手法の提案．|
- t-SNEの上位互換とも言える |

---

## 背景
- 大規模，高次元データを2or3次元空間に射影して可視化したい！
- 次元削減手法は色々あるが，どれもいまいち．
  - 線形の手法
    - PCA, MDS ... 線形なので実データにはあまり向かないことが多い
  - 非線形な手法
    - Isomap, LLE, Laplacian Eigenmaps等 ... 小規模なデータには良い結果を示すが，高次元の実データを扱う際は局所的，大域的な構造をよく表現できないことが多い(？)
    - t-SNEは局所的，及び大域的な構造を捉えてられている(?)


+++
## t-SNE
- t-SNEは近年非常に有名でよく使われるが，今はビックデータの時代．大規模データには向いていない

欠点
- K近傍グラフの構築にvantage-point treeを使っており，計算コストが高い
- グラフの可視化ステップにおいてもデータ数に比例して効率が悪くなる |
- 異なるデータに対する最適なパラメータが大きく異なる．パラメータに敏感 |
**→これらを主に改善したのがLargeVis.** $O(N\log N)$ |

---

## contributions
- 数百万，数百次元のデータでも計算できる可視化手法の提案
- 高次元，大規模データに対する効率的なK近傍グラフの構築をした
- グラフの可視化のための確率モデルの提案．
  - 目的関数は非同期SGDで効率的に最適化できる．
  - 時間複雑度 $O(N)$，t-SNEは $O(N\log N)$
- 実データにおけるt-SNEとのパフォーマンス比較

---

## 大まかな流れ

![typical pipeline of data visualization](assets/pipeline.png)



---

## k-NN graphの構築
Random Projection tree(RP-tree)に基づくアルゴリズムを提案．

元のアルゴリズムより近傍の探索方法を工夫している．

グラフ構造の可視化:
- よくある次元削減の方法(PCAからt-SNEとか)
- force-directedな方法

うまく可視化できるのはforce-directed(力指向)な方法だが，計算コストが高い．

+++
force-directedな手法:
- fruchterman-Reingo $O(N^2)$
- ForceAtlas  $O(N^2)$
- ForceAtlas2 $O(N\log N)$
- Openord $O(N\log N)$

---
## 余談

各種embeddingの手法を適用して100次元程度に落としてからLargeVisを適用するのもあり！

- [LINE: Large-scale information network embedding](https://github.com/tangjianpku/LINE):
  - 著者が以前提案したネットワークorグラフのembedding手法
- Skip-gram

---

おわり
