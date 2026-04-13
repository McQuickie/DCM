# DCM — Detection Coverage Model

> *A practitioner model for achieving meaningful alerting coverage across any technology deployment, from universal detection fundamentals to platform-specific depth to environmental awareness.*

**Author:** Kerry McQuarrie  
**Version:** v0.1 (Working Draft)  
**Status:** 🚧 Active Development — Collaborators Welcome  
**License:** [Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE.md)

---

## The Problem

Your organization just onboarded a new HCM platform. Logs exist — barely. The functional team that understands the platform doesn't prioritize the cybersecurity conversation. Your SIEM connector is ingesting *something*, but nobody can tell you what matters. You search for Sigma rules. You find none. You check ATT&CK. It tells you what adversaries do — but not what *this platform* should alert on, given how *your organization* has deployed it.

So you start from scratch. Again.

But it goes deeper than onboarding. Large platform vendors continuously expand their ecosystems — Microsoft adds Power Platform, Salesforce adds new automation capabilities, Google Workspace gets new sharing features — and business users adopt them organically. Security teams find out when something goes wrong. There is no native alert for *"someone in your organization just operationalized Power Platform and started sharing PII with an external user."* The vendor doesn't provide it. The community hasn't written a Sigma rule for it. And nobody warned you it was happening.

The security industry has produced excellent resources for *describing adversary behavior* (MITRE ATT&CK), *governing security programs* (NIST CSF), and *sharing detection rules for known platforms* (Sigma). What it has not produced is a structured, practitioner-facing model for answering the question every detection engineer actually faces:

> **"For this specific technology, in my specific environment — what should I be detecting, and how do I get there from wherever my logging is today?"**

DCM is designed to answer that question — at every level of logging maturity, for every type of technology, including the ones nobody has written a detection rule for yet.

---

## Why Existing Resources Don't Fully Solve It

| Resource | What It Does Well | The Gap |
|---|---|---|
| MITRE ATT&CK | Describes adversary tactics and techniques | Abstract, doesn't tell you what field to query in your specific tool |
| NIST CSF | Governs security program structure | Governance-focused, not operationally prescriptive for detection content |
| Sigma Rules | Community detection rules for known platforms | Coverage clustered on common platforms; niche, application-layer, and emerging tools largely absent |
| Existing maturity models | Measure detection program or team maturity | Measure *how you work*, not *what to detect* for a specific technology |
| Vendor documentation | Platform-specific logging guidance | Security-agnostic — tells you what logs exist, not what to alert on |

Research published at USENIX Security found that while Sigma achieves approximately 79% ATT&CK technique coverage in aggregate, coverage is heavily concentrated on the same popular techniques, with roughly 10–13% of techniques having only a single detection rule across all major community rulesets. The platforms where organizations carry the most data risk (e.g., ERP systems, HCM platforms, proprietary SaaS tools, internally developed applications) are precisely the ones the community has left underserved.

DCM does not replace any of these resources. It provides the operational bridge between them and the detection work practitioners actually need to do.

---

## What DCM Is

DCM is a **three-level detection coverage model** built around a single organizing principle: every technology an organization deploys can be evaluated against a consistent set of detection requirements — regardless of what it is, how well it logs, or whether the community has ever written a rule for it.

The three levels form a maturity progression. Organizations start at Level 1 and grow. Each level builds on the one before it.

```
LEVEL 1 — Detection Fundamentals
  The universal detection baseline every organization should have
  for every technology they deploy. These are the foundational
  questions any deployment should be able to answer.
  "We have baseline alerting. The fundamentals are covered."

        ↓ builds on Level 1 ↓

LEVEL 2 — Platform Detection Depth
  How to extract maximum detection value from whatever logging
  a specific technology provides — including niche platforms,
  poor logging, and proprietary tools with no community coverage.
  Includes a structured methodology for holding vendors
  accountable for detection gaps.
  "We are getting real signal from this platform, and we know exactly where the gaps are."

        ↓ builds on Level 2 ↓

LEVEL 3 — Environmental Awareness
  Detection for emergent capability adoption — when platforms
  you already own grow new features that get used before security
  has reviewed them. The Microsoft Power Platform problem.
  The shadow IT problem. The "nobody told us" problem.
  "We know when our environment changes
   before it becomes an incident."
```

---

## The 10 Detection Domains

Every technology is evaluated against the domains it touches. Most tools touch 2–4 directly.

| # | Domain | Covers |
|---|---|---|
| 1 | Identity & Access | Authentication, authorization, privilege, MFA, SSO, service accounts |
| 2 | Endpoint & Workload | Servers, workstations, containers, process execution, file activity |
| 3 | Network & Perimeter | Traffic flows, firewall policy, DNS, VPN, east-west movement |
| 4 | Cloud & Infrastructure | IaaS/PaaS/SaaS control planes, APIs, misconfiguration |
| 5 | Data & Secrets | Databases, file stores, vaults, sensitive data access |
| 6 | Application Layer | Web apps, SaaS platforms, APIs, custom applications |
| 7 | Supply Chain & Integration | Third-party access, vendor integrations, CI/CD pipelines |
| 8 | Insider & Privilege Abuse | Privileged user behavior, policy violations, data staging |
| 9 | Resilience & Availability | Backup integrity, ransomware staging, log tampering, DoS |
| 10 | Compliance & Audit Integrity | Regulated data access, audit trail integrity, policy enforcement |

Each domain includes:
- Relevant MITRE ATT&CK tactics and techniques
- Universal detection questions with typical log sources and ATT&CK tactic tags
- Relevant NIST CSF controls
- A universal use case template for structured output

---

## The Three Levels in Detail

### Level 1 — Detection Fundamentals

**Who it's for:** Every organization, every size, every budget.  
**What it delivers:** A baseline detection posture for any technology deployment.  
**The standard:** If a technology touches a domain, it should be able to answer the universal detection questions for that domain.

Level 1 uses the 10 detection domains as a lens. For each domain a technology touches, a defined set of universal detection questions establishes the minimum detection requirement. These questions are platform-agnostic — they apply to any tool. The answers differ by platform.

Level 1 is achievable by any security team. It does not require advanced tooling, a dedicated detection engineering function, or deep platform expertise. It requires asking the right questions and documenting what the answers look like in the specific technology being deployed.

**You are at Level 1 when:** Every technology in your environment has documented use cases covering the detection questions for the domains it touches, mapped to ATT&CK and NIST, with coverage status tracked.

---

### Level 2 — Platform Detection Depth

**Who it's for:** Organizations ready to go beyond the baseline and extract maximum signal from the technology they have — including the hard ones.  
**What it delivers:** Platform-specific use cases grounded in actual available logging, plus a structured methodology for vendor gap conversations.  
**The standard:** Every detection question that cannot be answered natively should be documented as a gap, with a compensating control identified or a vendor gap report generated.

Level 2 addresses the hardest detection engineering problem: getting meaningful alerting from platforms with poor, limited, or poorly documented logging. The methodology covers:

- **Analog tool research** — when a platform has no community detection content, find functionally similar tools that do and adapt their use cases
- **Log source inventory** — systematically document what the platform actually logs, at what fidelity, and what's missing
- **Gap classification** — distinguish between gaps that can be compensated by other tools in the stack versus gaps that require vendor remediation
- **Vendor gap reporting** — a structured output that tells vendors specifically what logging capability is absent and what it would need to provide to meet the DCM baseline. Gives vendor conversations teeth.

Level 2 is also where organizational context becomes critical — the SIL diagram showing how the tool is actually deployed, the existing tool stack that may compensate for logging gaps, and regulatory requirements that elevate certain detection questions to mandatory status.

**You are at Level 2 when:** Every significant technology has platform-specific use cases grounded in its actual log sources, coverage gaps are formally documented with compensating controls identified, and vendor gaps have been formally raised.

---

### Level 3 — Environmental Awareness

**Who it's for:** Organizations with solid Level 1 and Level 2 coverage who want to stay ahead of their own environment changing beneath them.  
**What it delivers:** Detection for when platforms you already own develop new capabilities that get adopted before security reviews them.  
**The standard:** Known platform sprawl vectors are monitored. New capability adoption within existing platforms triggers security review before operationalization.

Level 3 addresses a problem distinct from the previous two: not "what should this known platform alert on" but "how do we know when a platform we already have just became something new."

This includes:
- **Emergent capability detection** — first-time use of features within existing platforms (Power Platform, Power Automate, new M365 workloads, new Salesforce automation capabilities)
- **Organic adoption monitoring** — detecting when business users operationalize capabilities that haven't been through security review
- **Platform sprawl visibility** — new OAuth consent grants, new service principals, new API connections, new external sharing configurations
- **Vendor ecosystem expansion** — tracking when platform vendors add new capabilities that change the security surface of tools already in production

Level 3 requires the strongest logging and SIEM correlation capability — but the detection patterns are definable and documentable. This is not theoretical. The signals exist. They are just not collected and acted on by most organizations because nobody has defined them as a detection category.

**You are at Level 3 when:** Your detection posture updates when your environment updates — not after an incident reveals that something changed.

---

## How DCM Relates to Existing Frameworks

DCM complements, not competes with, existing resources:

- **MITRE ATT&CK** — DCM uses ATT&CK as its adversary behavior foundation. Every domain traces back to ATT&CK tactics and techniques. *ATT&CK tells you what adversaries do. DCM tells you what to look for in the technology you actually have.*
- **NIST CSF** — DCM maps each domain to relevant NIST CSF controls for organizations using NIST as their governance framework
- **Sigma** — DCM detection questions are designed to be translatable into Sigma rules. Every universal detection question should eventually have a community Sigma rule
- **Existing detection maturity models** — existing models (Kyle Bailey's DEMM, Elastic's DEBMM) measure how mature your detection *program and team* are. DCM measures whether you have *coverage* for a specific technology. They are complementary, not competing.

---

## Repository Structure

```
DCM/
├── README.md                          ← You are here
├── LICENSE.md                         ← CC BY 4.0
├── CONTRIBUTING.md                    ← How to contribute
├── CHANGELOG.md                       ← Version history
│
├── model/
│   ├── DCM-overview.md                ← Full model narrative
│   ├── level-1-fundamentals.md        ← Level 1 detailed guide
│   ├── level-2-platform-depth.md      ← Level 2 detailed guide
│   ├── level-3-environmental.md       ← Level 3 detailed guide
│   └── use-case-template.md           ← Universal use case template
│
├── domains/
│   ├── 01-identity-access.md
│   ├── 02-endpoint-workload.md
│   ├── 03-network-perimeter.md
│   ├── 04-cloud-infrastructure.md
│   ├── 05-data-secrets.md
│   ├── 06-application-layer.md
│   ├── 07-supply-chain-integration.md
│   ├── 08-insider-privilege-abuse.md
│   ├── 09-resilience-availability.md
│   └── 10-compliance-audit-integrity.md
│
├── worked-examples/
│   └── README.md                      ← Contributions welcome
│
├── vendor-gap-reports/
│   ├── README.md                      ← How to use the vendor gap report
│   └── TEMPLATE.md                    ← Vendor gap report template
│
├── level-3-patterns/
│   ├── README.md                      ← Environmental awareness patterns
│   └── microsoft-365-ecosystem.md     ← M365 / Power Platform patterns (in progress)
│
└── sigma-coverage/
    └── README.md                      ← ATT&CK/Sigma gap analysis (in progress)
```

---

## Current Status

DCM is at **v0.1** — a working draft representing the initial model structure, domain taxonomy, and detection question sets. Published early to invite community scrutiny, contribution, and validation.

**What exists today:**
- [x] Three-level model structure and rationale
- [x] 10 detection domain definitions with ATT&CK technique mappings
- [x] Universal detection questions per domain (7–8 per domain)
- [x] Log source and NIST CSF mappings per domain
- [x] Universal use case template (16-field standard)

**Actively being developed:**
- [ ] Level 2 platform methodology guide (log inventory, analog tool research, gap classification)
- [ ] Vendor gap report template
- [ ] Level 3 detection patterns (starting with Microsoft 365 ecosystem)
- [ ] Sigma rule coverage gap analysis by domain
- [ ] First worked example: SAP HCM / Splunk PowerConnect
- [ ] Extended ATT&CK sub-technique mapping per domain
- [ ] Regulatory overlay (PCI-DSS, HIPAA, SOX annotations)

---

## How to Contribute

DCM is explicitly a community project. The model is only as strong as the breadth of practitioner experience behind it.

**What we need most:**

- **Platform worked examples** — applied DCM to a real technology? Document it. Especially valuable for niche platforms with limited community coverage
- **Level 3 detection patterns** — environmental awareness detections for specific platforms (M365, Google Workspace, Salesforce, ServiceNow, etc.)
- **Vendor gap documentation** — formal gap reports for platforms that fail to meet Level 1 detection requirements. Makes vendor accountability a community effort
- **Sigma rule contributions** — detection rules mapped to DCM domains and universal detection questions
- **Domain subject matter experts** — deep knowledge in a specific domain? Help refine the detection questions and technique mappings
- **Challenge and critique** — if something is wrong or missing, say so. This model improves through honest practitioner feedback

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

All contributors will be credited. Attribution is the foundation this project is built on.

---

## License & Attribution

Licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE.md).

Free to share, adapt, and build upon — including commercially — with appropriate credit.

**Suggested attribution:**  
*McQuarrie, Kerry. "DCM — Detection Coverage Model." GitHub, 2026. https://github.com/[your-username]/DCM*

---

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for version history.

---

*DCM is an independent practitioner model. It is not affiliated with, endorsed by, or a product of MITRE, NIST, or the Sigma project — though it builds on the excellent work of all three.*

