# Changelog

## [0.1.5] - 2026-09-17

Correction and validator-hardening patch driven by factual errors found in the v0.1.4 sample expansion.

### Fixed

- `examples/applecare-warranty-layers.md`
  - removed the false claim that sales law contains no corresponding one-year rule
  - added Civil Code Article 566 as a one-year notice period for certain lack-of-conformity claims in sales
  - separated notice period, limitation period, commercial warranty, and AppleCare service coverage
  - retained the narrower conclusion that Apple's one-year limited warranty is a voluntary commercial warranty offered in addition to consumer-law rights
- `examples/google-photos-unlimited.md`
  - replaced unsupported `永久 / 恒久` language with the narrower current-policy statement actually supported by Google's official help
  - separated quota exemption from retention guarantees
  - stopped treating `Pixel 5 and earlier` as a fully homogeneous detailed cohort without model/quality/date-specific sourcing

### Added

- `tests/TEST_REPORT_v0.1.5-corrections.md`
- anti-patterns for:
  - overconfident negative/exclusive claims
  - promoting current state to permanence
- validator checks for:
  - `存在しない / never / only / 唯一` claims
  - current-state → permanent-promise inference
  - neighboring-dimension conflation such as `quota != retention` and `notice period != limitation period`

### Changed

- `SKILL.md` version bumped to v0.1.5
- Falsification now explicitly applies to decisive replacement claims created while refuting the original premise
- no new mandatory workflow step was added; the fast path remains `Premise → Document Function → Claim Dimensions → Falsification`

### Reason

The new examples showed that a method can correctly invalidate the user's initial premise and still hallucinate an overbroad replacement explanation. The appropriate fix was not another reasoning stage, but stricter falsification of negative/exclusive claims and stricter dimension boundaries.

---

## [0.1.4] - 2026-09-17

Content patch: two new worked examples in untested domains, both built from primary-source investigation.

### Added

- `examples/applecare-warranty-layers.md` — warranty-layer investigation across Japanese law, Apple commercial warranties and EU consumer-sales rules
- `examples/google-photos-unlimited.md` — cohort coexistence after the 2021-06-01 storage-policy change

### Changed

- README example list and validation status now record the consumer-law and platform-terms domains

### Reason

The method had only been demonstrated on addresses and telecom. These two cases exercise the core path in new domains and intentionally expose new failure modes.

---

## [0.1.3] - 2026-09-17

Execution-cost and validation patch driven by an external audit of the v0.1.2 method.

### Added

- compact mandatory fast path: Premise → Document Function → Claim Dimensions → Falsification
- explicit `tests/VALIDATOR_CHECKLIST.md`
- compact `examples/anti-patterns.md`
- minimal required Evidence Identity fields
- contributor-facing Definition of Done

### Changed

- Evidence Identity Tuple required fields reduced to `issuer / function / object_level / valid_at / source`
- exception, scope/cohort, timeline/source drift, operation/enforcement, legacy and implementation checks are now conditional expansions rather than always-on steps
- Agent Prompt shortened substantially to reduce instruction dilution
- README redesigned around trigger / fast path / DoD / validation status
- common core frozen against unnecessary domain-specific growth; new domain knowledge should prefer modules

### Reason

The method had become increasingly capable but also increasingly expensive to execute. The audit found that the next quality step was not adding more reasoning stages, but making the method shorter and making omissions mechanically visible.

The v0.1.3 design goal is:

> short enough to run consistently, strict enough to fail when evidence structure is missing.

---

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
- `tests/TEST_REPORT_v0.1.2-regression.md`

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
