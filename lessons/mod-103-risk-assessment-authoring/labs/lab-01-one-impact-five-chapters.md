# Lab 01 — One MAP 5 Impact, Walked Through All Five Chapters

**Duration:** 2 hours.
**Grounding chapters:** [01](../01-nist-rmf-map-walkthrough.md), [02](../02-iso-23894-risk-sources-overlay.md), [03](../03-genai-profile-scoring-and-register-entry.md), [04](../04-sr-11-7-shape-for-financial-services.md), [05](../05-routing-residuals-and-executive-framing.md).
**Difficulty:** Core — threads all five chapters through a single artefact.

## Objective

Take **one** pre-written MAP 5 impact on **one** fixed system and walk it end-to-end through every chapter's mechanics: impact-framing shape (ch 01) → two-lens overlay (ch 02) → three-column scoring with proposed controls (ch 03) → SR 11-7 pillar mapping and FSI inventory-row extension (ch 04) → routing packet, negotiation stub, and the one-line executive mention (ch 05). Produce a single `impact-walk.md` artefact that reads like the first-draft trace of a single risk from MAP 5 to the executive summary.

The module's exercises each exercise *one* chapter's mechanics on a batch of inputs — exercise 01 walks the whole MAP 1–5; exercise 02 produces a 20-row two-lens scan sheet plus a register of four or more entries; exercise 03 scores the whole register with inherent / residual / control-defeated and a profile summary; exercise 04 produces a seven-section SR 11-7 overlay on a chosen FSI use case; exercise 05 runs the full routing round against the whole scored register. This lab is the inverted shape — *one* impact, *five* chapters chained — so the analyst feels every anchor fire on the same row without losing the thread between stages. It is the integration muscle an analyst actually uses when a reviewer asks "walk me through this one entry end-to-end."

## Prerequisites

- All five chapters read.
- Exercises 01 and 02 completed, or at minimum read, so the MAP walk and the two-lens overlay mechanics are not being learned here.
- A markdown editor.

## The fixed input

Use *exactly* this impact description on *exactly* this system — do not substitute. A fixed input lets you compare your walk to the chapter-anchored expected shape in the checkpoint section.

> **System.** CreditBoost Explainer, v0.9.0 (pre-production). US-federally-chartered mid-size bank (OCC-supervised).
>
> **Purpose.** Generates the plain-language explanation attached to an adverse-action notice when the bank's existing credit-decisioning model declines an application. Fully automated on the generation step; the underlying decision is not touched. Users: denied credit applicants (external) and a compliance analyst who samples 5% of outputs weekly (internal).
>
> **System shape.** Prompted use of a hosted foundation model (Vendor V) with structured input drawn from the separate, non-AI credit-decisioning model's reason codes. No personally-identifying application content is passed in the prompt; applicant name and case ID only.
>
> **The MAP 5 impact (pre-written, framed per chapter 01's shape).**
>
> *Type of harm:* a generated explanation misstates the principal reasons for the adverse action — e.g., it paraphrases a reason code into language that does not meet the "specific" and "accurate" test the regulation requires.
>
> *Affected population:* denied applicants (disproportionately first-time applicants, thin-file borrowers, and applicants in protected classes where disparate-impact review is already a live concern).
>
> *Plausible mechanism:* the hosted LLM confabulates a nearby-but-wrong reason, or paraphrases a technically-correct reason into language a reasonable applicant cannot act on. Weekly 5% sampling catches some but not most instances.
>
> *Likelihood-and-magnitude claim:* likelihood Medium under normal operation (confabulation on reason-code paraphrase is observed in evaluation at a non-trivial rate); magnitude High per realised instance (ECOA / Regulation B adverse-action-notice compliance exposure, plus CFPB Circular 2022-03 adverse-action-notification scrutiny for complex-algorithm decisions).
>
> *NIST MAP anchor:* MAP 5.1.

Treat the pre-written framing as *given* — do not re-author it. The lab starts from this framing and carries it through the five stages. If, during the walk, you find the framing needs a correction, annotate the correction but do not silently rewrite.

## Steps

### Step 1 — Scaffold the artefact (10 min)

Create the working folder and file.

```bash
mkdir -p ~/aicg-labs/mod-103-lab-01
cd ~/aicg-labs/mod-103-lab-01
touch impact-walk.md
```

Open `impact-walk.md` and lay in the five section headers up front:

```markdown
# Impact walk — CreditBoost Explainer v0.9.0 — adverse-action explanation misstatement

## 1. MAP framing (chapter 01) — the impact as cited
## 2. Two-lens overlay (chapter 02) — GenAI Profile + ISO 23894
## 3. Scored register entry (chapter 03) — inherent, residual, control-defeated, controls
## 4. SR 11-7 overlay (chapter 04) — FSI framing for this entry
## 5. Routing and executive mention (chapter 05) — packet, negotiation stub, one-line framing
```

The scaffolded order matters: chapter 01's framing first, then the overlay, then the scoring, then the SR 11-7 shape (the system is at a US-federally-chartered bank — SR 11-7 fires), then the routing round. Walking out of order is where real analysts drift — follow the scaffold.

Add a one-line `Analyst / date:` entry at the top so the artefact is time-stamped.

### Step 2 — Fill section 1: cite the MAP framing (15 min)

Copy the pre-written framing into section 1, verbatim, but *as a cited artefact*: preserve the four-part shape and name each part. Use the exact chapter 01 vocabulary — *type of harm; affected population; plausible mechanism; likelihood-and-magnitude claim; MAP subcategory anchor*. Do not edit the framing.

Below the framing, add two sub-sections:

- **Why this is MAP 5.1 and not another subcategory.** One or two sentences citing chapter 01's description of MAP 5.1 as the *likelihood and magnitude of each identified impact* subcategory, including the chapter's note that MAP 5 draws on public incident reports where available.
- **Supporting evidence options.** List one or two *plausible* evidence sources the register entry could cite — the [AI Incident Database](https://incidentdatabase.ai/) or the [OECD AI Incidents Monitor](https://oecd.ai/en/incidents) search for adverse-action-notice or algorithmic-explanation incidents, or an internal eval report. If you do not know a specific incident, mark it as `<!-- needs-research: search AIID for adverse-action-notice explanation misstatement incidents to cite in register-entry evidence field -->` rather than inventing one.

Chapter 01 is explicit that fabricating incidents is a fail. Be disciplined.

### Step 3 — Fill section 2: apply the two-lens overlay (20 min)

Open chapter 02 in a second window. Author section 2 as *two* mini-passes, in order — do the ISO 23894 pass *first*, then the GenAI Profile pass, per the chapter's starter guidance ("If you start with the Profile you tend to see 'Confabulation' everywhere and miss the deployment-context and human-factors sources").

**Pass 1 — ISO 23894 risk-source categories applied to this impact.** For each of the eight paraphrased categories from chapter 02, write one line: *applies / does not apply*, with a one-line reason either way. The eight categories: Complexity of AI systems; Life-cycle stage; Level of automation; Machine-learning risks; System hardware and software; Deployment context; Human factors; Environmental factors.

Two field-level tripwires to watch:

- **Level of automation.** The explanation-generation step is fully automated; the underlying credit decision is not touched. The chapter's rule is that risk correlates with autonomy. Is the automation-level source "applies" or "does not apply" for *this* impact? Write the reasoning.
- **Human factors.** The weekly 5% compliance sample is a human review loop. The chapter's starter guidance warns not to skip human factors because "the human always reviews" — the review *is* a mitigation, not evidence the source does not exist. Write the reasoning.

**Pass 2 — GenAI Profile risks applied to this impact.** Name every applicable Profile risk with a one-line description in the system's context. Chapter 02's example shows that one entry can tie to multiple Profile risks. For *this* impact, at minimum consider: Confabulation (risk #2), Information Integrity (risk #8), Harmful Bias or Homogenization (risk #6 — because the affected population skews toward protected classes), and Value Chain and Component Integration (risk #12 — because Vendor V is the hosted model provider). For each, decide applies / does not apply and write the one-line reason.

At the end of section 2, write a one-sentence **cross-lens diff** stating what the ISO 23894 lens surfaced that the GenAI Profile lens alone would have missed (or vice versa). Chapter 02's rule: "if neither lens surfaced anything the other missed, you probably have not been asking the questions independently."

### Step 4 — Fill section 3: score the register entry (25 min)

Open chapter 03 in a second window. Author section 3 as a single register entry with every field chapter 03 requires.

**Field list** (copy chapter 02's minimum-viable register-row shape, carry chapter 03's scoring columns):

```markdown
- **Risk ID:** RR-2026-0501 (lab-fabricated).
- **System:** CreditBoost Explainer, v0.9.0.
- **Risk title:** Adverse-action explanation misstatement.
- **Description:** ...
- **GenAI Profile risk(s):** ... (from section 2 pass 2)
- **ISO 23894 risk source(s):** ... (from section 2 pass 1)
- **NIST RMF subcategory anchor:** MAP 5.1.
- **Owner (proposed):** ... (use the chapter 03 routing table)
- **Inherent:** likelihood × magnitude, one-line rationale.
- **Residual:** likelihood × magnitude, one-line rationale.
- **Control-defeated:** likelihood × magnitude, one-line rationale.
- **Load-bearing control (named):** ...
- **Proposed controls by category:** preventive / detective / corrective / transfer / accept.
- **Status:** proposed.
- **Evidence link(s):** ... (or needs-research marker)
```

Three field-level tripwires to watch:

- **Owner.** Chapter 03's routing table places confabulation and groundedness with the *product owner* and *bias / disparate impact* with the *product owner + legal (EEOC / LL 144 / disparate-impact overlays)*. This entry carries both patterns. Chapter 03 says the register entry is not complete until the owner is named — write the owner explicitly, not "TBD".
- **Three ordinal columns.** Score *inherent first*, before you look at the controls. Score *control-defeated before residual* per chapter 03's discipline — if you know the control-defeated case is High × High you will not lazily land the residual at Low × Low. Name the load-bearing control by name (not "controls").
- **Control categories.** Chapter 03 says High-magnitude entries carry at least one control per applicable category (preventive / detective / corrective). This entry is High-magnitude — a single-category proposal would be under-cooked. The compliance-analyst weekly sample is a *detective* control; what *preventive* and *corrective* controls does the entry also need? (Reason-code grounding templates; a correction-and-reissue runbook for a misstatement that has already been mailed.)

Every ordinal claim carries a one-line rationale. No naked ordinals. No "Medium because it feels right."

### Step 5 — Fill section 4: apply the SR 11-7 overlay (25 min)

Open chapter 04 in a second window. The system is at a US-federally-chartered bank; SR 11-7 fires. Author section 4 as the *per-entry* slice of chapter 04's seven-section overlay — exercise 04 produces the full seven-section document; this lab produces the slice as it applies to *this one entry*.

Required sub-sections:

**4.1 Model-definition check.** One or two sentences confirming CreditBoost Explainer meets the SR 11-7 model definition ("a quantitative method, system, or approach that applies statistical, economic, financial, or mathematical theories, techniques, and assumptions to process input data into quantitative estimates"). Chapter 04 notes the definition is broad; the system qualifies. Write the trigger clause you relied on.

**4.2 Pillar mapping, this entry only.** A three-row table: for each SR 11-7 pillar (development / implementation / use; independent validation; governance), name the NIST AI RMF subcategory and the ISO/IEC 42001 clause that satisfies the pillar *for this risk entry* — not for the whole system. Use chapter 04's mapping table as the starting template. For the specific-artefact column, either name a plausible enterprise artefact (e.g., "MRM validation report VR-2026-0044 draft") or mark as a gap with a routing (`gap — routed to MRM lead <name>, due <date>`).

**4.3 Materiality tier for this entry.** Chapter 04's materiality lens is three-way: decision materiality, regulatory materiality, customer-impact materiality. Score each on a line and write a two-sentence conclusion. Tripwire: this is an *assistive* system on the generation step and the underlying credit decision is not touched. Chapter 04's evaluation note warns against treating "the model is assistive" as a reason to under-tier — CFPB 2022-03 explicitly does not. Score the tier honestly.

**4.4 Developer / validator independence.** Name the developer (the ML team / platform team that configured the prompts and built the reason-code grounding) and the validator (the MRM group). State the evidence of independence — reporting-line independence, funding independence, challenge authority. If any is weak, name the compensating control. Fabricate team names if you have to, but flag them as fabricated at the bottom of section 4.

**4.5 Overlays beyond SR 11-7, applied to this entry.** List the overlays the chapter names where they fire on *this specific risk*:

- OCC 2023-17 third-party relationships — Vendor V is the hosted model.
- OCC 2020-10 — if third-party model use adds validation complications.
- ECOA / Regulation B — the explanation is regulated content in an adverse-action-notice path.
- CFPB Circular 2022-03 — adverse-action-notification requirements for complex-algorithm decisions.
- NIST GenAI Profile — the AI-specific gap SR 11-7 does not cover (confabulation, specifically).

For each, one line on what it adds for this entry.

**4.6 FSI-extended inventory-row fields, this entry only.** Six fields from chapter 04's FSI-extended inventory shape: model tier / materiality rating; validation status (pre-validation / conditionally approved / approved / suspended / retired); last validation date; next validation due; validator name; assumptions and limitations. Populate as `pending — routed to MRM lead <name>, due <date>` for any field not yet resolvable, per chapter 04's discipline.

### Step 6 — Fill section 5: routing and the executive mention (20 min)

Open chapter 05 in a second window. Author section 5 in three parts.

**5.1 Routing packet (this entry only).** Chapter 05 names the packet field list. Write one packet for RR-2026-0501:

- Register ID and system link (lab-fabricated — note as such).
- Risk title + one-paragraph description.
- The three taxonomy anchors (NIST MAP 5.1 + GenAI Profile risks + ISO 23894 sources).
- Inherent, proposed residual, and control-defeated with rationales (from section 3).
- Proposed controls by category (from section 3).
- The specific ask (chapter 05's five options: accept the residual as claimed; propose alternate controls; contest the routing; accept the risk with rationale; escalate).
- SLA (five business days for acknowledgement; two weeks for substantive response — chapter 05 default).
- Analyst contact (you).

**5.2 Negotiation stub.** Chapter 05 names three characteristic pushback shapes. Pick *one* to simulate on this entry — the one you find most plausible for a CreditBoost Explainer owner. Write a short three-turn exchange: (a) owner response in owner voice; (b) analyst reply; (c) register update (residual re-scored / control added / routing changed / no change). Flag fabricated owner names explicitly. This is a stub, not a full negotiation log — exercise 05 writes the full log; this lab only observes one turn.

**5.3 Executive mention.** Chapter 05's one-page executive framing reports the register profile for the whole system, not one entry per line. Author one to two sentences of executive copy *about this entry only*, in the voice the executive framing uses — e.g., "The highest-residual-and-highest-magnitude entry on this system is the adverse-action explanation misstatement risk (residual Low × High; control-defeated Medium × High if the weekly compliance sample lapses or misses a misstatement pattern). The ECOA / Regulation B and CFPB Circular 2022-03 overlay drive the magnitude." Respect the three do-nots: no aggregated single score, no legal-opinion language ("compliant with Regulation B"), no release-sign-off language ("safe to launch").

### Step 7 — Cross-check the five sections (10 min)

Walk the five sections side-by-side. Every value that appears on more than one section must be identical across all of them. High-tripwire fields:

- **The impact framing.** Section 1's four-part framing is the source; section 2's overlay must reference the same mechanism and population; section 3's description must not drift from the framing.
- **Three taxonomy anchors.** Section 2 enumerates the GenAI Profile risks and ISO 23894 sources; section 3's register entry carries the same enumeration; section 5's packet repeats them. Any drift between sections 2, 3, and 5 is a bug.
- **The three ordinal columns.** Inherent / residual / control-defeated from section 3 appear again in section 5's packet. Silent drift here is the common failure mode the routing round catches — fix it here, not there.
- **Owner.** Section 3's proposed owner, section 4's developer/validator split, section 5's packet addressee must line up. If section 3 proposes "Consumer Lending Product (product owner, with Legal secondary)" and section 5's packet addresses only "Legal", the register is already drifting.
- **Load-bearing control.** Section 3 names it; section 5's control-defeated rationale in the packet must name the same control.

Any mismatch is a bug — fix it before the artefact is considered complete.

### Step 8 — Self-check (5 min)

Walk the artefact top-to-bottom and verify:

- Every NIST AI RMF subcategory, Annex / Article reference, ISO clause, ISO 23894 category, GenAI Profile risk, and SR 11-7 pillar number is sourced from the chapter it appears in or marked `<!-- needs-research: ... -->`. Do not invent subcategory codes, pillar numbers, or risk names.
- The three do-nots from chapter 05 are respected in section 5.3: no aggregated single score, no legal-opinion language, no release-sign-off language.
- Any fabricated owner, team, date, or placeholder ID is flagged at the bottom of the file in a *Fabrication note* block, per chapter 05's discipline.
- No *second* register entry has crept in. This lab is one impact — a second entry means you have drifted into exercise 02 or exercise 03 scope.

## Expected output

One markdown file in `~/aicg-labs/mod-103-lab-01/`:

- `impact-walk.md` — five populated sections (plus optional fabrication note), one timestamp, one named analyst.

Total length: roughly 1,200–2,000 words. A senior reviewer or governance lead should be able to read it in ten minutes and either accept the entry as drafted or push back on specific fields.

## Checkpoint

A mentor, peer, or self-review walk. Answer honestly:

1. **Did the impact framing from section 1 survive unchanged into sections 2, 3, and 5?** Chapter 01's four-part shape (*type × population × mechanism × likelihood-and-magnitude*) is the source. If the mechanism drifted ("confabulation of a reason code" in section 1 → "LLM hallucination" in section 3 → "content-safety failure" in section 5), the walk is already incoherent before downstream reviewers see it.
2. **Are the three ordinal columns actually separate?** Chapter 03's discipline: inherent is not silently equal to residual; residual is not silently equal to control-defeated. If all three columns carry the same ordinal pair, you have collapsed the discipline and the reviewer will catch it. For this impact, inherent is roughly Medium × High (confabulation is Medium-likelihood under normal operation; magnitude is High because of the ECOA / CFPB exposure); residual should be lower on likelihood (reason-code grounding + prompt constraints + weekly sampling) but magnitude does not move; control-defeated should rise on likelihood (if the weekly sample lapses) with magnitude staying High.
3. **Did you pick the load-bearing control honestly?** The compliance-analyst weekly sample is a *detective* control. If the preventive controls (reason-code grounding, prompt-template constraints) are the primary residual driver, the load-bearing control is one of those — not the detective. Chapter 03 is strict: the load-bearing control is *the control whose failure moves the residual to the control-defeated case*, not the easiest-named control.
4. **Did you under-tier the SR 11-7 materiality?** Chapter 04's evaluation note is explicit: "the model is assistive" is not a reason to under-tier an adverse-action-notice-path system. A Low-materiality claim on this entry needs a written defence citing decision materiality, regulatory materiality, and customer-impact materiality. If you wrote Low without that defence, revise.
5. **Did you respect the three do-nots in section 5.3?** No single aggregated score. No "compliant with Regulation B" language (use "ECOA / Regulation B adverse-action-notice obligation is in scope and findings are being driven to closure" or equivalent). No "safe to release" (use "acceptable-to-proceed pending evaluation-engineer sign-off and MRM validation approval" or equivalent). If any of the three slipped in, revise section 5.3 only — do not rewrite the whole page.

If any of the five is "no", revise *that section* before considering the lab done.

## Why this is a lab, not an exercise

Exercise 01 produces a whole MAP walk across MAP 1 through MAP 5 for a chosen intake. Exercise 02 produces a 20-row two-lens scan sheet and a register of four or more entries. Exercise 03 scores the whole register and writes the profile summary. Exercise 04 produces the full seven-section SR 11-7 overlay. Exercise 05 drives the whole scored register through a full routing round with three pushback shapes and a one-page executive framing.

This lab inverts the shape. It takes *one* impact — pre-written in chapter 01's framing shape — and chains all five chapters' mechanics against it on a single page, with cross-section consistency enforced. The failure mode an analyst actually has in review is not "cannot walk MAP 1 through MAP 5" or "cannot produce a 20-row scan". It is "walks one impact from MAP 5 to the executive framing and the mechanism, the population, the GenAI Profile anchor, the load-bearing control, and the materiality tier each drifted silently between sections". This lab exercises the cross-section consistency that the module requires and the exercises — each anchored in one chapter at a time — do not directly test.
