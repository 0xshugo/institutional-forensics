# Institutional Forensics

Evidence-first skill for investigating apparently contradictory rules, exceptions, legacy behavior, and real-world operations.

**Version:** v0.1.0 — experimental

## What it does

制度・規則・仕様の「なぜこうなっている？」を、次のレイヤーに分けて追跡します。

```text
Observation
  ↓
General Rule
  ↓
Exception
  ↓
Scope / Jurisdiction / Version
  ↓
Timeline
  ↓
Actual Operation
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
└── examples/
    └── kusunokamicho-2-1-2.md
```

## v0.1.0 scope

v0.1.0では共通調査フレームワークを定義し、日本の住所制度を最初のドメインモジュールとして実装しています。

住所固有のロジックをコアへ埋め込まず、今後、

```text
pricing-and-fees
contracts-and-terms
tax-and-subsidy
technical-standards
public-procurement
legacy-it-specs
```

などを追加できる構成にしています。

## Core rule

> A contradiction is not an error until rule, exception, scope, timeline, and operation have been separated.

調査結果は必ず、

- 確認済み事実
- 制度上の説明
- 最も整合的な仮説
- 未確認事項

に分けます。

## Usage

AIエージェントに `SKILL.md` を読み込ませ、対象現象を渡します。

例:

```text
この料金プランは公式料金表と請求額が違って見える。
institutional-forensics の手順で、一般則・例外・契約時期・経過措置を分けて調査して。
```

住所問題では `modules/jp-address.md` も併用します。

## Status

Experimental. The method is designed for reproducible research, but domain modules still need expansion and real-world validation.

## License

MIT
