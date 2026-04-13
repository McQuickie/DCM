# Contributing to DCM

Thank you for your interest in contributing to DCM — Detection Coverage Model. This model improves through honest practitioner experience. Every contribution — a worked example, a Level 3 detection pattern, a vendor gap report, a Sigma rule, or a direct critique — makes it more useful for the community it exists to serve.

---

## Ground Rules

**Attribution matters here.** DCM was built on the principle that practitioners deserve credit for their work. Every contributor will be acknowledged. Please extend the same respect to others — do not submit work that isn't yours without proper attribution.

**Practitioners first.** DCM is a practitioner model, not a vendor product or a consulting framework. Contributions should serve detection engineers and security analysts doing real work, not market a product or service.

**Challenge openly.** If something in the model is wrong, missing, or poorly framed — say so. Open an Issue. The model only improves through honest critique.

**No bullshit.** Keep contributions concrete and actionable. Theoretical additions that don't help a practitioner get better alerting are out of scope.

---

## What We're Looking For

### Highest Priority

**Platform Worked Examples (Level 2)**
The most valuable contribution you can make. Show how DCM's detection questions mapped to a specific technology in a real deployment — which questions the tool could answer, which it couldn't, what the log source fields looked like, what compensating controls filled the gaps. Sanitize organizational details but keep the technical specifics.

Format: See `worked-examples/TEMPLATE.md`  
Location: `worked-examples/[platform-name]/`

Especially needed:
- SAP / ERP platforms
- HCM systems (Workday, SuccessFactors, UKG)
- Legacy and proprietary applications
- Niche SaaS platforms with limited security documentation
- Industrial/OT adjacent systems

**Level 3 Detection Patterns**
Environmental awareness detection patterns for specific platforms — the signals that tell you when a capability within a platform you already own has been newly adopted or changed. Especially needed for:
- Microsoft 365 ecosystem (Power Platform, Power Automate, Teams, SharePoint)
- Google Workspace
- Salesforce automation and integration capabilities
- ServiceNow workflows and integrations
- Any platform where organic adoption creates security risk before review

Location: `level-3-patterns/[platform-name].md`

**Vendor Gap Reports**
Formal, structured documentation of detection capabilities that platforms fail to provide — mapped to the DCM Level 1 baseline. Makes vendor accountability a community effort rather than an individual security team's uphill battle.

Location: `vendor-gap-reports/[vendor-platform].md`

### Also Highly Valued

**Sigma Rule Contributions**
Detection rules mapped to DCM domain taxonomy and universal detection questions. Follow the [Sigma specification](https://sigmahq.io) and include ATT&CK technique tags aligned with the relevant DCM domain.

Location: `sigma-coverage/rules/[domain-name]/`

**Domain Refinements**
Additional detection questions, updated ATT&CK technique mappings, improved log source guidance, or regulatory annotations (PCI-DSS, HIPAA, SOX) for existing domains.

Location: `domains/[domain-file].md`

**ATT&CK Coverage Gap Analysis**
Analysis of Sigma rule coverage against the ATT&CK technique sets in each DCM domain. Source data from [MITRE CAR](https://car.mitre.org/coverage/) or the SigmaHQ repository.

Location: `sigma-coverage/`

### Also Welcome

- Corrections to ATT&CK or NIST mappings
- New domain proposals (open an Issue first)
- Regulatory framework mapping improvements
- Translations of model content
- Academic or practitioner citations that support or challenge the model

---

## How to Submit a Contribution

### Step 1 — Open an Issue first (for significant additions)
Before investing time in a pull request for a new domain, a Level 3 pattern, a major methodology change, or a worked example, open an Issue to describe what you're planning. This avoids duplicate effort and lets the community weigh in.

For small fixes (typos, broken links, minor corrections) go straight to a pull request.

### Step 2 — Fork the repository

### Step 3 — Create a descriptively named branch
Examples:
- `add/worked-example-sap-hcm`
- `add/level3-patterns-m365-power-platform`
- `add/vendor-gap-report-microsoft-powerplatform`
- `add/sigma-rules-domain-01-identity`
- `fix/domain-06-technique-mapping`

### Step 4 — Make your changes
Follow the formatting and structure of existing files. Keep Markdown clean and consistent. Be specific — vague additions that don't help a practitioner get better alerting will not be merged.

### Step 5 — Submit a Pull Request
Open a pull request against `main` with:
- A clear title
- A brief description of what you added and why it's useful
- Any relevant Issue numbers

---

## Attribution for Contributors

All contributors will be credited in `CONTRIBUTORS.md` when their pull request is merged. Significant methodology contributions (worked examples, Level 3 patterns, domain additions) will be credited by name in the specific document as well.

---

## A Note on Vendor Gap Reports

Vendor gap reports should be factual and specific. Document what logging capability is absent, what DCM baseline requirement it fails to meet, and what the platform would need to provide to address the gap. Do not editorialize beyond what the evidence supports. The goal is to give organizations structured language for vendor conversations — not to publicly attack vendors.

---

## Code of Conduct

Be direct. Be honest. Be respectful.  
Critique the work, not the person.  
This is a practitioner community — keep it useful.

---

*Questions? Open an Issue tagged `question`.*
