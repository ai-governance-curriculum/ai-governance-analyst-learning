# Exercise 03 — GenAI Profile Risk Scoring

**Estimated effort:** 2 hours
**Grounding chapter:** [03 — Scoring the Register Entry — GenAI Profile Risks and the Likelihood-Magnitude Pass](../03-genai-profile-scoring-and-register-entry.md)

## Objective

Take the register from exercise 02 and complete the scoring pass — inherent, residual, and control-defeated ordinal claims for each entry, each backed by a one-line rationale, and each with a proposed mitigation set categorised as preventive / detective / corrective / transfer / accept. The output is a fully scored register a routing round (exercise 05) can consume without further rework.

After this exercise you should be able to hold the *three separate columns* discipline under review pressure and translate the register into the profile-based executive framing without collapsing it into a single aggregate score.

## Prerequisites

- Exercise 02 completed. This exercise consumes your `mod-103-ex-02-register.md` output — bring it forward.
- Chapter 03 (this module) read; the 3×3 grid definitions memorised.
- The [NIST AI RMF Generative AI Profile (AI 600-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) 12 risks handy — the suggested-actions sections offer control ideas per risk.
- The [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) MEASURE and MANAGE sections for control-family cues.
- Optional: the [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) for security-flavoured mitigation ideas on prompt-injection / data-leakage entries.

## Problem statement

Working from the register you produced in exercise 02, do the scoring pass. For each register entry produce:

### Part 1 — the three ordinal claims

For each entry, three columns:

- **Inherent** — likelihood × magnitude, before any control fires. Each ordinal (Low / Medium / High) carries a one-line rationale.
- **Residual** — likelihood × magnitude, after the proposed controls fire as designed.
- **Control-defeated** — likelihood × magnitude, if the *load-bearing* control fails, is bypassed, or is silently misconfigured. Name the load-bearing control explicitly.

Every ordinal claim carries a rationale. No naked ordinals. No "Medium because it feels right."

### Part 2 — the proposed control set

For each entry, propose a control set of one to four controls, categorised by:

- **Preventive** — reduces likelihood.
- **Detective** — surfaces the risk when it happens.
- **Corrective** — mitigates the impact when it fires.
- **Transfer** — moves the risk to a third party (indemnification, insurance).
- **Accept** — knowingly retained, with rationale.

At least one entry must use **Transfer** and at least one must use **Accept** — even if you have to reach for an entry where those categories are the honest answer. The point is to practise the framing, not to over-transfer or over-accept.

### Part 3 — the profile summary

Write a *one-page* profile summary of the register (not one entry per line; not an aggregate score). Follow the chapter 03 executive-translation shape:

- **Overall residual profile.** One sentence — how many entries, at what residual severities.
- **Highest-residual concern.** One entry, with the entry title and residual pair.
- **Boundary condition.** The entry whose control-defeated case is the highest; call it out explicitly.
- **The rule you did not break.** State the discipline: no single aggregated system score; the profile *is* the answer.

### Part 4 — a rework note

Write a short (5–10 sentences) note that identifies at least one entry whose residual claim you *changed* between draft and final because either (a) the control you assumed was in place turned out not to be, (b) the control was in place but you had over-credited it, or (c) the control-defeated case forced you to re-examine the residual. This is the entry that will be the most interesting one to negotiate with an owner in exercise 05.

If you cannot honestly identify one entry that shifted, be self-suspicious — the scoring pass usually moves at least one entry, and analysts who never move any are usually not stress-testing their own assumptions.

## Requirements

- **Every register entry has three ordinal columns filled.** Inherent, residual, control-defeated. Each with a one-line rationale.
- **Every entry names the load-bearing control by name.** "PII / confidentiality scanner on prompts pre-flight" is a load-bearing control; "controls" is not.
- **Every entry has a categorised mitigation set.** At least one control per applicable category (preventive / detective / corrective) for High-magnitude entries; single-category proposals are allowed for Low-magnitude entries where honest.
- **At least one entry uses Transfer.** Vendor indemnification is a common landing; state the specific contractual clause you are relying on (or mark `<!-- needs-research: verify Vendor V master agreement clause on training-data indemnification -->` if you do not know).
- **At least one entry uses Accept.** The Accept rationale is written out — what the enterprise is knowingly retaining and why the residual is tolerable.
- **The profile summary is one page or less** (≤500 words) and reports the shape, not a score. Any aggregated number that pretends to summarise "the system's risk" is a fail; the discipline is to report the profile.
- **The rework note is honest.** One entry whose residual moved between draft and final, with the reason. If nothing moved, say so and explain why — but expect the reviewer to probe.
- **No fabricated control names, statute references, or vendor clauses.** Uncertain claims marked `<!-- needs-research: -->`.

## Starter guidance

- Score inherent *first* — before you look at the controls. Force yourself to answer the "if nothing were in place" question, because it is the frame that keeps residual honest. Analysts who go control-first tend to over-credit whatever control they picked and land at a Low residual that dissolves under review.
- Score control-defeated *before* you score residual. This inverts the usual habit and it works: if you know the control-defeated case is High × High, you will not lazily land the residual at Low × Low.
- Use the routing-table hint from chapter 03 as a check on your owner assignment. If your entry's default owner (from exercise 02) does not match the routing-table default and you have not written down why, revisit.
- For the Transfer category, remember that Transfer is *not* "the vendor does it"; it is *the risk of loss moves to the vendor*. Contractual indemnification, insurance, and shared-liability clauses are transfer instruments. A vendor operating a control is a preventive control, not a transfer.
- For the Accept category, write the rationale as though you were the executive signing the acceptance. "We accept this residual because [reason]" — first person, plain language. If the rationale sounds thin, the acceptance is thin.
- Do not aggregate. If the executive summary tempts you to write "overall system risk: Medium", stop. Read chapter 03's executive-translation section again. Report the profile.

## Acceptance criteria

- A `mod-103-ex-03-scored-register.md` with every entry from exercise 02 carrying three ordinal columns (inherent, residual, control-defeated), each with a one-line rationale, and each with a categorised mitigation set.
- The load-bearing control named explicitly for every entry.
- At least one entry uses Transfer with a named contractual mechanism; at least one uses Accept with an executive-voice rationale.
- A `mod-103-ex-03-profile.md` (or embedded section) of ≤500 words following the four-part shape (overall profile, highest-residual concern, boundary condition, no-aggregation rule).
- A rework note of 5–10 sentences identifying at least one entry whose residual moved between draft and final, or an honest note on why nothing moved.
- Every ordinal claim has a rationale; every uncertain claim is marked `<!-- needs-research: -->`.

## Stretch goals

- **Move to a 5×5 grid.** Re-score at least two entries on a 5×5 (Very Low / Low / Medium / High / Very High) and write a paragraph on which entries benefited from the precision and which just added argument surface.
- **Control-family cross-reference.** Map each proposed control to a specific control family — [NIST SP 800-53](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf) if your enterprise is US-federal-adjacent; ISO/IEC 27002:2022 for general enterprise; ISO/IEC 42001 Annex A for AI-specific. This is preview work for `mod-108`.
- **Adversarial residual challenge.** Take your two lowest-residual entries and write a paragraph each arguing the opposite — that the residual should be one grade higher. This is the exercise a strong reviewer will do to you in exercise 05; do it to yourself first.
- **Monitoring hook per detective control.** For every detective control you proposed, name the metric it monitors and the threshold at which it fires. This is preview work for `mod-109`.
- **Executive-audience redraft.** Take your profile summary and rewrite it for a specific executive audience — the CEO, the general counsel, the chief risk officer. Note which parts of the profile each audience actually needs to see. This is preview work for `mod-110`.

## Deliverables

- `mod-103-ex-03-scored-register.md` — the fully scored register.
- `mod-103-ex-03-profile.md` — the one-page profile summary (or the summary as a section of the scored register).
- Optional `mod-103-ex-03-rework-note.md` (or embedded at the end of the scored register).
- Optional stretch artefacts named clearly.

## Notes on evaluation

The solutions repo produces a scored register for the CareTriage reference case, including one Transfer entry (BAA-based indemnification) and one Accept entry. Your register will differ. What is graded is (a) whether the three columns are honestly separate — inherent is not silently equal to residual; (b) whether the load-bearing control is named; (c) whether the profile summary resists the pull toward an aggregate score; (d) whether the rework note reflects real reconsideration rather than a rubber-stamped final draft. A cleanly-scored, cleanly-reasoned register with three entries beats a rough register with ten.
