# DCM Model Overview

**Detection Coverage Model**  
Author: Kerry McQuarrie | Version: v0.1 | April 2026

---

## Why DCM Exists

Every security team has a version of the same problem. A new technology gets onboarded. Logs exist. Nobody can tell you what to alert on. The vendor documentation describes what the logs contain — not what matters from a security standpoint. MITRE ATT&CK tells you what adversaries do in the abstract — not how this specific tool surfaces that behavior. The Sigma community has rules for common platforms — but the platform you just onboarded may have zero.

And it gets harder. Large platform vendors continuously expand their ecosystems. Microsoft adds Power Platform. Salesforce adds new automation capabilities. A business user discovers a feature, turns it on, and starts sharing data externally. Security finds out later. There was no alert. The vendor didn't provide one. The community hadn't written one. Nobody warned you it was happening.

Existing detection maturity models measure how mature your detection *program* is. They don't tell you what to *detect* for the technology you just deployed. Existing community rule sets cover well-known platforms deeply and niche platforms almost not at all. Existing frameworks map adversary behavior at a level of abstraction that doesn't translate cleanly into "here is the query I should write for this SAP HCM deployment."

DCM fills that gap. It is a practitioner model — built for the person doing the work, not reviewing it — that answers:

> **"For this specific technology, in my specific environment — what should I be detecting, and how do I get there from wherever my logging is today?"**

---

## The Core Design Principle

DCM is built on one organizing principle:

**Every technology can be evaluated against a consistent set of detection requirements — regardless of what it is, how well it logs, or whether the community has ever written a rule for it.**

The consistency comes from the 10 detection domains — universal areas of organizational risk that apply to every deployment. The flexibility comes from the three-level maturity model — which meets organizations where they are and gives them a clear path forward.

---

## The 10 Detection Domains

The domains are the foundation of DCM. They represent the organizational areas that are universally exploitable or critical — the things adversaries always end up targeting regardless of what specific technology they're attacking.

Every technology touches one or more domains. Identifying which domains a technology touches is the first step in applying DCM. Most tools touch 2–4 directly.

| # | Domain | Core Question |
|---|---|---|
| 1 | Identity & Access | Who is authenticating, how, and from where? |
| 2 | Endpoint & Workload | What is executing, and is it expected? |
| 3 | Network & Perimeter | What is communicating, to where, and why? |
| 4 | Cloud & Infrastructure | What is changing in the control plane? |
| 5 | Data & Secrets | Who is accessing sensitive data, and in what volume? |
| 6 | Application Layer | Is the application being used as designed? |
| 7 | Supply Chain & Integration | Are third parties and integrations behaving as expected? |
| 8 | Insider & Privilege Abuse | Are privileged users operating within expected patterns? |
| 9 | Resilience & Availability | Is anything disrupting detection, backups, or availability? |
| 10 | Compliance & Audit Integrity | Is regulated data being accessed appropriately and audit trails intact? |

For full domain documentation including ATT&CK technique mappings, detection questions, log sources, and NIST controls — see the `domains/` directory.

---

## The Three-Level Model

### Level 1 — Detection Fundamentals

**The baseline. No excuses for not being here.**

Level 1 establishes the minimum detection requirement for any technology deployment. It is achievable by any organization regardless of size, budget, or dedicated detection engineering capability.

**How it works:**
For each domain a technology touches, DCM defines a set of universal detection questions — platform-agnostic questions that any technology in that domain should be able to answer. These questions form the baseline use case set for that technology.

The detection questions do not change by platform. The *answers* do. A question like "Did a service account authenticate interactively?" looks different in Active Directory, in Okta, in SAP, and in a cloud-native application — but it's the same question, and every tool that manages identity should be able to answer it.

**Level 1 workflow:**
1. Identify which domains the technology touches
2. For each domain, review the universal detection questions
3. Map each question to the available log sources in the technology
4. Document each as a use case using the DCM template
5. Track coverage status — what can this tool answer, what can't it?

**You are at Level 1 when:** Every technology in your environment has documented use cases covering the detection questions for the domains it touches, with ATT&CK and NIST mapping and coverage status tracked.

**The promise of Level 1:** Most adversary activity — regardless of sophistication — eventually touches the behaviors Level 1 detects. Privilege abuse. Unusual authentication. Lateral movement. Data staging. These are not APT-specific behaviors. They are universal. A solid Level 1 gives you residual coverage against threats you didn't specifically anticipate.

---

### Level 2 — Platform Detection Depth

**Extracting real signal from whatever logging exists — and holding vendors accountable for what doesn't.**

Level 2 addresses the hardest practical detection engineering problem: getting meaningful alerting from platforms with poor, limited, sparse, or poorly documented logging. This is the SAP HCM problem. The proprietary middleware problem. The internally developed application problem. The "we have logs but they're not great" problem.

**The Level 2 methodology:**

**Step 1 — Log Source Inventory**
Systematically document what the platform actually logs. Not what the vendor claims it logs — what it actually emits in your deployment. Field names. Event types. What triggers an event and what doesn't. Gaps between the vendor documentation and reality.

**Step 2 — Domain Mapping**
For each Level 1 detection question that the platform's native logging cannot answer, classify the gap:
- *Compensable* — another tool in your stack (IDP, firewall, EDR, CASB) can answer this question at a different layer
- *Vendor gap* — the platform simply does not provide this logging. Requires vendor remediation.
- *Configuration gap* — the logging exists but is not enabled or not collected. Requires internal remediation.

**Step 3 — Analog Tool Research**
For niche or proprietary platforms with no community detection content, identify functionally similar tools with better-documented security content and adapt their detection patterns. A proprietary HCM system that functions like Workday can borrow Workday detection patterns as a starting point.

**Step 4 — Compensating Control Mapping**
Document which tools in your environment provide coverage for gaps in the platform's native logging. "SAP HCM does not log failed authentication attempts at the session layer — Okta SSO captures this at the IDP layer for all federated logins."

**Step 5 — Vendor Gap Report**
For gaps that cannot be compensated, generate a structured vendor gap report using the DCM template. This gives the conversation with the vendor teeth — instead of "we need better logging," you can say "your platform cannot answer Detection Question 4 in Domain 1 because you do not emit authentication failure events at the session layer. Here is specifically what your platform needs to provide."

**You are at Level 2 when:** Every significant technology has platform-specific use cases grounded in its actual available logging, gaps are formally documented with compensating controls identified or vendor gaps formally raised, and your use case set reflects the reality of the deployment rather than an idealized version of it.

---

### Level 3 — Environmental Awareness

**Knowing when your environment changes before it becomes an incident.**

Level 3 addresses a problem distinct from Levels 1 and 2. Not "what should this known technology alert on" but "how do we detect when a platform we already own just became something different."

Large platform vendors continuously expand their ecosystems. Microsoft adds Power Platform capabilities. Salesforce adds new automation workflows. Google Workspace adds new sharing features. ServiceNow gets new integration options. Business users discover these capabilities and adopt them organically — often without security review, change management, or any awareness from the security team.

The security team finds out when something goes wrong. There was no alert for "Power Platform was first used in your tenant today." There was no alert for "an external user was just added to a Power Automate flow that has access to HR data." The vendor doesn't provide these alerts natively. The business team didn't know to tell you. And the Sigma community hasn't written rules for it because it's not adversary behavior — it's organic adoption behavior that creates risk.

**What Level 3 detects:**

- **First-time capability use** — a feature within an existing platform is used for the first time in your environment
- **New external connections** — data from a platform you own starts flowing somewhere it hasn't before
- **New privileged configurations** — sharing settings, external access, API connections, or data export configurations are created or modified
- **New service principals and OAuth grants** — applications getting new permissions within platforms you already operate
- **New automation and workflow creation** — business users building automations that security hasn't reviewed
- **Platform ecosystem expansion** — vendor-added capabilities that change the security surface of tools already in production

**The key distinction:** Level 3 detection is not about detecting adversary behavior. It is about detecting environmental change that creates security risk before that risk is exploited. The signal is not "something malicious happened" — it is "something changed that security needs to know about."

**Level 3 requires:**
- Strong unified audit logging from platform vendors
- SIEM correlation across platform-native audit logs
- A defined list of "platform sprawl signals" for each major platform in the environment
- A review workflow — Level 3 detections don't mean something is wrong, they mean something needs to be reviewed

**You are at Level 3 when:** Your detection posture updates when your environment updates. New capability adoption within major platforms triggers a security review before operationalization, not after an incident.

---

## How the Levels Work Together

The levels are not alternatives — they are a progression. Level 2 builds on Level 1. Level 3 builds on Level 2.

| Level | Question It Answers | Coverage Type |
|---|---|---|
| Level 1 | What should every technology alert on? | Universal baseline |
| Level 2 | How do we get real signal from this specific technology? | Platform-specific depth |
| Level 3 | How do we know when our environment changes? | Environmental awareness |

An organization with solid Level 1 coverage is significantly better protected than one with none. An organization with Level 2 coverage knows both what to detect and the actual reality of what their specific platforms can deliver. An organization with Level 3 coverage knows when the environment itself is changing in ways that create new detection requirements.

Most organizations should set Level 1 as the immediate goal across all critical technologies, Level 2 as the goal for their highest-risk platforms, and Level 3 as the advanced program goal for major platform ecosystems.

---

## The Universal Use Case Template

Every use case produced by DCM — at any level — uses the same 16-field template. See `model/use-case-template.md` for the full template and field guidance.

The template captures: use case name, domain, detection question, technology, log source, key log fields, detection logic, MITRE technique, MITRE tactic, NIST control, regulatory relevance, priority, coverage status, compensating control, draft detection rule, and tuning guidance.

---

## DCM and the Agentic AI Use Case

DCM was designed with agentic AI implementation in mind. An AI agent that takes DCM as its operating framework — combined with technology inputs, SIL diagrams, organizational tool stack context, and regulatory requirements — can automate the Level 1 and Level 2 workflows at scale, dramatically reducing the time from "we just onboarded a new technology" to "we have a reviewed use case set ready for SIEM implementation."

This is the detection engineering acceleration use case: DCM provides the methodology, the agent provides the scale.

---

*For domain reference: see `domains/`*  
*For level guides: see `model/level-1-fundamentals.md`, `level-2-platform-depth.md`, `level-3-environmental.md`*  
*For worked examples: see `worked-examples/`*  
*To contribute: see `CONTRIBUTING.md`*
