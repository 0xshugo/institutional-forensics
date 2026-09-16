# Changelog

## [0.1.2] - 2026-09-17

Cross-domain patch driven by a blind test against current Japanese mobile-carrier contract and plan documentation.

### Added

- `Document Stack / Document Function` analysis
- `Claim Decomposition / Semantic Dimensions`
- explicit contract-subscriber cohort handling
- normalized-dimension rule for cross-provider comparisons
- distinction between fixed-volume throttling and congestion/fair-use controls
- `modules/telecom-contracts.md`
- `examples/mobile-unlimited-jp-4carriers.md`
- `tests/TEST_REPORT_v0.1.1-telecom.md`

### Changed

- Evidence Identity Tuple now records document type, function, effective range, applicability and cohort
- Premise Validation now checks semantic-dimension equivalence, not only object/time equivalence
- Mandatory output can include Document Stack and Claim Dimensions
- Agent prompt now prevents treating product pages as complete contract definitions
- Stop Conditions require document-function analysis where multiple documents jointly define a rule or contract

### Reason

The four-carrier telecom test showed that a source can be official and still have a different function from another official source. It also showed that labels such as `unlimited` are too coarse to compare directly: billing, total volume, high-speed volume, speed control, tethering, geography and measurement window can vary independently.

---

## [0.1.1] - 2026-09-17

Validation-driven patch after the first regression and cross-domain tests.

### Added

- Mandatory `STEP -1 — Premise Validation`
- Object granularity checks
- Evidence Identity Tuple
- `H0` for premise error / granularity mismatch
- Source Drift / Version Drift handling
- `Premise not established` result state
- legality / operation / enforcement separation
- `tests/TEST_REPORT_v0.1.0.md`

### Changed

- JP Address module now distinguishes facility / building / unit / parcel granularity
- Kusunokamicho 2-1-2 example downgraded from `Highly likely` to `Unresolved`
- Stop Conditions now require premise validation and source-granularity alignment

### Reason

The first regression test showed that a legally plausible explanation could be constructed before the underlying duplication was proven at the same object granularity. v0.1.1 makes verification of the anomaly itself a mandatory gate.

---

## [0.1.0] - 2026-09-17

Initial experimental release.

### Added

- Core Institutional Forensics workflow
- Evidence Classes A-F
- Hypothesis-first investigation model
- Exception / transition / legacy checks
- Contradiction Matrix
- Falsification step
- Confidence levels
- Japanese address forensics domain module
- Kusunokamicho 2-1-2 case study
