# Lab 02 — Quarterly Incident Roll-up and Pattern-Recognition Sweep Against the Escalation Register

**Duration:** 2 hours.
**Grounding chapters:** [09](../09-delegation-boundary-and-escalation-patterns.md), [03](../03-incident-record-and-register-linkage.md), [06](../06-monitoring-signal-escalation-patterns.md), [02](../02-ai-specific-incident-taxonomy.md).
**Difficulty:** Core — exercises chapter 09's five pattern-recognition rules against a fixed, pre-assembled set of six closed-or-open incident records from a rolling quarter, plus the chapter-03 weekly-roll-up discipline scaled up to the quarter boundary and the chapter-06 escalation-record shape for monitoring signals already filed in the quarter. The module's four exercises each drill the *within-incident* authoring (intake-ticket classification, one `INC-<year>-<sequence>` record, one monthly monitoring-reading note, one quarterly PMS summary against one high-risk system). None of them asks the analyst to walk a *rolling-quarter cross-incident view* across six records on four inventory rows and apply the chapter-09 pattern-recognition rules to open the right module-level escalations — the specific analyst act that converts a set of individually-well-handled incidents into a council-visible pattern the enterprise can act on. This lab is that specific sweep.

## Objective

Take a *fixed, pre-assembled* rolling-quarter view — six incident records (five closed, one open) across four inventory rows, filed between 2026-09-01 and 2026-11-30 — and run a quarter-end pattern-recognition sweep. For each chapter-09 pattern-recognition rule, apply the rule against the six-record set, identify the specific recurrence (if any) that triggers the rule, and open the correct module-level escalation (class 1 incident-command handoff; class 2 monitoring redesign; class 3 regulatory filing; class 4 governance-council decision) per the chapter-09 trigger / owner / what-the-analyst-supplies / what-the-analyst-does-not-do template. Close by composing the standing-governance-council briefing slot the sweep produces — a short summary of the patterns surfaced and the escalations filed, feeding the standing council agenda `mod-110` will later package.

The deliverables are two Markdown files in `~/aicg-labs/mod-109-lab-02/`:

- `quarter-sweep-log.md` — the sweep log, one sub-section per pattern-recognition rule with the applied-or-not-applied verdict against the six-record set, and a closing per-record acknowledgement block.
- `escalation-register-entries.md` — the chapter-09 register entries authored from the sweep, each with the full trigger / owner / what-the-analyst-supplies / what-the-analyst-does-not-do template, projected into the chapter-09 register-table shape at the bottom.

A reviewer should be able to read both files in twenty minutes and see every record acknowledged, every chapter-09 pattern-recognition rule explicitly walked (triggered or not, with reasoning), every escalation routed to the correct chapter-09 class with the correct owner, and the governance-council briefing-slot summary ready to roll into `mod-110`.

## Prerequisites

- Chapters 09, 03, 06, and 02 read; the four module-level escalation classes (class 1 incident-command handoff; class 2 monitoring redesign; class 3 regulatory filing; class 4 governance-council decision), the five pattern-recognition rules (three incidents of the same class on one inventory row within a rolling quarter; three incidents of the same class across different inventory rows within a quarter; repeated class-B monitoring escalations on jailbreak / prompt-injection signals; repeated class-3 regulatory-filing escalations concentrated in one system; class-4 escalations resolving with *no decision*), the chapter-03 weekly-roll-up interaction with the escalation register, and the chapter-06 escalation-record shape fresh in memory.
- A Markdown editor; no Python, GRC, or vendor tooling required — the record set below is a Markdown-only stand-in for what would live in the GRC platform in production.
- Exercise 01 completed, or at minimum skimmed, so the chapter-02 six AI-specific classes (model regression, jailbreak, prompt-injection exploitation, biased-outcome escalation, hallucination-driven harm, unauthorised model use) are fresh in memory.
- Lab 01 completed, or at minimum skimmed, so the chapter-08 evidence-pack discipline the class-4 escalation's attached pack would use is familiar. The lab-02 sweep does *not* re-compose packs — it files the escalations that would then require packs on `mod-110`'s next cycle.
- The MCDA (`INV-2026-0088`), MCDA-Benefits (`INV-2026-0311`), the contract-review-assistant (`INV-2026-0104`), and the CV-screening-assistant (`INV-2026-0512`) inventory rows from `mod-102` conceptually in mind; the record set references all four.

## The fixed input — six incident records across a rolling quarter

Use *exactly* this record set. Do not substitute identifiers, dates, classes, or inventory-row attributions, and do not rewrite any record's class — the fixed state is the point of the lab. Each record is reproduced at the level of fields a quarter-end pattern-sweeper reads from. Treat the whole block as `pedagogic example — identifiers, numbers, and dates illustrative`.

### A. The six incident records

```
INC-2026-0231 — hallucination-driven harm on contract-review-assistant
  Status:           closed-with-open-follow-through (per lab 01's record)
  Opened:           2026-09-04
  Closed:           2026-10-19
  Class:            class 5 — hallucination-driven harm
  Affected INV:     INV-2026-0104 (contract-review-assistant; High-tier)
  Affected FRIA:    FRIA-2026-0033 re-opened v3 → v4
  Follow-through:   corrective complete; preventive (v) prompt-template-change-
                    requires-eval control open with senior-ai-governance-architect
                    under ESC-2026-0431 (class-1 escalation already filed)
  Pack composed:    PACK-2026-INC-2026-0231-v1 (per lab 01)
  Comment:          First class-5 event this quarter.

INC-2026-0244 — hallucination-driven harm on MCDA
  Status:           closed
  Opened:           2026-09-20
  Closed:           2026-10-05
  Class:            class 5 — hallucination-driven harm
  Affected INV:     INV-2026-0088 (MCDA; High-tier marketing-copy assistant with
                    RAG-augmented product-knowledge corpus)
  Affected IA:      IA-2026-0019 re-opened and signed v2 2026-10-02 (Q3 falsified
                    claim: *grounding-to-approved-product-content measure* was
                    technically met but produced a competitor-disparagement
                    statement from a partial retrieval match — the IA's *measure*
                    did not envelop partial-retrieval-match confabulation)
  Follow-through:   corrective complete (partial-match retrieval-threshold raised;
                    output-filter on competitor-mention prompt added); preventive
                    (vi) RAG-scaffold citation-provenance-check pattern adopted
  Pack composed:    PACK-2026-INC-2026-0244-v1
  Comment:          Second class-5 event this quarter against a RAG-based tool;
                    a *different* system from INC-2026-0231.

INC-2026-0253 — hallucination-driven harm on MCDA-Benefits
  Status:           closed
  Opened:           2026-10-18
  Closed:           2026-11-02
  Class:            class 5 — hallucination-driven harm
  Affected INV:     INV-2026-0311 (MCDA-Benefits; High-tier RAG-based assistant
                    responding to benefits-eligibility queries from the enterprise's
                    benefits-platform customer base)
  Affected FRIA:    FRIA-2026-0311 re-opened v2 → v3 signed 2026-11-01 (Q3 fail:
                    *every output cites a specific benefits-policy source* measure
                    was technically met but the cited source was outdated by one
                    policy-revision cycle — the model produced a statement
                    consistent with the prior-version source as if it were current)
  Follow-through:   corrective complete (policy-source-currency check added to
                    the RAG scaffold); preventive (v) prompt-template-change-
                    requires-eval control — same as INC-2026-0231 — joined with
                    ESC-2026-0431
  Pack composed:    PACK-2026-INC-2026-0253-v1
  Comment:          Third class-5 event this quarter against a RAG-based tool;
                    across three *different* inventory rows now.

INC-2026-0271 — prompt-injection exploitation on CV-screening-assistant
  Status:           closed
  Opened:           2026-09-18 (per exercise 04's scenario)
  Closed:           2026-10-10
  Class:            class 3 — prompt-injection exploitation (indirect, via
                    candidate CV document)
  Affected INV:     INV-2026-0512 (CV-screening-assistant; Annex III item 4(a)
                    high-risk under EU AI Act)
  Affected FRIA:    FRIA-2026-0512 re-opened v2 → v3 2026-09-28
  Article 73:       drafted 2026-09-18; executive determined no-submission 2026-09-25
                    (per exercise 04); draft retained on record
  Follow-through:   system-prompt-injection classifier deployed 2026-09-24; red-team
                    retrospective complete; scope-review of Article 3(49) walk
                    recorded on PMS-2026-INV-2026-0512-Q3
  Pack composed:    PACK-2026-INC-2026-0271-v1
  Comment:          Only class-3 event this quarter. Article 73 draft opened but
                    no-submission determined by executive with legal counsel.

INC-2026-0289 — prompt-injection exploitation on CV-screening-assistant
  Status:           closed
  Opened:           2026-11-05
  Closed:           2026-11-19
  Class:            class 3 — prompt-injection exploitation (indirect, via a
                    candidate-cover-letter PDF with embedded instruction block
                    using a *rot-13-encoded* payload the September classifier
                    did not detect)
  Affected INV:     INV-2026-0512 (same system as INC-2026-0271)
  Affected FRIA:    FRIA-2026-0512 re-opened v3 → v4 2026-11-18
  Article 73:       drafted 2026-11-05; executive determined no-submission
                    2026-11-12 after legal review (same rationale as
                    INC-2026-0271 — no realised harm materialised; customer
                    human-review workflow interrupted the injected ranking)
  Follow-through:   classifier updated to detect encoded-payload variants; red-
                    team retrospective scheduled for 2026-11-26
  Pack composed:    PACK-2026-INC-2026-0289-v1
  Comment:          Second class-3 event this quarter against the same inventory
                    row; second Article-73-drafted-but-not-submitted event on
                    INV-2026-0512 this quarter.

INC-2026-0304 — biased-outcome escalation on CV-screening-assistant
  Status:           open — containment in progress; post-mortem scheduled
  Opened:           2026-11-21
  Closed:           — (open as of sweep date 2026-11-30)
  Class:            class 4 — biased-outcome escalation
  Affected INV:     INV-2026-0512 (same system)
  Affected FRIA:    FRIA-2026-0512 re-open trigger evaluated 2026-11-24 — Q3
                    triggered (segment-monitoring cadence measure from the v3
                    update was not operating as described on the Spanish
                    customer deployment; monthly cadence had slipped to
                    quarterly); re-open in flight with FRIA accountable executive
  Article 73:       evaluation open; Spanish customer's HR team has flagged the
                    pattern as possibly implicating Article 3(49)(c) fundamental-
                    rights infringement (non-discrimination); legal + compliance
                    function in triage; executive looped in same-day per chapter 07
  Follow-through:   containment: segment monitoring restored to monthly cadence
                    2026-11-26; disaggregated re-eval in flight; deployer-side
                    human-review verification underway
  Pack composed:    PACK-2026-INC-2026-0304-v0 (in-draft; pending post-mortem)
  Comment:          Second class-4 event against INV-2026-0512 this calendar year
                    (the first was INC-2026-0177 in Q3 per exercise 04). First
                    class-4 event this *rolling* quarter.
```

### B. Related artefact identifiers

```
INV-2026-0088    MCDA (marketing-copy assistant; High-tier; RAG-augmented)
INV-2026-0104    contract-review-assistant (High-tier; RAG-based; EU customer base)
INV-2026-0311    MCDA-Benefits (High-tier; RAG-based)
INV-2026-0512    CV-screening-assistant (Annex III item 4(a); EU AI Act high-risk)
ESC-2026-0431    chapter-9 class-1 library-design-fix on CTL-2026-0411 (prompt-
                 template-change-requires-eval control authoring); open with
                 senior-ai-governance-architect since 2026-09-20
ESC-2026-0455    chapter-9 class-4 pattern-recognition escalation — second class-5
                 hallucination-driven-harm against a RAG-based tool within a
                 rolling quarter — filed 2026-10-05; on the 2026-11-20 governance-
                 council standing agenda as item 4 (status: read at the meeting;
                 council resolved to defer decision pending Q4 sweep — per lab 02)
ESC-2026-0498    chapter-6 class-B monitoring escalation — first class-3 prompt-
                 injection signal from INC-2026-0271 — filed 2026-09-18; resolved
                 2026-09-24 with classifier deployment
ESC-2026-0521    chapter-6 class-B monitoring escalation — second class-3 prompt-
                 injection signal from INC-2026-0289 — filed 2026-11-05; resolved
                 2026-11-12 with classifier update
PMS-2026-INV-2026-0512-Q3  per exercise 04
PMS-2026-INV-2026-0512-Q4  in flight — Q4 PMS summary draft due 2027-01-10
CSR-2026-Q4      drafting control-status report (per mod-108 lab 01's shape)
MON-2026-10-*    monthly monitoring-reading notes per system for October
MON-2026-11-*    monthly monitoring-reading notes per system for November
```

### C. The 2026-11-20 council meeting outcome (already in the record)

The council read `ESC-2026-0455` (the first pattern-recognition escalation — second class-5 hallucination-driven-harm against a RAG-based tool) at the 2026-11-20 standing meeting as agenda item 4. The resolution recorded: *"Council acknowledges the pattern surfaced by the analyst. Council defers decision on whether to scope the prompt-template-change-requires-eval control across the RAG-based tool portfolio until the 2026-Q4 sweep lands and any further class-5 recurrence is read against the then-current record set. Head-of-ai-governance to bring the Q4 sweep as agenda item 1 at the 2026-12-18 meeting."*

The sweep this lab produces is the input to that 2026-12-18 council slot.

## Steps

### Step 1 — Scaffold the two files and build the per-record acknowledgement block (10 min)

Create the working folder and files.

```bash
mkdir -p ~/aicg-labs/mod-109-lab-02
cd ~/aicg-labs/mod-109-lab-02
touch quarter-sweep-log.md escalation-register-entries.md
```

Open `quarter-sweep-log.md` and lay in the structure.

```markdown
# Quarter-end incident pattern-recognition sweep — 2026-09-01 through 2026-11-30 — composed 2026-11-30

Walker:           [analyst-name]
Sweep date:       2026-11-30
Window:           rolling quarter 2026-09-01 → 2026-11-30 (90 days)
Record set:       INC-2026-0231, -0244, -0253, -0271, -0289, -0304
Prior-escalation  ESC-2026-0431 (class-1, open); ESC-2026-0455 (class-4, deferred
carry-forward:    by council 2026-11-20); ESC-2026-0498 and -0521 (class-B
                  monitoring escalations, both resolved)
Downstream read:  2026-12-18 standing council meeting agenda item 1

## Per-record acknowledgement (chapter-03 weekly-roll-up discipline, scaled)

### INC-2026-0231 — hallucination-driven harm on INV-2026-0104
### INC-2026-0244 — hallucination-driven harm on INV-2026-0088
### INC-2026-0253 — hallucination-driven harm on INV-2026-0311
### INC-2026-0271 — prompt-injection on INV-2026-0512
### INC-2026-0289 — prompt-injection on INV-2026-0512
### INC-2026-0304 — biased-outcome escalation on INV-2026-0512

## Pattern-recognition rule walk (chapter 9)

### Rule 1 — Three class-X incidents on the same INV in a rolling quarter
### Rule 2 — Three class-X incidents across different INV in a rolling quarter
### Rule 3 — Repeated class-B monitoring escalations on jailbreak / prompt-injection signals
### Rule 4 — Repeated class-3 regulatory-filing escalations concentrated in one system
### Rule 5 — Class-4 escalations resolving with *no decision*

## Escalations authored from this sweep

## Governance-council briefing-slot summary (2026-12-18 agenda item 1)

## Sweep verdict

## Pre-close completeness check
```

Open `escalation-register-entries.md` and lay in the entries-plus-table skeleton.

```markdown
# Escalations from the 2026-11-30 quarter-end pattern-recognition sweep

## ESC entries

## Register table
```

For each of the six records, populate the per-record acknowledgement sub-section with a four-line block in the chapter-03 weekly-roll-up shape:

```
status:          open | contained | post-mortem-in-flight | closed | closed-with-open-follow-through
class:           per chapter 02
inv:             the affected INV-<year>-<sequence>
open-follow:     any open corrective / preventive action / escalation / Article 73 draft
```

This is the chapter-03 weekly-roll-up discipline scaled to the quarter — the six-record view the sweep reads from.

### Step 2 — Walk Rule 1 (three incidents of the same class on the same INV in a rolling quarter) (15 min)

Chapter 09 rule 1: *three incidents of the same class against the same inventory row within a rolling quarter* is a pattern. The affected system has a specific failure mode the assurance model is not enveloping. Recommend to `head-of-ai-governance` and the assessment's original owner a *targeted re-assessment*.

Count, in `quarter-sweep-log.md` §"Rule 1":

- `INV-2026-0088` (MCDA): one class-5 incident (INC-2026-0244).
- `INV-2026-0104` (contract-review-assistant): one class-5 incident (INC-2026-0231).
- `INV-2026-0311` (MCDA-Benefits): one class-5 incident (INC-2026-0253).
- `INV-2026-0512` (CV-screening-assistant): two class-3 incidents (INC-2026-0271, INC-2026-0289) and one class-4 incident (INC-2026-0304). The two class-3 incidents are the same class on the same INV within the quarter. The count is two, not three.

Expected verdict: **Rule 1 does not trigger on any INV this quarter.** The two class-3 incidents on `INV-2026-0512` are at the two-count warning threshold; a third class-3 on `INV-2026-0512` before 2027-02-05 (90 days from INC-2026-0271 = 2026-12-17) would trigger. Record the *does-not-apply-but-approaching* observation in the sweep log for the governance-council briefing-slot summary.

Note the chapter-09 discipline: rule 1 is *three*, not two. The sweep records the two-count on `INV-2026-0512` as an observation, not an escalation — opening a Rule-1 escalation on a two-count is the chapter-09 *overuse-of-pattern-recognition* failure mode. The right action is to flag the approaching threshold in the council briefing-slot and bring it into the next quarter's sweep.

### Step 3 — Walk Rule 2 (three incidents of the same class across different INVs in a rolling quarter) (15 min)

Chapter 09 rule 2: *three incidents of the same class across different inventory rows within a rolling quarter* is a *class-of-system* pattern, not a *specific-system* pattern. Recommend to `senior-ai-governance-architect` and `head-of-ai-governance` a library-level review and a possible policy-work agenda item.

Count, in `quarter-sweep-log.md` §"Rule 2":

- **Class 5 (hallucination-driven harm).** `INV-2026-0088` (INC-2026-0244), `INV-2026-0104` (INC-2026-0231), `INV-2026-0311` (INC-2026-0253) — **three different inventory rows**. All three are RAG-based tools; all three incidents reached a user or a downstream workflow. Rule 2 triggers on class 5.
- **Class 3 (prompt-injection exploitation).** `INV-2026-0512` only (both incidents on the same INV). Rule 2 does not trigger on class 3 (rule 1's domain, not rule 2's).
- **Class 4 (biased-outcome escalation).** `INV-2026-0512` only. One event does not trigger rule 2.
- Other classes: no events this quarter.

Expected verdict: **Rule 2 triggers on class 5.** The pattern is three class-5 hallucination-driven-harm events across three different RAG-based High-tier tools within a rolling quarter. The chapter-09 escalation routing: this is a *class-of-system* pattern — route to `senior-ai-governance-architect` for library-level review and to `head-of-ai-governance` for a possible policy-work agenda item.

Open the escalation. The right chapter-09 class to file the pattern under is **class 4 governance-council decision** — the pattern crosses from technical / architectural (which would be class 2 monitoring redesign on a specific gap) into policy (whether the enterprise's prompt-template-change-requires-eval control and the citation-provenance-check RAG-scaffold pattern should be mandatory across the RAG-based tool portfolio, with a cadence and a scope the council sets). The analyst supplies the pattern, the three underlying incident records and their packs, the two library-level artefacts (`ESC-2026-0431`, the Q1 2027 scheduled adoption of the `citation-provenance-check` RAG-scaffold pattern), and the Q4 2026 PMS summary trajectory for the affected systems. The analyst does not take the policy decision; the council does.

Record the escalation ID as `ESC-2026-LAB02-01` and author its register entry in Step 7.

### Step 4 — Walk Rule 3 (repeated class-B monitoring escalations on jailbreak / prompt-injection signals) (10 min)

Chapter 09 rule 3: *repeated class-B monitoring escalations on jailbreak or prompt-injection signals across multiple systems* is a pattern suggesting the enterprise's guardrail architecture is not keeping pace with attack innovation. Recommend to `ai-infra-security` and `senior-ai-governance-architect` an evaluation of platform-level guardrail solutions.

Count, in `quarter-sweep-log.md` §"Rule 3":

- `ESC-2026-0498` — class-B monitoring escalation on a class-3 prompt-injection signal (INC-2026-0271) on `INV-2026-0512`. Resolved with a system-prompt-injection classifier deployment.
- `ESC-2026-0521` — class-B monitoring escalation on a class-3 prompt-injection signal (INC-2026-0289) on `INV-2026-0512`. Resolved with a classifier update to detect encoded-payload variants.
- No class-B escalations on other systems this quarter.

Expected verdict: **Rule 3 triggers in a *soft* form.** Chapter 09's rule 3 names *multiple systems*, not multiple escalations on the same system. The two class-B escalations are on the *same* system (`INV-2026-0512`), so the *across multiple systems* criterion is not met. But the shape is approaching: a second attack-innovation event bypassed the classifier the first event's response deployed (the September classifier did not detect the rot-13-encoded payload the November event used), which is itself a *the guardrail architecture is not keeping pace with attack innovation* signal on a single system — a chapter-06 class-B *re-opening-on-innovation* pattern rather than a chapter-09 rule-3 multi-system pattern.

Record the *does-not-apply-in-strict-form-but-approaching* observation. The right routing is a chapter-06 class-B *recurrence-pattern* observation on `INV-2026-0512` to `ai-infra-security` plus a cross-copy to `senior-ai-governance-architect` for the library-level question (whether the enterprise's attack-innovation evaluation cadence against the class-B classifier families is adequate). The analyst does not open a module-level class escalation; the right-sized action is a class-B pattern-recognition observation attached to `PMS-2026-INV-2026-0512-Q4` and to the control-status-report-Q4 drafting. Record the observation ID as `OBS-2026-LAB02-02` (a chapter-06 observation, not a chapter-09 escalation — the distinction matters).

### Step 5 — Walk Rule 4 (repeated class-3 regulatory-filing escalations concentrated in one system) (10 min)

Chapter 09 rule 4: *repeated class-3 regulatory-filing escalations concentrated in one system* is a pattern suggesting the system may not be safely operable at its current scope; the accountable executive should consider a scope reduction, a re-authorisation review, or a sunset.

Count, in `quarter-sweep-log.md` §"Rule 4":

- `INV-2026-0512` has two Article 73 notification drafts in the quarter (`A73-2026-INV-2026-0512-0001` on INC-2026-0271, `A73-2026-INV-2026-0512-0002` on INC-2026-0289). Both resulted in *no-submission* determinations. The Article 73 drafts are *module-level class-3 escalations* under chapter 09 (the accountable-executive review on the notification is the chapter-09 class-3 shape).
- `INC-2026-0304` has an Article 73 evaluation *in flight* as of 2026-11-30; a third draft on `INV-2026-0512` is possible if the Spanish customer's fundamental-rights-infringement claim matures into *established causal link* under Article 3(49)(c).

Expected verdict: **Rule 4 triggers in a *provisional* form.** The two drafts are the two-count on a system; chapter-09 rule 4 is *repeated* (which the chapter does not fix to a specific count but which the analyst reads against the rule-1 *three-or-more* baseline for consistency). Two no-submission-determined drafts within the quarter against the same system, with a third in-flight, is a pattern the analyst raises to the accountable executive and to `head-of-ai-governance` *as an observation requiring the Q4 PMS summary's §7 to address* — specifically, whether the Annex III classification and the deployment scope remain the correct posture given the attack-pattern density.

The right chapter-09 class to file this pattern under is **class 4 governance-council decision** — the decision the council (or the enterprise's EU AI Act compliance function at that board-adjacent altitude) may be asked to take is whether `INV-2026-0512`'s scope should contract, whether the Annex III classification should drive a tighter deployment envelope, whether the deployer notification should include a scope-review attachment. The analyst does not make any of those decisions; the analyst files the escalation with the pattern, the three underlying incident records (one post-mortem pending), the two Article 73 drafts and their no-submission rationales, and the in-flight INC-2026-0304 status.

Record the escalation ID as `ESC-2026-LAB02-03` and author its register entry in Step 7.

### Step 6 — Walk Rule 5 (class-4 escalations resolving with *no decision*) (10 min)

Chapter 09 rule 5: *class-4 escalations resolving with "no decision"* is a pattern suggesting the council is under-resourced or under-informed for the volume of AI decisions. Recommend to `head-of-ai-governance` that decision-rights be delegated or that the council cadence increase.

Count, in `quarter-sweep-log.md` §"Rule 5":

- `ESC-2026-0455` was read at the 2026-11-20 council meeting with the resolution *"Council defers decision ... until the 2026-Q4 sweep lands"*. The chapter-09 definition of *no decision* is explicit — deferral without a named follow-through milestone that produces a decision at a specific later meeting is a *no-decision* resolution; deferral *with* a named follow-through (as here — *head-of-ai-governance to bring the Q4 sweep as agenda item 1 at the 2026-12-18 meeting*) is a *staged-decision*, not a *no-decision*.
- No other class-4 escalations landed at the council this quarter.

Expected verdict: **Rule 5 does not trigger in a strict sense.** The council's 2026-11-20 resolution on `ESC-2026-0455` is a *staged decision* — deferral with named milestone — which satisfies the chapter-09 rule's intent (the council is making a decision, just staged over multiple reads). Record the *does-not-apply* observation with the staged-decision rationale. The sweep log must still name rule 5 explicitly with the *does-not-apply-because-deferral-is-staged* reasoning — chapter-09 discipline is the full walk, not just the triggered rules.

### Step 7 — Author the escalation entries (15 min)

Open `escalation-register-entries.md`. The sweep generates two chapter-9 class-4 escalations plus one chapter-6 class-B pattern observation plus prior carry-forwards. Walk them in order and populate each with the chapter-9 template.

- **`ESC-2026-0431` (carried forward, Class 1 library-design-fix).** Not re-authored; referenced in the register table with status *open — architect acknowledged; prompt-template-change-requires-eval control authoring in flight; target 2026-12-31*. Note the age (filed 2026-09-20; open 71 days as of 2026-11-30) in the roll-up — approaching the chapter-09 *registers-that-grow-without-triage* threshold but not yet past the 2026-12-31 target.
- **`ESC-2026-0455` (carried forward, Class 4 pattern-recognition).** Not re-authored; referenced in the register table with status *staged-decision — council deferred on 2026-11-20 pending 2026-Q4 sweep (this sweep); next read scheduled 2026-12-18 council agenda item 1*. The sweep's `ESC-2026-LAB02-01` below *joins* this escalation.
- **`ESC-2026-LAB02-01` — Class 4 governance-council decision on the three-class-5-across-three-RAG-tools pattern.** Trigger: chapter-09 rule 2 (three class-X incidents across different inventory rows within a rolling quarter). Source: INC-2026-0231, INC-2026-0244, INC-2026-0253. Owner: governance council (convened by `head-of-ai-governance`). What the analyst supplies: (i) the three incident records and their evidence packs (`PACK-2026-INC-2026-0231-v1`, `PACK-2026-INC-2026-0244-v1`, `PACK-2026-INC-2026-0253-v1`); (ii) the `head-of-ai-governance` recommendation obtained during the pack-review cycle (to be solicited by the analyst before the 2026-12-18 meeting); (iii) the specific decision being asked (whether to adopt the prompt-template-change-requires-eval control and the citation-provenance-check RAG-scaffold pattern across the RAG-based tool portfolio on a specific cadence and scope); (iv) the timing constraints (the Q1 2027 scaffold-adoption rollout is already scheduled per INC-2026-0244's preventive action (vi); council decision by 2026-12-18 supports or re-scopes that rollout). What the analyst does *not* do: take the policy decision; draft the control statement (that is `senior-ai-governance-architect`'s work and is already in flight under `ESC-2026-0431`); downgrade the class to a lower one to avoid the council slot. Join this entry to `ESC-2026-0455` and `ESC-2026-0431` so the council sees the full pattern on one read.
- **`ESC-2026-LAB02-03` — Class 4 governance-council decision on the repeated-Article-73-drafts-on-a-single-system pattern.** Trigger: chapter-09 rule 4 (repeated class-3 regulatory-filing escalations concentrated in one system). Source: INC-2026-0271, INC-2026-0289, INC-2026-0304 (in-flight). Owner: governance council (convened by `head-of-ai-governance`); the enterprise's EU AI Act compliance function copied; `legal` copied; the CV-screening-assistant's product-owner-accountable-executive copied. What the analyst supplies: (i) the three incident records (two closed with Article 73 no-submission determinations; one open); (ii) the two Article 73 drafts and their no-submission rationales (`A73-2026-INV-2026-0512-0001`, `A73-2026-INV-2026-0512-0002`); (iii) the in-flight Article 3(49)(c) evaluation on INC-2026-0304; (iv) the Q3 and Q4 PMS summary trajectories for `INV-2026-0512` (`PMS-2026-INV-2026-0512-Q3` and the drafting `-Q4`); (v) the specific decision being asked (whether `INV-2026-0512`'s scope should contract, whether the Annex III classification drives a tighter deployment envelope, whether the deployer notification should include a scope-review attachment, whether further red-team or evaluation work is required before Q1 2027 renewal). What the analyst does *not* do: determine that any of the three incidents is a serious incident under Article 3(49) (that is `legal` and the compliance function's call); sign or submit any notification; take the scope-contraction decision; negotiate the wording of the deployer notification; speak to the Spanish customer directly on Article 73 scope.
- **`OBS-2026-LAB02-02` — Chapter-6 class-B pattern observation on `INV-2026-0512` attack-innovation.** Not a chapter-9 escalation. Trigger: the second prompt-injection attack (INC-2026-0289) bypassed the classifier deployed in response to the first (INC-2026-0271) — the *guardrail architecture is not keeping pace with attack innovation* shape on a single system. Owner: `ai-infra-security` (primary); `senior-ai-governance-architect` copied for the library-level question (attack-innovation evaluation cadence). Rationale: chapter-9 rule 3 requires the pattern across *multiple systems*; the two-escalations-on-same-system shape is a chapter-6 class-B pattern observation attached to `PMS-2026-INV-2026-0512-Q4` and to the control-status-report-Q4 drafting. Target: 2026-12-18 (same council slot — the observation feeds the Q4 PMS summary's §7).

Projection into the register table at the bottom of `escalation-register-entries.md`:

```markdown
## Register table

| ID | Class | Source | Filed | Route | Status | Resolution | Impact on 2026-12-18 council |
|---|---|---|---|---|---|---|---|
| ESC-2026-0431 | 1 (library-design-fix) | CTL-2026-0411 + INC-2026-0231, -0253 joined | 2026-09-20 | senior-ai-governance-architect | open — target 2026-12-31 | — | carried forward; 71 days open; approaching chapter-09 registers-that-grow-without-triage threshold |
| ESC-2026-0455 | 4 (pattern-recognition, first) | second class-5 on RAG-based tool | 2026-10-05 | governance council | staged-decision; deferred 2026-11-20 to 2026-12-18 | — | joined with ESC-2026-LAB02-01 for 2026-12-18 agenda item 1 |
| ESC-2026-LAB02-01 | 4 (governance-council decision) | chapter-9 rule 2 — three class-5 across three RAG-based INVs | 2026-11-30 | governance council (via head-of-ai-governance) | open; filed to 2026-12-18 council slot | — | 2026-12-18 agenda item 1 — joined with ESC-2026-0455 |
| ESC-2026-LAB02-03 | 4 (governance-council decision) | chapter-9 rule 4 — repeated class-3 regulatory filings on INV-2026-0512 | 2026-11-30 | governance council (via head-of-ai-governance); EU AI Act compliance function cc; legal cc; product-owner-accountable-executive cc | open; filed to 2026-12-18 council slot | — | 2026-12-18 agenda item 2 |
| OBS-2026-LAB02-02 | — (chapter-6 class-B observation; not a chapter-9 class) | second-injection-bypass on INV-2026-0512 | 2026-11-30 | ai-infra-security; senior-ai-governance-architect cc | open — attached to PMS-2026-INV-2026-0512-Q4 | — | §7 of PMS-2026-INV-2026-0512-Q4 drafting |
| ESC-2026-0498 | B (resolved earlier) | INC-2026-0271 class-3 signal | 2026-09-18 | ai-infra-security | resolved 2026-09-24 | classifier deployment | audit-trail only |
| ESC-2026-0521 | B (resolved earlier) | INC-2026-0289 class-3 signal | 2026-11-05 | ai-infra-security | resolved 2026-11-12 | classifier update | audit-trail only |
```

### Step 8 — Compose the 2026-12-18 council briefing-slot summary (10 min)

Open `quarter-sweep-log.md` §"Governance-council briefing-slot summary (2026-12-18 agenda item 1)". Four or five sentences, in `mod-110` house style, that `head-of-ai-governance` can read aloud at the opening of the 2026-12-18 meeting:

*Quarter-end pattern-recognition sweep ran 2026-11-30 against six AI incident records across four High-tier systems (two of which — `INV-2026-0512` — are in Annex III scope under the EU AI Act); five records closed and one open with containment in progress. Two chapter-9 pattern-recognition rules triggered: rule 2 — three class-5 hallucination-driven-harm events across three different RAG-based tools within a rolling quarter — filed as `ESC-2026-LAB02-01` and joined with the first-quarter `ESC-2026-0455` the council deferred on 2026-11-20; and rule 4 — repeated class-3 regulatory-filing escalations concentrated in one system — filed as `ESC-2026-LAB02-03` against `INV-2026-0512`'s two no-submission-determined Article 73 drafts and an in-flight third evaluation on INC-2026-0304. The decisions the council is being asked to take at this meeting are (agenda item 1) whether to adopt the prompt-template-change-requires-eval control and the citation-provenance-check RAG-scaffold pattern across the RAG-based tool portfolio on a specific cadence and scope, and (agenda item 2) whether `INV-2026-0512`'s scope should contract given the pattern of Article 73 drafts. Pattern-recognition rules 1, 3, and 5 did not trigger this quarter; rule 1's two-count on `INV-2026-0512` class-3 and rule 3's two-escalations-on-same-system shape are observations carried into Q1 2027. Three evidence packs (`PACK-2026-INC-2026-0231-v1`, `-0244-v1`, `-0253-v1`) are attached as pre-read; a fourth (`PACK-2026-INC-2026-0304-v0`) is in draft and will ship when the INC-2026-0304 post-mortem lands.*

### Step 9 — Compose the sweep verdict and the pre-close completeness check (5 min)

Open `## Sweep verdict` at the bottom of `quarter-sweep-log.md`. Three or four sentences:

*Quarter-end pattern-recognition sweep ran 2026-11-30 across six AI incident records on four High-tier systems; five records closed, one open with containment in progress; two chapter-9 pattern-recognition rules (2 and 4) triggered — two class-4 governance-council-decision escalations (`ESC-2026-LAB02-01`, `ESC-2026-LAB02-03`) filed to the 2026-12-18 council slot as agenda items 1 and 2 respectively, joined to the carried-forward `ESC-2026-0455`. One chapter-6 class-B pattern observation (`OBS-2026-LAB02-02`) attached to `PMS-2026-INV-2026-0512-Q4`. One class-1 library-design-fix escalation (`ESC-2026-0431`) carried forward; approaching but not yet past the chapter-9 registers-that-grow-without-triage threshold on 71 days open against a 2026-12-31 target. Pattern-recognition rules 1, 3, and 5 did not trigger in strict form; the approaching-threshold observations on rules 1 and 3 are carried forward to the Q1 2027 sweep.*

Record the four chapter-09 pre-close completeness checks at the bottom as `## Pre-close completeness check`:

1. **Every record acknowledged.** Six per-record sub-sections populated with the four-line roll-up block. Confirm pass.
2. **Every pattern-recognition rule explicitly walked.** Rules 1–5 each have their own sub-section with triggered / does-not-apply verdict plus reasoning. Confirm pass.
3. **Every escalation filed under the correct chapter-9 class.** `ESC-2026-LAB02-01` and `ESC-2026-LAB02-03` are class 4 (governance-council decision); `OBS-2026-LAB02-02` is correctly a chapter-6 observation, not a chapter-9 escalation. Confirm pass.
4. **The 2026-12-18 council briefing-slot summary names specific decisions.** Agenda items 1 and 2 are each phrased as a decision the council is being asked to take, with the supporting evidence pack identifiers attached. A summary that reads *"council to discuss"* is off-side — the council takes decisions, not discussions. Confirm pass.

If any of the four is "no", revise *that artefact* before considering the lab done.

## Expected output

Two Markdown files in `~/aicg-labs/mod-109-lab-02/`:

- `quarter-sweep-log.md` — (a) the sweep header with walker, date, window, record set, carry-forwards, and downstream read; (b) a per-record acknowledgement block with the four-line roll-up for each of the six records; (c) a pattern-recognition-rule-walk section with one sub-section per chapter-9 rule 1–5 explicitly walked (triggered or does-not-apply with reasoning); (d) an escalations-authored-from-this-sweep section naming the entries by ID with one-line summaries; (e) the 2026-12-18 council briefing-slot summary; (f) the sweep verdict; (g) the pre-close completeness check.
- `escalation-register-entries.md` — the chapter-9 register entries per the trigger / owner / what-the-analyst-supplies / what-the-analyst-does-not-do template (two class-4 entries plus the chapter-6 class-B observation plus the carry-forward summaries), plus the register-table projection beneath.

Total length: roughly 2,500–3,500 words across the two files. A reviewer should be able to read both in twenty minutes and see every record acknowledged, every chapter-9 pattern-recognition rule walked, every escalation routed to the correct class with the correct owner, and the 2026-12-18 council briefing-slot ready for `head-of-ai-governance` to read aloud.

## Checkpoint

A mentor, peer, or self-review walk. Answer honestly:

1. **Does the sweep walk every chapter-9 pattern-recognition rule explicitly, including the ones that do not trigger?** Chapter-9 discipline is the full walk; a sweep that silently omits rule 5 because it did not trigger is reading-by-silence, not reading.
2. **Is the two-count on `INV-2026-0512` class-3 incidents correctly recorded as an observation, not a rule-1 escalation?** Chapter-9 rule 1 is *three*, not two; opening a rule-1 escalation on a two-count would be the chapter-9 *overuse-of-pattern-recognition* failure mode and dilutes the council's queue on future triggered rules.
3. **Is the chapter-9 rule 3 result correctly recorded as *approaching* rather than *triggered*?** Rule 3's text names *multiple systems*; the two class-B escalations are both on the same `INV-2026-0512`. The right action is the chapter-6 class-B observation `OBS-2026-LAB02-02`, not a chapter-9 rule-3 class-4 escalation. A sweep that over-escalates here reads the chapter-9 class-vs-chapter-6-class distinction wrong.
4. **Does `ESC-2026-LAB02-01` *join* with `ESC-2026-0455` rather than replacing it?** Chapter-9 carry-forward discipline is that the prior-quarter escalation stays open and the current-quarter sweep's related escalation is a *join*, not a re-open. Joining preserves the age-and-pattern visibility the council needs.
5. **Does `ESC-2026-LAB02-03` correctly route to the governance council rather than to `legal` or the compliance function alone?** Chapter-9 rule 4 is explicitly about the *accountable executive should consider a scope reduction, a re-authorisation review, or a sunset* — the scope question is a council-tier decision; routing it to `legal` or the compliance function alone misses the chapter-9 class-4 character.
6. **Is `OBS-2026-LAB02-02` correctly labelled as a chapter-6 class-B observation, not a chapter-9 escalation?** The distinction is load-bearing — chapter-6 class-B observations attach to PMS summaries and control-status reports as technical signals; chapter-9 escalations go on the `ESC-<year>-<sequence>` register with a module tag. Confusing the two inflates the register and dilutes the council's read.
7. **Does the 2026-12-18 council briefing-slot summary name specific decisions the council is asked to take?** Chapter-9 class-4 discipline is that the analyst supplies *the specific decision being asked*; a briefing that reads *"the council to review"* is an abdication of the analyst's framing responsibility.
8. **Does the carry-forward of `ESC-2026-0431` honestly flag the 71-days-open age?** Chapter-9 *registers-that-grow-without-triage* discipline requires the age to be visible; a carry-forward that reads *"status: open"* without the age masks the approaching-threshold signal.
9. **Does any register-table row fabricate a sub-process or a decision beyond what chapter 9 specifies?** The analyst files; the council decides; the specialist acts. A register-table row that reads *"analyst-to-approve"* or *"analyst-to-draft-policy"* has crossed the chapter-9 delegation boundary.
10. **Is the sweep's framing consistent with chapter-09's *pattern-recognition rules turn recurring incidents into policy-work signals* line?** The signals the sweep surfaces are policy-work signals for `senior-ai-governance-architect` and `head-of-ai-governance`; the analyst does not propose the policy. A sweep that reads *"the control should be X"* has crossed the boundary.

If any of the ten is "no", revise *that artefact* before considering the lab done.

## Why this is a lab, not an exercise

The module's four exercises each drill the *within-incident* authoring — exercise 01 classifies twelve intake tickets; exercise 02 composes one `INC-<year>-<sequence>` record across intake, triage, post-mortem, and closure; exercise 03 composes a monthly monitoring-reading note for one system; exercise 04 composes a quarterly PMS summary plus an Article 73 notification draft for one high-risk system. None of them asks the analyst to walk a *rolling-quarter cross-incident view* across six records on four inventory rows and apply the chapter-09 pattern-recognition rules — the specific analyst act that converts a set of individually-well-handled incidents into the council-visible pattern the enterprise can act on. This lab is that specific sweep. The failure mode it prevents is the analyst who can author every within-incident artefact in isolation but has never once walked a cross-incident set with the chapter-09 pattern-recognition rules against the board — and who, under pressure of a quarter-end council slot, either silently over-escalates (opening a rule-1 class-4 on a two-count on `INV-2026-0512`, inflating the register), silently under-escalates (missing rule 2's three-class-5-across-three-RAG-tools pattern because each individual incident closed cleanly), or silently misclasses (filing `OBS-2026-LAB02-02` as a chapter-9 class-2 instead of a chapter-6 class-B observation, confusing the register with the PMS-summary attachments).
