# Module: Telecom Contract Forensics

Version: 0.1.2
Status: experimental

このモジュールは `institutional-forensics` を、通信会社の契約約款・料金表・提供条件書・重要事項説明・商品表示・運用FAQの読解に適用するためのドメイン拡張である。

## 1. Why telecom contracts are hard

通信サービスでは、契約条件が一つの文書に閉じていない。

典型的には次の文書群に分散する。

```text
法令・規制
  ↓
基本契約約款
  ↓
料金表 / 別表 / 附則
  ↓
プラン固有の提供条件書
  ↓
重要事項説明
  ↓
運用ポリシー / FAQ
  ↓
商品ページ / 広告表示
```

ただし、これは単純な「上が常に優先」という序列ではない。

確認すべきなのは各文書の **document function** と **incorporation / applicability** である。

例:

- 約款: 基本的な契約関係・通信制御権限を定める
- 料金表: 料金、容量、速度制限条件を具体化する
- 提供条件書: 特定プラン・施策の条件を追加する
- 重要事項説明: 契約前に重要条件を利用者向けに説明する
- FAQ: 現在の運用・解釈を具体化する
- 商品ページ: 利用者向けの要約・訴求。脚注が重要

## 2. Document Stack Record

各文書を次の形式で記録する。

| Field | Meaning |
|---|---|
| issuer | 発行主体 |
| document_type | 約款 / 料金表 / 提供条件書 / 重要事項説明 / FAQ / 商品ページ |
| title | 文書名 |
| version | 版・改訂番号 |
| effective_from | 発効日 |
| effective_to | 終了日（あれば） |
| applies_to | 適用プラン / 契約者群 |
| function | 文書の役割 |
| normative_status | 契約条件そのもの / 説明 / 運用案内 / marketing |
| source | URL |

### Rule

```text
公式サイトに書いてある
!=
すべて同じ法的・契約的重みを持つ
```

また、

```text
約款に書いていない
!=
条件が存在しない
```

料金表、別表、提供条件書、重要事項説明、附則を必ず確認する。

## 3. Claim Decomposition

「無制限」「無料」「定額」「使い放題」「保証」などの語を、そのまま比較しない。

最低限、次の次元に分解する。

### Unlimited dimensions

```text
billing_limit        追加従量料金が発生しないか
volume_limit         利用できるデータ総量に上限があるか
high_speed_limit     高速通信として利用できる量に上限があるか
speed_guarantee      一定速度が保証されるか
throttling_trigger   速度制御の発動条件
throttled_speed      制御後速度
window               月間 / 直近30日 / 1日など
traffic_type         スマホ本体 / テザリング / データシェア / 特定通信
geography            国内 / 海外 / 衛星 / ローミング
network_condition    混雑 / 公平制御 / 設備状況
abuse_condition      機械的通信 / 大量通信 / 通常利用外
```

したがって、

```text
「データ容量無制限」
!=
「常時フルスピード無制限」
!=
「テザリングも同条件で無制限」
!=
「海外でも無制限」
```

## 4. Telecom-specific hypotheses

コア `SKILL.md` §5 の `H0`–`H10` とは別ラベル体系。`TH*` は通信契約ドメイン専用で、コア仮説を上書きしない。

```text
TH0 比較している「無制限」の意味が違う
TH1 商品ページの要約と契約文書の詳細条件の差
TH2 基本約款にある一般的通信制御権限
TH3 プラン固有の定量制限
TH4 テザリング / データシェアだけ別上限
TH5 国内 / 海外で条件が異なる
TH6 月間とrolling windowなど計測期間が異なる
TH7 新旧プラン / 既存契約者で条件が異なる
TH8 料金上限と通信品質上限の混同
TH9 混雑制御と容量超過制御の混同
TH10 広告表現の脚注に条件が集約されている
```

## 5. Workflow

1. 対象会社・ブランド・プラン・契約種別を固定する
2. 調査基準日を固定する
3. 商品ページのclaimを原文で採取する
4. claimを複数次元に分解する
5. Document Stackを作る
6. 基本約款で通信制御の一般権限を確認する
7. 料金表 / 提供条件書でプラン固有条件を確認する
8. 重要事項説明で契約者向け説明を確認する
9. FAQ / 運用案内で現在の運用を確認する
10. 旧版・改定履歴を確認しSource Driftを検出する
11. テザリング・海外・データシェア等を別Objectとして扱う
12. 同じ語を使う他社プランとはclaimではなくdimensionで比較する
13. 反証資料を探す
14. 結論を事実 / 契約上の権限 / 現在の運用 / 未確認に分離する

## 6. Cross-carrier comparison schema

| Dimension | Carrier A | Carrier B | Carrier C | Carrier D |
|---|---|---|---|---|
| Marketing claim | | | | |
| Domestic volume | | | | |
| Fixed numeric threshold | | | | |
| Speed after threshold | | | | |
| Tethering | | | | |
| Congestion control | | | | |
| Fair-use / abnormal-use control | | | | |
| Overseas | | | | |
| Measurement window | | | | |
| Source date | | | | |

## 7. Source priority

優先する。

1. 現行の公式契約約款 / 料金表 / 別表 / 附則
2. 現行の提供条件書・重要事項説明
3. 公式の商品ページ・FAQ・サポート
4. 改定履歴・過去版
5. 官公庁資料
6. 報道・比較サイトは探索用

比較サイトだけで契約条件を断定しない。

## 8. Special cautions

### Contract cohort

同名プランでも加入時期や改定適用日によって条件が異なる可能性がある。

```text
current plan conditions
!=
all historical subscriber conditions
```

### Marketing vs contract

広告表現が直ちに誤りであるとは判断しない。脚注・提供条件と合わせて意味を特定する。

### Network quality

ベストエフォート、混雑制御、設備制御と、契約上の容量上限を混同しない。

### No numeric threshold

固定GB閾値がないことと、通信制御が一切ないことは別である。

## 9. Definition of Done

通信約款調査は、最低でも以下が揃えば完了。

- プランと基準日が固定されている
- Document Stackが作られている
- claimがdimensionに分解されている
- 約款の一般的通信制御条項を確認している
- プラン固有の数値条件を確認している
- テザリング・海外など別scopeを確認している
- 新旧条件を混同していない
- marketing / contract / operationを分離している
- 反証可能性を提示している
