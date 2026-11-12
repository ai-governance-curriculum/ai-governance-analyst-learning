# Lab 02 — Benchmark Re-Run on a Vendor RSP Revision

**Duration:** 90 minutes.
**Grounding chapters:** [06](../06-reading-public-system-cards.md), [07](../07-responsible-scaling-policies-and-preparedness-frameworks.md), [08](../08-benchmarking-internal-artifacts-against-public-references.md), [10](../10-delegation-boundary-and-escalation-patterns.md).
**Difficulty:** Core — exercises the *benchmark revises* discipline chapter 08 fixed and the *version-in-flight trap* chapter 07 called out, against a pre-assembled `BENCH-<year>-<sequence>` row from a prior quarter and a newly-published vendor RSP revision. Exercise 02 drills benchmark authoring from scratch against the current vendor artefacts; this lab drills the complementary discipline of re-benchmarking an *already-filed* row when the vendor's framework version has revised in a way that changes an axis outcome.

## Objective

Take the pre-assembled `BENCH-2026-014` row (filed 2026-08-25 against Anthropic's Claude 3.5 Sonnet system card and RSP v2026-07, as referenced in chapter 08's worked example) and a *new* (fictional, for the lab) RSP revision `v2026-10` that tightens one of the tracked-category thresholds. Re-walk the four axes against the new RSP; identify which gap entries in the prior row are unchanged, which have changed in severity or owner, and which are new; refresh the `BENCH-2026-014` row and update the escalation register where a new Class-2 threshold-alignment gap has appeared.

The deliverable is a single Markdown file in `~/aicg-labs/mod-107-lab-02/`:

- `bench-refresh.md` — the re-benchmark walk, the refreshed benchmark row, an updated gap list, one Class-2 escalation entry authored from the new threshold-alignment gap, and a short packet-reference update for the next MCDA release gate.

A reviewer should be able to read it in ten minutes and see the four axes re-walked, the one new gap identified and routed, and the row's status moved from *evidence-current* to *evidence-provisional (vendor revised)* — not silently refreshed as if the prior gap list still applied.

## Prerequisites

- Chapters 06, 07, 08, and 10 read; chapter 08's four axes, chapter 07's *version-in-flight trap*, and chapter 10 Class 2's template fresh in memory.
- A Markdown editor; no code or notebook tooling required.
- Exercise 02 completed, or at minimum skimmed, so the benchmark row schema and the *scorecard-vs-gap-list* discipline are familiar.
- Chapter 08's MCDA worked example re-read as the reference shape — the fixture below is a compressed version of that same row, consistent with the illustrative MCDA chain in chapters 02–05.

## The fixed input

Use *exactly* the fixture below. The RSP revision is a pedagogic placeholder — the specific threshold-tightening is chosen to produce one clear Axis-2 gap. Treat the whole block as `pedagogic example — numbers, dates, and vendor framework version identifiers illustrative`.

### A. `BENCH-2026-014` as filed 2026-08-25 (prior quarter)

```
BENCH-2026-014
  System benchmarked:        INV-2026-0088 (MCDA)
  Model benchmarked:         anthropic/claude-3-5-sonnet-20241022
  Vendor artefacts (prior):  EVAL-2026-102 (vendor-system-card, dated 2026-05-10)
                             EVAL-2026-103 (vendor-rsp-disclosure, framework v2026-07)
  Internal artefacts:        EVAL-2026-088 (MCDA safety-eval, 2026-07-14)
                             EVAL-2026-091 (MCDA red-team RT-2026-014, 2026-08-12)

  Axis 1 — category coverage:
    Vendor covers: CBRN, cyber-offense, model-autonomy, persuasion, bias, hallucination.
    Internal covers: brand-guideline-violation, competitor-disparagement,
                     protected-class-generalisation, unsafe-medical-claim.
    Overlap: bias (protected-class is bias sub-category);
             hallucination (partially covered — MCDA has no RAG-triad row for
             MCDA directly).
    Non-overlap (Not applicable — MCDA use case): CBRN, cyber-offense,
             model-autonomy, persuasion.
    Gap: BENCH-GAP-2026-014-01 — hallucination coverage, Med severity,
         owner ai-evaluation-engineer, target 2026-Q4.

  Axis 2 — threshold alignment:
    Vendor classifies model at ASL-2 per RSP v2026-07 for all tracked categories
    relevant to MCDA. Enterprise controls for MCDA at ASL-2-equivalent per
    CTRL-2026-042. Aligned. No gap.

  Axis 3 — deployment-consideration honour:
    Vendor recommends human review before publication for marketing-adjacent
    generation — honoured by MCDA's human-review-before-publication workflow.
    Vendor recommends explicit AI-disclosure to customer where enterprise
    context requires — MCDA output has internal AI-assisted-draft watermark but
    no customer-visible AI-disclosure marker.
    Gap: BENCH-GAP-2026-014-02 — customer-visible AI-disclosure marker,
         Med severity, owner MCDA product owner, closure 2026-09-30.

  Axis 4 — external-evaluator alignment:
    Vendor's card names UK AISI collaboration on autonomy evaluations; MCDA
    has no tool use and no agentic surface; the autonomy category is Not
    applicable to the MCDA use case. No gap.

  Analyst summary: MCDA is deployed on claude-3-5-sonnet-20241022. Internal
  evals cover all MCDA-relevant categories except hallucination-under-grounding,
  which is scheduled. Vendor threshold classification honoured by internal
  control library. Two deployment-consideration gaps have owners and closure
  dates. No Axis-4 gap because the external-evaluator-covered categories are
  not applicable to MCDA.

  Benchmark date:            2026-08-25
  Next-benchmark-due:        2026-11-01 or upon vendor RSP revision, whichever sooner.
  Row status:                evidence-current.
  Last-verified / by:        2026-08-25 / <prior-quarter analyst>.
```

### B. The vendor's new RSP revision — `v2026-10` (fictional, for the lab)

```
Anthropic Responsible Scaling Policy — version v2026-10 (published 2026-10-02)

Change summary from v2026-07 to v2026-10 (per the framework's own change log):

  - Autonomy threshold (ASL-3 trigger) definition tightened: the previously
    separate "autonomous replication" and "agentic tool-use" tripwires are
    consolidated into a single "autonomous agentic capability" tripwire with
    a lower combined threshold. Pre-mitigation evaluation methodology is
    specified in an appendix (lab fixture: assume the appendix is published).

  - Deployment commitments at ASL-2 are unchanged for text-only, tool-less
    deployments.

  - For deployments that enable function-calling, tool use, browsing, code
    execution, or multi-step agentic planning — even where the base model
    remains classified at ASL-2 for text-only behaviour — the deployment
    tier is reclassified at ASL-2.5 with a new named control requirement
    for "agentic-surface monitoring" that is not part of the enterprise's
    current CTRL-2026-042 control.

  - The CBRN, cyber-offense, persuasion, bias, and hallucination tracked
    categories are unchanged from v2026-07 (naming, thresholds, and
    commitments carry over).

  - The named external evaluators for the autonomy category are retained
    (UK AISI, with an expanded engagement scope documented in the paired
    vendor-card revision dated 2026-10-02 — published together with the
    RSP revision).
```

### C. The enterprise's MCDA deployment state as of 2026-11-14

```
MCDA deployment state:
  - Model: anthropic/claude-3-5-sonnet-20241022 (unchanged — no migration yet).
  - Tool use: not enabled today; function-calling is on the MCDA v4.0 roadmap
    for 2027-Q1 as a candidate feature (not committed, pending design review).
  - System prompt: v1.8.1 (post-hot-fix; see lab-01's EVAL-2026-091 refresh).
  - Workflow: human review before publication, unchanged.
  - Customer-visible AI-disclosure marker: shipped on 2026-09-28 (two days ahead
    of the BENCH-GAP-2026-014-02 target closure 2026-09-30). Closure is confirmed
    by MCDA product owner on the marketing-site deployment.
```

<!-- needs-research: this RSP revision is a pedagogic placeholder. Verify the current Anthropic RSP version, the current ASL definitions, and the current commitments at each level against the Anthropic RSP page (https://www.anthropic.com/rsp) and news page (https://www.anthropic.com/news) before applying the lab's shape to real artefacts. The *shape* of the revision (one axis changed, one unchanged) is the pedagogic point; the specific threshold is not. -->

## Steps

### Step 1 — Scaffold the walk and copy in the prior row (10 min)

Create the working folder and file, and lay in the structure.

```bash
mkdir -p ~/aicg-labs/mod-107-lab-02
cd ~/aicg-labs/mod-107-lab-02
touch bench-refresh.md
```

Open `bench-refresh.md` and lay in the structure.

```markdown
# BENCH-2026-014 re-benchmark on Anthropic RSP v2026-10 — 2026-11-14

Walker:          <your-name>
Walk date:       2026-11-14
Benchmark row:   BENCH-2026-014 (MCDA, prior filed 2026-08-25)
Trigger:         Vendor RSP revision v2026-07 → v2026-10 (published 2026-10-02)
                 with paired vendor-card revision dated 2026-10-02.

## Prior-state summary

(Copy the Section A fixture here for cross-reference.)

## Vendor-change summary

(Copy the Section B RSP-change-log summary here, compressed to the delta that
 matters for MCDA.)

## Axis-by-axis re-walk

### Axis 1 — category coverage
### Axis 2 — threshold alignment
### Axis 3 — deployment-consideration honour
### Axis 4 — external-evaluator alignment

## Refreshed benchmark row (BENCH-2026-014 v2)

## Gap-list reconciliation

## Escalation authored

## Packet-reference update

## Walk verdict
```

### Step 2 — Characterise the vendor-change scope (10 min)

Chapter 07's *version-in-flight trap* and chapter 08's *benchmarks revise* discipline both apply. Before re-walking the four axes, record the vendor change in `bench-refresh.md`'s *Vendor-change summary* section with three fields:

- **What changed.** The autonomy-threshold consolidation and the new ASL-2.5 reclassification trigger for deployments enabling tool use. Quote the vendor change-log language verbatim where possible.
- **What did not change.** CBRN, cyber-offense, persuasion, bias, hallucination categories; text-only deployment commitments at ASL-2; the named external evaluator (UK AISI) for autonomy.
- **Relevance to MCDA.** Today's deployment is text-only and tool-less; the ASL-2.5 reclassification is *not triggered today*. However, function-calling is on the MCDA v4.0 roadmap for 2027-Q1 as a candidate feature — the reclassification trigger becomes live *if and when* function-calling ships.

This is the chapter 07 *RSPs revise regularly; record both what the paired card cites and what is currently in force, and flag any material divergence* discipline applied at the row level.

### Step 3 — Re-walk Axis 1 — category coverage (10 min)

Open the `### Axis 1 — category coverage` sub-section. The vendor's tracked categories relevant to MCDA have not changed in v2026-10 vs v2026-07 — CBRN, cyber-offense, persuasion, bias, hallucination carry over with unchanged definitions. The autonomy category has consolidated its tripwires but its applicability to MCDA is still *Not applicable — MCDA has no tool use today*.

Record the per-category walk mirroring the prior row's Axis-1 output:

- **CBRN, cyber-offense, persuasion, model-autonomy.** *Not applicable — MCDA use case does not generate scientific content, does not generate cyber-relevant content, is not user-facing persuasion, has no tool use.* Unchanged from prior row.
- **Bias.** *Covered — protected-class-generalisation is a bias sub-category under `EVAL-2026-088`.* Unchanged.
- **Hallucination.** *Partially covered — MCDA has no RAG-triad row for the MCDA system directly (MCDA-Benefits has `EVAL-2026-089` but that is a different system).* Unchanged. **Gap `BENCH-GAP-2026-014-01` carries forward** (hallucination coverage, Med, owner `ai-evaluation-engineer`, target 2026-Q4).

Axis 1 is unchanged. Record *axis unchanged from prior row; gap list carries forward*.

### Step 4 — Re-walk Axis 2 — threshold alignment (15 min)

Open the `### Axis 2 — threshold alignment` sub-section. This is the axis the vendor revision moves. The walk has two parts.

- **For today's deployment (text-only, tool-less).** Vendor classifies the model at ASL-2 per v2026-10 — unchanged from v2026-07 for text-only deployments. Enterprise controls for MCDA at ASL-2-equivalent per `CTRL-2026-042`. Aligned. No gap *today*.
- **For the MCDA v4.0 function-calling roadmap item.** v2026-10 introduces an ASL-2.5 reclassification trigger for deployments enabling tool use, function-calling, browsing, code execution, or multi-step agentic planning — *even where the base model remains classified at ASL-2 for text-only behaviour*. The MCDA v4.0 roadmap item would cross the trigger; `CTRL-2026-042` does not include the new *agentic-surface monitoring* control the ASL-2.5 tier commits to. This is a **threshold-alignment gap** that opens *conditionally* on the v4.0 roadmap item shipping, and must be flagged now so the v4.0 scoping incorporates the control.

Record both findings in the sub-section:

- *Current-state (text-only).* Aligned — no gap.
- *Conditional (MCDA v4.0 function-calling roadmap).* Gap `BENCH-GAP-2026-014-03` — threshold-alignment gap at the ASL-2.5 tier for the agentic-surface monitoring control not in `CTRL-2026-042`. Severity: Medium (conditional — graduates to High if the v4.0 feature ships without the control). Owner: MCDA product owner (to confirm roadmap intent) jointly with the enterprise control-library owner (to author the ASL-2.5-equivalent control). Target: 2026-12-15 (design-review deadline for the v4.0 scoping).

This is the specific place where chapter 08 Axis 2 moves. The prior row's *aligned — no gap* conclusion is no longer sufficient because the framework has added a new trigger that the prior framework version did not have. Chapter 10 Class 2 (mis-scoped eval — the eval and control scoping do not cover the newly-defined deployment category) applies to the control library and triggers an escalation in step 8.

### Step 5 — Re-walk Axis 3 — deployment-consideration honour (10 min)

Open the `### Axis 3 — deployment-consideration honour` sub-section. The vendor's deployment considerations for text-only deployments are unchanged in v2026-10. The paired card revision (2026-10-02) may expand the deployment-considerations section for tool-enabled deployments, but since MCDA is text-only today the expansion applies conditionally alongside the Axis-2 reclassification.

Record:

- **Human review before publication.** Honoured (unchanged).
- **Customer-visible AI-disclosure marker.** Previously `BENCH-GAP-2026-014-02` — target closure 2026-09-30. Section C of the fixture confirms the marker shipped 2026-09-28. **Gap closed.** Mark the gap *closed as of 2026-09-28* and retain it in the row for continuity per chapter 09's *gaps that have closed since the last packet version are marked closed and retained*.
- **Tool-enabled deployment considerations (new in the paired v2026-10 card revision).** *Not applicable today — MCDA is text-only; applies conditionally if MCDA v4.0 function-calling ships.* No new gap today; cross-reference the Axis-2 conditional gap.

### Step 6 — Re-walk Axis 4 — external-evaluator alignment (5 min)

Open the `### Axis 4 — external-evaluator alignment` sub-section. UK AISI's named engagement on autonomy is retained in v2026-10 with an expanded engagement scope documented in the paired card revision. Today's MCDA has no tool use, so the autonomy category remains *Not applicable to the MCDA use case* and the previously-recorded *no gap* conclusion is unchanged.

If the MCDA v4.0 function-calling feature ships, the autonomy category becomes applicable and the enterprise's lack of an independent line of evidence on autonomy becomes a new Axis-4 gap. Flag this as a *conditional gap tied to the same roadmap trigger as Axis 2* and record it without filing a separate gap ID today — chapter 08's *every not applicable carries a one-line justification* discipline applies, and the justification ties forward to the Axis-2 conditional entry.

### Step 7 — Compose the refreshed benchmark row (10 min)

Open the `## Refreshed benchmark row (BENCH-2026-014 v2)` section. Author the row's new state against the chapter 08 schema, calling out what has changed from v1:

- **Vendor artefacts benchmarked against.** Update `EVAL-2026-103` to cite framework v2026-10 (instead of v2026-07) and `EVAL-2026-102` to cite the vendor-card revision dated 2026-10-02 (snapshot the live URL plus archive.org per chapter 06's *deprecated-card trap*). Note that the paired vendor rows themselves require re-refresh in a separate walk — out of scope for this lab, but flagged as a cross-row trigger.
- **Internal artefacts benchmarked from.** Carry forward `EVAL-2026-088` and `EVAL-2026-091` (both have been refreshed per lab-01 if sequenced after it; cite the current row-status of each). If lab-01 was run first, the rows cited here are the post-lab-01 refreshed state; otherwise record the pre-lab-01 state and note the forward dependency.
- **Axis-1 / Axis-2 / Axis-3 / Axis-4 outputs.** Updated per steps 3–6.
- **Gap list.** Three entries: `BENCH-GAP-2026-014-01` (hallucination coverage, Med, owner `ai-evaluation-engineer`, target 2026-Q4 — carried forward); `BENCH-GAP-2026-014-02` (customer-visible AI-disclosure marker, Med, closed as of 2026-09-28 — retained for continuity); `BENCH-GAP-2026-014-03` (ASL-2.5 agentic-surface control, Medium conditional, owner MCDA product owner + control-library owner, target 2026-12-15 — new).
- **Analyst summary.** One paragraph updated from the prior summary, naming the one new conditional gap and the one closed gap. The summary is the paragraph a release-assurance packet or council briefing will quote.
- **Benchmark date.** 2026-11-14.
- **Next-benchmark-due.** 2027-02-14 or upon any of: (a) further vendor RSP revision, (b) MCDA deployment migration to a successor model identifier, (c) MCDA v4.0 function-calling feature shipping — whichever is soonest.
- **Row status.** `evidence-current` → `evidence-provisional (vendor revised; conditional Axis-2 gap pending v4.0 roadmap resolution)` → **`evidence-current` once step 8's escalation is routed** — chapter 08's discipline is that the refreshed row status reads *evidence-current* when the walk itself is current, even with an open conditional gap, as long as the gap is itemised and routed.
- **Last-verified / verified-by.** 2026-11-14 / current analyst.

### Step 8 — Author the one Class-2 escalation (10 min)

Open the `## Escalation authored` section. One escalation is warranted from this walk — the Axis-2 conditional threshold-alignment gap.

Author `ESC-2026-LAB02-01` using chapter 10 Class 2's template verbatim:

- **Class.** 2 — mis-scoped eval / control, chapter 10 definition extended to control-library scoping as chapter 08's *into the control library* downstream-flow explicitly accommodates.
- **Source row.** `BENCH-2026-014` v2 (this lab's refresh). Cross-reference `CTRL-2026-042` as the control-library entry under scope.
- **Filed date.** 2026-11-14.
- **Scope as reported.** MCDA's release-gating control `CTRL-2026-042` was authored at ASL-2-equivalent per the vendor RSP v2026-07; v2026-10 introduces an ASL-2.5 reclassification trigger for tool-enabled deployments and a new *agentic-surface monitoring* control requirement that `CTRL-2026-042` does not cover.
- **Scope required for the deployed system.** Today: unchanged (MCDA is text-only; ASL-2 controls remain sufficient). Conditional on MCDA v4.0 function-calling shipping: ASL-2.5-equivalent control required including agentic-surface monitoring.
- **Divergence.** Framework version drift from v2026-07 to v2026-10 adds a new deployment-tier definition the enterprise's control library does not yet cover. Not a model-version drift; a framework-version drift with a control-library scope gap.
- **Options.** (a) Author an ASL-2.5-equivalent control in the control library as part of MCDA v4.0 scoping, in time for the v4.0 design review on 2026-12-15; (b) de-scope function-calling from the v4.0 roadmap until the control is in place; (c) accept a documented conditional risk-treatment note from the governance council if (a) or (b) is not feasible within the roadmap.
- **Route.** MCDA product owner (to confirm v4.0 roadmap intent) + enterprise control-library owner (to author the new control — `mod-108` scope, pending the module's authoring). Copy `head-of-ai-governance` as a recurring-pattern signal if a second enterprise system's benchmark row has produced the same conditional gap this quarter — chapter 10's *recurring-escalation patterns feed policy work* discipline applies.
- **Requested resolution date.** 2026-12-15 (v4.0 design-review deadline).
- **Impact on packet.** The next MCDA release gate (likely v3.9 — text-only patch release, no function-calling) does not require resolution today; the v4.0 release gate cannot be handed off until the control is in place or option (c) is applied. Record this on the next MCDA packet's section 7 (escalation hooks) when the v4.0 packet is composed.
- **Status.** *open*.

### Step 9 — Packet-reference update (5 min)

Open the `## Packet-reference update` section. Short block for the downstream consumers:

- *`PACKET-2026-096` (MCDA v3.6 release-assurance packet, prior quarter, closed).* No action — packet closed per chapter 09's superseding-vs-revising discipline.
- *Next MCDA release gate (v3.9 — text-only patch, 2027-Q1 target).* The refreshed `BENCH-2026-014` v2 rides into the v3.9 packet with Axis-2 noted as *aligned for text-only* and the conditional gap `BENCH-GAP-2026-014-03` noted inline as a planning signal for v4.0. v3.9 does not require escalation closure.
- *Next-next MCDA release gate (v4.0 — function-calling, 2027-Q1 roadmap item).* Packet composition for v4.0 requires resolution of `ESC-2026-LAB02-01` (either the new control authored per option (a), or option (b) de-scoping, or option (c) council sign-off). If the escalation is not closed by the v4.0 release gate, chapter 10 Class 4 (packet-cannot-be-handed-off) applies to the v4.0 packet — flag this forward-looking risk now so the roadmap owner sees the deadline.

### Step 10 — Walk verdict and completeness check (5 min)

Open `## Walk verdict`. Three or four sentences:

- *Re-benchmark ran on 2026-11-14 against Anthropic RSP revision v2026-10 (paired card dated 2026-10-02). Axes 1 and 3 and 4 are substantively unchanged — one gap closed (`BENCH-GAP-2026-014-02`, customer-visible AI-disclosure marker shipped 2026-09-28), one gap carried forward (`BENCH-GAP-2026-014-01`, hallucination coverage). Axis 2 opens a new conditional gap (`BENCH-GAP-2026-014-03`, ASL-2.5 agentic-surface control for the MCDA v4.0 function-calling roadmap item) and one chapter-10 Class-2 escalation (`ESC-2026-LAB02-01`) is routed to the MCDA product owner and the control-library owner. Benchmark row `BENCH-2026-014` moved to v2 state and remains *evidence-current* with the open gap itemised; next-benchmark-due 2027-02-14 or on roadmap or vendor change, whichever is sooner.*

Close with a short `## Pre-close completeness check`:

- **Prior row's gap list is reconciled, not re-written.** Prior entries 01 (carried), 02 (closed and retained), new entry 03.
- **Axis-2 re-walk distinguishes current-state from conditional (roadmap-dependent).** Chapter 08 does not force a current-state-only reading; the conditional framing is correct when the vendor revision creates a trigger that becomes live on a known future event.
- **Vendor-artefact snapshot references updated.** Paired card revision 2026-10-02 and RSP revision v2026-10 both snapshotted (per chapter 06's *deprecated-card trap* and chapter 09's provenance discipline); prior card and RSP versions retained for continuity.
- **No cross-vendor arithmetic.** The walk stays per-vendor per-model per chapter 07's *threshold-arithmetic trap* discipline.
- **No fabricated classifications.** The RSP revision is marked as a pedagogic placeholder; the real-world shape of a vendor RSP revision is the content being drilled, not the specific threshold.

## Expected output

One Markdown file in `~/aicg-labs/mod-107-lab-02/`:

- `bench-refresh.md` — ten sections: a header, a prior-state summary, a vendor-change summary, four axis-by-axis sub-sections, the refreshed benchmark row with the updated gap list, the one Class-2 escalation entry, the packet-reference update, the walk verdict, and the pre-close completeness check.

Total length: roughly 1,000–1,500 words. A reviewer should be able to read it in ten minutes and see the four axes re-walked, the one new conditional gap identified and routed, the one closed gap retained for continuity, and the refreshed row left in a state a downstream packet-composer could pick up.

## Checkpoint

A mentor, peer, or self-review walk. Answer honestly:

1. **Did every axis get re-walked, including the ones with no change?** Chapter 08's *the benchmark is a structured comparison; every axis has its own output* discipline reads every axis on every re-benchmark cycle. An axis skipped because *nothing changed there* is a chapter 08 *scorecard trap* inverted.
2. **Does the refreshed Axis-2 distinguish current-state (aligned) from conditional (gap on the roadmap trigger)?** A re-benchmark that says *no gap today* without the forward-looking flag will let the MCDA v4.0 roadmap ship without the control in place — the exact chapter 08 *the benchmark is required; not optional* discipline inverted.
3. **Is `BENCH-GAP-2026-014-02` marked *closed as of 2026-09-28* and retained in the row, not deleted?** Chapter 09's *gaps that have closed since the last packet version are marked closed and retained for continuity* discipline applies here too.
4. **Does `ESC-2026-LAB02-01` route to both the MCDA product owner *and* the control-library owner?** Chapter 10 Class 2 and chapter 08's *into the control library* downstream-flow both apply; routing to only one role is partial.
5. **Does the walk record the vendor-artefact snapshot for v2026-10, retaining the v2026-07 snapshot for continuity?** Chapter 06's *deprecated-card trap* and chapter 07's *version-in-flight trap* both apply; a walk that overwrites the vendor-artefact snapshot pin loses the continuity a six-months-later auditor would need.
6. **Does the packet-reference update distinguish v3.9 (no escalation closure required) from v4.0 (closure required or Class 4 applies)?** Chapter 09's *one packet per release gate* and chapter 10's Class-4 threshold both apply; the forward-looking distinction is what makes the refresh useful to the next packet-composer.

If any of the six is "no", revise the artefact before considering the lab done.

## Why this is a lab, not an exercise

Exercise 02 drills benchmark authoring from scratch against the current vendor artefacts. It does not drill the *refresh* cadence — the specific place where a prior-quarter benchmark row meets a new vendor revision and the analyst must reconcile the two without silently absorbing either. This lab is that specific discipline. Chapter 08 names benchmarks as revising with vendor artefacts; chapter 07 names RSPs as revising on their own cadence; chapter 10 Class 2 covers the control-library scope gap a framework revision can open. The failure mode this lab prevents is the analyst who re-walks the axes mechanically, misses the conditional-gap framing on an open roadmap trigger, and lets a framework-version drift propagate into a release gate the control library was never scoped for.
