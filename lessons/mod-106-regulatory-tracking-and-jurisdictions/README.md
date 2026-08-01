# mod-106 — Cross-Jurisdiction Regulatory Tracking

**Estimated effort:** 12 hours

Every impact assessment, register entry, and bias-review note the analyst has authored to this point in the track was written against a specific state of the regulatory landscape. The landscape does not sit still — AI Act provisions phase in, Colorado's AG issues implementing rules, Federal Register notices land, executive orders are issued and rescinded, sector regulators publish or revise guidance, and each of those events can invalidate the *this is what we knew when we signed off* footer on last quarter's artefact. This module is the discipline that keeps the situational awareness current, tied to the specific inventory rows the obligations attach to, and — critically — turned into routed action when a change lands.

## Learning objectives

- Maintain a rolling AI regulatory tracker across EU (AI Act, GDPR, CoE framework), US federal (EEOC, FTC, HHS, FDA, White House Executive Orders in force), US state (Colorado AI Act, NYC Local Law 144, Illinois BIPA implications for biometric AI), UK (AI regulation trajectory, ICO guidance), Canada (AIDA trajectory, TBS directive), and sector regulators (FDA GMLP, banking model risk, insurance actuarial oversight).
- Read GDPR Article 22 (automated decisioning) and Article 35 (DPIA), CCPA / CPRA, HIPAA, and know when to flag an AI use case to privacy counsel — deferring legal opinion to counsel.
- Position the IAPP AIGP certification body of knowledge as the shared vocabulary for this tracking work.
- Read the EU AI Office General-Purpose AI Code of Practice as an example of a voluntary code that anticipates regulator expectations.
- File a regulatory-change note into the governance inventory when a new obligation lands and route it to the affected system owners.

## Chapters

| # | Chapter | Focus |
|---|---|---|
| 01 | [The Rolling AI Regulatory Tracker — Method, Schema, and Cadence](01-rolling-regulatory-tracker-method.md) | Tracker as register (not memo); jurisdiction taxonomy; field shape; weekly / monthly / quarterly cadence; primary vs secondary sources |
| 02 | [The EU Stack — AI Act, GDPR, and the Council of Europe Framework Convention](02-eu-stack-ai-act-gdpr-coe.md) | AI Act four-tier structure and phase-in schedule; provider vs deployer; GDPR Article 22/35/36 hooks; CoE framework as international baseline |
| 03 | [The US Federal Patchwork — EEOC, FTC, HHS, FDA, and Executive Orders](03-us-federal-patchwork.md) | Joint statement; five authorities (EEOC, FTC, HHS OCR, FDA, NIST as framework); EO overlay refresh discipline |
| 04 | [The US State Stack — Colorado AI Act, NYC Local Law 144, and Illinois BIPA](04-us-state-stack.md) | Colorado AI Act developer/deployer duties; NYC LL 144 bias audit + notice; Illinois BIPA + biometric analogues; horizon-scan for state legislation |
| 05 | [The UK and Canada Trajectories — Principles-Based Regulation and Federal-Sector Directives](05-uk-canada-trajectories.md) | UK five principles, ICO as load-bearing regulator, DUA Act 2025; Canada TBS Directive, AIDA trajectory, PIPEDA + provincial |
| 06 | [Sector Regulators — FDA GMLP, Banking Model Risk, and Insurance Actuarial Oversight](06-sector-regulators.md) | FDA SaMD + PCCP + GMLP; SR 11-7 / OCC 2011-12 model risk; NAIC Model Bulletin + EIOPA; specialist-routing discipline |
| 07 | [Privacy Laws and the Flagging Discipline — GDPR Article 22, GDPR Article 35, CCPA/CPRA, and HIPAA](07-privacy-law-flagging-discipline.md) | Three tests for Article 22; WP 248 nine-criteria filter; CPPA ADMT regulations; HIPAA covered-entity / BAA discipline; question-not-conclusion flagging pattern |
| 08 | [The IAPP AIGP Body of Knowledge as the Shared Vocabulary](08-iapp-aigp-shared-vocabulary.md) | Five AIGP domains; tagging tracker rows; DPO / CISO / CRO / auditor audience alignment; certification decision framing |
| 09 | [Voluntary Codes — The EU AI Office General-Purpose AI Code of Practice](09-voluntary-codes-gpai-code-of-practice.md) | Voluntary codes as anticipatory intelligence; GPAI Code chapters (transparency, copyright, safety-and-security); Article 56 presumption; tracker treatment |
| 10 | [Filing the Regulatory-Change Note and Routing It to Affected System Owners](10-regulatory-change-note-routing.md) | Change-note structure; routing pattern (primary/secondary/tertiary); closure into the impact-assessment corpus; failure modes prevented |

## Exercises

Hands-on prompts; solutions live in the paired `ai-governance-analyst-solutions` repository.

| # | Exercise | Estimated |
|---|---|---|
| 01 | [Regulatory Tracker Schema](exercises/exercise-01-regulatory-tracker-schema.md) | 2 h |
| 02 | [EU AI Act vs US State Crosswalk](exercises/exercise-02-eu-ai-act-vs-us-state-crosswalk.md) | 2 h |
| 03 | [GDPR Article 22 Flagging Drill](exercises/exercise-03-gdpr-art22-flagging-drill.md) | 2 h |
| 04 | [Sector Regulator Shape Drill](exercises/exercise-04-sector-regulator-shape-drill.md) | 2 h |
| 05 | [Regulatory-Change Routing Note](exercises/exercise-05-regulatory-change-routing-note.md) | 2 h |

## Lab

- `lab-01` — Not yet authored; scheduled for the next content cycle.

## Quiz

- Knowledge check per the curriculum plan. Not yet authored; scheduled for the next content cycle.

## Resources

Curated primary references are in [`resources.md`](resources.md).

## Prerequisites

Fluency in `mod-101` (RMF, GenAI Profile, ISO 42001, EU AI Act tiers, role-scope), `mod-102` (inventory rows and tier tagging that this module cross-references), `mod-103` (register entries and residual routing that this module feeds change-notes into), `mod-104` (fairness-review notes on hiring AI that connect to LL 144 and EEOC), and `mod-105` (canonical impact-assessment document and the AIA / FRIA / DPIA / sector-view generation this module refreshes).

## Downstream dependencies

- `mod-107-reading-eval-and-audit-evidence` — evaluation and audit-evidence discipline reads the tracker's affected-inventory-row list to scope its walks.
- `mod-108-controls-and-compliance-evidence` — the control library refreshes on tracker updates; change-notes route into the control-mapping refresh.
- `mod-109-incident-response-and-continuous-monitoring` — incident-response plans reference tracker rows for regulator-notification obligations; continuous monitoring reads the tracker's last-verified dates.
- `mod-110-communication-and-council-support` — council briefings read from the tracker and from the change-note log; the AIGP body-of-knowledge tags on the tracker rows structure the briefing sections.
- `project-101` — end-to-end deliverable set uses the tracker as the situational-awareness spine.
