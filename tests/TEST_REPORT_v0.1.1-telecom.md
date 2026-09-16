# Test Report — Telecom Contracts Blind Test

Date: 2026-09-17 JST
Input skill version: v0.1.1
Domain: Japanese mobile telecom contracts
Carriers: NTT Docomo / KDDI-au / SoftBank / Rakuten Mobile

## Test question

> 携帯4社の「ギガ無制限」「データ使い放題」は同じ意味か。無制限なのに通信制御、速度制限、テザリング条件が存在するのはなぜか。

This was selected as a blind cross-domain test because the v0.1.1 core had not been designed specifically for telecom contracts.

## Pass criteria

- premise is validated before explanation
- current plan and current documents are identified
- marketing claims are not treated as full contract definitions
- contract terms and current operation are separated
- quantitative restrictions are recovered when present
- no restriction is invented when a fixed threshold is not published
- tethering / roaming / data share are handled as separate scopes
- historical and current conditions are not mixed
- the method can compare four carriers without forcing false equivalence

## Result summary

Overall: **PARTIAL PASS → design improvement required**

v0.1.1 correctly triggered premise validation, scope separation, source-drift checks and rule/operation separation. However, two missing abstractions became obvious.

### Failure / weakness 1 — Document hierarchy was underspecified

A telecom plan cannot be reconstructed from the base contract terms alone.

Relevant facts are distributed across:

```text
base contract terms
pricing tables / appendices
plan-specific provision documents
important-matters explanation
operational FAQ / support
product / marketing page
```

v0.1.1 classified evidence by source quality but did not sufficiently classify **document function**.

A product page can be an official source while still functioning as a summary rather than the complete contractual definition.

### Failure / weakness 2 — Ambiguous claims need dimensional decomposition

`unlimited` was initially one observed value.

That is too coarse.

It must be decomposed into dimensions such as:

```text
billing limit
volume limit
high-speed volume limit
speed guarantee
throttling trigger
throttled speed
measurement window
tethering / data-share scope
geography
congestion / fair-use conditions
```

Without this step, the investigator can manufacture a contradiction simply by comparing different meanings of the same label.

## Carrier observations

### NTT Docomo — Docomo MAX

Official current product material markets `ギガ無制限`, while explicitly noting that communication restrictions may apply during large-volume communication. Docomo's tethering page states that Docomo MAX can also use tethering without a stated plan-specific tethering volume cap. The base 5G terms contain general communication-restriction powers for congestion and certain large or continuous traffic.

Finding:

```text
no published fixed domestic GB cap found in the examined current product material
!=
no possible communication control
```

### KDDI / au — au Value Link Plan

Current official plan material states `データ容量使い放題`, while also stating:

- over 200GB/month → maximum 5Mbps for the remainder of the month
- tethering/data-share has a separate monthly cap for the base plan
- congestion restrictions may apply

This is not resolved by the base contract terms alone; the quantitative plan conditions live in plan/important-information material.

### SoftBank — Teigaku Unlimited

Current official material states `ギガ無制限`, while also stating:

- rolling previous 30 days over 300GB → max 4.5Mbps
- time-of-day controls may occur
- machine-generated communication may be controlled
- tethering usage contributes to the relevant data conditions

The use of a rolling 30-day window instead of calendar-month logic is a strong test of the timeline/window dimension.

### Rakuten Mobile — Rakuten Saikyo Plan

Current official material describes domestic high-speed data as unlimited, and current FAQ says there is basically no monthly domestic data-volume upper limit. At the same time, fair-service speed control can occur during congestion; the contract terms also permit certain bandwidth/speed/large-traffic controls.

Finding:

```text
no fixed monthly domestic volume ceiling
!=
no network-control conditions
```

## Structural finding

The test question should not be framed as:

```text
Why do unlimited plans have limits?
```

The reproducible formulation is:

```text
What exact dimension does each carrier describe as unlimited,
and which independent dimensions remain conditional?
```

This reframing is a direct application of premise validation.

## New core requirements

v0.1.2 should add:

### 1. Document Stack / Function

For every official source, record:

- document type
- legal/contractual function
- applicable plan/cohort
- version/effective date
- whether it is normative, explanatory, operational or marketing

### 2. Claim Decomposition

Before comparing an ambiguous label, list the dimensions that can vary independently.

### 3. Contract cohort

Explicitly record join date / legacy-plan status where conditions can differ by subscriber cohort.

### 4. Comparison rule

Cross-provider comparisons must compare normalized dimensions, not marketing labels.

## Regression assertions for v0.1.2

The following must remain true after future changes:

1. `unlimited` alone never produces a contradiction.
2. Marketing material is an observation source, not automatically the complete governing rule.
3. A base contract term is not assumed to contain all plan-specific numerical conditions.
4. Fixed-volume throttling and congestion/fair-use control remain distinct.
5. Calendar-month and rolling-window thresholds remain distinct.
6. Tethering, data share and roaming are separate scopes unless documents explicitly equate them.
7. Absence of a fixed threshold is not reported as absence of any restriction.
8. Current terms are not automatically applied to historical subscriber cohorts.

## Test verdict

v0.1.1: PARTIAL PASS

The core reasoning model generalized well, but telecom contracts exposed missing representations for document function and semantic dimensions.

Recommended next version: **v0.1.2**
