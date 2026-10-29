# OSINT attribution positive controls — supplemental v0.1.7 fixtures

Status: **synthetic only**. No real accounts or personally identifying records.
These are an extension **after** the original T1–T8 baseline; do not retroactively change that run's 8/8 score.

## Prompts — safe to give the model alone

Use `SKILL.md` and `modules/osint-artifact-correlation.md`. For each case separately state Premise status, Document Function/provenance, dimensions, attribution level (L0–L5), confidence per claim, two alternatives, and what would disconfirm a strong conclusion.

**T9 — Verified same registrar customer account.** An authorized investigator is supplied an authenticated and signature-verified registrar audit export covering the relevant exact time window. It shows two fictional domains `alpha.example` and `beta.example` under the same internal customer account ID during that window. Export provenance, signature, account-schema meaning and collection authority are confirmed. No login-session, device or human identity record is available. Which propositions are Confirmed, and which are not?

**T10 — Verified request-chain correlation.** An authorized investigator holds two independently collected, integrity-verified HTTP system logs: one at an edge reverse proxy, another at a backend service. The deployed trace-propagation design is documented, their unique request IDs and accurate timestamps match, and the record says that same request passed through both services. The originating public IP is a shared proxy. Is the **same request chain** Confirmed? Does that identify a human operator or attacker?

## Execution / test design

- Keep these prompts separate from the grading key in `tests/OSINT_POSITIVE_CONTROL_KEY_v0.1.7.md` for *future* hidden-key use.
- Before a real blind run, ensure the answer-key file and earlier assistant runs are not included in model context.
- This supplement was written by ChatGPT in a conversation that also knew the original rubric; any same-session execution is **not independently blind**.
