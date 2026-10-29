# Institutional Forensics Validator Checklist

Version: v0.1.6 (core: `SKILL.md` front matter / `README.md`)

Canonical validator and Definition of Done checklist for this skill. Other docs should link here instead of duplicating items.

Use this checklist before accepting an investigation result.

## Required checks

```text
[ ] Premise status is present
[ ] Major sources include issuer
[ ] Major sources include function
[ ] Compared objects have aligned object_level or the mismatch is explicit
[ ] valid_at is present when time/version matters
[ ] Ambiguous claims are decomposed into dimensions
[ ] Confirmed is not supported by Class F evidence alone
[ ] At least one falsification condition is stated
[ ] Decisive negative/exclusive claims were separately falsified
[ ] Current state was not promoted to a permanent promise without explicit evidence
[ ] Adjacent dimensions are not conflated (e.g. quota != retention, notice period != limitation period)
[ ] When identity/attribution is asserted, distinguish correlated artifacts from same account/operator/person
[ ] When multiple sources support one claim, check whether they depend on one original artifact or common upstream source
[ ] Unresolved remains an allowed outcome
```

## Decisive negative claim check

If the result contains claims such as:

```text
存在しない
一度もない
唯一
only
never
no rule
```

require at least one of the following before accepting them as Confirmed:

```text
[ ] full-text search of the governing primary source
[ ] inspection of adjacent provisions / appendices / transitional clauses
[ ] check for special laws or related governing documents
[ ] explicit primary-source statement supporting the absence/exclusivity claim
```

A successful refutation of the user's premise does **not** automatically validate the replacement explanation.

## Permanence / neighboring-dimension check

Before using words such as:

```text
永久
恒久
always
permanent
guaranteed forever
```

verify that the source actually establishes duration, not merely current status.

Examples:

```text
current quota exemption != permanent retention guarantee
1-year notice period != 1-year commercial warranty
limitation period != warranty period
```

## Failure policy

- Missing premise validation → FAIL
- Confirmed based only on F → FAIL
- Marketing label compared directly without needed dimension decomposition → FAIL
- Object-level mismatch hidden → FAIL
- Missing issuer/function for a major source → WARN or FAIL depending on impact
- Missing valid_at where historical/current conditions may differ → FAIL
- No falsification condition → FAIL
- Strong negative claim not separately checked → FAIL
- Current state promoted to permanence without explicit source → FAIL
- Adjacent dimensions conflated in a decisive conclusion → FAIL
- Correlated timestamps, IPs, metadata or hosting treated as proven actor identity without independent corroboration → FAIL
- Multiple mirrors/derivatives counted as independent evidence for decisive attribution → FAIL

## Confidence downgrade rule

If evidence is incomplete but the investigation remains useful:

```text
Confirmed → Highly likely → Plausible → Unresolved
```

Do not fill missing evidence with narrative confidence.

## OSINT identity / provenance gate (conditional)

Apply when the conclusion links artifacts to an account, device, operator, person or organization. Refer to `modules/osint-artifact-correlation.md`.

```text
[ ] Exact identity layer is specified: artifact / infrastructure / account / device / operator / individual
[ ] Source origins and shared-upstream dependencies are explicit
[ ] Claim-level confidence is separate from incident-level confidence
[ ] Benign/alternative explanations (shared hosting, registrar batch action, scanner, proxy, copy, spoof) were considered
[ ] No uncalibrated percentages or attribution from IP/metadata/time correlation alone
[ ] Only authorized, safe sources were accessed or preserved
```

Any definitive private-person identification without appropriate authorized evidence, or unauthorized collection from attacker-controlled sites, is **FAIL**. This gate is not required for ordinary contract/address cases.
