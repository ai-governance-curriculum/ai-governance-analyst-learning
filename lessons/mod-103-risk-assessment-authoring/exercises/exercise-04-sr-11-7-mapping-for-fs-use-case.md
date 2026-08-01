# Exercise 04 — SR 11-7 Mapping for a Financial-Services Use Case

**Estimated effort:** 2 hours
**Grounding chapter:** [04 — SR 11-7 Shape — Model Risk for Regulated Financial Institutions](../04-sr-11-7-shape-for-financial-services.md)

## Objective

Take an AI use case deployed in a US-regulated financial institution and produce the SR 11-7 overlay — the three-pillar mapping, the FSI-specific inventory-row extension, the developer/validator independence claim, the materiality tier, and the additional statutory overlays (CFPB / ECOA / OCC) that the NIST AI RMF frame alone does not surface. The output is what an analyst at a bank hands off to the Model Risk Management (MRM) group so the MRM group can accept the entry without redoing the risk assessment.

After this exercise you should be able to sit in a joint AI-governance / MRM review and speak both vocabularies — mapping MAP function output onto SR 11-7 pillars in real time, and knowing where the AI-specific overlays (GenAI Profile risks, third-party foundation-model exposure) plug in.

## Prerequisites

- Chapter 04 (this module) read.
- The [US Federal Reserve SR 11-7 letter](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) open — you will cite the three pillars and the model-definition language directly.
- The [OCC Bulletin 2011-12](https://www.occ.gov/news-issuances/bulletins/2011/bulletin-2011-12.html) as SR 11-7's companion.
- The [OCC Bulletin 2023-17 on Third-Party Relationships](https://www.occ.gov/news-issuances/bulletins/2023/bulletin-2023-17.html) — third-party risk overlay the analyst reaches for on any hosted-model use case.
- The [CFPB Circular 2022-03 on adverse action notification](https://www.consumerfinance.gov/compliance/circulars/circular-2022-03-adverse-action-notification-requirements-in-connection-with-credit-decisions-based-on-complex-algorithms/) and the underlying [ECOA / Regulation B](https://www.consumerfinance.gov/rules-policy/regulations/1002/) for any consumer-credit scenario.
- Optional: the [PRA SS1/23 model risk management principles](https://www.bankofengland.co.uk/prudential-regulation/publication/2023/may/model-risk-management-principles-for-banks-ss) if you want to add a UK-peer comparison.

## Problem statement

Pick **one** of the following FSI use cases as your target system. All three are deliberately shaped to force the SR 11-7 overlay to do real work — you cannot just re-file an AI risk assessment and call it done.

### FSI-A — SmallBiz Loan Pre-Qualifier (bank)

An ML model that scores small-business loan applicants for pre-qualification. Assistive to the loan officer — the officer makes the final decision. Input features: business financials, industry code, borrower's personal credit summary. The model is retrained quarterly; the deployment vendor is a third-party ML SaaS. The bank is US-federally-chartered (OCC-supervised). Deployed across US retail branches; no non-US operations.

### FSI-B — MarketWatch Sentiment (asset manager)

A hosted-LLM system that produces a daily market-sentiment digest from a mix of proprietary research feeds and public news. Used by portfolio managers as one of several inputs into position adjustments. Not a trade-decisioning model directly. The asset manager is a US-registered investment advisor (SEC-regulated). Vendor V provides the hosted LLM; a second vendor provides the retrieval / news-corpus SaaS.

### FSI-C — FraudSignal Prioritiser (insurer)

An ML model that scores incoming insurance claims for fraud likelihood and orders the queue for the Special Investigations Unit (SIU). Assistive — investigators do not deny claims based on the score, only prioritise workload. The insurer is US-regulated at the state level; the model was developed in-house on internal claims data. No third-party model dependencies for the scoring itself; the underlying data platform is third-party.

## Requirements

Produce one Markdown file with the following sections, in order.

### Section 1 — Intake summary

A short (1-page) intake summary for the chosen use case in the shape of the mod-102 intake row: system name, owner, purpose, users, data, third parties, jurisdictional footprint, model definition. Then explicitly cite the SR 11-7 model definition and state whether the system meets it. (Spoiler: all three do; the analyst writes down *why* — SR 11-7's model definition is broad and the trigger clause matters.)

### Section 2 — Three-pillar mapping

A table with three rows (one per SR 11-7 pillar) and, for each row:

- The pillar as SR 11-7 states it (short paraphrase acceptable; cite the SR letter).
- The NIST AI RMF anchor(s) that satisfy the pillar for this system — subcategory-specific, not "MAP function".
- The ISO/IEC 42001 clause(s) that satisfy the pillar — clause number and short paraphrase.
- The **specific enterprise artefact** that evidences the pillar for this system: which document, which model card, which validation report. If the artefact does not exist yet, note it as a gap and route to a named owner.

### Section 3 — Materiality tier

Assign a materiality tier (High / Medium / Low, or the enterprise-specific tier scheme if you know one). Write two to three sentences of rationale citing:

- The **decision materiality** — how central the model output is to the business decision, and how large the potential loss.
- The **regulatory materiality** — whether the model's outputs are directly regulated content (e.g., an ECOA adverse-action explanation is regulated content; a marketing digest is not).
- The **customer-impact materiality** — whether an incorrect output can produce a consumer-facing harm.

### Section 4 — Developer / validator independence

For the chosen use case, name:

- The **developer** — the team that built (or configured / prompt-engineered) the model.
- The **validator** — the team or individual that provides independent validation. If the enterprise has a formal MRM group, name it. If not (unusual for an FSI in scope, but possible for a small insurer or a start-up subsidiary), flag the gap and route.
- The **evidence of independence** — how the enterprise proves the validator is independent of the developer. Reporting-line independence is the simplest test; funding-independence and challenge-authority are peer tests.

### Section 5 — Overlays beyond SR 11-7

List every additional statutory or supervisory overlay that applies to the chosen use case, with a one-line note on what it adds:

- **OCC 2023-17** third-party relationships, for any third-party model or SaaS dependency.
- **OCC 2020-10** if third-party model use adds validation complications.
- **ECOA / Regulation B** if the system touches consumer credit decisioning or notice.
- **CFPB Circular 2022-03** if the system is in the adverse-action-notice path for a complex-algorithm decision.
- **[Federal Reserve SR 11-14](https://www.federalreserve.gov/supervisionreg/srletters/sr1114.htm) or equivalent** if the system is a stress-testing / capital-planning input. <!-- needs-research: confirm current supervisory posture on AI in CCAR / DFAST cycles. -->
- **State insurance regulator overlays** (for FSI-C) — the [NAIC Model Bulletin on AI Systems](https://content.naic.org/) as adopted by the relevant state. <!-- needs-research: confirm which state adoptions apply to the insurer's operating footprint. -->
- **SEC Investment Advisers Act obligations** (for FSI-B) — fiduciary and marketing-rule implications of AI-generated content.

### Section 6 — Inventory-row FSI extension

Extend the mod-102 inventory-row shape with the SR 11-7-specific fields called out in chapter 04:

- Model tier / materiality rating.
- Validation status (`pre-validation` / `conditionally approved` / `approved` / `suspended` / `retired`).
- Last validation date; next validation due.
- Validator name.
- Assumptions and limitations (formal field).
- Compensating controls.

Populate the extended row for the chosen system. Where a field cannot be populated (validation not yet done), write it as `pending — routed to MRM lead <name>, due <date>` rather than leaving blank.

### Section 7 — GenAI / AI-specific gap note

A short (5–10 sentence) section on what SR 11-7 does *not* cover for the chosen use case, and how the analyst fills the gap. FSI-B lands this hardest (GenAI-specific risks are largely outside SR 11-7's frame); FSI-A and FSI-C surface fairness and third-party-data-platform gaps.

## Requirements — cross-cutting

- **The chosen use case is walked all the way through.** Every section addressed; no "TBD" left in the deliverable. Where a field genuinely cannot be resolved without another team, write `pending — routed to X` and specify the SLA.
- **SR 11-7 citations are to the SR letter or the OCC companion, not to secondary summaries.**
- **Statutory overlays are cited to the source instrument** — ECOA to Regulation B section, CFPB Circular to the CFPB URL, OCC bulletin to the OCC URL. No blog-post citations.
- **Materiality is defended, not asserted.** A Low materiality on a customer-facing system needs a written defence.
- **Developer / validator independence is a claim, not a hope.** If independence is not clean (e.g., a small team where the developer is also the person best-placed to validate), say so and note the compensating controls.
- **Uncertain statutory claims are marked `<!-- needs-research: -->` rather than fabricated.** State insurance regulator adoption of NAIC bulletins is the classic trap — do not assert applicability without checking the state.

## Starter guidance

- Chapter 04's mapping table is your starting template for Section 2 — copy it and fill it in system-specifically. Do not try to memorise the mapping; the value is in the specific-artefact column, which chapter 04 leaves generic.
- For FSI-A (loan pre-qualifier), the ECOA / Regulation B overlay is the sharpest — even an assistive score is treated as part of the credit decision under CFPB guidance. Do not undercount.
- For FSI-B (market-sentiment digest), the SR 11-7 model-definition trigger is the interesting question. SR 11-7's definition is broad; a generated digest can be argued in or out depending on how the portfolio managers use it. Write the argument both ways and pick one — that is the analyst's job.
- For FSI-C (fraud prioritiser), the third-party data-platform dependency is the sharpest — the model itself is in-house, but the data platform is third-party and OCC 2023-17 / 2020-10 obligations layer on. Also, state insurance-regulator AI bulletins have moved fast in the last two years; the citation set here is more time-sensitive than the banking overlays.
- On developer / validator independence, if you have no direct FSI experience, use the shape from the chapter and pattern-match to a plausible org chart. The point is to hold the *frame* — reporting-line independence, funding independence, challenge authority — not to know the specific team names of a specific bank.
- Do not conflate SR 11-7 model validation with AI-specific evaluation (mod-107 territory). SR 11-7 validation is a governance function — a MRM group signs off; AI-specific evaluation is a technical function — an evaluation engineer produces the evidence the MRM group reviews. Both are required; they are different artefacts.

## Acceptance criteria

- A `mod-103-ex-04-sr-11-7-overlay.md` file with the seven sections above, in order, for the chosen FSI use case.
- SR 11-7 pillar mapping table complete with specific-artefact column filled or gap-with-routing noted for every cell.
- Materiality tier with three-lens rationale (decision, regulatory, customer-impact).
- Developer / validator named; independence claim explicit; any weakness in independence noted and compensated.
- Overlay list carries at least four applicable overlays for the chosen system, each cited to the source instrument.
- FSI-extended inventory row populated; fields that cannot be populated are marked `pending — routed to X, due Y`.
- GenAI / AI-specific gap note of 5–10 sentences.
- All statutory or supervisory citations are to primary instruments; any uncertain claim is marked `<!-- needs-research: -->`.

## Stretch goals

- **Jurisdictional peer overlay.** Add a short section that maps the same use case onto the UK PRA SS1/23 shape or (for FSI-B) the SEC + FINRA overlay. Note where the frame ports and where it does not.
- **A joint AI-governance / MRM RACI.** Draw a small RACI for the routine work of maintaining the model (revalidation, monitoring, retraining, retiring) with rows for the developer, MRM validator, AI governance analyst, business owner, and compliance. This is preview work for `mod-108` and `mod-109`.
- **A model-retirement plan.** Write a one-page retirement plan for the chosen system: triggers, dependency map, downstream users, transition state, evidence-preservation obligations. SR 11-7 explicitly requires ongoing management including retirement; the plan should reflect that.
- **A CFPB Circular 2022-03 explanation.** For FSI-A (or a hypothetical), write the specific plain-language adverse-action explanation the system would produce, and defend it against the CFPB's "principal reasons" test.
- **A joint AI-governance / MRM training module.** Author a 5-slide deck (or a 500-word note) that trains an MRM analyst on the AI-specific overlays (GenAI Profile risks, third-party foundation-model exposure) that an SR 11-7-native workflow does not cover. This is preview work for `mod-110`.

## Deliverables

- `mod-103-ex-04-sr-11-7-overlay.md` — the seven-section overlay.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The solutions repo works FSI-A (SmallBiz Loan Pre-Qualifier) as the reference. A strong deliverable against FSI-B or FSI-C is *not* penalised — the point is holding the SR 11-7 shape and adding the correct AI-specific overlays. The commonest failure modes are (a) treating "the model is assistive" as a reason to under-tier — SR 11-7 does not, and CFPB 2022-03 explicitly does not; (b) leaving the developer / validator independence claim vague when a small team makes it awkward; (c) forgetting the third-party overlay when the model or data platform is third-party. A cleanly-argued Low-materiality tier on FSI-B beats a Medium-materiality tier on FSI-A that leaves ECOA off the overlay list.
