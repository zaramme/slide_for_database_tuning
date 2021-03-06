# DB周りの最適化を考える基礎知識

---

# 大前提

---

- SQLの速度改善もアプリケーションの速度改善も、本質的には変わらない

---

## そもそもコンピュータにおける検索とはなにか

---

- 配列のデータ構造

---

- バイナリサーチ
- リニアサーチ

---

### オーダー記法


- [参考ページ](https://qiita.com/cotrpepe/items/1f4c38cc9d3e3a5f5e9c)

- O(1)
- O(n)　＝ リニアサーチ
- O(logn)　＝ バイナリサーチ
- O(n^2)　＝　リニアサーチが２種類存在する
- O(n^n)

---

- 処理速度が重いとはなにか
  - 計算時間が長い
  - メモリ使用量が多い
  - オーバーヘッド(通信時間やファイルI/O)が大きい

---

### チューニングの基本的な考え方

---

## 「常日頃から最適化を心がけ、様々な手法を組み合わせて処理速度を早くする」

---

# ではない

---

### 「早すぎた最適化」

### 「ボトルネック理論」

- 調べてね
---

- やみくもに色々試さない
- 定量的な速度低下に対して、
  - どこか重いかのボトルネックを調べて、
  - 最も効果のある手法から試す。
---

## SQLが重いとはなにか

- SQLの内部構造も基本は「配列」と「ソート」

---

- テーブル　= プライマリIDの配列
- インデックス = インデックスでソートされたプライマリIDのテーブル

---

## ・SQLチューニング

- 発行されるSQLをexplainしよう。

- [参考ページ]([https://woshidan.hatenablog.com/entry/2015/06/20/165817])



---
### N+1クエリの排除@ORM

- HasMany関連について、取得したレコードの数だけSQLが発行されている現象
---
### サブクエリ / exist in の排除

- 同様に、サブクエリ / exist in を使っている 場合も、取得レコードの数に対して検索が行われる
  - JOIN >>> サブクエリ / exist in 
- [参考ページ]([http://kkoudev.github.io/blog/2013/09/14/sql/])

---

### whereの最適化

- indexを貼る。
- 場合によっては複合カラムが必要なので注意

---
### join / selectの最適化

- ぶっちゃけあんまりいらない。

---

## DBチューニング / エンジン編
---

## ミドルウェア（MySQL, PostgreSQL, AWS Aurora)
---
- DBエンジン（★印はクラウドサービス
  - MyISAMとInnoDB
  - メモリDB（MemDB、Memcached）
  - 全文検索特化型（Groonga、★ElasticSearch)
  - キーワード検索特化型（★CloudSearch）
  - NoSQL（redis、MongoDB、★RealtimeDatabase、★DynamoDB)
---

- DBチューニング / インフラ編
  - そもそもDBを強くする
  - キャッシュ
  - レプリケーションスレーブ
---
- DBチューニング / インフラ編(その２)
  - クラウド型のDBに切り替え
  - シャーディング
  - 検索用中間テーブル
  - 並列処理


## 

