# The Control-Status Report for Internal Audit

## Why this chapter

Chapter 02 fixed the cycle and the evidence-artefact shape. This chapter fixes the *deliverable* the cycle produces: the control-status report an internal auditor picks up cold, reads front-to-back, and uses as the primary input to the periodic assurance opinion on operating effectiveness of the enterprise's AI controls.

Two design constraints govern the report shape. First, internal audit is not the analyst — the reader has not seen the pulls, does not know the owners by name, and needs the report to stand on its own. Second, the report is a governance artefact — signed, dated, and archived, with a stable identifier. A version stored in an email attachment or a chat thread is not a report.

The row schema and the report sections below are the analyst-tier defaults. `senior-ai-governance-architect` may extend either for a specific enterprise; the analyst should not silently trim either.

## The `CTL-<year>-<sequence>-<test-N>` row

Each control tested in the period contributes one row per test. A control tested twice in the period has two rows; a control not tested in the period has one row with the *not-tested-in-period* verdict. The row is the atomic unit of the report; the report sections aggregate rows.

Analyst-tier row schema (twenty columns):

| # | Column | Content |
|---|---|---|
| 1 | Test ID | `CTL-<year>-<sequence>-<test-N>` — the control identifier concatenated with the test-number-in-period |
| 2 | Control ID | `CTL-<year>-<sequence>` — from the master library |
| 3 | Control statement | The exact wording from the master library; not paraphrased |
| 4 | Applicable systems | Comma-separated `INV-<year>-<sequence>` identifiers from `mod-102`; or *enterprise-wide* if the control applies to every system |
| 5 | Owner | Named person or team from the master library |
| 6 | Cadence | The library-set cadence (quarterly / half-yearly / annual / on-release / on-change) |
| 7 | Test-in-period date | The date the analyst ran this test |
| 8 | Verdict | One of: *pass*, *fail*, *deviation*, *not-tested-in-period* |
| 9 | Evidence class expected | From the master library |
| 10 | Evidence class delivered | From the pulled artefact; annotated *downgrade* if weaker than expected |
| 11 | Evidence artefact IDs | Comma-separated `EV-<year>-<sequence>` identifiers attached to this test |
| 12 | Stale-evidence flags | Which of the four rules tripped, if any: *cadence-window*, *config-change*, *model-version-change*, *reg-obligation-change*, *none* |
| 13 | Prior-period verdict | Verdict of the immediately preceding test on the same control |
| 14 | Trend | *improved*, *unchanged*, *degraded* — computed from prior-period |
| 15 | Follow-up action | Named action + owner + due date, or *none* |
| 16 | Escalation class | If escalated: one of the four classes in chapter 09; else *none* |
| 17 | Regulatory obligations satisfied | `REG-<year>-<sequence>` identifiers from `mod-106` |
| 18 | Framework crosswalk | ISO/IEC 42001 clause(s), NIST AI RMF sub-category(ies), EU AI Act article(s), SR 11-7 pillar(s), internal-policy reference(s) — from chapter 07 |
| 19 | Analyst note | One or two sentences — anomalies, downgrade rationale, sample-rule caveats, unusual context |
| 20 | Analyst | The analyst who ran this test |

Nothing exotic — the row is the pulled evidence plus the interpretation plus the crosswalk pointer plus the follow-up. Internal audit reads the whole row when a rollup number looks wrong.

## The verdict language

The four verdicts read the same way every time. The analyst does not soften them.

- **Pass.** Evidence in the expected class, within the cadence window, consistent with the control statement, source-linked and content-pinned, produced by the named owner. No stale-evidence flag tripped. The control operated in the period as designed.
- **Fail.** Evidence missing, or evidence present but inconsistent with the control statement (a config that does not match the stated threshold, a log sample that shows the guardrail did not fire on inputs where the statement says it should have, a sign-off record that names the wrong signer, an eval-report link that resolves to a report with a residual-risk claim over threshold). The control did not operate in the period as designed. A follow-up action is mandatory.
- **Deviation.** Evidence present but produced or shaped differently than the control statement expects — a downgraded evidence class, a wider-than-expected sampling rule, a sign-off obtained after the deadline named in the statement, a control operated using a compensating control instead of the primary. The control operated with a caveat; internal audit reads *deviation* as *not clean-pass, needs review*. A follow-up action is mandatory.
- **Not-tested-in-period.** The control was out of scope for the period per the cadence and no on-change trigger fired. The row records the reason for out-of-scope and the next scheduled test. Internal audit reads *not-tested-in-period* as *deferred, not failed*.

The analyst does not invent a fifth verdict. A "*mostly-pass*", "*pass with reservations*", or "*pending*" verdict is a fail or a deviation with a follow-up; language-softening is the failure mode internal audit reads as *analyst under-reported*.

## The report sections

The report is a Markdown or Word document (per enterprise convention) with a stable identifier — `CSR-<year>-Q<n>` for a quarterly report, `CSR-<year>-H<n>` for half-yearly, `CSR-<year>` for annual. Every section below is present; missing sections read as *not run*, not *not needed*.

- **§0 Report header.** Report identifier, period covered, date issued, analyst author, `senior-ai-governance-architect` reviewer, distribution list. A report with a distribution list that does not include `internal-audit` is not a control-status report.
- **§1 Executive summary.** One page. The four verdict counts (pass / fail / deviation / not-tested-in-period), the top three findings, the top three escalations, and the trend against the prior period. No new information appears here; the summary is a projection of §2–§7.
- **§2 Scope.** The subset of the master control library tested in this period, per the scoping rule from chapter 02. Lists the controls in scope with their `CTL-<year>-<sequence>` identifier, statement, owner, and cadence. A reader must be able to see immediately which controls were and were not touched.
- **§3 Verdict rollup.** The full row set from chapter 03's §"The `CTL-…-<test-N>` row" grouped by verdict. Filterable by inventory-tier and by regulatory obligation. Internal audit spends most of their reading time here.
- **§4 Findings.** The failed and deviation rows, one per finding, with the finding statement, the evidence gap, the follow-up action, the owner, and the due date. Ordered by severity, then by risk-tier of the affected system.
- **§5 Escalations.** The rows escalated to `senior-ai-governance-architect` per the four classes in chapter 09. Each escalation lists the class, the rationale, the requested action, and the target resolution date. The escalation register outside this report tracks the roll-up over time; this section is the current-period snapshot.
- **§6 Stale-evidence roll-up.** Which of the four stale-evidence flag rules tripped on which controls, with the resulting re-test date. Includes the controls that passed but whose evidence went stale between test and report-issuance date.
- **§7 Delegation-boundary notes.** Controls where the analyst hit the delegation boundary — security-linked routing to `ai-infra-security` (chapters 04 and 05), library-level fixes routed to `senior-ai-governance-architect` (chapter 09), external-audit-scoped items excluded from the report (chapter 08). Named here so internal audit knows what was *out of scope by design* rather than *missed*.
- **§8 Trend against prior period.** The verdict-count delta, the top improving controls, the top degrading controls, and the *new-this-period* control set (controls added to the library since last report). The trend section makes the periodic reads compose into a picture.
- **§9 Appendix — evidence catalogue.** The full `EV-<year>-<sequence>` set attached in this period with source links and pull dates. Internal audit spot-checks by clicking through here.

The report is a document, not a dashboard. Dashboards live in the GRC platform and are useful for the analyst mid-cycle; the periodic report is what internal audit archives as the point-in-time record.

## Analyst-tier language on operating effectiveness

Internal audit's job is to issue an opinion on *operating effectiveness*. The analyst-tier language that supports that opinion — without over-claiming — is limited to what the row shape can substantiate.

- **The analyst writes.** *"Tested with expected evidence class; passed; no stale-evidence flag tripped."* — the maximal claim the row supports.
- **The analyst does not write.** *"Operating effectively."* — that is the auditor's opinion, not an analyst input. The analyst supplies the evidence; internal audit forms the opinion.
- **The analyst writes.** *"Tested with downgraded evidence class (expected config export; delivered interview note). Follow-up filed to `senior-ai-governance-architect` to redesign the control toward a produceable class."* — accurate, useful, and honest about the limit.
- **The analyst does not write.** *"Control operates in principle."* — a rhetorical hedge that does not resolve to *pass*, *fail*, *deviation*, or *not-tested-in-period* is a report-formatting failure, not a fifth verdict.
- **The analyst writes.** *"Prior-period verdict was fail; follow-up action was completed on \[date\]; current-period verdict is pass; trend is improved."* — the trend column made discoverable to the reader.
- **The analyst does not write.** *"Now working correctly."* — dropped the reference to the follow-up completion date and to the prior-period test that anchored the improvement.

The language is boring on purpose. Interpretive prose is where analyst reports drift into over- or under-claiming; the row schema and the verdict language keep the report anchored.

## The hand-off to `senior-ai-governance-architect`

Every report has a *review-before-issue* step with `senior-ai-governance-architect`. The purpose is not sign-off on the verdicts — the analyst owns those. The purpose is to review the *library-level items* the report surfaces so the library changes are queued before the report reaches internal audit.

The hand-off carries:

- The full report draft.
- The escalation-class roll-up from §5.
- A short library-change list: controls that repeatedly deviate for structural reasons (evidence class not produceable, statement ambiguous, owner unassigned, cadence unrealistic); controls new-since-last-period that need onboarding; controls whose crosswalk to `mod-106` obligations has drifted.
- The proposed report-issuance date and distribution list.

`senior-ai-governance-architect` returns:

- Comment on library-change list (accept / defer / redirect).
- Any wording adjustments the report needs before issuance.
- Confirmation of the distribution list.

The report is then issued. The library-change items ride the `senior-ai-governance-architect`-owned change-management workflow; the analyst does not need to close them before issuance.

## The hand-off to `internal-audit`

The analyst issues the report to the distribution list on the enterprise's convention (email, GRC-platform notification, ticket). The hand-off includes:

- The report itself, stored at a stable location.
- A short note listing the top three findings and the top three escalations, so the internal auditor knows where to look first.
- An offer of a walkthrough — a meeting where the analyst walks the report section by section, answers questions, and takes back any additional evidence requests.

The auditor's response is *not* the analyst's to write. If internal audit issues an opinion the analyst disagrees with, the analyst records the disagreement in the escalation register and raises it to `head-of-ai-governance` per the class in chapter 09; the analyst does not amend the report to align with the opinion.

## Worked-example row

An illustrative row (values indicative, not from a real system):

- **Test ID.** `CTL-2026-0341-Q2`
- **Control ID.** `CTL-2026-0341`
- **Control statement.** *"For every customer-facing endpoint, the input length is capped at 8000 tokens; the jailbreak-classifier fires and returns the refusal message on prompts scoring ≥ 0.85; the human-review queue is invoked when the classifier score is between 0.6 and 0.85."*
- **Applicable systems.** `INV-2026-0088` (MCDA), `INV-2026-0091` (support-chat-copilot), `INV-2026-0104` (contract-review-assistant).
- **Owner.** ML platform team, on-call rota, `ml-platform-lead@` as escalation.
- **Cadence.** Quarterly, plus on-change.
- **Test-in-period date.** 2026-05-14.
- **Verdict.** *deviation*.
- **Evidence class expected.** config export + log sample.
- **Evidence class delivered.** config export + log sample. Log sample downgraded on `INV-2026-0104` — the platform's sampling could not produce the *should-have-fired-but-did-not* subset. Delivered class is *log sample with sampling caveat*.
- **Evidence artefact IDs.** `EV-2026-0812`, `EV-2026-0813`, `EV-2026-0814`.
- **Stale-evidence flags.** *config-change* — the system prompt on `INV-2026-0091` changed 2026-05-10; the previous quarter's config export is invalid. This quarter's export re-baselines.
- **Prior-period verdict.** *pass*.
- **Trend.** *degraded*.
- **Follow-up action.** Escalate log-sample sampling limitation on `INV-2026-0104` to `senior-ai-governance-architect` for library-level fix; owner `senior-ai-governance-architect`; due 2026-06-14. Interim: annotate control record with sampling caveat.
- **Escalation class.** *library-design-fix-needed* (chapter 09).
- **Regulatory obligations satisfied.** `REG-2026-0044` (EU AI Act Article 15 — accuracy, robustness, cybersecurity, jailbreak-robustness subset), `REG-2026-0052` (internal responsible-AI policy, prompt-injection controls).
- **Framework crosswalk.** ISO/IEC 42001 — Annex A "*Data quality*" and "*System-life-cycle*" control families (specific control identifiers `<!-- needs-research: verify Annex A identifiers against the current 42001 text -->`); NIST AI RMF — MEASURE 2.7, MANAGE 4.1; EU AI Act — Article 15; SR 11-7 — Pillar 1 (development), Pillar 3 (governance); internal policy — `POL-2026-0018` §4.
- **Analyst note.** Config-change flag tripped on `INV-2026-0091` between last quarter and this one — re-baseline complete; sampling caveat on `INV-2026-0104` is a repeating theme across three log-sample controls, worth a library-level review.
- **Analyst.** `firstname lastname`.

The row reads like a small case file. That is on purpose: internal audit reads twenty of these in a quarter, and a row that skims well saves everyone time.

## Common failure modes

The report failures internal audit calls out most.

- **Missing rows.** Controls in the scope list (§2) with no corresponding row in the verdict rollup (§3). Reads as *analyst deferred the test and did not disclose it*. Fix: every scope-listed control has a row, even if the row's verdict is *not-tested-in-period*.
- **Verdict-language drift.** *pass with reservations*, *observed*, *satisfactory*. Reads as *analyst avoiding the honest verdict*. Fix: the four-verdict discipline.
- **Findings without follow-ups.** A row with verdict *fail* but no follow-up action, owner, or due date. Reads as *analyst logged the failure and moved on*. Fix: every fail / deviation row has a follow-up.
- **Executive summary that adds information.** A top-three-finding in the summary that is not present in §4. Reads as *analyst rewrote the finding for the summary*. Fix: the summary projects; it does not author.
- **Stale-evidence rollup that under-reports.** Section §6 shows fewer stale flags than the verdict rollup mentions. Fix: automated compare between §3 and §6 at report-composition time.
- **Trend column not populated.** Column 14 blank for controls that had a prior-period test. Fix: pre-compute from the GRC platform's history before opening the row.

Each of these is a report-quality failure, not a control-quality failure. Internal audit will surface them the same way; save the extra loop by catching them at the pre-issuance review.

## What to memorise

- **The row is the atomic unit** — twenty columns per test; nothing softened; every fail / deviation carries a follow-up.
- **The verdict language is four words.** Anything else is a report-formatting failure.
- **The report has nine sections.** All present; the executive summary projects; the appendix carries the evidence catalogue.
- **The analyst does not write "operating effectively."** That is internal audit's opinion; the analyst supplies the substantiating rows.
- **The report is issued through a review with `senior-ai-governance-architect`.** Library-level items get queued; report goes to internal audit unchanged.
- **A report is a document, not a dashboard.** Stable identifier, archived, on the distribution list every period.

## Summary

The control-status report is the analyst's headline deliverable for this module. Each control tested in the period contributes one row per test; the row is a twenty-column record with the pulled evidence, the four-word verdict, the stale-evidence flags, the trend against the prior period, the follow-up action, and the crosswalk pointer. The report has nine sections — header, executive summary, scope, verdict rollup, findings, escalations, stale-evidence roll-up, delegation-boundary notes, trend, and evidence catalogue — and is issued after a pre-issuance review with `senior-ai-governance-architect`. The analyst's language stays boring on purpose: *pass*, *fail*, *deviation*, *not-tested-in-period*, and no rhetorical softeners. Internal audit reads the report as the primary input to the periodic operating-effectiveness opinion; the analyst supplies the rows, internal audit issues the opinion. Chapters 04 and 05 fix the security-tagging convention that makes the routing-to-`ai-infra-security` visible in the report; chapters 06–08 fix the vendor-intake and crosswalk artefacts that the report references.
