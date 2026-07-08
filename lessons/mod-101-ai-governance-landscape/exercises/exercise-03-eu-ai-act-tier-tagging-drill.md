# Exercise 03 — EU AI Act Tier Tagging Drill

**Estimated effort:** 2 hours
**Grounding chapter:** [04 — EU AI Act risk tiers and Annex III](../04-eu-ai-act-risk-tiers-and-annex-iii.md)

## Objective

Take a set of realistic AI use-case intake descriptions and, for each one, produce an analyst-tier **tier tag** (unacceptable / high / limited / minimal / GPAI-provider), an **anchor citation** into the EU AI Act, and a **route** (self-serve intake, full impact assessment, legal escalation, or block).

This is the drill you will run every week in production. It is not a legal opinion — it is a defensible first pass that the risk owner, the legal team, and the head of governance can review.

## Prerequisites

- Chapter 04 read.
- [EU AI Act official text](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) open, especially Article 5, Article 6, Annex I, Annex III, and Article 50.
- Optional: [EU Commission AI Act hub](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai) for the official explanatory summaries.

## Problem statement

Below are **twelve short intake descriptions**. Each is deliberately compressed to the level a product manager would send in Slack — you do not always have the answer to every question. For each, produce a tier tag and a short justification.

### The intake descriptions

Copy these into your working file and tag them.

1. **Résumé screening for internal hiring.** A vendor tool that scores incoming résumés against job descriptions and produces a ranked shortlist. Deployment surface: internal HR portal. Used by recruiters for initial screen; final interview decisions made by humans.
2. **Customer-support agent-facing assistant.** A retrieval-augmented LLM assistant that answers agent-facing questions from an internal knowledge base. The human agent decides what to send to the customer. Hosted frontier model with a vector store.
3. **Chatbot on the public marketing site.** A generative chatbot that answers general product questions on the public marketing site. If a lead scores as high intent, it hands off to a human sales rep.
4. **Loan-underwriting decision assistant.** An ML model that produces a creditworthiness score used as one input in the loan-underwriting decision. Human underwriter makes the final call.
5. **AI-powered CCTV in a manufacturing plant.** A vision model watches the shop floor for PPE compliance and near-miss detection. Alerts a human safety supervisor.
6. **AI proctoring for internal training certifications.** A vision system watches employees during internal-training certification exams and flags suspected cheating for HR review.
7. **Marketing-copy generator (internal-only).** An LLM tool that generates first-draft marketing copy from a product brief. Copy is edited and approved by a human before publication.
8. **Deepfake-adjacent product feature.** A consumer image-editing app feature that allows a user to swap faces in uploaded photos. Watermarks the output, but the watermark is stripped by common editors.
9. **Emergency-dispatch triage assistant.** An LLM that reads incoming 911 calls in real time and suggests severity codes to the human dispatcher.
10. **Predictive-maintenance model for wind turbines.** A time-series ML model that predicts turbine-blade failures. Alerts a human maintenance planner.
11. **Employee-monitoring emotion-recognition tool.** A vendor tool that infers stress and engagement from webcam video during meetings and reports aggregated wellbeing metrics to HR.
12. **General-purpose LLM release.** Your employer trains and releases a general-purpose LLM available via API to any downstream developer.

### For each intake

Produce a row in a table with columns:

| Column | Content |
|---|---|
| Intake # | 1–12 |
| Tier tag | one of: `unacceptable`, `high (Annex I)`, `high (Annex III)`, `limited`, `minimal`, `GPAI provider`, or `needs-follow-up` |
| Anchor citation | The Article and, where applicable, the Annex III area (or Article 5 sub-item, or Annex I product family) that justifies your tag |
| Rationale | 2–3 sentences on why this tier — including what is uncertain |
| Route | one of: `self-serve intake row`, `full impact assessment`, `legal escalation`, `block` |
| Article 50 transparency? | Y/N — does an Article 50 disclosure obligation attach on top of the tier? |
| Notes / questions for the risk owner | Any question you would ask the intake submitter to disambiguate |

### Additionally, write

- A short **decision-tree diagram** (ASCII or markdown) showing the tagging heuristic you followed. It should look roughly like the one in chapter 04 but in your own words.
- A **reflection paragraph** of 5–8 sentences answering: which intakes were you most uncertain about? What information would resolve the uncertainty? Which ones would you *always* route to legal even if they look like a clear tag?

## Requirements

- Every anchor citation names an Article (and where relevant an Annex III area) — no bare "high risk" without a citation.
- Any `needs-follow-up` tag has a specific question you would send back to the intake submitter, not a vague "not enough information".
- Any `unacceptable` tag has an Article 5 sub-item cited by name, not just "Article 5".
- The reflection paragraph acknowledges at least one intake where your tag could reasonably be wrong.

## Starter guidance

- Start with the decision tree in chapter 04. Walk the tree for every intake in the same order. The rhythm makes the drill fast.
- The résumé screening (1), the loan underwriting (4), the emergency-dispatch (9), the AI proctoring (6), and the employee-monitoring emotion tool (11) are the ones you should look at with the most suspicion — they touch Annex III areas or Article 5 prohibitions.
- The customer-support agent-facing assistant (2), the internal marketing-copy generator (7), and the public marketing chatbot (3) are the "everyday enterprise" intakes — they are usually limited or minimal, but check Article 50 obligations for the chatbot.
- The deepfake feature (8) is a limited-risk-with-teeth intake — Article 50 disclosure applies but the risk owner will also flag safety concerns; treat as limited with a strong Article 50 obligation and a note about the watermark-stripping problem.
- The GPAI release (12) is a Chapter V provider case. Note that if it is above the systemic-risk threshold (per Article 51), a further layer applies. You are not expected to make the threshold determination — flag it.

## Acceptance criteria

- Working file `mod-101-ex-03-tier-tags.md` present with all 12 intakes tagged.
- Every row has a tier, an anchor citation, a rationale, a route, an Article 50 flag, and at least one clarifying question.
- Decision-tree section present.
- Reflection paragraph present and specific — names at least one intake and one uncertainty.
- No made-up Article numbers; use `<!-- needs-research: -->` for any citation you cannot verify against the OJ text.

## Stretch goals

- Add a column that flags **Article 6(3) derogation candidates** — intakes that are Annex III but might qualify as narrow procedural / preparatory tasks. Note that in production you would route these to legal, not decide yourself.
- Cross-tag the intakes with the applicable **NIST AI RMF trustworthy-AI characteristics**. This exercises the mental muscle for `mod-103-risk-assessment-authoring`.
- Cross-tag with the **NIST AI 600-1 GenAI Profile risks** for any generative-AI intake — that muscle gets exercised in exercise 04.
- Write **two additional intakes of your own**, chosen to sit right on a tier boundary, and tag them. Use these to test yourself later.

## Deliverables

- `mod-101-ex-03-tier-tags.md`.

## Notes on evaluation

The reference solution in the paired repo shows one defensible set of tags. There will be *legitimate disagreement* on some intakes — for example, the CCTV-in-plant case (5) can be argued either as Annex III critical-infrastructure adjacent or minimal-risk depending on the plant's classification. What matters is that your tag has a defensible anchor citation and an honest clarifying question, not that it matches the reference tag on every row.
