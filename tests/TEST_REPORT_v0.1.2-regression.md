# Test Report — v0.1.2 Telecom Regression

Date: 2026-09-17 JST
Skill version: v0.1.2
Domain: Japanese mobile telecom contracts

## Purpose

Re-run the four-carrier `unlimited` case after adding:

- Document Stack / Function
- Claim Dimensions
- Contract cohort handling
- normalized cross-provider comparison

## Regression assertions

### R1 — `unlimited` alone must not produce a contradiction

PASS.

The skill decomposes `unlimited` into volume, high-speed volume, speed guarantee, throttling trigger, tethering scope, geography and measurement window before comparing conditions.

### R2 — official product page must not be treated as the complete contract

PASS.

The workflow explicitly requires a Document Stack when conditions are distributed across base terms, pricing tables, provision documents, important-matters explanations and FAQ/support material.

### R3 — absence of a fixed GB threshold must not be reported as absence of any control

PASS.

Docomo and Rakuten examples can be represented as `no fixed threshold found in examined current plan material` while separately retaining congestion / large-traffic / fair-use controls.

### R4 — fixed-volume throttling and network congestion control must remain separate

PASS.

au and SoftBank have explicit quantitative thresholds in current plan material; generic congestion restrictions remain separate conditions.

### R5 — calendar month and rolling window must remain separate

PASS.

au's 200GB threshold is represented as monthly, while SoftBank's 300GB condition is represented as a rolling previous-30-days condition.

### R6 — tethering / data share must be separate scopes

PASS.

au's tethering/data-share allowance is represented separately from handset traffic. Docomo's current MAX tethering claim is separately sourced. SoftBank's tethering usage is associated with the relevant plan's data conditions.

### R7 — cross-carrier comparison must normalize dimensions rather than labels

PASS.

The resulting table can compare:

```text
claim
fixed threshold
throttled speed
window
tethering
congestion control
fair-use control
geography
```

without asserting that the four marketing labels have identical semantics.

### R8 — current conditions must not be assumed for all historical subscribers

PASS by design.

v0.1.2 adds `Cohort` and `applies_to` to Evidence Identity Tuple and requires Source Drift / join-date checks when historical contracts are in scope.

## Result

**PASS for the tested structural requirements.**

This does not mean the skill is mature. It means the specific failure modes exposed by the v0.1.1 telecom blind test are now represented in the workflow and pass the same-case regression.

## Remaining risks

1. Legal precedence among incorporated documents is domain-specific and cannot be inferred from visual hierarchy alone.
2. Carrier documents change frequently; reproducibility requires effective dates and archived copies where practical.
3. Product pages can update before PDF terms or vice versa, creating temporary Source Drift.
4. Individual subscriber contracts may differ from currently marketed plans.
5. Network controls may be described qualitatively, limiting exact operational verification.

## Next adversarial tests

Recommended before contributor onboarding:

1. insurance policy wording vs brochure
2. credit-card fee/benefit terms vs campaign page
3. public subsidy eligibility vs FAQ
4. software license / ToS vs product UI
5. public transport fare rules vs promotional pass description

The next tests should be blind: choose a question first, then run the skill without adapting its rules to the expected answer.
