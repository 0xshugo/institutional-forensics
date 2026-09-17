# Test Report — v0.1.5 Correction Regression

Date: 2026-09-17 JST  
Input: examples added in v0.1.4  
Purpose: turn sample-level factual errors into validator regressions without expanding the core workflow.

## Case A — AppleCare / Japanese Civil Code

### Failure found

The v0.1.4 sample correctly challenged the folk claim that Japanese consumer electronics have a simple statutory one-year manufacturer warranty, but then introduced a new overbroad negative claim:

```text
物の売買には対応する「1年」規定はない
```

This is false.

Current Civil Code Article 566 contains a one-year **notice period** for certain lack-of-conformity claims in sales: the buyer must generally notify the seller within one year after learning of the lack of conformity in kind or quality, subject to the statutory exception.

Official source:
- https://laws.e-gov.go.jp/law/129AC0000000089

### Corrected model

```text
Apple one-year limited warranty
!=
Civil Code Article 566 one-year notice period
!=
Civil Code Article 166 limitation period
```

Apple itself describes its one-year limited warranty as a voluntary manufacturer warranty offered in addition to consumer-law rights.

Official Apple source:
- https://www.apple.com/jp/legal/warranty/products/accessory-warranty-japanese.html

### Regression rule

A conclusion that refutes a user's premise must also falsify decisive replacement claims such as:

```text
不存在 / never / only / 唯一
```

Result: **PASS after v0.1.5 validator update.**

---

## Case B — Google Photos legacy storage

### Failure found

The v0.1.4 sample promoted a current policy statement into permanence by describing pre-2021 qualifying backups as:

```text
永久に容量カウント対象外
恒久除外
```

Google's current official help supports a narrower claim: qualifying photos/videos backed up before 2021-06-01 **do not count toward Google Account storage under the current stated policy**.

Official source:
- https://support.google.com/photos/answer/10100180?hl=ja

The same help ecosystem also distinguishes storage/quota policy from content-retention/deletion conditions.

### Corrected model

```text
current quota exemption
!=
permanent promise
!=
retention guarantee
```

The previous sample also treated `Pixel 5 and earlier` too coarsely. The current overview page supports the top-level statement, but detailed investigation should decompose:

```text
Pixel model × backup quality × upload date
```

before making device-generation-specific claims.

### Regression rule

Do not convert a current state into a perpetual commitment unless the source explicitly guarantees duration. Do not move between neighboring dimensions without evidence.

Result: **PASS after v0.1.5 validator update.**

---

## Core design conclusion

No new mandatory workflow step was required.

The existing fast path remains:

```text
Premise → Document Function → Claim Dimensions → Falsification
```

The defects were caused by insufficient use of the last two stages, not by a missing stage.

v0.1.5 therefore strengthens:

1. falsification of decisive negative/exclusive claims;
2. separation of current state from permanent promise;
3. separation of adjacent dimensions (quota/retention, notice/limitation/warranty).

This preserves the v0.1.3 design goal: **short enough to run consistently, strict enough to fail when evidence structure is missing.**
