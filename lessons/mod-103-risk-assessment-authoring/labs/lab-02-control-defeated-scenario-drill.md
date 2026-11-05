# Lab 02 — Control-Defeated Scenario Drill on a Fixed Scored Entry

**Duration:** 90 minutes.
**Grounding chapters:** [03](../03-genai-profile-scoring-and-register-entry.md) (inherent / residual / control-defeated; load-bearing control; mitigation categories), [05](../05-routing-residuals-and-executive-framing.md) (executive framing of control-defeated exposure).
**Difficulty:** Core — guided walkthrough of a single scored entry under four distinct control-failure scenarios.

## Objective

Take a **fixed, pre-scored** register entry and recompute its three ordinal columns under **four distinct control-failure scenarios**. Produce a single scenario table that shows how residual and control-defeated move as each named control fails in turn, identify which control is actually load-bearing, and author the one-sentence executive-framing mention for the highest-exposure scenario. The output is the discipline muscle for chapter 03's three-column split and chapter 05's control-defeated executive callout.

Exercise 03 scores a whole register and asks for one control-defeated claim per entry. Exercise 05 runs the register through a routing round with three characteristic pushback shapes. Neither exercise *stress-tests* the control-defeated column across multiple failure modes on a single entry. This lab fills that gap: four failure scenarios on one entry, with the three columns recomputed each time. It is the muscle an analyst uses when a reviewer asks the sharpest version of the control-defeated question — "what happens if *this specific* control fails instead of the one you wrote down?"

## Prerequisites

- Chapters 03 and 05 read.
- Exercises 02 and 03 completed, or at minimum read, so the register-row shape and the 3×3 scoring grid are not being learned here.
- A markdown editor.

## The fixed input

Use *exactly* this scored register entry — do not substitute. A fixed entry lets the lab's expected scenarios line up with the chapter-anchored expected shape in the checkpoint section.

> **RR-2026-0215 — Data leakage in prompts.**
>
> *System:* Marketing Copy Draft Assistant (MCDA), v1.3.2. Internal, assistive, hosted foundation model (Vendor V). Vendor P provides prompt-management SaaS.
>
> *GenAI Profile risk(s):* Data Privacy (#4).
>
> *ISO 23894 risk source(s):* Deployment context (training-time assumption does not match deployment reality); Human factors (users may paste more into a prompt than they realise).
>
> *NIST RMF subcategory anchor:* MAP 5.1.
>
> *Owner:* Privacy + Security.
>
> *Inherent:* Likelihood Medium (users paste unreleased brief content into prompts under normal operation). Magnitude High (Vendor V sees pre-release product strategy).
>
> *Proposed controls.*
>
> - **C1 — Preventive:** PII / confidentiality scanner on prompts pre-flight. Scans the prompt before it leaves the enterprise boundary; blocks on known-confidential patterns (release dates, codenames, unreleased SKUs).
> - **C2 — Preventive:** User-facing prompt-hygiene guidance in the Marketing team's onboarding doc.
> - **C3 — Detective:** Prompt audit-log review (monthly) by Security.
> - **C4 — Transfer:** Vendor V contract clause on confidentiality of customer prompt content (does *not* indemnify for enterprise's own leakage, only vendor-side disclosure).
>
> *Residual:* Likelihood Low. Magnitude High.
>
> *Control-defeated (as drafted — single-control case):* if C1 (the scanner) is bypassed or misses a novel confidentiality pattern — Likelihood Medium. Magnitude High.
>
> *Load-bearing control (as drafted):* C1 — PII / confidentiality scanner on prompts pre-flight.

This is the MCDA Data-leakage entry from chapter 03's worked example, lifted verbatim so the input is grounded in a chapter artefact. Do not re-author it.

## The four scenarios

Compute the three ordinal columns (inherent / residual / control-defeated) under each of the four scenarios below. Scenario A is the drafted shape — your job is to confirm it, not re-score it. Scenarios B, C, and D are the stress tests.

| Scenario | Shape |
|---|---|
| **A — as drafted** | Every proposed control fires as designed. This is the residual column from the fixed input. Reconfirm it so you have a baseline before you perturb. |
| **B — scanner fails silently** | C1 (the PII / confidentiality scanner) misses a novel confidentiality pattern — a new product codename the pattern library has not been updated for. C2, C3, C4 fire as designed. Recompute. |
| **C — scanner fails *and* audit-log review lapses** | C1 fails as in scenario B *and* C3 (the monthly audit-log review) lapses for two consecutive months (Security staffing turnover). C2 and C4 still fire. Recompute. |
| **D — transfer control is narrower than assumed** | C1, C2, C3 fire as designed, *but* the Vendor V contract clause (C4) turns out not to cover the enterprise's own leakage case — the transfer is narrower than the register assumed. Recompute. |

Each scenario is a *different* perturbation on the same entry. The goal is to see how the three columns move — and which control is actually load-bearing — under each.

## Steps

### Step 1 — Scaffold the artefact (5 min)

Create the working folder and file.

```bash
mkdir -p ~/aicg-labs/mod-103-lab-02
cd ~/aicg-labs/mod-103-lab-02
touch scenario-drill.md
```

Open `scenario-drill.md` and lay in the structure up front:

```markdown
# Control-defeated scenario drill — RR-2026-0215 Data leakage in prompts

## 1. Entry as drafted (reference)
## 2. Scenario A — all controls fire as designed
## 3. Scenario B — scanner fails silently
## 4. Scenario C — scanner fails and audit-log review lapses
## 5. Scenario D — transfer control is narrower than assumed
## 6. Load-bearing-control finding
## 7. Executive mention — highest-exposure scenario
```

Add a one-line `Analyst / date:` entry at the top.

### Step 2 — Copy the entry as drafted (5 min)

Section 1 is a reference. Copy the fixed-input text above into section 1 verbatim — the register entry including the four proposed controls and the three ordinal columns as drafted. Do not edit; the point is to have the baseline visible on the page next to the scenarios.

### Step 3 — Confirm scenario A (10 min)

Scenario A is *as drafted*. Your job is to confirm, not re-score. Write section 2 as:

```markdown
### Scenario A — all controls fire as designed

| Column | Ordinal | Rationale (one line) |
|---|---|---|
| Inherent | Medium × High | Users paste unreleased content under normal operation; vendor exposure to pre-release strategy is High. |
| Residual | Low × High | Scanner catches known patterns; audit-log review surfaces residuals; magnitude unchanged if a leakage still occurs. |
| Control-defeated | Medium × High | If the scanner (C1) is bypassed or misses a novel pattern, likelihood rises to Medium; magnitude unchanged. |

**Confirmation.** Does this match the fixed input? Yes / No — if No, note the drift.
```

Chapter 03's rule: every ordinal carries a one-line rationale. Keep the rationale column populated for every column, every scenario.

### Step 4 — Compute scenario B (10 min)

Scenario B perturbs C1 only. Author section 3 with the same three-row table, recomputed:

- **Inherent** does not change — inherent is before *any* control fires, by chapter 03's definition. Copy the Medium × High row verbatim.
- **Residual** changes meaningfully. C1 is the primary preventive control; if C1 is missing a novel pattern, the residual likelihood rises. The chapter 03 question: is C2 (prompt-hygiene guidance) alone, plus C3 (monthly audit-log review), enough to hold the residual at Low? Argue it on the page. Likely answer: residual likelihood rises to Medium; magnitude is still High. Write the rationale.
- **Control-defeated** also moves. If C1 is *already failed silently* and the question becomes "what if the *next* layer fails too", the control-defeated case is now the C1-and-C3-both-fail case — scenario C. Write that explicitly so the control-defeated column reflects the *next* failure beyond the one scenario B has already assumed.

Tripwire: it is tempting to leave inherent unchanged and residual unchanged and only move control-defeated. That is wrong — scenario B *is* a residual-shift scenario, because residual by chapter 03's definition is "after the controls the analyst *believes will be in place* fire". If the scanner is in fact missing novel patterns under normal operation, the residual claim as drafted is already stale.

### Step 5 — Compute scenario C (15 min)

Scenario C stacks C1 failure and C3 lapse. Both of the main preventive-and-detective pair are off. Author section 4 with the recomputed three-row table:

- **Inherent** still does not change.
- **Residual** under C1-missing and C3-lapsing is substantially higher. C2 (user-facing guidance) and C4 (vendor contract) are both weak controls on this failure path — C2 relies on user compliance under confusion, C4 covers vendor-side disclosure, not enterprise-side leakage. Expect residual likelihood High and magnitude High. Write the rationale.
- **Control-defeated** — if residual is already High × High, the "control-defeated" case is barely different. Write explicitly: "there is no further control to defeat; the entry is effectively at ceiling." This is the state chapter 05 calls out as the *boundary condition* in the executive framing.

Scenario C is the drill's hardest moment. Chapter 03's three-column discipline exists precisely so the analyst can see when an entry *has no slack* — that is, when the drafted residual depends on two controls stacking and both are known-fragile.

### Step 6 — Compute scenario D (10 min)

Scenario D perturbs C4 only — the transfer control turns out not to cover the enterprise's own leakage. Author section 5:

- **Inherent** does not change.
- **Residual** does not change *mechanically* — C1 and C3 are still firing. But chapter 03 is specific that Transfer is "the risk of loss moves to the vendor" — contractual indemnification. If the contract does not cover the enterprise's own leakage, the Transfer control was *miscategorised*: it is a vendor-side-preventive control, not a transfer of the enterprise's residual. Note the correction in the rationale. The residual likelihood stays Low; the *magnitude* may rise, because the enterprise bears the full loss rather than having it transferred.
- **Control-defeated** — same as scenario A for likelihood (scanner remains the load-bearing control); magnitude unchanged.

Tripwire: scenario D is a reminder that a mis-categorised control is a register-integrity bug even when the ordinals do not move much. Chapter 03's rule on Transfer ("Transfer is *not* 'the vendor does it'; it is *the risk of loss moves to the vendor*") catches exactly this pattern.

### Step 7 — Load-bearing-control finding (10 min)

Open section 6. In two to four sentences, name the control that moves the residual the most across scenarios B, C, and D. Answer the question chapter 03 asks: *which control, if it fails, most moves the residual to the control-defeated case?*

The expected finding (which you should write in your own voice, not copy): C1 is the single most load-bearing control — scenario B shows residual moving on C1 failure alone. C3 is the secondary load-bearer — scenario C shows residual jumping from Medium × High to High × High when C3 is also missing. C2 and C4 are weak on this failure path — C2 relies on user compliance, C4 is a mis-categorised transfer. The register as drafted correctly names C1 as load-bearing; the drill confirms it and surfaces C3 as the secondary dependency.

If your finding differs, write out *why* — the drill's value is in the reasoning, not in matching a prescribed answer.

### Step 8 — Executive mention for the highest-exposure scenario (10 min)

Open section 7. Pick the scenario that shows the highest exposure — expected to be scenario C (residual High × High; effectively no further slack). Author one to two sentences in the voice chapter 05's executive framing uses, calling it out as the *boundary condition*:

> Example shape (adapt in your voice): "The boundary condition on the MCDA Data-leakage entry is the case where the pre-flight scanner misses a novel confidentiality pattern *and* the monthly audit-log review lapses — at that point the entry is at Likelihood-High × Magnitude-High with no further control to defeat. The residual profile is acceptable only while both controls are maintained; a two-month gap in the audit-log review is the escalation trigger."

Respect the three chapter-05 do-nots:

- No aggregated single score ("overall MCDA risk is Medium" — prohibited).
- No legal-opinion language ("non-compliant with GDPR" — use "DPIA finding open" or equivalent).
- No release-sign-off language ("not safe to release" — use "acceptable-to-proceed contingent on the two load-bearing controls being maintained; monitor for lapse").

### Step 9 — Self-check (5 min)

Walk the file top-to-bottom and verify:

- Every ordinal claim (inherent / residual / control-defeated, every scenario) carries a one-line rationale. No naked ordinals.
- Inherent is identical across all four scenarios (chapter 03's definition: inherent is before any control fires; scenarios perturb controls, not inherent).
- Residual moves across the scenarios — if your residual is identical in A, B, C, and D, you have collapsed the three-column discipline into one column.
- The load-bearing-control finding in section 6 names *a specific control by ID* (C1, C3), not "controls" or "the scanner" in the abstract.
- Section 7 respects the three do-nots and names a specific escalation trigger (chapter 05's rule: the re-review cadence is not a vague promise; it is a specific trigger).

## Expected output

One markdown file in `~/aicg-labs/mod-103-lab-02/`:

- `scenario-drill.md` — seven populated sections, one timestamp, one named analyst.

Total length: roughly 900–1,400 words. Most of the content is tabular — the lab is a drill, not an essay.

## Checkpoint

A mentor, peer, or self-review walk. Answer honestly:

1. **Did inherent stay fixed across scenarios A, B, C, and D?** Chapter 03's definition is unambiguous: inherent is *before any control fires*. If your inherent column changed between scenarios, you have conflated inherent with residual, which is the single most common scoring mistake. Fix it.
2. **Did residual actually move between scenarios?** If scenarios A, B, C, and D all land at the same residual pair, the exercise did not do its work. Scenario B (C1 fails) should move residual on likelihood; scenario C (C1 and C3 both off) should move it further on likelihood with magnitude at ceiling; scenario D should move it on magnitude via the Transfer re-categorisation. If any of the three did not move, re-read chapter 03's three-column definitions and recompute.
3. **Did you catch the Transfer mis-categorisation in scenario D?** Chapter 03's rule is that Transfer is *the risk of loss moves to the vendor* — contractual indemnification, insurance, shared liability. A vendor operating a control is a *preventive* control, not a transfer. If you left C4 categorised as Transfer in your scenario D write-up without noting the mis-categorisation, revise.
4. **Does section 6 name the load-bearing control by ID, not by abstraction?** "C1 is load-bearing; C3 is secondary" is specific. "The preventive controls are load-bearing" is not. Chapter 03's discipline on naming the control explicitly ("PII / confidentiality scanner on prompts pre-flight" is a load-bearing control; "controls" is not) applies here.
5. **Does the executive mention in section 7 respect the three do-nots?** No aggregated score, no legal-opinion language, no release-sign-off language. If any of the three slipped in, revise section 7 only.

If any of the five is "no", revise *that section* before considering the lab done.

## Why this is a lab, not an exercise

Exercise 03 asks for one control-defeated claim per register entry, computed once. Exercise 05 drives the whole register through a routing round with three characteristic pushback shapes — one of which ("you're too high — we have a control you haven't seen") can move the control-defeated column but does not require the analyst to walk multiple perturbations on a single entry.

This lab is the gap between those two. It takes *one* entry — pre-scored, from the chapter 03 worked example — and perturbs the control set *four different ways*, recomputing the three columns each time. It surfaces the question a sharp reviewer always asks: "what happens if *this specific* control fails instead of the one you wrote down?" The muscle is in computing the move, naming the load-bearing control by ID, and surfacing the ceiling case as a boundary condition in the executive framing — which is where chapter 03's scoring discipline and chapter 05's executive-framing discipline actually meet.
