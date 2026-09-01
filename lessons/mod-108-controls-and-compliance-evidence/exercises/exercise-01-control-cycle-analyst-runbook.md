# Exercise 01 — Control Cycle Analyst Runbook

**Estimated effort:** 2 hours
**Grounding chapters:** [01 — The Analyst's Scope on Controls and Compliance Evidence](../01-analyst-scope-on-controls-and-compliance-evidence.md), [02 — The Control-Testing Cycle and Evidence-Artefact Shape](../02-control-testing-cycle-and-evidence-artefacts.md), [03 — The Control-Status Report for Internal Audit](../03-control-status-report-for-internal-audit.md), [09 — Delegation Boundary and Escalation Patterns](../09-delegation-boundary-and-escalation-patterns.md).

## Objective

Author the analyst-tier *runbook* for a single quarterly control-testing cycle end to end — scope in, evidence pulls, `CTL-<year>-<sequence>-<test-N>` test-rows, control-status report skeleton, and the escalation-register spine — for the pair of inventory systems you have carried across the track (MCDA and MCDA-Benefits, or your equivalent). The drill's point is not to invent controls; it is to *operate the cycle* against a plausible library subset the way the analyst does on Monday morning of scoping week, and to leave behind an artefact set another analyst could pick up cold.

After this exercise you should be able to sit down at the start of any quarterly control cycle and, within the first working day, produce a scoped control list with named owners and deadlines, a request pack the GRC platform can post, and a report skeleton with row placeholders — without pausing to re-derive the shape.

## Prerequisites

- Chapters 01, 02, 03, and 09 read; the four cycle phases (scope → pull → attach-and-test → report-and-flag), the six evidence-artefact classes (config export, log sample, eval-report link, sign-off record, screenshot, interview note), the four stale-evidence flag rules (cadence-window, config-change, model-version-change, reg-obligation-change), the four verdict labels (*pass*, *fail*, *deviation*, *not-tested-in-period*), and the twenty-column `CTL-<year>-<sequence>-<test-N>` row schema fresh in memory.
- The MCDA (`INV-2026-0088`) and MCDA-Benefits (`INV-2026-0311` or equivalent) inventory rows from `mod-102`, the paired risk-register entries from `mod-103`, the fairness-review notes from `mod-104`, the impact-assessment corpus entries with their *measures* sections from `mod-105`, the regulator-tracker rows from `mod-106`, and the eval-evidence rows from `mod-107` open — the master library the analyst is testing against does not exist in a vacuum; it references every one of these upstream artefacts.
- A whiteboard, spreadsheet, or Markdown table tool for laying out the request pack and the test-row placeholders. The exercise's deliverable is Markdown, but you will iterate in whatever gives you fastest layout feedback.
- The [ISO/IEC 42001 abstract](https://www.iso.org/standard/81230.html), the [NIST AI RMF](https://www.nist.gov/itl/ai-risk-management-framework) and its [Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook), the [EU AI Act consolidated text](https://eur-lex.europa.eu/eli/reg/2024/1689/oj), and [SR 11-7](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) open for the crosswalk column citations the test rows will need.

## Problem statement

The deliverable is a **single Markdown file, `mod-108-ex-01-control-cycle-runbook.md`**, structured as a working runbook — sections numbered as the cycle proceeds, with worked artefacts inline. Author the runbook as if you are executing the Q2-2026 cycle for the MCDA and MCDA-Benefits systems today.

### Step 1 — Assemble the master-library subset in scope for the period

Author a **§1 Scope** section listing eight to twelve controls you would expect to see in the master library for a mixed High-tier deployment set that includes MCDA (a decision-support system in a regulated context, per `mod-102`) and MCDA-Benefits (a benefits-adjacent decision system, per the same inventory). You are *not* designing the library — you are asserting the subset the analyst would be handed by `senior-ai-governance-architect` for this quarter's cycle. Each control needs:

- `CTL-2026-<sequence>` identifier.
- One-sentence control statement in the master-library voice ("*For every…*").
- Owner (team or role, plus an escalation contact).
- Cadence and expected evidence class(es) per chapter 02.
- Applicability (which `INV-<year>-<sequence>` rows the control applies to; or *enterprise-wide*).
- Scoping rationale — why this control is in scope this period (cadence-driven, on-change trigger, tier default, or `senior-ai-governance-architect` direction).

Cover at minimum: one input/guardrail control on a customer-facing endpoint, one fairness / disparate-impact-monitoring control, one release-assurance sign-off control, one impact-assessment or FRIA control, one vendor-artefact / supply-chain control, one eval-cadence control that cites a `mod-107` `EVAL-<year>-<sequence>` row, and one security-linked control that will use an OWASP LLM 2025 tag (chapter 04). The remaining slots can flex to whatever the inventory tiers make plausible.

Do not invent controls that require enterprise-specific configurations you cannot describe honestly. Where a control statement's specifics would depend on the enterprise, mark the specifics `<!-- needs-research: local library statement -->` rather than guessing.

### Step 2 — Draft the pull protocol per control

Author a **§2 Pull protocol** section that, for each in-scope control, records:

- Named recipient (owner from §1) and the recipient's manager (as escalation).
- Requested evidence-artefact class(es), matching the library expectation.
- Time window for log samples and sampling rule; version-of-record for config exports; specific eval-evidence row ID for eval-report links; specific sign-off record ID or template for sign-off records.
- Deadline (choose a plausible date five to ten working days before your target report-issuance date).
- Escalation path if the recipient does not respond by the deadline.

Render the pull requests as a single table plus, for one representative control, a full-text example of the request the analyst posts through the GRC platform's workflow tooling.

### Step 3 — Produce test-row placeholders

Author a **§3 Test rows (placeholders)** section that fills in the twenty-column `CTL-<year>-<sequence>-<test-N>` row schema from chapter 03 for each control in §1. Columns you can populate ahead of the pull (Test ID, Control ID, Control statement, Applicable systems, Owner, Cadence, Evidence class expected, Regulatory obligations satisfied, Framework crosswalk pointers, Analyst) go in verbatim. Columns that depend on the pulled evidence (Verdict, Evidence class delivered, Evidence artefact IDs, Stale-evidence flags, Prior-period verdict, Trend, Follow-up action, Escalation class, Analyst note) are populated with either a *TBD-<reason>* placeholder or, where the shape is predictable enough, the analyst's *expected* value with an *if-confirmed* qualifier.

Include at least two rows that model non-*pass* outcomes ahead of the pull — one *deviation* driven by a downgraded evidence class (e.g., an interview note delivered where a log sample was expected), and one *fail* driven by a stale-evidence flag (e.g., a config-change trigger tripped between the last-tested date and today). The point is to exercise the row shape's honesty, not to pretend every control will pass.

### Step 4 — Sketch the control-status report skeleton

Author a **§4 Report skeleton** section rendering the nine-section `CSR-2026-Q2` shape from chapter 03. §0 Header, §1 Executive summary (bullet placeholders projecting from the rows you drafted), §2 Scope (a pointer to §1 of the runbook), §3 Verdict rollup (grouped by verdict; placeholders for the counts), §4 Findings (one entry per non-pass row from §3 of the runbook), §5 Escalations (see §5 of the runbook, below), §6 Stale-evidence roll-up (one entry per triggered flag), §7 Delegation-boundary notes (which controls' findings are routed to `ai-infra-security`, which are held for `senior-ai-governance-architect` library-level fix, which are external-audit-scoped and out of report), §8 Trend against prior period (placeholders — this is the first period in the exercise), §9 Appendix — evidence catalogue (placeholders keyed to the `EV-2026-*` identifiers referenced in §3).

The skeleton is not the final report; it is the shape the analyst walks into the report-composition meeting with. Every §3-runbook row that produced a non-pass verdict shows up somewhere in the skeleton; §7's delegation-boundary notes name every routing you will make.

### Step 5 — Open the escalation-register spine

Author a **§5 Escalation-register spine** section that, for each non-*pass* row in §3 of the runbook, opens a placeholder `ESC-2026-EX01-<sequence>` entry using the row shape from chapter 09. Class assigned per chapter 09 definitions (Class 1 library-design fix, Class 2 security route, Class 3 vendor / contract action, Class 4 governance-council decision). Status is *open*; resolution note is empty; roll-up reference points at the `CSR-2026-Q2` skeleton section.

Mark clearly which escalations are *findings that should stay in §4 of the report* versus *escalations that warrant §5 treatment* — chapter 09's file-up threshold governs. Not every non-pass row is an escalation; the runbook must state which are and which are not.

### Step 6 — Write the Monday-morning checklist

Close the runbook with a **§6 Monday-morning checklist** — the twelve-to-twenty-line ordered list an analyst executes on the first day of the cycle. Steps in order, each with the artefact produced ("*Open GRC platform; scope query returns N controls; export scope list*", "*Post pull requests through platform workflow to owners named in §2; deadline set to \[date\]*", etc.). This is the artefact the *next* analyst reads before running the next quarter's cycle.

## Requirements

- **Every section of the runbook is present.** Missing §5 (escalation-register spine) or §6 (Monday-morning checklist) reads as *drafted the pretty parts and skipped the boring ones*. Chapter 09 was explicit that the escalation register is the connective tissue.
- **Between eight and twelve controls in §1**, spanning at minimum the seven categories listed above (input/guardrail, fairness, release-assurance sign-off, impact-assessment, vendor-artefact, eval-cadence, security-linked). A runbook with all input-guardrail controls does not exercise the cross-role pull protocol.
- **Every control names the specific evidence class(es) expected**, matching chapter 02's six. Vague values (*documentation*, *evidence*) are not accepted.
- **Every control names an owner and an escalation contact.** Anonymous ownership (*the team*) is not accepted.
- **Every pull-request row in §2 has a deadline and an escalation path.** The deadline is not the report-issuance date; it is the pull deadline set five to ten working days earlier.
- **The §3 test-row placeholders populate every column of the chapter-03 schema.** Columns dependent on the pull are populated with *TBD-<reason>* or an *if-confirmed* qualifier; blanks are not permitted.
- **At least two rows model non-pass outcomes** — one *deviation* driven by a downgraded evidence class, one *fail* driven by a stale-evidence flag.
- **The §4 report skeleton has all nine sections**, each with at least placeholder content projecting from §3 of the runbook. A missing section reads as *not run* per chapter 03.
- **The §5 escalation-register spine distinguishes findings from escalations** per chapter 09's file-up threshold — recurrence across periods, cross-role action, cross-window, cross-system, or exposing a process gap. A blanket *every non-pass row is an escalation* is a chapter-09 failure mode.
- **The Monday-morning checklist is ordered and each step produces a named artefact.** A checklist step that reads *review the library* without naming what the reviewer produces is not a checklist step.
- **Framework-crosswalk pointers in §3 rows cite the specific referent** — `NIST AI RMF MEASURE 2.7`, `EU AI Act Article 15`, `ISO/IEC 42001:2023 §<clause>` (with a `<!-- needs-research: -->` marker if you are paraphrasing from the abstract), `SR 11-7 Pillar <n>`, and the internal-policy anchor. Bare *NIST* or *EU AI Act* is not a citation.
- **The security-linked control's row carries an OWASP LLM 2025 tag** per chapter 04's rule. Version-cited (`LLM01:2025 — Prompt Injection`, not `LLM01`).
- **No fabricated evidence.** Where the runbook needs the shape of an evidence artefact you cannot honestly describe (e.g., a screenshot of an internal dashboard that does not exist in the exercise environment), describe the shape and mark `<!-- illustrative — not from a real system -->`.

## Starter guidance

- Do §1 before you look at §3. If you populate row placeholders before the scope list is stable, you will re-write the rows every time §1 shifts. The scope list is the anchor.
- The pull protocol (§2) is the single most-often-shortcut part of the cycle. Do not skip the *escalation path if the recipient does not respond by the deadline* field — chapter 02 was explicit that non-response is a control gap in itself.
- When drafting the *deviation* row for §3, prefer the *evidence-class-downgrade* shape (interview note delivered where a config export was expected) over more exotic deviations. Chapter 02 was explicit that this is the most common deviation the analyst sees, and it is the one internal audit reads most frequently in the report.
- When drafting the *fail* row for §3, prefer the *stale-evidence flag tripped between last-tested and today* shape (config-change or model-version-change). This is the failure mode that catches enterprises out — the last quarterly test passed, but the underlying config changed the following week, and the current cycle's evidence is invalid.
- The escalation-register spine (§5) should be smaller than the non-pass row count in §3. If it is not, you are filing an escalation for every finding — chapter 09's file-up threshold governs which findings become escalations.
- The Monday-morning checklist (§6) is the artefact the exercise is really testing. If your checklist can be executed step-by-step by a peer analyst who has never seen the cycle before, you have internalised the discipline. If it reads as narrative, you have written a story instead of a runbook.
- Where the enterprise-specific specifics (GRC platform name, ticket-tool name, dashboard URLs) are not honest to fill in, use bracket placeholders (`[GRC-platform]`, `[dashboard-URL]`) that a downstream reader replaces during real execution. Do not invent tool names.

## Acceptance criteria

- `mod-108-ex-01-control-cycle-runbook.md` filed with §1–§6, each populated per the requirements above.
- §1 has eight to twelve controls covering the seven category minimum; each control has an identifier, statement, owner, escalation contact, cadence, evidence-class expectation, applicability, and scoping rationale.
- §2 pull-protocol rows have named recipients, evidence-class expectations, time windows / sampling rules / version pins, deadlines set five to ten working days before report issuance, and escalation paths for non-response. One representative control has the full-text request example.
- §3 test-row placeholders populate every column of the chapter-03 schema; every column is either populated verbatim, marked *TBD-<reason>*, or carries an *if-confirmed* qualifier. At least one *deviation* row and one *fail* row are present.
- §4 report skeleton has nine sections, each with at least placeholder content projecting from §3.
- §5 escalation-register spine distinguishes findings from escalations per chapter 09; every escalation carries a class, source-row link, requested action, escalation owner, target date, and status.
- §6 Monday-morning checklist is ordered, each step names its produced artefact, and the whole list is executable by another analyst without narrative context.
- Framework-crosswalk pointers cite specific referents in every §3 row; the security-linked row carries a version-cited OWASP LLM 2025 tag.
- No fabricated evidence; illustrative placeholders are marked as such; enterprise-specific gaps are marked `<!-- needs-research: -->` rather than guessed.

## Stretch goals

- **A retrospective on last-period rows.** Author a mock §3.5 — a review of the *prior-period* test rows for the same controls (verdicts, follow-up actions, resolution dates) — to populate the *prior-period verdict* and *trend* columns of the current-period rows honestly. This exercises the trend discipline chapter 03 called out and prepares the ground for the §8 trend section of the report skeleton.
- **A cross-control coverage map.** After §5, add a short table that pivots the §1 controls against the seven risk categories from chapter 05 (prompt injection, data exfiltration, model theft, membership inference, adversarial evasion, supply-chain compromise, guardrail bypass) plus the fairness dimension. This surfaces where the library subset in scope for the period has coverage gaps at the *risk-category* level, which chapter 09's pattern-recognition section calls out as a class-1 escalation trigger.
- **A GRC-platform request-template artefact.** Take the full-text request example from §2 and abstract it into a reusable Jinja/mustache-style template the analyst can populate for any future control. Fields to templatise: control ID, control statement, evidence class, time window, deadline, escalation contact. This template lives in the analyst's toolbox and is used every cycle.
- **A stale-evidence audit of the prior period.** For each control in §1, walk backwards: if the prior period tested the control and passed, is any of the evidence still valid today, or has one of the four stale-evidence flag rules tripped in the interim? Author this as a short table alongside §3 that predicts which controls' *prior-period* evidence is stale and needs re-baselining this quarter regardless of the on-cadence expectation.
- **A pre-issuance-review agenda for `senior-ai-governance-architect`.** After §4, add a **§4.5 pre-issuance review** section that lists the library-change items the report will surface (per chapter 03's hand-off section), the target review date, and the analyst's requested action from `senior-ai-governance-architect`. This is the artefact the analyst sends alongside the report draft before the report reaches internal audit.

## Deliverables

- `mod-108-ex-01-control-cycle-runbook.md` — six numbered sections (§1 scope, §2 pull protocol, §3 test rows, §4 report skeleton, §5 escalation-register spine, §6 Monday-morning checklist) plus any stretch sections.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works one reference runbook shaped around the MCDA / MCDA-Benefits pair with a ten-control scope subset, one full-text pull-request example, five test-row placeholders (three *pass-expected*, one *deviation*, one *fail*), a nine-section report skeleton, and a twelve-step Monday-morning checklist. Yours will differ in the specific controls chosen, the specific owners named, the specific dates set, and the specific escalations opened. What should not differ is (a) the seven-category coverage minimum in §1, (b) the pull-protocol discipline in §2 (deadline + escalation path per request), (c) every column of the chapter-03 row schema populated in §3 (with TBD-<reason> where dependent on the pull), (d) all nine report sections in §4, (e) the finding-vs-escalation distinction in §5, and (f) an executable Monday-morning checklist in §6. A tight runbook that another analyst could execute cold beats a longer runbook that reads as narrative and leaves the operational specifics to the reader's imagination.
