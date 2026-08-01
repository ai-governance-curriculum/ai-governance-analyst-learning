# Exercise 02 — ISO/IEC 23894 Risk Sources Overlay

**Estimated effort:** 2 hours
**Grounding chapter:** [02 — Overlaying ISO/IEC 23894 Risk Sources on the MAP Walk](../02-iso-23894-risk-sources-overlay.md)

## Objective

Take the MAP walkthrough from exercise 01 and apply the two-lens sweep — NIST GenAI Profile risks plus ISO/IEC 23894 risk-source categories — to convert MAP 5 impacts into a first-draft register-entry set. The output is a small, defensible risk register that carries three anchors per row (NIST subcategory + GenAI Profile risk + ISO 23894 risk source) and enough shape to route in exercise 03.

After this exercise you should be able to defend a completed register at a technical review with the answer *"here is the impact; here is the taxonomy hook; here is the source lens; here is the subcategory that identified it"* — and hold that shape without paraphrasing.

## Prerequisites

- Exercise 01 completed. This exercise consumes your `mod-103-ex-01-map-walkthrough.md` output — bring it forward. If you have not done exercise 01, do it first.
- Chapter 02 (this module) read.
- The [NIST AI RMF Generative AI Profile (AI 600-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) 12 risks open — you will cite them by name (Confabulation, Data Privacy, Value Chain and Component Integration, etc.).
- The [ISO/IEC 23894:2023 abstract](https://www.iso.org/standard/77304.html) open; if you have licensed access to the full text, use it — otherwise use the paraphrased category list from chapter 02 and mark verbatim quotations as `<!-- needs-research: -->`.
- Optional: the [ISO 31000:2018 abstract](https://www.iso.org/standard/65694.html) to remind you where the AI-specific overlay sits in the larger risk-management standard family.

## Problem statement

Working from the MAP walk you produced in exercise 01, do a two-lens sweep and produce a **register-entry set** for the system.

### Part 1 — the taxonomy scan

For each of the eight paraphrased ISO 23894 risk-source categories (Complexity of AI systems; Life-cycle stage; Level of automation; Machine-learning risks; System hardware and software; Deployment context; Human factors; Environmental factors), produce a short row:

- **Applies to this system?** Yes / No.
- **If yes,** one-line description of the source in *this* system's context — not the standard's language, the analyst's paraphrase for this system.
- **If no,** one-line justification. "No" is a valid, audit-defensible answer when the reasoning is present.

Do this for each of the 12 GenAI Profile risks as well. Same shape: applies yes / no; if yes, one-line description in this system; if no, one-line justification.

That is a **20-row scan sheet** (8 ISO categories + 12 GenAI risks) which is the audit-facing evidence that the analyst did in fact ask every category.

### Part 2 — the register entries

Take every MAP 5 impact from exercise 01 (four or more entries) and expand each into a register-entry row with the field set from chapter 02:

- **Risk ID** — e.g., `RR-2026-0301`, `RR-2026-0302`, ...
- **System** — the system name from exercise 01.
- **Risk title** — one line.
- **Description** — two to three sentences.
- **GenAI Profile risk(s)** — one or more of the 12 risks; use the Profile's exact name.
- **ISO 23894 risk source(s)** — one or more of the eight categories; paraphrase permitted.
- **NIST RMF subcategory anchor** — the MAP subcategory that identified this risk (e.g., MAP 5.1, or MAP 4.1 for third-party-driven risks).
- **Owner (proposed)** — the routing table hint from chapter 03 of this module; leave as a proposal for now — exercise 05 tightens the routing.
- **Inherent likelihood / magnitude** — ordinal (Low / Medium / High), each with a one-line rationale. (You will score residual in exercise 03.)
- **Proposed mitigation category** — one of preventive / detective / corrective / transfer / accept, with a one-line proposal.
- **Status** — `proposed`.
- **Evidence link(s)** — to the incident you cited in exercise 01, or to any internal artefact if one applies.

### Part 3 — cross-lens diff

Write a short reflection (5–10 sentences) on what the ISO 23894 lens surfaced that the GenAI Profile lens *alone* did not, and vice versa. This is the point of the two-lens sweep. If neither lens surfaced anything the other missed, you probably have not been asking the questions independently.

## Requirements

- **The scan sheet is a real table.** Twenty rows across the two lenses, with the yes / no and one-line reasoning for each. Any "no" without a one-line reason is a fail.
- **At least four register entries.** More is fine; the shape has to hold. Every entry carries all three taxonomy anchors — MAP subcategory, GenAI Profile risk, ISO 23894 source. Missing an anchor is a fail.
- **Every entry has an inherent likelihood and magnitude claim.** Ordinal with rationale. Residual is a later pass; do not pre-empt it here.
- **Every entry proposes one mitigation category.** Preventive / detective / corrective / transfer / accept. If you catch yourself picking two, pick the primary and keep the deliverable clean; a longer mitigation list is exercise 03.
- **The cross-lens diff is written down.** Five to ten sentences. This is the artefact that says "the sweep was actually two-lens, not one-lens with post-hoc labels."
- **Traceability to exercise 01 is intact.** Register-entry Risk ID → MAP impact (from exercise 01) → intake row → framework anchor. A reviewer should be able to follow the chain.
- **No fabricated Profile risks, ISO categories, or subcategory numbers.** If uncertain about the ISO category verbatim, use the paraphrase from chapter 02 and add `<!-- needs-research: verify the exact clause title of ISO/IEC 23894:2023 X.Y before external citation -->`.

## Starter guidance

- Do the ISO 23894 scan first for every impact — force yourself into the source-lens frame before you look at GenAI Profile hooks. If you start with the Profile you tend to see "Confabulation" everywhere and miss the deployment-context and human-factors sources.
- The **Human factors** category is where the analyst-fresh-from-checklist most often under-invests. Over-reliance, automation bias, unclear handoff, and deskilling apply to almost every assistive system. Do not skip it because "the human always reviews" — the human *review* is the mitigation, not a reason the source does not exist.
- The **Life-cycle stage** category is where slow-burn risks (homogenisation, drift, calibration decay) surface. Static systems have this too — the source category still applies.
- For the GenAI Profile lens, remember risk #12 (Value Chain and Component Integration). It fires on any system with a third-party model, retrieval provider, or embedding provider — which in practice is every system in the CareTriage / CreditBoost / SkillMatch set from exercise 01.
- Do not attempt to score residual in this exercise. If you catch yourself writing residual claims, park them for exercise 03. The mental discipline of *first enumerate; then score* is what makes exercise 03 fast.
- If the scan surfaces a risk the MAP walk missed, that is exactly what the overlay is for. Update the MAP walk output (annotate it, do not silently rewrite) and add the register entry.

## Acceptance criteria

- A `mod-103-ex-02-scan-sheet.md` with the 20-row two-lens scan (8 ISO categories + 12 GenAI Profile risks), each row carrying an applies-yes/no and a one-line justification either way.
- A `mod-103-ex-02-register.md` with at least four register entries, each carrying the full field set described above, each with all three taxonomy anchors, each with an inherent claim and rationale, each with one proposed mitigation category.
- Traceability from register entries to the MAP walk from exercise 01 (Risk ID → MAP impact ID or MAP subcategory reference).
- A cross-lens diff of 5–10 sentences at the bottom of the register file (or in a separate `mod-103-ex-02-diff.md`).
- Any uncertain ISO or GenAI Profile citation marked `<!-- needs-research: -->` rather than fabricated.

## Stretch goals

- **A register template.** Extract the register-row shape into an empty template file (`mod-103-ex-02-register-template.md` or a `register.yaml`) that a peer could fill in for a different system.
- **Second-system pass.** Run the two-lens sweep against a *second* intake from exercise 01 (or a hypothetical you author). This is where the analyst reflex gets fluent — the first system takes an hour, the fifth takes fifteen minutes.
- **ISO 23894 clause-level citation.** If you have licensed access to the standard, tighten the ISO citations to clause and sub-clause level; note which paraphrases in your register would need verbatim replacement before external filing.
- **Add controlled-vocabulary tags.** Author a short controlled vocabulary for the "risk title" field (a set of ~20 titles the register will draw from repeatedly — Confabulation, Data leakage, Adversarial prompt injection, Homogenisation, IP contamination, Vendor concentration, etc.). This keeps register entries comparable across systems.
- **Cross-reference to enterprise controls.** If you know your target enterprise's control library, map each proposed mitigation category to a specific enterprise control ID as a fifth column. This is preview work for `mod-108`.

## Deliverables

- `mod-103-ex-02-scan-sheet.md` — the 20-row two-lens scan.
- `mod-103-ex-02-register.md` — the at-least-four register entries.
- Optional `mod-103-ex-02-diff.md` or the cross-lens diff embedded in the register file.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The solutions repo works from the reference exercise 01 (CareTriage Chat) and produces a five-entry register with a full 20-row scan. Your register will differ — different system, different impacts, different scan outcomes. What is graded is (a) whether every register entry carries the three anchors; (b) whether the scan sheet is complete with a reason on every row (including the no rows); (c) whether the cross-lens diff shows real thinking; (d) whether the traceability from register → MAP → intake holds. A register that lands on plausible entries with no scan sheet behind it is a weaker deliverable than one with fewer entries and a rigorous sweep.
