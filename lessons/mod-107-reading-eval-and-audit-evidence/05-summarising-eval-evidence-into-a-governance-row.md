# Summarising Eval Evidence into a Governance-Record Row

## Why this chapter

Chapters 02, 03, and 04 walked the three most common report shapes — Inspect-style eval, RAG-triad, red-team engagement. The point of reading each of them is not the reading itself but the *row*: a per-system, per-report piece of evidence in the governance repository that captures the three load-bearing claims (residual-risk, threshold-decision rationale, unresolved findings) alongside enough provenance for a downstream auditor, a release-assurance engineer, or a governance council to trust and act on it.

This chapter fixes the row schema. It is the analyst's tangible output for this module. Every eval-adjacent line in the register (`mod-103`), every control assertion in the control library (`mod-108`) whose evidence type is *evaluated-and-below-threshold*, every impact-assessment refresh-trigger (`mod-105`) that fires on an eval finding, and every council briefing (`mod-110`) that cites *the eval says X* traces back to a row shaped like the one specified here.

## The row is a register entry, not a memo

The same discipline as `mod-106`'s regulatory-tracker row: a row is a discoverable, versioned, cited piece of evidence, not tacit knowledge in the analyst's head or a slide in the last council deck. The row lives in the same governance repository or GRC platform that holds the inventory, the register, the impact-assessment corpus, and the regulatory tracker. It uses a stable identifier convention that never re-uses.

Identifier convention used throughout this chapter: `EVAL-<year>-<sequence>` (parallel to `INV-`, `REG-`, `RSK-`, `IA-` conventions established in earlier modules). Every eval / red-team / audit report the analyst files becomes one row with this identifier.

## The row schema

The full analyst-tier row schema, column by column, in the order the analyst populates them:

### Identity and provenance

- **Eval row ID.** `EVAL-<year>-<sequence>`. Stable; never re-used.
- **Report title.** Verbatim from the report header.
- **Report type.** Controlled vocabulary: *capability-eval* / *safety-eval* / *fairness-eval* / *rag-triad-eval* / *red-team* / *external-audit* / *vendor-system-card* / *vendor-rsp-disclosure*.
- **Author / evaluator.** The team that produced the report (internal team name, external vendor name, or the frontier lab whose card this is).
- **Report date.** The date the report was published or dated.
- **Report version.** The report's own version identifier.
- **Source-artefact link.** A stable link to the report — a repository path, a GRC-platform document identifier, or (for public artefacts) a stable URL. For enterprise-internal reports, prefer a repository-controlled path over a shared-drive URL.
- **Log / raw-evidence link.** For evals with underlying log files (Inspect `.eval` files, RAG-eval trace records, red-team reproduction transcripts), a link or path.

### System under evaluation

- **Inventory row ID.** Foreign key to the `INV-<year>-<sequence>` row in the inventory (`mod-102`). The row is unusable without this — an eval that cannot be tied to an inventoried system is an eval of nothing.
- **System version(s) evaluated.** Application version, and for RAG systems the four dimensions (application, retrieval index, embedding model, generation model) from chapter 03.
- **Deployment configuration snapshot.** System prompt version, tool inventory, guardrails, temperature, and any other solver-level parameters from chapter 02 that shape the result.
- **Delta since deployment.** A one-line note: is the deployed system materially different from the evaluated system? If yes, the row is *provisional* (see status field below).

### The three load-bearing claims

- **Residual-risk claim.** One or two sentences, in the report's own words where possible, augmented with the disaggregated per-slice values where a headline aggregate hides a subset failure. This is the field the council reads.
- **Threshold-decision rationale.** The named threshold (internal policy reference, vendor RSP / Preparedness-Framework capability threshold, regulator-recognised benchmark) and the yes-or-no call. If no threshold is cited in the report, this field is populated with *no threshold cited in report — follow-up filed [ID]* and the row is flagged for escalation (chapter 10).
- **Unresolved findings list.** Itemised. Each item: finding identifier (from the report), one-line description, severity (with rubric version), likelihood or exploitability, current status, owner, target closure date. Empty (no unresolved findings) is a valid answer; blank (analyst did not check) is not.

### Cross-artefact references

- **Register entries updated.** Foreign key list to `RSK-<year>-<sequence>` rows updated in the risk register (`mod-103`) as a result of this eval.
- **Impact-assessment refresh triggers fired.** Foreign key list to `IA-<year>-<sequence>` rows in the impact-assessment corpus (`mod-105`) that this eval triggers a refresh on.
- **Regulatory-tracker rows linked.** Foreign key list to `REG-<year>-<sequence>` rows in the regulatory tracker (`mod-106`) whose scope-trigger this eval addresses.
- **Related eval rows.** Foreign key list to prior or companion `EVAL-<year>-<sequence>` rows — the prior run of the same eval, a paired red-team engagement, a companion capability-eval that this safety-eval sits alongside.

### Provenance for the eval configuration

- **Task / dataset.** For eval reports: the task identifier(s), dataset identifier(s), dataset version(s), and sample count. For red-team reports: the methodology summary and taxonomy references (OWASP LLM Top 10, MITRE ATLAS, NIST 600-1).
- **Solver configuration.** Prompting scaffold, tool inventory, temperature, best-of-N configuration. For red-team: multi-turn depth, agent-vs-human, external vendor identity.
- **Scorer configuration.** Scorer type (exact-match, rubric-based, LLM-as-judge, human-labelled), and for LLM-as-judge scorers the judge model identifier and judge-prompt version. For red-team: severity rubric name and version.
- **Aggregate result.** The headline numbers verbatim from the report.
- **Per-slice breakdown.** A short structured summary of the disaggregated results — enough to make clear where any failure clusters. Full breakdowns stay in the report; the row carries a summary.

### Status, review, and cadence

- **Row status.** Controlled vocabulary: *evidence-current* / *evidence-provisional* (deployed system has drifted from evaluated system) / *evidence-stale* (report is beyond its own refresh cadence) / *escalated* (under-evidenced, mis-scoped, or stale — see chapter 10) / *retired* (system decommissioned or eval superseded).
- **Refresh cadence.** How often this eval is due to be re-run. Populated from the report's own change-log section or from the enterprise's per-report-type policy. Typical: safety evals per model version change plus quarterly; RAG-triad evals per index refresh plus monthly; red-team engagements annually or per material change.
- **Next-due date.** The date by which the next refresh is expected.
- **Last-verified date.** The date the analyst last confirmed the row is still current (parallel to the tracker's *last-verified* in `mod-106`).
- **Verified-by.** The analyst who last verified.

### Governance-package fields

- **Council-relevant flag.** Boolean: does this row feed a council briefing? A row with a Critical or High unresolved finding, a threshold-decision reversal, or a novel-risk-category finding is council-relevant by default.
- **Release-assurance-relevant flag.** Boolean: is this row an input to a release-assurance sign-off packet (chapter 09)? Any row on a system approaching a release gate is release-assurance-relevant.
- **Counsel-flag.** Boolean plus one-line question — is there an under-specified legal / regulatory implication that counsel should be asked about? Parallel to `mod-106`'s *notes for counsel* column.
- **Notes.** Free-text field for anything the schema does not accommodate. Kept short.

Nineteen columns split across six groups. Every column is populated in every row; where a field genuinely does not apply, the value is `Not applicable — [one-line reason]` (parallel to the `mod-106` convention).

## Populating the row from an Inspect-style report

Walked in chapter 02. The mapping:

| Row field | Source in Inspect-style report |
|---|---|
| Report title / date / author | Header (section 1) |
| Report type | *safety-eval*, *capability-eval*, or *fairness-eval* depending on scope (section 2) |
| System version(s) | Model section (section 3) |
| Deployment configuration snapshot | Solver configuration (section 5) |
| Task / dataset / solver / scorer | Sections 4, 5, 6 |
| Aggregate result | Section 7 |
| Per-slice breakdown | Section 8 |
| Residual-risk claim | Section 10 |
| Threshold-decision rationale | Section 11 |
| Unresolved findings | Section 12 |
| Refresh cadence / next-due | Section 13 |
| Log / raw-evidence link | Section 14 |

## Populating the row from a RAG-triad report

Walked in chapter 03. The mapping:

| Row field | Source in RAG-triad report |
|---|---|
| Report title / date / author | Header (section 1) |
| Report type | *rag-triad-eval* |
| System version(s) | Header + retrieval-config section (sections 1, 4) — record all four dimensions |
| Deployment configuration snapshot | Generation-config section (section 5) |
| Task / dataset / solver / scorer | Sections 3, 4, 5, 6 |
| Aggregate result | Section 7 — record all three triad metrics separately |
| Per-slice breakdown | Section 8 |
| Residual-risk claim | Sections 9 (failure-mode catalogue) and 10 |
| Threshold-decision rationale | Section 11 — per-metric thresholds, not composite |
| Unresolved findings | Section 12 (cross-referenced with section 9) |
| Refresh cadence / next-due | Section 13 |
| Log / raw-evidence link | Section 14 |

## Populating the row from a red-team engagement report

Walked in chapter 04. The mapping:

| Row field | Source in red-team report |
|---|---|
| Report title / date / author | Header (section 1) |
| Report type | *red-team* |
| System version(s) | Test-setup section (section 4) |
| Deployment configuration snapshot | Test-setup section (section 4) |
| Task / dataset / solver | Methodology section (section 3) — record taxonomy references |
| Scorer configuration | Severity rubric section (referenced in section 5's findings) |
| Aggregate result | Findings-summary section (section 6) — distribution by severity and status |
| Per-slice breakdown | Findings section (section 5) — per-category counts |
| Residual-risk claim | Residual-risk narrative (section 8) evidenced by section 6 |
| Threshold-decision rationale | Section 9 |
| Unresolved findings | Section 10 (cross-referenced with any section-5 findings whose status is open) |
| Refresh cadence / next-due | Section 11 (change log) plus enterprise red-team-engagement-cadence policy |
| Log / raw-evidence link | Appendix (section 11), with access-control notes preserved |

## A worked example — the MCDA row set

Bringing forward chapters 02 and 04's illustrative MCDA examples (both illustrative — not real reports), the analyst files two rows in this module:

**`EVAL-2026-088` — MCDA safety-eval (from chapter 02):**

- Report title: *MCDA safety eval, run 2026-07-14*.
- Report type: *safety-eval*.
- Inventory row: `INV-2026-0088` (MCDA).
- System version: application v3.6, system prompt v1.7, model `anthropic/claude-3-5-sonnet-20241022`.
- Residual-risk claim: *Overall safe-answer rate 96.4% (above internal 95% threshold). Protected-class-generalisation category at 89.0%, below its category-specific 92% threshold; graded amber requiring follow-up.*
- Threshold-decision rationale: *Overall threshold met; category-specific threshold missed. Per safety-eval-policy v2.4, amber grading requires a follow-up eval within 60 days.*
- Unresolved findings: SE-2026-114 (protected-class-generalisation, Med severity, MCDA product owner, closure 2026-09-14); SE-2026-115 (judge-prompt calibration, Low, Safety Eval Team, closure 2026-Q4).
- Task / dataset: `mcda_harm_suite_v3_2` (1,200 samples, four categories).
- Solver: single-turn, temperature=0.7, three-trial majority.
- Scorer: LLM-as-judge (`anthropic/claude-3-opus-20240229`, judge-prompt v2.1, calibrated 0.83 IAA on 50 samples).
- Aggregate: 96.4% safe overall.
- Per-slice: 99.3 / 98.7 / 89.0 / 98.7 by category.
- Related eval rows: `EVAL-2026-053` (prior MCDA safety eval, 2026-05-02).
- Register entries updated: `RSK-2026-0088-04` (protected-class residual severity refreshed to Medium).
- Impact-assessment refresh triggers fired: `IA-2026-0088` (refresh scheduled 2026-09-30).
- Row status: *evidence-current*.
- Refresh cadence: *safety evals per system-prompt version change plus quarterly*.
- Next-due: 2026-10-14.
- Last-verified / verified-by: 2026-08-01 / analyst.
- Council-relevant: true (category-specific miss on protected-class).
- Release-assurance-relevant: true (MCDA v3.7 release gate 2026-09-15).
- Counsel-flag: true — *does the category-specific miss on protected-class generalisation, given the enterprise operates in Colorado and NYC, need to be surfaced to counsel for the Colorado AI Act consumer-notice and NYC LL 144 bias-audit implications on any MCDA-adjacent hiring or credit use? Row `REG-2026-US-STATE-003` and `REG-2026-US-STATE-005` linked.*

**`EVAL-2026-091` — MCDA red-team engagement (from chapter 04):**

- Report title: *RT-2026-014, MCDA red-team engagement, 2026-08-01 through 2026-08-12*.
- Report type: *red-team*.
- Inventory row: `INV-2026-0088` (MCDA).
- System version: application v3.7, system prompt v1.7 (with v1.8 draft validated in-engagement), model `anthropic/claude-3-5-sonnet-20241022`.
- Residual-risk claim: *Protected-class-generalisation via analogy-prompt closed under system-prompt v1.8. Competitor-disparagement via indirect prompting and over-refusal on benign paraphrases open with named owners.*
- Threshold-decision rationale: *Per internal red-team-acceptance-policy v1.5, no High-severity findings may remain open at release; Medium-severity findings must have named owner and target closure within 30 days. State meets release-gating conditional on system-prompt v1.8 rollout.*
- Unresolved findings: RT-2026-014-002 (competitor-disparagement, Medium, MCDA product owner, closure 2026-09-11); RT-2026-014-003 (over-refusal, Medium, MCDA product owner, closure 2026-09-11); RT-2026-018 (prompt-injection via retrieved-context, scheduled 2026-10).
- Task / dataset: internal harm-suite protected-class subset, MITRE ATLAS AML.T0043 / AML.T0051 techniques, OWASP LLM04 over-refusal check.
- Solver: manual multi-turn iterated 3 rounds, 3 internal + 1 external evaluators.
- Scorer: internal red-team severity rubric v1.5 (four-tier).
- Aggregate: 3 findings, 0 High open, 2 Medium open, 1 High closed in-engagement.
- Per-slice: protected-class 0/25 residual after v1.8 mitigation; competitor-disparagement 1/25; over-refusal 40% of benign paraphrase set.
- Related eval rows: `EVAL-2026-088` (chapter 02's MCDA safety eval).
- Register entries updated: `RSK-2026-0088-04` (residual severity Med, mitigation validated); `RSK-2026-0088-07` (new — over-refusal business-impact risk).
- Impact-assessment refresh triggers fired: `IA-2026-0088` (already flagged from `EVAL-2026-088`).
- Row status: *evidence-current*.
- Refresh cadence: *red-team engagements annually per system or per material change*.
- Next-due: 2027-08-01 or upon next material change.
- Last-verified / verified-by: 2026-08-15 / analyst.
- Council-relevant: true (mitigation validation and open Medium findings).
- Release-assurance-relevant: true.
- Counsel-flag: false (no new legal question surfaced beyond `EVAL-2026-088`).

Two rows, filed together, form the eval-evidence view of MCDA for the current release window. Chapter 09 packages both into the review packet handed to `ai-evaluation-engineer`.

## Failure modes when populating the row

- **The report-title-and-nothing-else row.** A row with the report title and a link to the artefact but empty three-claims fields is not an evidence row — it is a bookmark. The analyst does not file it and call the work done.
- **The interpret-the-metric row.** The analyst quotes the aggregate number but does not carry through the threshold-decision rationale. Without the threshold call, the number is not evidence for or against release; the row is incomplete.
- **The one-row-many-versions row.** The analyst updates a single row across three system versions rather than filing a new row per material system change. The audit trail collapses. One row per report; new report → new row.
- **The absent-cross-artefact-linkage row.** The analyst files the row and does not update the linked register, impact-assessment, and regulatory-tracker rows. The evidence is siloed; downstream reads miss it.
- **The stale-row row.** The analyst never re-verifies the row after the initial filing. The last-verified date crosses the refresh cadence. The row silently transitions from evidence to claim. Chapter 10 covers the stale-row escalation.

## What to memorise

- **`EVAL-<year>-<sequence>` per report.** Never re-used; new report → new row.
- **The nineteen columns across six groups** — identity, system under evaluation, three load-bearing claims, cross-artefact references, provenance, status / review / cadence, governance-package fields.
- **Every row's inventory row ID is populated.** An eval of nothing is not evidence.
- **The residual-risk claim is quoted from the report.** The analyst does not paraphrase in a way that sharpens or softens the claim.
- **The threshold-decision rationale must cite a named threshold.** No threshold → escalate.
- **The cross-artefact linkage fields are populated.** A row that does not connect to the register, the impact-assessment, or the regulatory tracker is a filing-cabinet entry, not a governance record.

## Summary

The governance-record row is the analyst's tangible output for this module. Nineteen columns across six groups turn a read of an eval, RAG-triad, or red-team report into a versioned, cited, cross-referenced piece of evidence that a council, an auditor, and a release-assurance engineer can trust and act on. The row's three load-bearing claims — residual-risk, threshold-decision rationale, unresolved findings — quote the report; the provenance columns capture the exact configuration under which the claims hold; the cross-artefact columns wire the row into the register, the impact-assessment corpus, and the regulatory tracker. Chapters 06 and 07 turn to the public references — system cards and Responsible Scaling Policies — that populate a different subset of rows (report-type: *vendor-system-card* and *vendor-rsp-disclosure*) and inform the benchmarking chapter 08 covers.
