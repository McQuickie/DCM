# Vendor Gap Reports

This directory contains community-contributed DCM Vendor Gap Reports — formal documentation of detection capabilities that platforms fail to provide, mapped to the DCM Level 1 baseline.

---

## What a Vendor Gap Report Is

A Vendor Gap Report formally documents where a specific platform fails to meet DCM's Level 1 detection requirements. It identifies:

- Which universal detection questions the platform cannot answer natively
- What specific logging capability is absent
- What the platform would need to provide to close the gap
- Whether compensating controls in the broader stack provide coverage

---

## Why This Matters

Most security teams have vendor conversations that go nowhere. "We need better logging" gets a shrug. A structured gap report that says "your platform cannot answer Detection Question 4 in Domain 1 because you do not emit session-layer authentication failures — here is specifically what you need to provide" is a different conversation.

Making vendor gap reports a community artifact also creates collective pressure. When multiple organizations document the same gap against the same platform, vendors have something concrete to respond to. It becomes a community standard they are visibly failing to meet, not an individual customer's request they can deprioritize.

---

## Reports In Progress

*(None yet — be the first)*

---

## How to Submit a Vendor Gap Report

See [TEMPLATE.md](TEMPLATE.md) for the report format.  
See [CONTRIBUTING.md](../CONTRIBUTING.md) for submission guidelines.

Name your file: `[vendor]-[platform]-gap-report.md`

---

## Important Notes

- Reports document missing *logging capabilities*, not security vulnerabilities
- Be factual, specific, and fair — note compensating controls where they exist
- Do not include confidential organizational information
- Reports represent the assessment of the contributor at the time of submission — platform capabilities change with vendor updates
