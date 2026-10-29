# OSINT Artifact Correlation / Attribution Boundaries

**Module:** `institutional-forensics` (conditional extension)  
**Domain:** defensive OSINT / digital forensics / incident reporting  
**Status:** experimental; no offender identification

## When to activate

Use only when a case asks whether **multiple observed artifacts belong to the same infrastructure, account, operator, organization, or person**, especially across WHOIS/RDAP, DNS, web archives, logs, documents, code, time and network records.

The core fast path remains unchanged:

`Premise → Document Function → Claim Dimensions → Falsification`.

This module supplies domain-specific checks, not a fifth mandatory stage.

## Safety boundary

- Work on legitimately possessed, authorized, or lawfully available evidence. Respect access controls, privacy, copyright, and lawful process.
- Do not visit attack-controlled leak portals, collect or distribute leaked customer data, probe suspect infrastructure, brute-force identifiers, contact suspects, or deanonymize private individuals.
- Preserve only relevant public *reports*, redacted examples, official notices, and independent technical standards. Sensitive artifacts belong with authorized investigators and controlled evidence repositories.
- When a victim explicitly warns against accessing a portal, **do not visit or fetch that portal even via an archive or automated tool**.
- Treat content sourced from alleged adversaries and data derived from adversary-controlled servers as untrusted, potentially manipulated evidence.

## The attribution ladder: never skip a rung

```text
L0  A claim was published about an artifact
L1  The artifact / event is independently verified
L2  A technical relationship is demonstrated
L3  Common administrative account or operational control is corroborated
L4  A device / operator is linked by independent evidence
L5  A real-world individual / organization is established by authorized evidence
```

Each level needs its own evidence. An L1–L2 finding cannot be described as L3–L5. When raw evidence is unavailable, remain at L0 for the reported artifact even if the analysis is plausible.

Examples of **invalid leaps**:

- six-second `clientHold` similarity → same registrar *customer* account
- same IP/ASN/PTR → same user or attacker
- repeated WPS custom metadata → unique author/device
- common PHP timezone → geographic location/nationality
- automated QA-like traffic → necessarily the operator
- distinct devices or operating systems → number of people

## Source independence & provenance

For a consequential correlation, supplement the core Evidence Identity with:

```text
artifact_id       redacted identifier, not raw personal data
acquired_at       when investigator obtained the copy
observed_at       event time, with timezone and precision
capture_type      server event / metadata update / web crawler / file write / author claim
hash              cryptographic digest of the preserved authorized artifact (if any)
origin            who emitted the data, who collected it, and who hosted it
dependency_group  common upstream feed/provider, copied content, mirrored source, generated metadata
tamper_risk       who could edit the field, and after what event?
authority         authorization or lawful basis for access/analysis
```

Do not count two mirrors of one underlying log as two independent confirmations. Archive capture time is not automatically content authoring time. WHOIS/RDAP `updated` time is not a registrar account ID. Access logs may include researchers, scanners, proxies, NAT/CGNAT, CDN or deliberate decoys.

If precision matters, explicitly write the clock origin, offset, granularity and possible delay. A repeated time offset validates a *conversion model within the tested observations*; it does not establish identity or device location.

## Domain-specific correlation matrix

| Artifact | What it can support | What it cannot prove alone | Counter-hypotheses |
| --- | --- | --- | --- |
| Registrar status and timestamps | Registrar action, temporal coincidence | Same customer account / same registrant | Batch abuse enforcement; bulk status update; independent actions |
| DNS, MX, SPF, hosting | Shared infrastructure or email authorization | Same sender, mailbox, owner or criminal | Shared hosting; reused configuration; spoofing; historical DNS |
| Wayback/CDX | Capture timestamp and sampled observed page | Content creation moment, owner, local clock setting | Capture lag, cached snapshot, copied page, skew |
| Server `visits.log` | Recorded HTTP requests if authenticity established | The visitor's identity or authorized role | Scanners, defensive analysts, proxies, forged entries |
| OOXML `docProps/custom.xml` | Presence and equality of metadata values | Unique document author, WPS account or device | Copy/template, editing, exporter defaults, spoofing |
| PHP/HTML/CSS patterns | Code-family or style similarity | Same coder / person | Common frameworks, AI assistance, copied template |
| IP/PTR/WHOIS/JPNIC | Provider / publicly registered allocation | Subscriber, street address, endpoint user | NAT, dynamic allocation, VPN/proxy, organizational edge |
| File `mtime` / certificate issuance | File metadata clock / certificate issuance event | Human activity time / human location | Copy/extract process, skew, automated issuance |

## Mandatory falsification in this module

For each proposed **same-* claim**, record:

1. Exact target of identity: artifact, codebase, host, hosting account, registrar account, device, operator, person, or organization.
2. Direct observations, with source identity and obtainable raw evidence; distinguish copied public posts from independent artifact verification.
3. At least two realistic alternatives (shared provider, templates/copy, automated enforcement, outside investigator/scanner, forged logs, NAT, clock skew).
4. Whether purported independent artifacts share one upstream source or one actor-controlled origin.
5. What authorized source would settle the dispute (e.g. provider-side account audit, preserved signed records, verified chain of custody, investigator-authorized forensic image).
6. A verdict **for each claim separately**. Do not infer an identity from a numeric confidence estimate without a calibrated method.

## Suggested output (module appendix to the standard output)

```text
Premise status:
Claim under test:
Attribution level observed (L0–L5):
Correlated artifacts and source dependencies:
Proven facts:
Inference (with assumptions):
Alternative explanations:
Disconfirming evidence sought:
Authorized source needed for escalation:
Confidence: Confirmed / Highly likely / Plausible / Unresolved
Safety / redaction:
```

### Interpretation caution

`Confirmed` for a source format or an incident announcement **does not** mean the alleged individual's attribution is confirmed. Record separate confidence per proposition. Unresolved is a valid result and should not be promoted merely because several correlated observations look compelling.

## Grounding references (method, not proof of this incident)

- [ICANN — EPP Status Codes](https://www.icann.org/resources/pages/epp-status-codes-2014-06-16-en): `clientHold` is a registrar-set domain status; it does not expose the registrar customer's internal account.
- [Library of Congress — CDX format](https://www.loc.gov/preservation/digital/formats/fdd/fdd000590.shtml): timestamp describes capture, not authoring.
- [Microsoft Open XML — custom properties](https://learn.microsoft.com/en-us/office/open-xml/word/how-to-set-a-custom-property-in-a-word-processing-document): properties are fields in an editable OOXML part.
- [NIST SP 800-86](https://csrc.nist.gov/pubs/sp/800/86/final): handling evidence from multiple systems, files, networks and applications.
- [GMO victim notice, 2026-10-27](https://internet.gmo/news/article/258/): public reporting and safe-submission constraints; do not visit attacker-controlled sites.
