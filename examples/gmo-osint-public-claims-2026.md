# Case Study — GMO incident: public OSINT correlation claims without false attribution

**Case status:** public-claim verification / **attribution unresolved**  
**Skill:** institutional-forensics + `modules/osint-artifact-correlation.md`  
**Review date:** 2026-10-29 (JST)  
**Safety:** public, redacted, no attacker-host access or leaked data

## Scope and precise premise

Question: A public OSINT post about the October 2026 Onamae.com Desktop Cloud incident describes WHOIS/RDAP, DNS, Wayback, HTTP tracker logs, XLSX custom metadata, PHP code patterns and ISP lookups. **Do these correlations justify the asserted shared-account / operator / person attribution?**

This case evaluates the **evidence reasoning** of the published report; it does **not** independently authenticate its alleged raw logs, documents, IPs, domain account records, or identify a criminal.

### What is independently established

- GMO publicly reported an unauthorized-access incident affecting Onamae.com Desktop Cloud and launched a cybercrime-bounty reporting channel on 2026-10-28. The official notice asks for concrete, verifiable information, and for facts and inferences to be separated.
- GMO warns that alleged attacker-controlled leak pages can collect visitor information, and requests **no access to those pages and no spread of leaked data**.
- ICANN documents `clientHold` as a domain status set by a registrar, restricting DNS publication.
- The CDX specification identifies archive `timestamp` as **capture time**, not creation time.
- OOXML `docProps/custom.xml` contains document property values and is not intrinsically a cryptographic author credential.

These official/technical facts do not by themselves verify the external investigator's specific measurements.

## Premise status

- **Established:** incident and bounty public notice; technical meanings of clientHold, CDX timestamp, OOXML property file.
- **Partially established:** a public OSINT account **asserts** that multiple correlated traces were observed; the account's existence is observable, its underlying raw data is not independently checked here.
- **Not established:** the proposed registrar customer-account equivalence, QA-rig ownership, a unique WPS author identifier, precise physical location, or a specific count of offenders.

**Confidence on attribution:** **Unresolved**. Do not reinterpret this as an assertion that the author fabricated evidence; it means this review lacks raw, independently corroborated records.

## Document Function & Evidence Identity

| Source | Issuer / origin | Function | Object level | valid_at | Scope and limit |
| --- | --- | --- | --- | --- | --- |
| Incident report / bounty notice | GMO Internet | official incident notice; explanatory / operational (D) | incident & response | 2026-10-27/29 | Confirms case and safety policy, not suspect identity |
| Technical OSINT publication | public investigator's account, redistributed online | self-report / investigation commentary (E for narrative; F for its unverified inferences) | purported artifacts | 2026-10 (posted) | No source logs or original document bytes were inspected here |
| EPP status guide | ICANN | technical explanatory standard (D) | domain registration | consulted 2026-10-29 | Defines `clientHold`; no proof of same Namecheap login |
| CDX description | Library of Congress | format documentation (D) | archive capture | consulted 2026-10-29 | Capture time is not necessarily content/event time |
| Open XML custom properties guidance | Microsoft | technical explanatory (D) | document metadata | consulted 2026-10-29 | Custom metadata can be edited/copied; not a verified unique author ID |
| SP 800-86 | NIST | forensic process guidance (D) | investigative process | 2006 publication | Collection/integrity guidance, not case attribution |

## Correlation matrix and falsification

| Published observation (not independently reproduced here) | Narrow defensible interpretation | Forbidden leap | At least one alternative / disproof |
| --- | --- | --- | --- |
| Two `clientHold` times differ by six seconds | Closely timed registrar state changes, **if archived event semantics verified** | Same customer account proven | Registrar batch abuse takedown / timestamp reflects provider update; need registrar audit |
| Repeated apparent PHP–Wayback time offset (15 of 15 samples) | Time conversion model fits the claimed samples | Author's timezone, origin or device location confirmed | Crawler latency, common source clock, publication vs capture timestamp |
| HTTP logs show an alleged 39-burst QA-like pattern | Apparent automated/test behavior, **if provenance established** | That IP is the attacker or specific operating device | Public scanner, investigator, shared NAT/proxy, fabricated/injected entries |
| Equal WPS custom `ICV` field values / creator labels | Metadata values match; potential grouping lead | Uniquely same human, account or workstation | Copied templates, shared export tool, editable properties; need vendor semantics and independent chain |
| PTR and JPNIC allocation shows certain providers | Public network allocation and reverse DNS at query time | Person, street, operator and culpability | Dynamic IP, CGNAT, carrier gateway, VPN, nonauthoritative PTR |
| CSS/HTML source signatures, file paths, hash algorithms | Code/document family similarities | Same coder or the perpetrator | AI generation, widely copied code, tool defaults |
| Multiple software stacks / simultaneous activity | Multiple environments reported | Exactly 2–4 people involved | One operator controlling many virtual devices, shared automation |

### Key technical correction

`WHOIS/RDAP + 6-second clientHold` is **not proof** of the same Namecheap *customer account*. It is a useful provider inquiry lead. Only appropriately authorized registrar-side account/change logs, or independent authenticated evidence, could upgrade the attribution.

Likewise, a claim that all samples reproduce a salt-derived hash proves only a reproducible **mapping under the proposed formula**. It does not establish the person behind a request; avoid inversion/doxxing.

## Claim Dimensions and attribution ladder

```text
L0 published assertion
L1 artifact or event independently authenticated
L2 a correlation between artifacts established
L3 an administrative account/controller linked
L4 an operator/device linked by independent records
L5 an individual / organization proven with authorized evidence
```

Current independent verification of **specific alleged artifacts** is L0. The generic method is valid as an investigative approach; the **same-actor conclusion is unresolved**.

`Same registrar` ≠ `same registrar account` ≠ `same administrator` ≠ `same operator` ≠ `same individual`.

## Failure modes discovered

1. **Correlation-to-attribution leap:** treating timing, IP, or code similarity as personal attribution.
2. **Evidence multiplication:** calling mirrors or derivatives of the same actor-controlled log multiple independent sources.
3. **Precision laundering:** turning seconds/percentages into calibrated confidence without reproducible ground truth.
4. **Control contamination:** neglecting researchers, scanners, hosted infrastructure, virtual machines, and intentionally manipulated logs.
5. **Source-class promotion:** an individual's public claim is evidence they reported it, not automatic primary evidence that underlying events occurred.
6. **Unsafe preservation:** copying alleged leaked customer data or visiting dangerous sites to create a reproducible dataset.

## Mandatory output verdict for this case

- **Incident exists?** Confirmed (GMO official).
- **OSINT techniques are applicable?** Confirmed as possible evidence types (technical standards).
- **Specific reported measurements all independently verified?** Not established in this test.
- **Same Namecheap customer account?** Unresolved.
- **QA rig is attacker-controlled?** Unresolved.
- **Unique WPS creator identity?** Unresolved.
- **Number/location of participants?** Unresolved.
- **Next defensible action:** preserve public *descriptions* and request authoritative evidence via the official channel, not personal doxxing or unauthorized acquisition.

## Verification scope & safety note

The fixture intentionally **does not fetch suspect domains, malware/leak archives, attacker logs, real IP identifiers, credentials, or personal information**. It relies on public commentary (for the claims) and official independent standards/notices (for how to reason about them). Any future raw-artifact reanalysis is out of scope without authorization and controlled handling.

## References

- [GMO — incident update / bounty, 2026-10-27](https://internet.gmo/news/article/258/)
- [GMO — incident update, 2026-10-28](https://internet.gmo/news/article/260/)
- [ICANN — EPP status codes](https://www.icann.org/resources/pages/epp-status-codes-2014-06-16-en)
- [Library of Congress — CDX Internet Archive Index File](https://www.loc.gov/preservation/digital/formats/fdd/fdd000590.shtml)
- [Microsoft — Open XML custom properties](https://learn.microsoft.com/en-us/office/open-xml/word/how-to-set-a-custom-property-in-a-word-processing-document)
- [NIST SP 800-86](https://csrc.nist.gov/pubs/sp/800/86/final)

**Original post provenance:** A public investigation thread corresponding to the user-provided summary was observed in a third-party social mirror. Because the original post identifier and raw evidence could not be independently authenticated in this review, the specific measurements are correctly classified as **reported, not confirmed**.
