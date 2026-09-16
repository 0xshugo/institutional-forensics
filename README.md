# Institutional Forensics

Evidence-first skill for investigating apparently contradictory rules, exceptions, legacy behavior, and real-world operations.

**Version:** v0.1.1 — experimental

## What it does

制度・規則・仕様の「なぜこうなっている？」を、まず前提そのものから検証し、次のレイヤーに分けて追跡します。

```text
Premise Validation
  ↓
Observation
  ↓
Entity / Object Granularity
  ↓
General Rule
  ↓
Exception
  ↓
Scope / Jurisdiction / Version
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
- 料金・契約
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
│   └── jp-address.md
├── examples/
│   └── kusunokamicho-2-1-2.md
└── tests/
    └── TEST_REPORT_v0.1.0.md
```

## v0.1.1 change

v0.1.0の実地試験で、制度上もっともらしい説明を作る前に「その謎の前提が一次資料で本当に成立しているか」を強制確認する必要があることが判明しました。

v0.1.1では以下を追加しています。

- mandatory `Premise Validation`
- object granularity check
- `H0 = premise error / granularity mismatch`
- Source Drift / Version Drift check
- `Premise not established` confidence state
- legality / operation / enforcement separation

試験記録:

- `tests/TEST_REPORT_v0.1.0.md`

## Core rule

> Verify the contradiction before explaining the contradiction.

そのうえで、

> A contradiction is not an error until rule, exception, scope, timeline, representation, and operation have been separated.

調査結果は必ず、

- 確認済み事実
- 制度上の説明
- 最も整合的な仮説
- 未確認事項

に分けます。

## Domain modules

v0.1.1時点では日本の住所制度を最初のドメインモジュールとして実装しています。

```text
modules/jp-address.md
```

住所固有ロジックはコアへ埋め込まず、今後、

```text
pricing-and-fees
contracts-and-terms
tax-and-subsidy
technical-standards
public-procurement
legacy-it-specs
```

などを追加できる構成です。

## Usage

AIエージェントに `SKILL.md` を読み込ませ、対象現象を渡します。

例:

```text
この料金プランは公式料金表と請求額が違って見える。
institutional-forensics の手順で、まず前提を検証し、対象粒度、一般則、例外、契約時期、Source Drift、経過措置を分けて調査して。
```

住所問題では `modules/jp-address.md` も併用します。

## Validation

Initial tests cover:

1. address-system regression / adversarial premise
2. My Number card vs electronic-certificate validity periods
3. bicycle roadway rule vs sidewalk exceptions and enforcement operation

The original Kusunokamicho case is deliberately retained as an **Unresolved regression case** because it exposed the need for premise validation.

## Status

Experimental. The core method has passed cross-domain tests, but additional domain modules and more adversarial cases are still needed before treating it as mature research infrastructure.

## License

MIT
