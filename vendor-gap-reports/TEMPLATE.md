# Vendor Gap Report Template

A DCM Vendor Gap Report formally documents detection capabilities that a platform fails to provide — mapped to the DCM Level 1 baseline. It gives security teams structured language for vendor conversations and creates a community record of platform detection gaps.

---

## How to Use This Template

Complete one report per platform. Be factual and specific. Document what logging capability is absent, which DCM requirement it fails to meet, and what the platform would need to provide to address the gap. The goal is to give your vendor account team something concrete to escalate — not to publicly attack the vendor.

When submitting to the DCM repository, name the file: `[vendor]-[platform]-gap-report.md`
Example: `microsoft-power-platform-gap-report.md`

---

## Template

```markdown
# Vendor Gap Report — [Vendor] [Platform]

**Prepared by:** [Your name or handle]  
**Date:** [Date]  
**DCM Version:** [Version this was assessed against]  
**Platform Version / Tier:** [Version or licensing tier assessed]

---

## Platform Overview

Brief description of the platform, its primary function, and the organizational
context in which it was assessed (e.g., cloud-hosted SaaS, on-premise, hybrid).

---

## Assessment Summary

| DCM Level | Domains Assessed | Questions Evaluated | Covered | Partial | Gap |
|---|---|---|---|---|---|
| Level 1 | [list] | [#] | [#] | [#] | [#] |

---

## Gap Details

For each gap, complete the following:

### Gap [#] — [Short Description]

| Field | Detail |
|---|---|
| DCM Domain | Domain [#] — [Name] |
| Detection Question | [The universal detection question that cannot be answered] |
| Gap Type | Vendor gap / Configuration gap / Architecture gap |
| Impact | What adversary behavior or risk this gap leaves undetected |
| MITRE Technique | [Technique ID and name] |
| What the Platform Provides | [What logging currently exists, if anything] |
| What Is Missing | [Specifically what event, field, or capability is absent] |
| What the Platform Needs to Provide | [Specific technical ask for the vendor] |
| Compensating Control | [Which other tool provides coverage, if any] |
| Compensating Coverage Status | Full / Partial / None |

---

## Vendor Ask Summary

A concise summary of what you are formally requesting from the vendor.
This section is intended to be shareable with vendor account teams.

[Platform] currently fails to provide the following logging capabilities
required to meet the DCM Level 1 detection baseline:

1. [Gap 1 — one sentence description and specific ask]
2. [Gap 2 — one sentence description and specific ask]
...

---

## References

- DCM Detection Domain documentation: [link]
- Vendor documentation reviewed: [links]
- Related CVEs or security advisories, if applicable: [links]
```

---

## Example: Completed Gap Entry

### Gap 1 — No Native Authentication Failure Logging at Session Layer

| Field | Detail |
|---|---|
| DCM Domain | Domain 1 — Identity & Access |
| Detection Question | Was authentication attempted outside normal hours or location? |
| Gap Type | Vendor gap |
| Impact | Failed authentication attempts and credential stuffing activity targeting this platform cannot be detected natively |
| MITRE Technique | T1110 — Brute Force |
| What the Platform Provides | Successful login events only (AU1 transaction) |
| What Is Missing | Failed authentication events with source IP, timestamp, and user identifier |
| What the Platform Needs to Provide | Emit a failed authentication event (equivalent to AU2) that includes: timestamp, source IP address, username, client identifier, and failure reason |
| Compensating Control | Okta SSO captures authentication failures for federated users at the IDP layer |
| Compensating Coverage Status | Partial — covers federated SSO users only; direct platform authentication bypasses IDP and has no coverage |

---

## Notes on Responsible Disclosure

Vendor gap reports document missing logging capabilities, not vulnerabilities. There is no responsible disclosure requirement. However, please:

- Be factual — document gaps based on testing and evidence, not assumptions
- Be specific — vague gap descriptions are not actionable for vendors or the community
- Be fair — note compensating controls and partial coverage where they exist
- Do not include confidential organizational information in reports submitted to the DCM repository
