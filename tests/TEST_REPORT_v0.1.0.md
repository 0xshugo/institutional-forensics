# Institutional Forensics v0.1.0 Test Report

Date: 2026-09-17  
Target: `SKILL.md` v0.1.0  
Method: one regression case + two cross-domain generalization cases

## Purpose

Test whether the skill can:

- separate observation from explanation
- identify the governing rule
- find exceptions and scope conditions
- separate different entities/objects that share one representation
- reconstruct timeline/operation where needed
- resist a plausible but insufficiently evidenced story
- state what evidence would falsify or confirm the explanation

The most important test is not whether the skill can explain a mystery, but whether it can detect that the stated mystery itself is not yet sufficiently established.

---

# Test A — Regression / adversarial premise

## Prompt

> Why do 高松高等予備校楠上寮 and 楠上第二住宅2号棟 both have the address 高松市楠上町2-1-2?

## Expected behavior

Before explaining the duplication, verify that both objects are actually evidenced at the same address at the same granularity and time.

## Findings

### Confirmed

- 高松高等予備校’s official dormitory page currently lists 楠上寮 as `高松市楠上町2-1-2`.
  - https://takayobi.com/takayobi_life/dormitory.php
- GSI explains that its `住居表示住所` dataset is a dataset of **基礎番号**, does not identify individual buildings, and not every住居番号 necessarily has a corresponding基礎番号.
  - https://www.gsi.go.jp/kihonjohochousa/jukyo_jusho.html
- 高松市 says 楠上町二丁目 is a住居表示実施地区 and explicitly acknowledges that duplicate住居番号 can exist; since 2022-04-01, branch numbers can be assigned to duplicates by application.
  - https://www.city.takamatsu.kagawa.jp/kurashi/kurashi/shomei/zyuukyo/ichiran.html
  - https://www.city.takamatsu.kagawa.jp/kurashi/kurashi/shomei/zyuukyo/jukyo.html
  - https://www.city.takamatsu.kagawa.jp/smph/kurashi/kurashi/shomei/zyuukyo/edabanngou.html
- The national `街区方式による住居表示の実施基準` contains an exception allowing an orderly building number to be used as the住居番号 for certain mid/high-rise buildings.
  - Example official municipal reproduction of 自治省告示第117号:
  - https://www.city.gosen.lg.jp/material/files/group/12/27820583.pdf

### Conflicting / insufficient evidence

- Current private map sources identify `楠上第二住宅2号棟` as `楠上町2丁目1-2`.
  - Example: https://map.yahoo.co.jp/v3/place/MwVkxxRBx_w
- However, accessible government material from 2010/2011 lists **楠上第二住宅 as a facility** at `楠上町2-1-1`, not `2-1-2`.
- A 2026 procurement exists on the Shikoku Local Finance Bureau site for `令和8年度楠上住宅ほか2住宅 住宅用火災警報器取替業務`.
  - https://lfb.mof.go.jp/shikoku/bid/results_products/general/index.html
- A secondary mirror of the tender specification reports both `楠上第二住宅1号棟` and `2号棟` under `楠上町2丁目1-1外`.
- The 2009 Cabinet Secretariat PDF URL cited in the original investigation is currently unavailable (404), so the claimed historical `2-1-2` government entry could not be independently reproduced in this test.

## Result

**v0.1.0: PARTIAL / defect found**

The institutional hypothesis (mid/high-rise building-number exception) is legally plausible, but the **premise that the second building’s official住居番号 is currently and authoritatively `2-1-2` is not yet established**.

The correct output at this stage is **Unresolved**, not `Highly likely`.

### Defect exposed

v0.1.0 starts from `STEP 0 — anomalyを一文で定義する`, but it does not strongly require a prior step that verifies:

1. both sides of the anomaly are true,
2. the sources refer to the same object granularity (complex vs building vs unit),
3. source dates/versions match,
4. a historical citation has not changed or disappeared.

This creates a risk of producing an elegant explanation for an unverified premise.

---

# Test B — Cross-domain: entity separation

## Prompt

> マイナンバーカードは10年有効なのに、なぜ電子証明書は5年で更新なのか。同じカードなのに矛盾していないか？

## Expected behavior

Separate the physical/identity card from the electronic certificate stored on its IC chip before looking for exceptions.

## Findings

Digital Agency explicitly treats them as two separately expiring objects:

- card issued at age 18 or older: until the 10th birthday after issuance
- card issued under age 18: until the 5th birthday after issuance
- electronic certificate: until the 5th birthday after issuance regardless of age

The agency also explains the policy rationale:

- card: face-photo changes and anti-counterfeiting technology lifecycle
- electronic certificate: cryptographic safety can degrade as computing and password-analysis capabilities improve

Primary official source:

- https://www.digital.go.jp/policies/mynumber/expiration-date

## Result

**PASS**

The apparent contradiction disappears at the `Entity / Object` step. No speculative historical narrative is required.

Confidence: **Confirmed**

---

# Test C — Cross-domain: rule vs exception vs operation

## Prompt

> 自転車は道路交通法上「車両」で車道通行が原則なのに、実際には歩道を走れる場合がある。ルールが矛盾していないか？

## Expected behavior

Separate:

1. general rule,
2. statutory exceptions,
3. behavior required while using the exception,
4. enforcement practice.

## Findings

The National Police Agency states:

- bicycles are light vehicles and roadway travel is the principle;
- sidewalk travel is exceptional;
- ordinary bicycles may use sidewalks under specified conditions, including relevant signs, specified rider categories, or concrete road/traffic safety conditions;
- when using sidewalks, pedestrians remain prioritized and speed/position rules apply.

The NPA’s 2026 FAQ also distinguishes legal violation from enforcement operation: merely riding on a sidewalk may ordinarily lead to guidance/warning, while malicious or dangerous violations may lead to enforcement under the bicycle traffic offense system.

Official sources:

- https://www.npa.go.jp/bureau/traffic/bicycle/info.html
- https://www.npa.go.jp/bureau/traffic/bicycle/portal/rule.html
- https://www.npa.go.jp/bureau/traffic/bicycle/portal/faq.html

## Result

**PASS**

The skill correctly separates `General Rule`, `Exception`, and `Operation`. This is an important institutional-forensics pattern: **legality and enforcement policy are not the same layer**.

Confidence: **Confirmed**

---

# Overall result

v0.1.0 has a useful core structure and generalized successfully outside the address domain. However, Test A exposes a release-blocking research-quality weakness:

> The skill can explain a contradiction before proving that the contradiction actually exists in authoritative evidence.

## Required v0.1.1 changes

1. Add a mandatory **STEP -1 — Premise Validation**.
2. Require an **Object Granularity Check** (system / facility / building / unit / account / contract, etc.).
3. Add explicit **Source Drift / Version Drift** handling.
4. If the premise cannot be independently reproduced, stop explanatory escalation and return `Unresolved` or `Premise not established`.
5. Treat historical, inaccessible, or superseded official material as historical evidence, not automatically as current evidence.
6. Add `premise validated` and `source granularity aligned` to Stop Conditions.

## Regression expectation after patch

- Test A → `Unresolved` pending住居表示台帳 / individual assignment record
- Test B → `Confirmed`
- Test C → `Confirmed`

This test report should remain as a regression fixture for future versions.
