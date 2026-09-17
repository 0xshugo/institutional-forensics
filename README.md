# Institutional Forensics

Evidence-first Skill for investigating contradictions in rules, contracts, policies, specifications, and real-world operations.

**Version:** v0.1.6 — experimental

> Verify the contradiction before explaining it.

## When to use it

Use this Skill when something looks inconsistent:

- a rule says one thing, operations do another
- two official sources disagree
- a contract says “unlimited”, “free”, or “guaranteed” but conditions exist
- old and new customers appear to have different treatment
- the same number or label appears to mean different things

## Fast path

The mandatory path is intentionally short:

```text
Premise
→ Document Function
→ Claim Dimensions
→ Falsification
```

Only expand into exceptions, scope/cohort, timeline/source drift, operation/enforcement, legacy, or implementation issues when needed.

## Definition of Done

A result is acceptable only when every item in the canonical checklist passes: [`tests/VALIDATOR_CHECKLIST.md`](tests/VALIDATOR_CHECKLIST.md).

## Why this exists

The Skill started from a Japanese address anomaly and immediately failed its first regression test: it could produce a legally plausible explanation before proving that the anomaly itself was real at the same object granularity.

That produced mandatory Premise Validation.

A later blind test on Japanese mobile-carrier contracts exposed two more weaknesses:

- official documents have different functions
- labels such as “unlimited” must be decomposed into independent dimensions

That produced Document Function and Claim Dimensions.

The v0.1.4 sample expansion then exposed a different failure mode: **a correct refutation can still produce a false replacement explanation.** The AppleCare sample incorrectly claimed that sales law contained no corresponding one-year rule; Civil Code Article 566 provides a one-year notice period for certain lack-of-conformity claims. The Google Photos sample also promoted a current quota rule into an unsupported “permanent” guarantee.

v0.1.5 keeps the same short fast path and strengthens Falsification instead of adding another mandatory step.

## Evidence minimum

Each major source needs only five required fields:

```text
issuer
function
object_level
valid_at
source
```

Optional when needed:

```text
version
published
applies_to
status
field
```

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
│   ├── mobile-unlimited-jp-4carriers.md
│   ├── applecare-warranty-layers.md
│   ├── google-photos-unlimited.md
│   └── anti-patterns.md
└── tests/
    ├── VALIDATOR_CHECKLIST.md
    ├── TEST_REPORT_v0.1.0.md
    ├── TEST_REPORT_v0.1.1-telecom.md
    ├── TEST_REPORT_v0.1.2-regression.md
    └── TEST_REPORT_v0.1.5-corrections.md
```

## Modules

### Japanese address forensics

`modules/jp-address.md`

Separates parcel number, block number, basic number, residence number, building number, and unit number.

### Telecom contract forensics

`modules/telecom-contracts.md`

Separates base terms, pricing tables, plan conditions, important-matters documents, FAQ/support, and marketing pages; decomposes ambiguous claims such as “unlimited”.

## Examples and anti-examples

Good/real investigation cases:

- `examples/kusunokamicho-2-1-2.md` — premise / granularity / address system
- `examples/mobile-unlimited-jp-4carriers.md` — document function / unlimited decomposition
- `examples/applecare-warranty-layers.md` — statutory remedy vs notice period vs limitation period vs commercial warranty; includes a documented self-correction
- `examples/google-photos-unlimited.md` — cohort coexistence / quota counting vs retention / current-state vs permanence

Compact failure examples:

- `examples/anti-patterns.md`

The anti-patterns are intentional: contributors should be able to see not only what a good answer looks like, but how the method fails.

## Validation status

Tested so far:

1. address-system regression / adversarial premise
2. My Number card vs electronic-certificate validity periods
3. bicycle roadway rule vs sidewalk exceptions and enforcement
4. Japanese four-carrier telecom-contract blind test
5. telecom regression after Document Function / Claim Dimensions changes
6. warranty-layer case: AppleCare + Japanese Civil Code / EU directive; v0.1.4 factual overreach corrected in v0.1.5
7. Google Photos storage sunset: cohort coexistence; permanence overreach corrected in v0.1.5
8. old-law anchor verification: pre-2017 Civil Code full-text check resolved the "one year" folk claim's true source (former Art. 566(3) via former Art. 570) and rejected our own six-month hypothesis

## Contribution direction

Before broad contributor onboarding, the project is still being hardened through blind tests.

Useful contributions include:

- cases that break the current method
- missing domain-specific checks
- validator improvements
- test fixtures
- domain modules that avoid expanding the common core

For now, prefer **one new domain module at a time**. Domain knowledge should live in modules unless repeated failures prove that the core itself needs to change.

## Status

Experimental. The goal is not to make AI sound more confident about institutions, but to make unsupported confidence harder.

## License

MIT
