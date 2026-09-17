# Case Study: 「家電には法定保証1年がある」という通説（AppleCare / 日本・米国）

Status: verified case / minor items unresolved  
Skill: `institutional-forensics`  
展開した機構: Claim Dimensions / Scope / Cohort（法域） / Timeline / Source Drift / Legacy / Transition

## Premise status

**崩壊**

検証対象の通説:

```text
家電には「法定保証1年」がある
```

この前提は、現行の日本法を直接当たると成立しない。

- 物販（iPhone等の購入）の法定の責任根拠は消費者契約法ではなく**民法の契約不適合責任**（民法415条・562条・563条）。時効は**権利を行使することができることを知った時から5年**（民法166条1項1号）。
- 「1年」という数字の実在の所在は**請負**の通知期間（民法637条: 不適合を知った時から1年以内）。物の売買には存在しない。
- 消費者契約法には**法定保証期間の規定そのものが存在しない**（現行法・2009年codificationの両方で条文上確認）。
- 「法定2年」は**EU**の枠組み（Directive (EU) 2019/771 Art.10(1): 引渡しから2年）。日本の法源ではない。
- Appleの「1年」は**契約上の有限保証**（commercial warranty）であり、法定ではない。

したがって「法定保証1年」は、**別レイヤーの語（H10）と別法域の数字（Scope/Cohort）と旧法の記憶（Timeline Drift）が混ざった複合誤り**である。

Confidence: **前提は誤りと確認**（詳細は下記。細部はUnresolved節参照）

---

## Anomaly

同じ「1年保証」「無制限」という語が、少なくとも4つの別概念を指して流通している。

```text
「1年」
→ ① Apple Limited Warranty（契約・全世界共通の商用保証）
   ② 民法637条（請負のみ・知った時から1年の通知期間）
   ③ EU指令（実は2年。記憶と混同されやすい）
   ④ 旧民法瑕疵担保（売買は原則6ヶ月。1年ですらない）

「無制限」
→ ① サービスイベント「回数」が無制限（2025年〜日本・米国）
   ② 回数以外の次元は無制限ではない:
      - 都度のサービス料（日本: 画面のみ¥3,700 / その他¥12,900、米国: $29 / $99）
      - 対象範囲（標準AppleCare+は盗難・紛失を除外）
      - プラン有効期間（解約・終了まで）
```

比較はラベル同士ではなく、レイヤーとdimensionに分解して行う。

---

## Entities / object levels

| Object | レイヤー | 日本 | 米国 | function |
|---|---|---|---|---|
| 契約不適合責任（民法） | 法定 | 知った時から5年（166条1項1号） | — | normative |
| 請負の瑕疵通知（民法） | 法定 | 知った時から1年（637条） | — | normative |
| 消費者契約法 | 法定 | 法定保証期間の規定なし | — | normative |
| Sales of Goods指令 | 法定(EU) | 適用なし | 適用なし（引渡しから2年） | normative |
| Apple Limited Warranty | 契約(基本) | 1年 | 1年 | normative |
| AppleCare+ 標準 | 契約(延長) | 事故破損 無制限 / 盗難紛失 除外 | 同左 | normative |
| AppleCare+ 盗難・紛失プラン | 契約(別プラン) | 年2回（約款別紙） | Theft & Loss variant | normative |
| AppleCare One | 契約(バンドル) | — | 事故無制限 / 個人3件・家族6件/年 | normative |
| apple.com/applecare | マーケ | 「回数制限なし」 | "unlimited accidents" | marketing |

---

## Initial hypotheses

```text
H0 前提誤り / 日本法に「法定保証1年」は存在しない
H3 例外規定 / 標準AppleCare+は盗難・紛失を除外 → 別プラン
H4 適用範囲違い / 「2年」はEUの数字。日本と米国の法ではない
H5 新旧ルール混在 / 事故破損は2022年「12か月につき2回」→2025年「無制限」
H6 経過措置 / 旧約款PDFが公開残り、新旧が併存流通
H10 同じ語が別概念を表す / 「保証」= 法定 / 商用 / 延長プラン / 回数制限の4レイヤー
```

---

## Confirmed institutional facts

以下はすべて2026-09-17にcurlで取得し、本文を直接確認した。

### 日本 — 法定レイヤー

**1. 現行消費者契約法に法定保証期間の規定はない**

現行の消費者契約法（最終改正: 令和4年法律第59号）の2条は消費者・事業者・消費者契約・適格消費者団体の定義のみ。適合性担保・解除・期間の規定は存在しない。

- https://www.japaneselawtranslation.go.jp/ja/laws/view/4624 （法務省公式翻訳サイト / B）

2009年codification（最終改正: 平成21年法律第49号）でも2条の構造は同じであり、「瑕疵」「不適合」の語は8条（免責条項の無効）にしか現れない。

- https://www.japaneselawtranslation.go.jp/ja/laws/view/2036 （C）

**2. 物販の法定責任は民法の契約不適合責任・時効5年**

- 民法415条（債務不履行による損害賠償）
- 民法562条（買主の追完請求権: 種類・品質・数量が契約の内容に適合しないとき）
- 民法563条（代金減額請求権）
- 民法166条1項1号（権利を行使することができることを**知った時から5年**）

- https://ja.wikisource.org/wiki/民法_(日本) （全文照合 / E・コミュニティ管理、法務省サイトの現行codification構造と整合）

**3. 「1年」の実在の所在は請負（民法637条）**

> 注文者がその**不適合を知った時から一年以内**にその旨を請負人に通知しないときは…履行の追完の請求、報酬の減額の請求、損害賠償の請求及び契約の解除をすることができない。（民法637条）

物の売買には対応する「1年」規定はない。

- https://ja.wikisource.org/wiki/民法_(日本) （E）

### EU — 法定レイヤー

**4. 「法定2年」はEU指令**

> The seller shall be liable to the consumer for any lack of conformity which exists at the time when the goods were delivered and which becomes apparent **within two years** of that time.（Directive (EU) 2019/771, Article 10(1)）

- https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32019L0771 （B）

### Apple — 契約レイヤー（日本）

**5. AppleCare+約款日本版 2022-03-08: 事故破損は「12か月につき2回」**

> Apple がお客様に対して 本プランの領収書原本に記載されている購入日を基準に **12 か月の期間につき 2 回のサービスイベント**を提供することにより、ADH のサービスは終了し…

- https://www.apple.com/legal/sales-support/applecare/applecareplus/2203/220308_applecareplus_jp.pdf （B/C）

**6. AppleCare+約款日本版 2025-03-04 §3.4: 「サービスイベントを無制限に」**

> お客様は、本プランが有効である間…サービスイベントを**無制限**に受けることができます。

各イベントにサービス料（iPhone 画面のみ¥3,700等）は残る。

- https://www.apple.com/legal/sales-support/applecare/applecareplus/2503/250304_applecareplus_jp.pdf （B）

**7. 標準約款は盗難・紛失を除外（2022年版・2025年版とも）**

> Apple は、以下に関するハードウェアサービスまたは ADH サービスを提供しません。…（c）**紛失または盗難にあった対象機器の交換**

- 同上PDF 2件（B）

**8. 盗難・紛失は別約款（AppleCare+ 盗難・紛失プラン）**

改定版PDFが日付付きアーカイブとして公開され続けている（例: 2026-09-09版あり）。

- https://www.apple.com/legal/sales-support/applecare/applecareplus/ （index / B）

**9. 約款自身が消費者契約法の適用を認める**

> 本プランのその他の規定にかかわらず、**日本の消費者契約法の適用がある場合**、Appleの債務不履行または不法行為により生…（2025年版）

- 2503版PDF（B）

### Apple — 契約レイヤー（米国）

**10. AppleCare+約款米国版 2022-03-08: "two (2) Service Events within each twelve (12)-month period"**

- https://www.apple.com/legal/sales-support/applecare/applecareplus/2203/220308_applecareplus_us.pdf （B/C）

**11. AppleCare+約款米国版 2025-03-04 §3.4: "unlimited Service Events"**

> You are eligible to receive **unlimited Service Events** for your Covered Device while the Plan is active…

- 同一URLの2503版: https://www.apple.com/legal/sales-support/applecare/applecareplus/2503/250304_applecareplus_us.pdf （B）

**12. 米国版も標準約款は盗難・紛失を除外（§4(c)）**

> (c) To replace Covered Equipment that is **lost or stolen**

米国では盗難・紛失は "AppleCare+ with Theft & Loss" variant として別途。

- 2503版US PDF（B）

**13. Apple自身が「1年保証は法定権利に加算される」と表明**

> the benefits conferred by Apple's **One Year Limited Warranty** are **in addition to** all rights and remedies conveyed by such consumer protection laws and regulations…

- https://www.apple.com/legal/warranty/statutoryrights.html （D）

### Apple — マーケティングレイヤー

**14. 日本語マーケ: 「回数制限なし」＋盗難・紛失は「1年間に2回まで」**

- https://www.apple.com/jp/applecare/ （marketing / D）

**15. 英語マーケ: AppleCare One は "unlimited" だが事故クレームは個人3件/家族6件・年**

- https://www.apple.com/applecare/ （marketing / D）

---

## Timeline / Source Drift issue

```text
2022-03-08  日本・米国とも 事故破損 = 12か月につき2回（約款本文で確認）
     ↓      （中間改定版の特定は未実施。indexには多数の日付版が並ぶ）
2025-03-04  日本・米国とも 事故破損 = 無制限（約款本文で確認）
```

- Appleは旧版PDFを削除せず公開アーカイブに残すため、**同一製品名・同一URL系列で異なる値が併存流通**する。検索で2022年版を引くと「2回」が、2025年版を引くと「無制限」が「一次資料」として現れる。
- 民法は2017年改正（2020年施行）で瑕疵担保→契約不適合責任へ転換。旧法の記憶（売買は短期時効）が「法定1年」通説の温床になった可能性が高いが、旧法条文（旧566条の6ヶ月等）は今回の取得経路では本文を確定できていない → Unresolved。

---

## Contradiction Matrix

| 観察 | H0 前提誤り | H4 法域違い | H5 新旧混在 | H10 別概念 |
|---|---:|---:|---:|---:|
| 現行消費者契約法に保証期間規定なし | ◎ | - | - | - |
| 民法166条=5年（売買） | ◎ | - | - | - |
| 民法637条=1年（請負のみ） | ○ | - | - | ◎ |
| EU指令=2年 | - | ◎ | - | - |
| Apple 1年 Limited Warranty | - | - | - | ◎ |
| 2022約款=2回/12か月 | - | - | ◎ | - |
| 2025約款=無制限 | - | - | ◎ | - |
| マーケ「回数制限なし」+従量課金残存 | - | - | - | ◎ |

---

## Current conclusion

### 確認済み事実

- 日本の現行法に「法定保証1年」は**存在しない**。物販は契約不適合責任で原則5年（知った時から）、請負のみ1年（637条）。
- 消費者契約法には法定保証期間の規定がない（現行・2009年の両codificationで確認）。
- 「2年」はEU指令の数字（Art.10(1)）。
- Appleの1年は契約上の商用保証であり、Apple自身の法定権利ページも「加算」と明記。
- AppleCare+の事故破損は2022年「12か月につき2回」→2025年「無制限」に改定（日本・米国とも約款本文で確認）。
- 標準約款は盗難・紛失を除外（日本・米国とも）。盗難・紛失は別プラン・別約款。
- マーケの「無制限/回数制限なし」は**回数次元のみ**真であり、回数・対象・期間・料金の次元分解が必要。

### まだ言えないこと

```text
「法定保証1年」通説の歴史的出典
（旧民法瑕疵担保の記憶か、EU2年との混同か、
  Apple 1年保証の「法定」への誤付着か）
```

### Confidence

**前提「法定保証1年」は誤り（Confirmed）。通説の発生源はUnresolved。**

---

## What would resolve it

1. 旧民法566条・570条・旧637条の本文（官報NDLデジタル化資料の直接取得。Wikisourceの公布時版はindexトランスクリプションで本文inline取得不可だった）
2. AppleCare+約款の2022→2025の正確な改定点（indexの日付版を順に差分）
3. 「法定保証1年」を掲げる販売店ページ・Q&Aサイトの一次収集（通説の流通経路特定）
4. カリフォルニア州の保証法（SB 210等）の条文 — leginfoが取得不可のため未検証

---

## Why this case matters

このケースは `institutional-forensics` の**Claim Dimensions × H10 × Timeline Drift**の複合デモである。

```text
「保証」を分解しないまま比較すると、
法定（民法5年 / EU 2年）
商用（Apple 1年）
延長プラン（AppleCare+ 回数無制限・回数2回）
盗難紛失（別プラン 年2回）
の4レイヤーが一つの「1年/無制限」に潰れる。
```

最初の問いを

```text
「なぜAppleCare+は高いのか」
```

にすると、このレイヤー混同ごと飲み込んで間違った土俵で議論する。

正しい順序は、

```text
「法定保証1年」は本当に法源があるのか（Premise）
↓
その「1年」は何の1年か（H10 / レイヤー分解）
↓
どの法域の数字か（Scope / Cohort）
↓
約款はいつの版か（Timeline / Source Drift）
↓
「無制限」は何が無限で何が有限か（Claim Dimensions）
```

である。

さらに重要な点として、**このケースは調査中に調査者自身の前提を崩した**。当初の作業仮説は「法定保証2年（適合性担保）vs 商用1年」だったが、消費者契約法の現行条文を直接確認したところ適合性担保の規定自体が存在せず、仮説の法源配置が誤りであった。これは「記憶で条文番号を語らない」というEvidence-first原則の実演である。
