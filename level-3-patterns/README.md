# Level 3 Detection Patterns — Environmental Awareness

This directory contains platform-specific detection patterns for Level 3 of the DCM — environmental awareness detections that tell you when a platform you already own has changed in ways security needs to know about.

---

## What Level 3 Patterns Are

Level 3 patterns are not adversary behavior detections. They are **environmental change detections** — signals that something within a platform you already operate has been newly adopted, configured, or connected in a way that creates security risk before it is reviewed.

The question Level 3 answers is not "was this malicious?" It is "did something change that we need to look at?"

---

## Why This Matters

Large platform vendors continuously expand their ecosystems. Microsoft, Salesforce, Google, ServiceNow — all of them regularly add new capabilities to platforms organizations already operate. Business users discover these capabilities and adopt them organically. Security teams find out when something goes wrong.

There is no native alert for:
- "Power Platform was first used in your tenant today"
- "A new Power Automate flow was created with access to HR data and an external user connector"
- "A new OAuth consent grant was issued to a third-party application in your M365 tenant"
- "External sharing was enabled in a SharePoint site that previously had no external access"

Vendors don't provide these alerts natively. The business team doesn't know to tell you. The Sigma community hasn't written rules for it.

Level 3 patterns define these signals systematically so security teams can detect environmental change before it becomes an incident.

---

## Pattern Sets In Progress

- [ ] **Microsoft 365 Ecosystem** — Power Platform, Power Automate, Teams, SharePoint, new workload adoption (`microsoft-365-ecosystem.md`)
- [ ] **Google Workspace** — new sharing configurations, Drive external access, new app integrations
- [ ] **Salesforce** — new automation flows, external API connections, new user provisioning
- [ ] **ServiceNow** — new workflow creation, integration hub connections, external data access

---

## Pattern Structure

Each Level 3 pattern documents:

| Field | Description |
|---|---|
| Platform | The specific platform and capability |
| Signal | What event or condition indicates the change |
| Log Source | Where this signal appears |
| Detection Logic | How to detect it in a SIEM |
| Review Trigger | What security review this should initiate |
| Risk Context | Why this matters from a security standpoint |
| MITRE Relevance | Related ATT&CK techniques if the change were abused |
| False Positive Guidance | Expected legitimate scenarios that may trigger this |

---

## Contributing Level 3 Patterns

Level 3 patterns are among the most valuable contributions to DCM because this content essentially doesn't exist anywhere else in the community. If you have developed detection logic for platform sprawl or organic capability adoption in your environment, please contribute it.

See [CONTRIBUTING.md](../CONTRIBUTING.md) for guidelines.
