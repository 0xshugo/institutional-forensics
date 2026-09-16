# Institutional Forensics

Evidence-first skill for investigating apparently contradictory rules, exceptions, contracts, legacy behavior, and real-world operations.

**Version:** v0.1.2 — experimental

## What it does

制度・規則・契約・仕様の「なぜこうなっている？」を、まず前提そのものから検証し、必要に応じて文書の役割と言葉の意味まで分解して追跡します。

```text
Premise Validation
  ↓
Entity / Object Granularity
  ↓
Document Stack / Function
  ↓
Claim Dimensions
  ↓
General Rule
  ↓
Exception
  ↓
Scope / Cohort / Version
  ↓
Timeline + Source Drift
  ↓
Actual Operation
  ↓
Falsification
  ↓
Evidence-backed explanation
```

対象例:

- 行政制度
- 住所・地番・住居表示
- 料金・契約・通信約款
- 税制・補助制度
- 標準・規格
- 公共調達
- レガシーIT仕様
- 組織内ルール

## Repository structure

```text
.
├── SKILL.md
├── README.md
├── CHANGELOG.md
├── LICENSE
├── modules/
│   ├── jp-address.md
│   └── telecom-contracts.md
├── examples/
│   ├── kusunokamicho-2-1-2.md
│   └── mobile-unlimited-jp-4carriers.md
└── tests/
    ├── TEST_REPORT_v0.1.0.md
    └── TEST_REPORT_v0.1.1-telecom.md
```

## Why v0.1.2 exists

v0.1.1を日本の携帯4社の通信約款・料金条件へブラインド適用したところ、骨格は機能した一方で2つの不足が見つかりました。

### 1. Document Stack / Document Function

通信サービスの条件は基本約款だけでは完結せず、料金表、別表、提供条件書、重要事項説明、FAQ、商品ページに分散します。

公式資料であることと、その資料が完全な契約条件を定めることは同義ではありません。

### 2. Claim Dimensions

「無制限」「無料」「定額」「保証」のような言葉は、そのまま比較できません。

たとえば通信の「無制限」は、

```text
料金上限
データ総量
高速通信量
速度保証
速度制御条件
テザリング
地域
計測期間
```

などに分解して比較します。

これにより「同じ言葉だが、実際には別の条件を比較していた」という偽の矛盾を減らします。

## Core rules

> Verify the contradiction before explaining the contradiction.

> Compare normalized dimensions, not labels.

> An official source still needs a document-function check.

そのうえで、

> A contradiction is not an error until rule, exception, scope, timeline, representation, and operation have been separated.

調査結果は必ず、

- 確認済み事実
- 制度・契約上の説明
- 最も整合的な仮説
- 未確認事項

に分けます。

## Domain modules

### Japanese address forensics

```text
modules/jp-address.md
```

地番、基礎番号、住居番号、棟番号、各戸番号などを別レイヤーとして扱います。

### Telecom contract forensics

```text
modules/telecom-contracts.md
```

約款、料金表、提供条件書、重要事項説明、FAQ、商品ページをDocument Stackとして扱い、「無制限」等を意味次元へ分解します。

## Case studies

### Kusunokamicho 2-1-2

元の住所ケースは、Premise Validationの必要性を発見した **Unresolved regression case** として残しています。

### Japanese four-carrier unlimited plans

```text
examples/mobile-unlimited-jp-4carriers.md
```

NTTドコモ、au、SoftBank、楽天モバイルの現行無制限系プランを使い、ラベルではなく容量・速度・テザリング・計測期間等を分解して比較したケースです。

## Usage

AIエージェントに `SKILL.md` と必要なdomain moduleを読み込ませ、対象現象を渡します。

例:

```text
この通信プランは「無制限」と書いてあるのに速度制御があります。
institutional-forensics と telecom-contracts module を使い、
まず前提を検証し、Document Stackを作り、
「無制限」の意味を独立したdimensionへ分解して調査してください。
```

## Validation status

Current validation includes:

1. address-system regression / adversarial premise
2. My Number card vs electronic-certificate validity periods
3. bicycle roadway rule vs sidewalk exceptions and enforcement operation
4. Japanese four-carrier telecom-contract blind test

The telecom test exposed missing abstractions in v0.1.1 and directly produced v0.1.2.

## Status

Experimental. The method is intentionally being tested with unfamiliar domains before broader contributor onboarding.

## License

MIT
