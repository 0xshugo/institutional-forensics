# Changelog

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
