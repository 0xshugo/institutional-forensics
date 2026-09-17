# Institutional Forensics Validator Checklist

Version: v0.1.3

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
[ ] Unresolved remains an allowed outcome
```

## Failure policy

- Missing premise validation → FAIL
- Confirmed based only on F → FAIL
- Marketing label compared directly without needed dimension decomposition → FAIL
- Object-level mismatch hidden → FAIL
- Missing issuer/function for a major source → WARN or FAIL depending on impact
- Missing valid_at where historical/current conditions may differ → FAIL
- No falsification condition → FAIL

## Confidence downgrade rule

If evidence is incomplete but the investigation remains useful:

```text
Confirmed → Highly likely → Plausible → Unresolved
```

Do not fill missing evidence with narrative confidence.
