# Lab 01 — Quarterly Refresh Walk on a Drifted MCDA Eval-Row Set

**Duration:** 2 hours.
**Grounding chapters:** [02](../02-inspect-style-eval-report-anatomy.md), [03](../03-rag-triad-and-quality-eval-reports.md), [04](../04-red-team-engagement-reports.md), [05](../05-summarising-eval-evidence-into-a-governance-row.md), [09](../09-composing-and-handing-off-the-review-packet.md), [10](../10-delegation-boundary-and-escalation-patterns.md).
**Difficulty:** Core — exercises the *refresh cadence* and *row-level escalation* disciplines from chapters 05 / 09 / 10 against a pre-assembled MCDA row set that has gone stale in three specific, deliberate ways. The module's four exercises each drill authoring-from-scratch (exercise 01 drills row authoring on fresh reports, exercise 02 drills benchmark authoring, exercise 03 drills packet composition, exercise 04 drills triage against short vignettes). None of them asks the analyst to walk a *pre-filed row set across a cadence cycle* — the specific place where the chapter 05 status-field discipline, the chapter 09 pre-hand-off completeness check, and the chapter 10 four-class escalation protocol converge into the hour of work the analyst will do every quarter.

## Objective

Take a *fixed, pre-assembled* MCDA eval-row set — four rows filed in prior quarters with deliberately-induced drift — and run a quarterly refresh walk over it. For each row, compute staleness against the chapter 05 cadence, re-verify the columns against the source reports where the lab provides them, refresh the status / last-verified fields, and — for the rows where drift has crossed into an escalation trigger — author a chapter-10 escalation entry of the correct class. Close by projecting the escalation entries into the chapter-10 escalation register and updating an existing review-packet reference (`PACKET-2026-096`) with the refreshed row status so that a downstream `ai-evaluation-engineer` would see the current state.

The deliverable is two Markdown files in `~/aicg-labs/mod-107-lab-01/`:

- `row-refresh.md` — the walk log, one sub-section per row.
- `escalation-register.md` — the `ESC-<year>-<sequence>` entries authored from the walk, projected into the chapter 10 register shape.

A reviewer should be able to read both in fifteen minutes and see every row walked, every drift tagged, every escalation routed, and the packet reference updated.

## Prerequisites

- All ten chapters read; chapter 05's nineteen-column row schema, chapter 09's pre-hand-off completeness checklist, and chapter 10's four escalation classes fresh in memory.
- A Markdown editor; no Python or GRC-platform tooling required — the row set below is a Markdown-only stand-in for the records that would live in the GRC platform in production.
- Exercises 01 and 04 completed, or at minimum skimmed, so the row schema and the escalation-class triage are familiar. The row set below is written to the exercise-01 schema at the level of the columns a walker reads from.

## The fixed input — a deliberately-drifted MCDA row set

Use *exactly* this row set. Do not substitute identifiers, dates, model versions, or report titles, and do not pre-correct the drift — the drift is the point. Each row is reproduced only at the level of fields a quarterly-walker reads from. Treat the whole block as `pedagogic example — numbers and dates illustrative`.

### A. The eval rows as filed in prior quarters

```
EVAL-2026-088 — MCDA safety-eval, run 2026-07-14
  Report type:        safety-eval
  Author:             Internal Safety Eval Team
  Inventory row:      INV-2026-0088 (MCDA)
  System version:     Application v3.6; system prompt v1.7;
                      model anthropic/claude-3-5-sonnet-20241022
  Residual-risk:      Overall safe-answer rate 96.4% (above internal 95% threshold).
                      Protected-class-generalisation category 89.0%
                      (below category-specific 92% threshold); graded amber.
  Threshold rationale: Overall met; category-specific missed. Per internal
                      safety-eval-policy v2.4, amber grading requires follow-up
                      eval within 60 days.
  Unresolved findings: SE-2026-114 (protected-class-generalisation, Med, MCDA
                      product owner, closure 2026-09-14);
                      SE-2026-115 (judge-prompt calibration, Low,
                      Safety Eval Team, closure 2026-Q4).
  Solver:             single-turn, temperature=0.7, three-trial majority vote.
  Scorer:             LLM-as-judge (anthropic/claude-3-opus-20240229,
                      judge-prompt v2.1, IAA 0.83 on 50-sample calibration).
  Refresh cadence:    per system-prompt version change plus quarterly.
  Next-due:           2026-10-14.
  Last-verified:      2026-08-01.
  Row status:         evidence-current.
  Council-relevant:   true.
  Release-assurance-relevant: true.

EVAL-2026-091 — MCDA red-team engagement RT-2026-014, 2026-08-01 → 2026-08-12
  Report type:        red-team
  Author:             Internal red-team of 3 + 1 external evaluator
  Inventory row:      INV-2026-0088 (MCDA)
  System version:     Application v3.7; system prompt v1.7 (v1.8 draft
                      validated in-engagement);
                      model anthropic/claude-3-5-sonnet-20241022
  Residual-risk:      Protected-class-generalisation via analogy prompt closed
                      under system prompt v1.8. Competitor-disparagement via
                      indirect prompting and over-refusal on benign paraphrase
                      open with named owners.
  Threshold rationale: Per internal red-team-acceptance-policy v1.5, no High
                      may remain open at release; Medium must have named owner
                      and target closure within 30 days.
  Unresolved findings: RT-2026-014-002 (competitor-disparagement, Med, MCDA
                      product owner, closure 2026-09-11); RT-2026-014-003
                      (over-refusal, Med, MCDA product owner,
                      closure 2026-09-11); RT-2026-018 (prompt-injection via
                      retrieved-context, scheduled 2026-10).
  Solver:             manual multi-turn iterated 3 rounds; 3 internal
                      + 1 external evaluator.
  Scorer:             internal red-team severity rubric v1.5 (four-tier).
  Refresh cadence:    annually per system or per material change.
  Next-due:           2027-08-01 or upon next material change.
  Last-verified:      2026-08-15.
  Row status:         evidence-current.
  Council-relevant:   true.
  Release-assurance-relevant: true.
  Notes:              RT-2026-014-001 (protected-class via analogy) was
                      Severity High; mitigation under system prompt v1.8
                      was validated in round 3 of the engagement
                      (0/25 in retest, prior 2/25).

EVAL-2026-089 — MCDA-Benefits RAG-triad eval, run 2026-06-30
  Report type:        rag-triad-eval
  Author:             Internal Safety Eval Team
  Inventory row:      INV-2026-0311 (MCDA-Benefits)
  System version:     Application v2.4; retrieval index v2026-06-15;
                      embedding text-embedding-3-large;
                      generation openai/gpt-4o-2024-11-20;
                      system prompt v3.1.
  Residual-risk:      In-scope quality meets thresholds. Negative-query handling
                      materially below threshold (groundedness 0.71;
                      answer relevance 0.58); restricted-tier chunk leakage
                      single-instance finding.
  Threshold rationale: Per-metric thresholds: context relevance ≥ 0.80,
                      groundedness ≥ 0.90, answer relevance ≥ 0.85. In-scope
                      met; negative queries fail both groundedness and
                      answer relevance. Graded red on negative-query subset
                      pending mitigation.
  Unresolved findings: SE-2026-141 (restricted-tier chunk leakage,
                      Retrieval Platform, closure 2026-07-15);
                      SE-2026-142 (negative-query over-answering,
                      MCDA-Benefits product owner, mitigation plan due
                      2026-07-14; re-eval 2026-08-01).
  Solver:             top-5 cosine retrieval; generation temperature 0.2;
                      no tool use; guardrails on PII leakage.
  Scorer:             LLM-as-judge (openai/gpt-4o-2024-11-20 as judge,
                      judge-prompt v1.2, IAA 0.86 on 120-sample calibration).
  Refresh cadence:    per retrieval index refresh plus monthly.
  Next-due:           2026-07-30.
  Last-verified:      2026-07-05.
  Row status:         evidence-current.
  Council-relevant:   true.
  Release-assurance-relevant: true.

EVAL-2026-102 — vendor-system-card for anthropic/claude-3-5-sonnet-20241022
  Report type:        vendor-system-card
  Author:             Anthropic
  Inventory row(s):   INV-2026-0088 (MCDA)
  System version:     anthropic/claude-3-5-sonnet-20241022
  Residual-risk:      Vendor publishes safety-evaluation coverage across refusal
                      categories, bias assessments, and hallucination-under-
                      grounding; known-limitations catalogue is detailed.
  Threshold rationale: Vendor classifies model at the tier its paired RSP
                      disclosure (EVAL-2026-103) describes for ASL-2 obligations;
                      see paired row for current ASL definitions.
  Unresolved findings: Known limitations per vendor card §8 recorded verbatim
                      in row; vendor deployment-considerations per card §10
                      recorded in row's notes.
  Refresh cadence:    per vendor card revision or per model-version change.
  Next-due:           per vendor publication cadence (annual re-read at minimum).
  Last-verified:      2026-07-10.
  Row status:         evidence-current.
```

### B. The inventory and adjacent-artefact identifiers

```
INV-2026-0088    MCDA (marketing-copy draft assistant)
INV-2026-0311    MCDA-Benefits (benefits-copy RAG assistant for health benefits)
RSK-2026-0088-04 MCDA protected-class residual
RSK-2026-0088-07 MCDA over-refusal business-impact residual
RSK-2026-0311-02 MCDA-Benefits negative-query hallucination residual
IA-2026-0088     MCDA canonical impact assessment
IA-2026-0311     MCDA-Benefits canonical impact assessment
REG-2026-US-STATE-003  Colorado AI Act
REG-2026-US-STATE-005  NYC LL 144
CTRL-2026-042    MCDA release-gating control (pending mod-108)
PACKET-2026-096  MCDA v3.6 release-assurance packet (prior quarter,
                 sign-off-recorded with MCDA v3.6 shipped)
```

### C. What has changed in the quarter since the rows were filed

Treat today as **2026-11-14**. The following events are known to have occurred since the rows above were last verified; some are reflected in the rows above and some are *not*. The walker's job is to notice which is which.

1. **MCDA application** moved from v3.6 → v3.7 → v3.8. System prompt moved from v1.7 → v1.8 (in-engagement draft from `EVAL-2026-091` round 3) → v1.8.1 (minor hot-fix 2026-10-05 tightening the competitor-disparagement refusal). Model version remains `anthropic/claude-3-5-sonnet-20241022`.
2. **MCDA-Benefits retrieval index** was refreshed on 2026-09-01 and again on 2026-10-15. The embedding model and generation model are unchanged. System-prompt v3.1 is unchanged.
3. **Anthropic** has (as the lab's fictional scenario, consistent with chapter 06's *version-drift trap* language) published a successor model identifier `anthropic/claude-3-5-sonnet-20260301` with a paired vendor-card revision dated 2026-09-20. MCDA's deployment has *not* migrated to the new identifier as of 2026-11-14. <!-- needs-research: verify current Anthropic model identifiers and card revisions against the Anthropic model overview (https://www.anthropic.com/claude) and news page (https://www.anthropic.com/news) at the date of use; identifiers and card URLs change on the vendor's cadence. For the lab, the fictional successor is a pedagogic placeholder — the row drift applies regardless of the actual vendor publication state. -->
4. **MCDA red-team finding** `RT-2026-014-002` (competitor-disparagement, Medium) was reported mitigated under the 2026-10-05 system-prompt hot-fix. The hot-fix was deployed but the mitigation was *not* re-tested by the red-team before deployment. Red-team finding `RT-2026-014-003` (over-refusal, Medium) target-closure date has passed.
5. **Colorado AI Act** consumer-notice provisions have entered a new enforcement window (regulator-tracker row `REG-2026-US-STATE-003` was last verified after that window opened; the tracker row's own status reflects the new enforcement posture).
6. **`EVAL-2026-089` (MCDA-Benefits RAG-triad)** has *not* been re-run since the two index refreshes. Finding `SE-2026-141` (restricted-tier chunk leakage) is reported closed on 2026-07-15 per the row's own closure target; finding `SE-2026-142` (negative-query over-answering) re-eval scheduled for 2026-08-01 has *not* occurred — the re-eval was deferred twice without the deferral being logged in the row.

## Steps

### Step 1 — Scaffold the walk log (10 min)

Create the working folder and files.

```bash
mkdir -p ~/aicg-labs/mod-107-lab-01
cd ~/aicg-labs/mod-107-lab-01
touch row-refresh.md escalation-register.md
```

Open `row-refresh.md` and lay in the structure up front.

```markdown
# MCDA eval-row quarterly refresh — 2026-11-14

Walker:       <your-name>
Walk date:    2026-11-14
Row-set:      EVAL-2026-088, EVAL-2026-089, EVAL-2026-091, EVAL-2026-102
Cadence:      Quarterly per chapter 05 refresh-cadence discipline.

## Row-by-row refresh

### EVAL-2026-088 — MCDA safety-eval
### EVAL-2026-091 — MCDA red-team engagement
### EVAL-2026-089 — MCDA-Benefits RAG-triad eval
### EVAL-2026-102 — Anthropic Claude 3.5 Sonnet vendor-system-card

## Escalations authored from this walk

## Packet-reference update
  (PACKET-2026-096 — MCDA v3.6 release-assurance packet closure, prior quarter.
   Status transitions and cross-references recorded here.)

## Walk verdict
```

The four-section-plus-per-row scaffold is what the reviewer reads to confirm the walk ran; the per-row sub-sections carry the evidence.

### Step 2 — Compute each row's refresh verdict against the cadence (15 min)

For each of the four rows, compute days-stale against the walk date 2026-11-14, cross-check against the Section-C change list, and record a per-row verdict. Chapter 05's row-status vocabulary applies — *evidence-current* / *evidence-provisional* (deployed system drifted from evaluated system) / *evidence-stale* (report beyond its refresh cadence) / *escalated* (under-evidenced, mis-scoped, or stale per chapter 10).

Expected per-row verdict after this step — these drive what each later step does:

- `EVAL-2026-088` — *evidence-provisional* with *escalated* trigger. Reasons: (a) the evaluated system version is application v3.6 / system prompt v1.7, but the deployed system is application v3.8 / system prompt v1.8.1 — model version is unchanged, so the drift is *solver-regime drift* not *model-version drift*; (b) next-due 2026-10-14 has passed, so the row is also *evidence-stale*; (c) finding `SE-2026-114` target closure 2026-09-14 has passed without an update recorded on the row. Chapter 10 class: 2 (mis-scoped eval on system-prompt and application version drift, chained with a Class 3 stale on the passed next-due date). Record *drift catalogued; escalation to be filed in step 7*.
- `EVAL-2026-091` — *evidence-provisional* with *escalated* trigger. Reasons: (a) the engagement's in-engagement-validated mitigation was under system prompt v1.8; the hot-fix to v1.8.1 on 2026-10-05 was not re-tested by the red-team before deployment — per chapter 04, *mitigation-without-retest* is *proposed* not *validated*, and the row's status cannot silently promote the hot-fix to validated; (b) finding `RT-2026-014-003` target-closure 2026-09-11 has passed. Chapter 10 class: 1 (under-evidenced — the hot-fix's efficacy is claimed in the deployment but is not supported by evidence in the row; the status field cannot read *validated* without a re-test). Record *drift catalogued; escalation to be filed in step 7*.
- `EVAL-2026-089` — *evidence-stale* with *escalated* trigger. Reasons: (a) the next-due date 2026-07-30 has passed by over three months; (b) the retrieval index has been refreshed twice since the eval ran (chapter 03's *ignoring index freshness* failure mode); (c) finding `SE-2026-142` scheduled re-eval 2026-08-01 did not occur. Chapter 10 class: 3 (stale eval — index-version and system drift). Record *drift catalogued; escalation to be filed in step 7*.
- `EVAL-2026-102` — *evidence-provisional*. Reasons: (a) the vendor has published a successor model identifier `anthropic/claude-3-5-sonnet-20260301` with a paired card revision dated 2026-09-20; (b) MCDA's deployment has *not* migrated to the new identifier and remains on `anthropic/claude-3-5-sonnet-20241022`. Chapter 06's *version-drift trap* and chapter 10 Class-3 criteria both apply: the card for `-20241022` remains the applicable card for the deployed model, so the row is not stale for MCDA *today*; but the migration decision for MCDA is a known upcoming event that will transition the row to *evidence-stale* the moment the deployment moves. Record *drift catalogued; no escalation yet — planning note for the next packet and re-benchmark trigger set in the notes*.

Record the four per-row verdicts in the sub-sections of `row-refresh.md`.

### Step 3 — Refresh `EVAL-2026-088` (15 min)

Open the row's sub-section in `row-refresh.md` and record the refresh in three parts.

- **Column updates.** Record the before / after for the fields that change:
  - *System version*: `application v3.6; system prompt v1.7` → `application v3.6 → v3.8 drift noted; system prompt v1.7 → v1.8.1 drift noted; model anthropic/claude-3-5-sonnet-20241022 unchanged. Evaluated system is v3.6/v1.7; deployed system is v3.8/v1.8.1. Delta since deployment: material (system-prompt version change; application version drift of two increments).`
  - *Row status*: `evidence-current` → `evidence-provisional (deployed system drifted from evaluated system) + evidence-stale (next-due 2026-10-14 passed by 31 days)`.
  - *Last-verified*: 2026-08-01 → 2026-11-14.
  - *Verified-by*: current analyst.
  - *Notes*: append `Escalation ESC-2026-LAB01-01 open per chapter 10 Class 2 (mis-scoped — system-prompt and application version drift) and Class 3 (stale — next-due passed). Finding SE-2026-114 closure 2026-09-14 passed without row update; closure verification pending with MCDA product owner.`
- **Cross-artefact check.** Walk the related `RSK-2026-0088-04`, `IA-2026-0088`, `REG-2026-US-STATE-003`, and `REG-2026-US-STATE-005` references. Record whether each needs a change-note trigger in response to the drift catalogued here. For the lab: the Colorado AI Act consumer-notice provisions entering a new enforcement window (Section-C event 5) means the `REG-2026-US-STATE-003` linkage is itself refreshing; record that as a cross-artefact-change signal in the row's notes field and route to the regulatory-tracker owner — but do not author the tracker-row refresh in this lab (that is `mod-106` scope and belongs in the tracker walker's log, not here).
- **Packet reference.** The `PACKET-2026-096` reference does not carry forward — chapter 09's *packet is a per-release-decision artefact* discipline means the next release gate (MCDA v3.9 or v4.0, not in this lab) will get its own packet. Record *prior packet closed; row refresh triggers new benchmark-cycle work (chapter 08) and new packet work (chapter 09) on the next release gate — out of scope for this lab's refresh walk*.

### Step 4 — Refresh `EVAL-2026-091` (15 min)

Chapter 04's *mitigation-without-retest trap* is the load-bearing discipline here. The engagement validated a mitigation under system prompt v1.8 in a formal re-test round; the 2026-10-05 hot-fix to v1.8.1 was deployed but did not go through a re-test. The row's status fields must reflect this honestly.

- **Column updates.**
  - *System version*: `application v3.7; system prompt v1.7 (v1.8 draft validated in-engagement); model anthropic/claude-3-5-sonnet-20241022` → `application v3.7 → v3.8 drift noted; system prompt v1.8 → v1.8.1 (2026-10-05 hot-fix tightening competitor-disparagement refusal — hot-fix not re-tested by red-team before deployment); model unchanged.`
  - *Residual-risk*: keep the chapter 04 wording verbatim but append `*Hot-fix v1.8.1 (2026-10-05) applied to the competitor-disparagement category where finding RT-2026-014-002 was open; hot-fix was not re-tested by red-team pre-deployment — per chapter 04, this is a proposed-not-validated mitigation. Status of RT-2026-014-002 remains open on this row pending re-test.*` The row does not silently promote the hot-fix to a closed finding.
  - *Unresolved findings*: `RT-2026-014-002` status: *open — hot-fix proposed and deployed 2026-10-05, re-test not run*. `RT-2026-014-003` status: *open — target closure 2026-09-11 passed without row update; current closure expectation pending with MCDA product owner*.
  - *Row status*: `evidence-current` → `evidence-provisional (mitigation-without-retest on hot-fix) + escalated (ESC-2026-LAB01-02, Class 1)`.
  - *Last-verified / verified-by*: 2026-08-15 → 2026-11-14 / current analyst.
  - *Notes*: append `Escalation ESC-2026-LAB01-02 open per chapter 10 Class 1 (under-evidenced — the status of RT-2026-014-002 cannot read closed without a re-test round). Routed to ai-red-team-engineer and MCDA product owner; ai-evaluation-engineer copied.`

### Step 5 — Refresh `EVAL-2026-089` (15 min)

Chapter 03's *ignoring index freshness* failure mode is the load-bearing discipline. Two index refreshes since the eval ran means the eval's context-relevance and groundedness numbers describe a corpus that is no longer the deployed corpus.

- **Column updates.**
  - *System version*: `application v2.4; retrieval index v2026-06-15; embedding text-embedding-3-large; generation openai/gpt-4o-2024-11-20; system prompt v3.1.` → `application v2.4 unchanged; retrieval index v2026-06-15 → v2026-09-01 → v2026-10-15 (two refreshes without a re-run of the RAG-triad eval); embedding and generation models unchanged; system prompt v3.1 unchanged.`
  - *Row status*: `evidence-current` → `evidence-stale (next-due 2026-07-30 passed; index refreshed twice) + escalated (ESC-2026-LAB01-03, Class 3)`.
  - *Last-verified / verified-by*: 2026-07-05 → 2026-11-14 / current analyst.
  - *Unresolved findings*: `SE-2026-141` status: *closed as of 2026-07-15 per prior-quarter report; closure confirmed against Retrieval Platform team's log*. `SE-2026-142` status: *open — scheduled re-eval 2026-08-01 deferred twice without row update; current re-eval expectation pending*.
  - *Notes*: append `Escalation ESC-2026-LAB01-03 open per chapter 10 Class 3 (stale — next-due 2026-07-30 passed; retrieval index refreshed twice since eval). Routed to ai-evaluation-engineer (to schedule refresh) and MCDA-Benefits product owner (to decide whether to accept interim risk or gate deployment until refresh completes).`

### Step 6 — Refresh `EVAL-2026-102` (10 min)

Chapter 06's *version-drift trap* and the *vendor-rows-come-in-pairs* discipline apply. Today, the row's vendor card is still the applicable card for the deployed model. But the vendor has published a successor identifier with a paired revision; the row is not stale *for the deployed system today* but carries a *planning note* for the imminent migration.

- **Column updates.**
  - *Row status*: `evidence-current` → `evidence-provisional (vendor has published successor identifier anthropic/claude-3-5-sonnet-20260301 with paired card revision dated 2026-09-20; MCDA deployment has not migrated as of 2026-11-14; row is applicable for the currently-deployed identifier and will transition to evidence-stale upon migration)`.
  - *Last-verified / verified-by*: 2026-07-10 → 2026-11-14 / current analyst.
  - *Notes*: append `Planning note: migration to anthropic/claude-3-5-sonnet-20260301 is anticipated per MCDA roadmap; on migration, this row transitions to evidence-stale and a new vendor-system-card row (EVAL-<year>-<sequence>) is filed for the successor identifier, with a new paired vendor-rsp-disclosure row if the RSP has also revised. A new benchmark row (BENCH-<year>-<sequence>) will be required per chapter 08's benchmarks-revise discipline. Ingest the successor card revision into the row-set snapshot (per chapter 09's vendor-artefact snapshot discipline) when the migration lands; archive the current card version alongside for continuity.`
  - *Next-due*: per vendor publication cadence (annual re-read at minimum) → `per vendor publication cadence or on MCDA migration to anthropic/claude-3-5-sonnet-20260301, whichever is sooner`.

No chapter 10 escalation is authored from this row today. The row is accurately characterised as *evidence-provisional* with a planning note; the migration will trigger the next row-set refresh and benchmark-cycle work.

### Step 7 — Author the three escalation entries (20 min)

Open `escalation-register.md`. For each of `ESC-2026-LAB01-01`, `ESC-2026-LAB01-02`, and `ESC-2026-LAB01-03`, author the chapter-10 escalation entry using the per-class template verbatim.

- **`ESC-2026-LAB01-01` — Class 2 mis-scoped eval (chained with Class 3 stale) on `EVAL-2026-088`.** Template fields:
  - *Scope as reported.* *Application v3.6; system prompt v1.7; model anthropic/claude-3-5-sonnet-20241022; single-turn, temperature=0.7, three-trial majority; harm suite v3.2.*
  - *Scope required for the deployed system.* Application v3.8; system prompt v1.8.1; otherwise unchanged.
  - *Divergence.* System-prompt version drift (v1.7 → v1.8.1 — the hot-fix changes competitor-disparagement refusal behaviour, which overlaps the eval's categories); application version drift of two increments (v3.6 → v3.8).
  - *Options.* (a) Re-run `EVAL-2026-088` against the deployed configuration before the next release gate; (b) narrow deployment to v3.6 / v1.7 pending re-eval (likely infeasible given hot-fix is already live); (c) accept interim divergence with a documented risk-treatment note from the MCDA product owner and schedule re-eval within 60 days per chapter 05 safety-eval-policy v2.4 amber-grading cadence.
  - *Route.* Safety Eval Team owner (eval owner); MCDA product owner (accountable role). `ai-evaluation-engineer` copied.
  - *Requested resolution date.* 2026-11-28.
  - *Impact on packet.* `PACKET-2026-096` is closed; the next packet (MCDA v3.9 or v4.0 release) must cite this refreshed row with the drift noted.
- **`ESC-2026-LAB01-02` — Class 1 under-evidenced claim on `EVAL-2026-091`.** Template fields:
  - *Row.* `EVAL-2026-091` (MCDA red-team engagement RT-2026-014).
  - *Claim.* Deployment-side narrative treats the 2026-10-05 system-prompt v1.8.1 hot-fix as closing finding `RT-2026-014-002` (competitor-disparagement, Medium).
  - *Evidence gap.* The hot-fix was deployed but not re-tested by the red-team; chapter 04's *mitigation-without-retest* discipline says a mitigation without a re-test round is *proposed*, not *validated*. The finding's status remains *open* on the row until a re-test round is run.
  - *Question to eval owner (`ai-red-team-engineer`).* Please schedule a short re-test round covering the competitor-disparagement category under system prompt v1.8.1; recommended coverage: the same 25-sample subset used in `RT-2026-014` round 3 for direct comparability, plus the hot-fix's intended-blocked patterns. Alternatively, confirm that a lightweight check satisfies the chapter 04 validation discipline.
  - *Route.* `ai-red-team-engineer` (eval owner); MCDA product owner (accountable role). `ai-evaluation-engineer` copied.
  - *Requested resolution date.* 2026-11-28.
  - *Impact on packet.* `PACKET-2026-096` is closed; the next packet must cite the row's updated status (`RT-2026-014-002` open pending re-test) and include this escalation inline.
- **`ESC-2026-LAB01-03` — Class 3 stale eval on `EVAL-2026-089`.** Template fields:
  - *Row.* `EVAL-2026-089` (MCDA-Benefits RAG-triad eval).
  - *Last-verified.* 2026-07-05.
  - *Refresh cadence.* Per retrieval index refresh plus monthly (per chapter 03 RAG-eval cadence).
  - *Staleness trigger.* Next-due 2026-07-30 passed by over three months; retrieval index refreshed on 2026-09-01 and 2026-10-15 without a re-run of the RAG-triad eval; finding `SE-2026-142` scheduled re-eval 2026-08-01 deferred twice without row update.
  - *Impact on residual-risk claim.* The eval's context-relevance, groundedness, and answer-relevance numbers describe a corpus that is no longer the deployed corpus; the negative-query over-answering residual (`SE-2026-142`) cannot be re-characterised without a fresh run.
  - *Refresh options.* (a) Re-run the RAG-triad eval against the 2026-10-15 retrieval index within the next monthly cycle; (b) accept documented interim risk through the next cycle with a risk-treatment note from the MCDA-Benefits product owner; (c) narrow the deployment scope until the re-run completes (likely infeasible for a benefits-information RAG with live users).
  - *Route.* `ai-evaluation-engineer` (to schedule the refresh); MCDA-Benefits product owner (to decide interim-risk posture). Copy to `head-of-ai-governance` if this is the second consecutive quarter the row has entered Class 3 — chapter 10's recurring-pattern discipline treats repeated Class-3 escalations on RAG-triad evals as a cadence-policy signal.
  - *Requested resolution date.* 2026-11-28 (re-eval scheduling decision); 2026-12-15 (re-eval completion).
  - *Impact on packet.* `PACKET-2026-096` does not cover MCDA-Benefits; the next MCDA-Benefits packet cannot be handed off with this row in *escalated* status unless the escalation entry is inline per chapter 09's *hand off with the entry inline, do not delay* discipline.

### Step 8 — Fill the packet-reference update section (10 min)

Open the `## Packet-reference update` section in `row-refresh.md` and record one short block per packet-reference consequence.

- **`PACKET-2026-096` (MCDA v3.6 release-assurance packet, prior quarter, closed).** Status: *sign-off-recorded with MCDA v3.6 shipped* — no changes to the packet itself. However, every row cited by the packet has now moved from `evidence-current` to `evidence-provisional` or `evidence-stale`. Per chapter 09's *superseding vs revising* discipline, no new version of `PACKET-2026-096` is cut (the release gate closed); the next MCDA release gate (v3.9 or v4.0) will trigger a new packet, which will cite the refreshed row state from this walk.
- **Next-packet trigger.** The next MCDA release gate requires: (a) resolution of `ESC-2026-LAB01-01` (Class 2 mis-scope); (b) resolution of `ESC-2026-LAB01-02` (Class 1 under-evidenced on hot-fix re-test); (c) a decision on `EVAL-2026-102` migration timing to the successor vendor identifier (which, when it lands, will trigger a new benchmark cycle per chapter 08). Author a one-paragraph note in this section so a future analyst picking up the next packet knows what state the row-set left this quarter in.

### Step 9 — Project the escalation register (10 min)

Open `escalation-register.md` and, below the three escalation entries authored in step 7, project them into the chapter-10 escalation-register shape.

```markdown
## Escalation register — MCDA row-set, 2026-11-14 walk

| ID | Class | Source row | Filed | Route | Status | Resolution | Impact on packet |
|---|---|---|---|---|---|---|---|
| ESC-2026-LAB01-01 | 2 | EVAL-2026-088 | 2026-11-14 | Safety Eval Team owner; MCDA product owner (ai-eval-engineer cc) | open — awaiting owner response | — | prior packet closed; next MCDA packet depends on resolution |
| ESC-2026-LAB01-02 | 1 | EVAL-2026-091 | 2026-11-14 | ai-red-team-engineer; MCDA product owner (ai-eval-engineer cc) | open — awaiting owner response | — | prior packet closed; next MCDA packet depends on resolution |
| ESC-2026-LAB01-03 | 3 | EVAL-2026-089 | 2026-11-14 | ai-evaluation-engineer; MCDA-Benefits product owner | open — awaiting owner response | — | next MCDA-Benefits packet must cite entry inline |
```

The escalation register is the first-class artefact chapter 10 names. Auditors read it to check the enterprise's response to identified evidence gaps.

### Step 10 — Fill the walk-verdict section (10 min)

Open the `## Walk verdict` section at the bottom of `row-refresh.md`. Three or four sentences:

- *Walk ran on 2026-11-14 across four rows; four last-verified dates refreshed; one row (`EVAL-2026-102`) is evidence-provisional with a planning note and no escalation; three rows (`EVAL-2026-088`, `EVAL-2026-091`, `EVAL-2026-089`) have transitioned to evidence-provisional or evidence-stale and escalated with `ESC-2026-LAB01-01`, `-02`, and `-03` routed per chapter 10. Prior packet `PACKET-2026-096` is closed and not re-cut. Next-cadence dates recorded on the three escalations (requested resolution 2026-11-28 across the three); a follow-up quarterly refresh on this row-set is due 2027-02-14, or on any of (a) migration of MCDA to `anthropic/claude-3-5-sonnet-20260301`, (b) a new MCDA release gate, (c) a new MCDA-Benefits release gate, whichever is sooner. No Class 4 escalation was warranted on this walk; the three Class 1/2/3 escalations are all in-scope analyst-tier work and resolvable within the release cadence.*

### Step 11 — Self-check against the pre-hand-off completeness checklist (5 min)

Chapter 09's eleven-check completeness list is designed for a review packet; the subset relevant to a refresh walk is these four. Walk the walk-log against them before closing:

1. **Every cited row has a stable identifier, a source-artefact link reference (even if omitted from this lab's compressed fixture), and a last-verified date within its refresh cadence.** Confirm pass / fail per row.
2. **No cited row's `row status` is *evidence-stale* or *escalated* without being explicitly acknowledged in the walk log.** The three escalated rows are each named in `## Escalations authored from this walk` and in `escalation-register.md`. Confirm pass.
3. **The escalation hooks section lists every escalation in flight.** Three escalation IDs listed; register projection populated. Confirm pass.
4. **No fabricated numbers, vendor identifiers, or regulator claims.** The pedagogic placeholders are tagged as such; the fictional successor Anthropic identifier is marked with the chapter 06 needs-research pattern. Confirm pass.

Record the four checks at the bottom of `row-refresh.md` as a short `## Pre-close completeness check` block.

## Expected output

Two Markdown files in `~/aicg-labs/mod-107-lab-01/`:

- `row-refresh.md` — one walk log with (a) four per-row sub-sections each recording the pre-walk state, the staleness verdict from step 2, the column updates from steps 3–6, and any cross-artefact-change signal; (b) an `## Escalations authored from this walk` section naming the three escalation IDs with one-line summaries each; (c) a `## Packet-reference update` section; (d) a `## Walk verdict` paragraph; (e) a `## Pre-close completeness check` block.
- `escalation-register.md` — three full chapter-10 escalation entries (Class 2, Class 1, Class 3) using the per-class templates verbatim, plus the chapter-10 escalation-register table projection beneath.

Total length: roughly 1,500–2,500 words across both files. A reviewer should be able to read both in fifteen minutes and see every row walked, every drift tagged, every escalation routed, and the register populated.

## Checkpoint

A mentor, peer, or self-review walk. Answer honestly:

1. **Did every row get walked, including `EVAL-2026-102` where no escalation was warranted?** Chapter 05's refresh-cadence discipline reads every row on the quarterly walk; the row with no material change still gets a last-verified refresh and a planning note.
2. **Does `EVAL-2026-091`'s `RT-2026-014-002` status read *open — hot-fix proposed and deployed 2026-10-05, re-test not run*, not *closed*?** Chapter 04's *mitigation-without-retest trap* is the load-bearing discipline — a walk that silently promotes the hot-fix to closed is the exact chapter-10 *version-drift silence* failure mode inverted.
3. **Does `EVAL-2026-089`'s refresh route both to `ai-evaluation-engineer` and to the MCDA-Benefits product owner?** Chapter 10 Class 3 routing is explicit — the eval owner schedules the refresh, the product owner decides the interim-risk posture. Routing only to one is partial.
4. **Does `EVAL-2026-102`'s notes field record the planning signal for the imminent migration, the benchmark-cycle trigger, and the row-transition expectation?** Chapter 06's *version-drift trap* and chapter 08's *benchmarks revise* discipline both apply.
5. **Is the escalation register populated with every escalation and no fabricated ones?** Three entries, three source rows, three routes. A register with four entries is manufacturing an escalation; a register with two is missing one.
6. **Did any row get silently absorbed as *evidence-current* when it should have moved to *evidence-provisional* / *evidence-stale* / *escalated*?** Chapter 10's four silence failure modes (silent-launder, version-drift silence, stale-refresh silence, packet-shipped-anyway silence) are what this check tests for.

If any of the six is "no", revise *that artefact* before considering the lab done.

## Why this is a lab, not an exercise

The module's four exercises each drill authoring-from-scratch — exercise 01 on fresh eval reports, exercise 02 on vendor cards and RSPs, exercise 03 on a packet, exercise 04 on short triage vignettes. None of them asks the analyst to walk a *pre-filed row set across a cadence cycle*, which is the specific place where the chapter 05 status-field discipline, the chapter 09 pre-hand-off completeness check, and the chapter 10 four-class escalation protocol all converge into the hour of work the analyst will do every quarter. This lab is that convergence. The failure mode it prevents is the analyst who can author each artefact in isolation but has never once walked a row set that had gone stale through a quarter, caught the drift, tagged the escalation class correctly, routed each entry, and closed the loop into the register.
