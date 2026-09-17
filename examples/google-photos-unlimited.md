# Case Study: Google Photos「無制限ストレージ」の日落とコホート併存

Status: verified case / minor items unresolved  
Skill: `institutional-forensics`  
展開した機構: Claim Dimensions（「無料」分解） / Scope / Cohort / Legacy / Transition / Timeline / Source Drift / H10

## Premise status

**コホートごとに真偽が分裂**

検証対象の通説:

```text
Google Photosのストレージは「無制限」である
（あるいは「無制限だった」）
```

現行のGoogle公式ヘルプを直接確認すると、「無制限」は**同一ページ内で3つの別コホートに対して別々の意味**を持ち続けている。

```text
① 2021年6月1日より前のアップロード
   → 高画質・エクスプレス画質分は「永久に容量カウント対象外」
      = 実質的な無制限の既得権（レガシーコホート）
② Pixel 5以前の端末
   → 「無制限ストレージに無料でバックアップできます」と現行明記
      = 端末限定の生存した無制限
③ 一般新規ユーザー
   → 最大15GB（Gmail・ドライブと共有プール）
      = 無制限は完全に撤廃
```

したがって「無制限は終わった」も「無制限は今もある」も、**コホートを指定しなければ半分ずつ正しい**。ラベルではなくコホート×次元で答える必要がある。

Confidence: **分裂構造はConfirmed（公式ヘルプ日英両版で条文相当の記載を確認）**

---

## Anomaly

```text
「無料」の次元分解:
→ ① 15GBの割当が無料（一般）
   ② 無制限バックアップが無料（Pixel 5以前）
   ③ 旧アップロードの容量課金が発生しない（2021年6月1日前コホート）
の3種類が「無料」の一言で潰れている。
```

さらに保持ポリシー側にも条件が潜む。

```text
「Google フォトを 2 年以上使用していない場合や、
  保存容量を使い切った場合は、写真と動画が削除される可能性があります」
```

「無料保存」の語と「削除リスク」の語が同じページに併存する。

---

## Entities / object levels

| Object | コホート | 現行の値 | function |
|---|---|---|---|
| 一般アカウント | 2021-06-01以降のアップロード | 最大15GB（Gmail/ドライブ共有） | normative |
| レガシーアップロード | 2021-06-01より前の高画質・Express | 容量カウント対象外（恒久） | normative |
| Pixel 5以前の端末バックアップ | 端末限定 | 無制限・無料 | normative |
| 「高画質」ラベル | 表記 | 「保存容量の節約画質」に改称（旧称併記） | explanatory |
| 旧マーケページ | 2021年より前 | "free unlimited photo storage" | marketing |

---

## Initial hypotheses

```text
H4 適用範囲違い / 無制限はコホート（Pixel・旧ユーザー）ごとに生き残っている
H5 新旧ルール混在 / 2021-06-01の制度断層が1つのライブラリ内に併存
H6 経過措置 / 旧アップロードのカウント除外は既得権型の経過措置
H10 同じ語が別概念を表す / 「無制限」= 容量 / 画質 / コホート / 期間の4次元
H1 表記・省略 / 「高画質」→「保存容量の節約画質」への改称
```

---

## Confirmed institutional facts

以下はすべて2026-09-17にcurlで取得し、本文を直接確認した（現行版）。

### 1. 一般枠は15GB・共有プール（日英同一記載）

> You get up to 15 GB of storage or you can buy more.

> 利用できる保存容量は最大 15 GB です。容量は追加購入することもできます。

- https://support.google.com/photos/answer/10100180 （B/D）
- https://support.google.com/photos/answer/10100180?hl=ja （B/D）

### 2. Pixel 5以前は無制限が現行生存

> If you have a Pixel phone that is Pixel 5 or earlier, you get unlimited storage for photos and videos backed up from your device at no charge.

> Google Pixel 5 以前の Google Pixel をお使いの場合、そのデバイスから無制限ストレージに写真と動画を無料でバックアップできます。

「無制限」という語は撤廃されず、**端末コホート限定で現行ヘルプに存在し続けている**。

- 同上（B/D）

### 3. 2021年6月1日前のアップロードは恒久除外（経過措置）

> Any photos or videos backed up in High quality or Express quality before June 1, 2021 don't count on your Google Account storage.

> 2021 年 6 月 1 日より前に高画質またはエクスプレス画質でバックアップした写真と動画は、Google アカウントの保存容量にカウントされません。

同一アカウント内で、**アップロード日によって別レジーム**が適用される。

- 同上（B/D）

### 4. ラベル改称: 高画質 → 保存容量の節約画質

> Storage saver (previously named high quality)

> 保存容量の節約画質（旧称「高画質」）

- https://support.google.com/photos/answer/9284827 （ Manage your storage / B）
- 10100180 日本語版（B）

改称により「画質」の語は残ったが「高」が消え、さらに「Express quality」という別階層が増えた。**ラベルの数が増えるほど「無制限」の記憶と対応付けにくくなる**構造。

### 5. 保持ポリシー側の削除条件

> Google フォトを 2 年以上使用していない場合や、保存容量を使い切った場合は、写真と動画が削除される可能性があります。

- https://support.google.com/photos/answer/10100180?hl=ja （D）

「無料保存」と「削除される可能性」が同一ページに併存する。

---

## Timeline / Source Drift issue

```text
〜2021-05-31  「無制限・無料」（高画質）        ← 旧マーケの記憶の根拠
2021-06-01     一般枠15GBへ。旧アップロードは恒久除外（コホート断層）
2021〜         「高画質」→「保存容量の節約画質」改称 / Express画質追加
現行           Pixel 5以前は無制限の記述が生存 / 旧マーケURLは消失・404
```

- 2020年11月の制度変更告知ブログ（blog.google）は、複数の推定URLが本ラウンドで404。**告知ページ自体がURL漂移**しており、「旧約束の原文」を公式一次で引けなくなる構造が生じている。
- Internet Archiveが一時的オフラインだったため、旧マーケページ（"free unlimited photo storage"）のアーカイブ原文は本ラウンドでは再検証できず → Unresolved。

---

## Contradiction Matrix

| 観察 | H4 コホート | H5/H6 新旧併存 | H10 別概念 | H1 改称 |
|---|---:|---:|---:|---:|
| 一般=15GB（現行明記） | ◎ | - | - | - |
| Pixel 5以前=無制限（現行明記） | ◎ | - | ◎ | - |
| 2021-06-01前=カウント除外（現行明記） | ○ | ◎ | ◎ | - |
| 「高画質」ラベル消滅・節約画質へ | - | ○ | - | ◎ |
| 旧告知ブログURL消失 | - | ○ | - | - |

---

## Current conclusion

### 確認済み事実

- 「無制限」は2021-06-01に一般枠では撤廃（15GB・共有プール）。
- ただし同一ヘルプページ上で、Pixel 5以前（無制限）と2021-06-01前アップロード（恒久除外）という**2つの生存した無制限コホート**が現行明記されている。
- ラベルは「高画質→保存容量の節約画質」に改称され、Express画質が追加された。
- 保持ポリシーには2年非使用・容量超過時の削除条件がある。

### まだ言えないこと

```text
旧マーケ「free unlimited」の原文アーカイブ（IAオフライン）
2020年告知の正確なURLと告知文言
Pixel 6以降の「元の画質」特典の有無・期間（本ラウンド未検証）
```

### Confidence

**コホート分裂構造はConfirmed。旧約束の原文特定はUnresolved。**

---

## What would resolve it

1. Internet Archive復帰後の旧マーケページ（about.google/products/photos、photos.google.com）の2020年時点スナップショット
2. 2020-11-11告知の現行存活URL（blog.google検索インデックス）
3. Pixel 6/7/8世代の元画質バックアップ特典の現行条件（Google One側ヘルプ）

---

## Why this case matters

このケースは `institutional-forensics` の**Scope / Cohort × Legacy / Transition**の中核デモである。

```text
「無制限は終わった」と言ってはいけない
→ Pixel 5以前では終わっていない（現行明記）
→ 2021年6月1日前の分は永久に終わっていない（恒久除外）

「無制限だと言ってはいけない」
→ 一般の新規アップロードは15GB
```

同一プロダクト・同一ページ内でコホートごとに答えが違うとき、**単一のyes/noは構造上存在しない**。問われたら最初に返すべき答えは

```text
「どのコホートの、どの次元の無制限ですか？」
```

である。これは telecom-unlimited と同じ次元分解機構の**コホート併存版**であり、さらに「告知URL自体が漂移する」というSource Driftの二次被害まで含んでいる。
