---
name: institutional-forensics
description: 見かけ上の矛盾・重複・不整合を、前提・文書機能・意味次元・反証の最小必須パスで検証し、必要時だけ例外・時系列・運用へ展開するEvidence-first Skill。
version: 0.1.6
language: ja
status: experimental
---

# Institutional Forensics / 制度フォレンジック

制度・規則・契約・仕様の「なぜこうなっている？」を、AIがもっともらしく説明する前に、まず壊れにくい最小手順で検証する。

## Core principle

```text
Verify the contradiction before explaining it.
Compare dimensions, not labels.
Official != same function.
Confirmed must not rest on inference alone.
A refutation also needs falsification.
Current state != permanent promise.
```

---

# 1. Mandatory Fast Path

通常はこの4段階だけを必須とする。

## 1. Premise

その「矛盾」「重複」「例外」は本当に存在するか。

必須:
- 両側の事実を別々に確認
- 同じ対象粒度か確認
- 同じ時点・版か確認
- 古い資料なら後続版を確認

出力:

```text
Premise status:
- Established
- Partially established
- Not established
- Refuted
```

`Not established` / `Refuted` なら、元の謎の説明を進めない。

---

## 2. Document Function

主要Sourceが何をする文書かを分ける。

```text
normative     ルール・契約を定める
explanatory   条件や制度を説明する
operational   実運用を説明する
marketing     商品・制度を要約して表示する
historical    過去時点の状態を示す
```

ルール:

```text
公式資料である
!=
完全な条件をその文書だけで確定できる
```

複数文書に条件が分散する場合だけ、Document Stackを作る。

例:

```text
法令 / 基本約款
→ 別表 / 料金表 / 附則
→ 個別提供条件
→ 重要事項説明
→ FAQ / 運用案内
→ 商品ページ / 広告
```

---

## 3. Claim Dimensions

「無制限」「無料」「保証」「永久」「対象」「同一」など、複数解釈できる言葉は分解する。

例:

```text
無制限
→ 容量 / 高速容量 / 速度 / 料金 / テザリング / 地域 / 計測期間

無料
→ 初期費用 / 月額 / 従量 / 条件付き割引 / 期間限定 / 還元

保証
→ 法定救済 / 通知期間 / 時効 / 商用保証 / サービス契約

保存
→ quota counting / upload entitlement / retention / deletion policy
```

比較はラベル同士ではなく、正規化したdimension同士で行う。

特に次を禁止する。

```text
current state → permanent promise への無根拠な昇格
quota exemption → retention guarantee への無根拠な横滑り
```

---

## 4. Falsification

有力な説明を補強する前に、壊せる証拠を探す。

最低1つ答える。

```text
この説明が誤りなら、どんな一次資料が存在するはずか？
どんな事例が見つかれば、この結論は覆るか？
```

### Decisive negative claims

次のような強い否定・排他命題は、最終結論と同じくらい厳しく反証する。

```text
存在しない
一度もない
唯一
only
never
no rule
```

必要なら:
- 一次資料全文を検索
- 隣接条文・附則・別表を確認
- 同じ制度の関連法・特別法を確認
- 別Document Functionの資料に反例がないか確認

**誤った通説を否定しただけで、代替説明が正しいことにはならない。**

反証確認後にのみ結論を出す。

---

# 2. Conditional Expansion

以下は必要な場合だけ展開する。毎回全部実行しない。

## Object / Granularity

対象粒度が違う疑いがあるとき。

例:

```text
施設 != 建物 != 住戸
プラン != 個別契約 != アカウント
規格 != 製品実装
```

## General Rule / Exception

一般則と例外の差が問題の中心であるとき。

## Scope / Cohort

地域、対象者、加入時期、旧契約者、新規契約者、端末世代などで条件が違うとき。

## Timeline / Source Drift

制度改正、約款改定、古い資料、新旧UIなどが混在するとき。

## Operation / Enforcement

制度上のルールと実際の運用・取締・監査が違うとき。

## Legacy / Transition

経過措置、既得権、従前扱いが疑われるとき。

## Implementation / Human Error

実装制約、データ不備、単純誤記が候補になるとき。

---

# 3. Evidence Model

## Evidence Classes

| Class | 定義 |
|---|---|
| A | 個別案件へ直接適用される一次資料 |
| B | 制度・契約を定める一次資料 |
| C | 歴史的一次資料 |
| D | 公式な説明・運用資料 |
| E | 信頼できる二次資料 |
| F | 観測・推定 |

原則:

```text
Confirmed の骨格 = A〜D
補強 = E
探索・仮説 = F
```

**F単独でConfirmedにしない。**

---

# 4. Minimal Evidence Identity

主要Sourceごとに、必須は5項目だけ。

```text
issuer        発行主体
function      normative / explanatory / operational / marketing / historical
object_level  制度 / 施設 / 建物 / 契約 / プラン / アカウント等
valid_at      どの時点を表すか
source        URL / 文書ID / 資料名
```

必要時のみ追加:

```text
version
published
applies_to
status
field
```

---

# 5. Hypothesis Set

必要なら次を初期仮説として使う。

```text
H0 前提誤り / 粒度違い
H1 表記・省略
H2 誤記・データ不備
H3 例外規定
H4 適用範囲違い
H5 新旧ルール混在
H6 経過措置
H7 実運用差
H8 実装制約
H9 個別特例
H10 同じ語が別概念を表す
```

---

# 6. Mandatory Output

```markdown
# Conclusion
Confidence: Confirmed / Highly likely / Plausible / Unresolved

## Premise status
Established / Partially established / Not established / Refuted

## What is actually being compared
対象と必要なClaim Dimensions。

## Governing evidence
主要SourceとDocument Function。

## Explanation
確認済み事実 / 制度・契約上の説明 / 仮説を分離。

## Falsification
何が見つかれば結論が覆るか。
決定的な否定命題がある場合、その反証確認も記録。

## Unresolved
未確認事項。
```

必要な場合のみ追加:

```text
Timeline
Exception matrix
Document Stack
Cohort comparison
Operation / enforcement
```

---

# 7. Validator

出力前に共通チェックリストで自己検査する。必須項目・決定的否定命題・永久表現・FAIL条件の全文は **`tests/VALIDATOR_CHECKLIST.md`** を参照（ここでは重複掲載しない）。

重大な欠落があれば、Confidenceを下げるか調査を追加する。

---

# 8. Anti-examples

## BAD 1 — Premiseを飛ばす

```text
楠上第二住宅2号棟は棟番号特例で2-1-2になった。
```

GOOD:

```text
制度上は説明可能。ただし個別住所の一次資料が不足しているためUnresolved。
```

## BAD 2 — 基本約款だけで契約全体を決める

```text
基本約款に200GB制限がないので、このプランは完全無制限。
```

GOOD:

```text
固定容量閾値と、混雑時制御・速度制御を別dimensionとして確認し、必要なDocument Stackを辿る。
```

## BAD 3 — 通説の反証から新しい過剰一般化を作る

```text
「法定保証1年」は誤り → 売買には1年の規定は存在しない。
```

GOOD:

```text
購入日起点の商用保証と、民法566条の通知期間、166条の消滅時効を別dimensionとして確認する。
```

## BAD 4 — 現在の扱いを永久保証と読む

```text
現在カウント対象外 → 永久にカウントされず永久保存される。
```

GOOD:

```text
現行のquota ruleだけをConfirmedとし、将来不変性とretentionは別途確認する。
```

詳細: `examples/anti-patterns.md`

---

# 9. Compact Agent Prompt

```text
あなたはInstitutional Forensics Agentです。

対象: {{PHENOMENON}}

必須:
1. Premiseを検証
2. 主要SourceのDocument Functionを分類
3. 曖昧なclaimを必要なdimensionへ分解
4. 有力説明と、その説明を支える強い否定命題の反証を探す

必要な場合だけ、例外、scope/cohort、timeline/source drift、operation/enforcement、legacyを追加調査してください。

主要Sourceごとに最低限 issuer / function / object_level / valid_at / source を記録してください。

ConfirmedはF（推定・観測）単独では認めません。
現行状態から「永久」を推定しないでください。
証拠不足ならUnresolvedを選んでください。

最後にvalidatorを実行してください。
```

---

# 10. Domain Modules

現在:

```text
modules/jp-address.md
modules/telecom-contracts.md
```

コアを増やす前に、ドメイン固有知識はmodule側へ寄せる。

各 module の仮説ラベル（例: `AH0`–`AH10`、`TH0`–`TH10`）は §5 のコア `H0`–`H10` とは別体系であり、上書きしない。

次の新規moduleは一度に1本だけ追加し、共通SKILLの変更が本当に必要かを先に検証する。

---

# 11. Definition of Done

```text
短く走れる
欠落がvalidatorで分かる
事実と仮説が分かれる
反証可能
否定命題も反証済み
第三者が追試できる
Unresolvedで止まれる
```
