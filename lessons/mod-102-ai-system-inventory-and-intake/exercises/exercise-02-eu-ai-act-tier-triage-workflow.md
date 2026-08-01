# Exercise 02 — EU AI Act Tier Triage Workflow

**Estimated effort:** 2 hours
**Grounding chapters:** [02 — Intake Triage — In-Scope / Out-of-Scope / Needs-Follow-Up](../02-triage-and-tier-tagging-workflow.md), [mod-101 chapter 04 — EU AI Act Risk Tiers and Annex III](../../mod-101-ai-governance-landscape/04-eu-ai-act-risk-tiers-and-annex-iii.md)

## Objective

Build the analyst reflex that turns an incoming intake into a triage decision (in-scope / out-of-scope / needs-follow-up) and, when in-scope, into a defensible EU AI Act tier tag plus an internal-tier tag — inside minutes, with citations, and with the analyst's assumptions written down so a reviewer can second-guess them.

After this exercise you should be able to sit an intake queue and, for a normal-shape enterprise intake, produce a triage row and tier tag in under ten minutes.

## Prerequisites

- Chapter 02 read; mod-101 chapter 04 (EU AI Act tiers) fresh in memory.
- The [consolidated CELEX text of Regulation (EU) 2024/1689](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32024R1689) open — you will cite Article 5, Article 6, Annex III, and Article 50 by number.
- An [EU AI Act tier decision-tree diagram or checklist](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — printed or on-screen. Some teams keep a one-pager in Confluence; if yours does not, draw one at the top of your deliverable.
- Optional but useful: the [EU AI Act Compliance Checker](https://artificialintelligenceact.eu/assessment/eu-ai-act-compliance-checker/) as a *sanity-check* only — not a substitute for reading the Regulation. <!-- needs-research: confirm this third-party tool is still maintained before recommending it externally. -->

## Problem statement

You will be handed **ten intake vignettes** below and asked to triage each one. For every vignette you produce a triage row that would go into the governance-record register. Write the triage rows in the format:

```
Intake ID: <slug>
Decision: in-scope | out-of-scope | needs-follow-up
Reason: <one paragraph — cite the enterprise definition, the Article, the Annex, or the specific missing field>
EU AI Act tier: <Unacceptable | High-risk (Annex I) | High-risk (Annex III item N) | Limited-risk (Article 50) | Minimal | N/A>
Enterprise tier: <Critical | High | Medium | Low | N/A>
Rationale: <one to three sentences citing the specific Article / Annex clause>
Routing: <who owns the next step; SLA>
Assumptions: <anything you inferred that the requester did not confirm — flagged so the risk assessment re-checks it>
```

### The ten vignettes

Assume the enterprise is a global company with US, UK, and EU operations, an internal AI definition that scopes to "any system using ML, statistical learning, or generative AI to produce or materially influence a decision or output". Enterprise-internal tier scheme is Critical / High / Medium / Low as described in chapter 02.

1. **Résumé Screener.** HR wants to pilot a hosted LLM to rank inbound résumés against a job description before a recruiter reviews them. Roles include EU-based positions. Recruiters always see all shortlisted candidates.
2. **Clinical Prior-Authorisation Assistant.** An external vendor sells an AI system that predicts likelihood of insurance prior-authorisation approval to speed hospital staff decisions. Enterprise is the deployer via an insurance subsidiary.
3. **Marketing Segment Predictor.** Internal ML model predicts customer propensity to churn from anonymised aggregate cohort features (no individual PII). Feeds a marketing dashboard read by campaign managers.
4. **Public-Facing Chatbot.** A hosted GenAI customer-support chatbot on the public website, US, UK, and EU. Escalates to a human on request. No decisioning about customers; produces information and can trigger a support-ticket creation flow.
5. **CV Recommendation for Internal Mobility.** Same underlying screener as vignette 1 but running internally to recommend existing employees for open roles.
6. **Rolling-Average Ops Dashboard.** A nightly SQL job computes and displays rolling 30-day averages of order-fulfilment metrics. A product manager filed the intake because "our leadership wants us to inventory all AI".
7. **Content Moderation for User Uploads.** An ML classifier flags user-uploaded images for adult content on a consumer platform. Flagged images are reviewed by a human moderator before removal. EU users are in scope.
8. **Real-Time Facial Recognition in Retail.** A retail-loss-prevention vendor proposes real-time facial-recognition cameras in stores, matching faces against an internal watchlist of known shoplifters. UK and EU retail locations. No law-enforcement partnership.
9. **Emotion-Recognition in a Call-Centre Coaching Tool.** Internal tool listens to agent-customer calls and produces a real-time "customer sentiment" score used to coach the agent live. Rolled out across US and EU call centres.
10. **RAG-Backed Legal-Research Assistant.** Internal tool used only by the enterprise's own legal team to search internal contracts and case notes using retrieval-augmented generation over a hosted LLM. Suggestions are always reviewed by a lawyer before use.

## Requirements

- **All ten vignettes triaged.** No skipping. Even the two you find "obvious" earn a written rationale.
- **Every tier tag cites a specific Article, Annex item, or the residual-minimal category.** "High-risk" alone is not enough; write "High-risk (Article 6 + Annex III item 4 — employment / recruitment)". If your tag depends on a derogation (Article 6(3)), say so and route to legal.
- **Every out-of-scope decision documents the exclusion path.** Where does the intake go instead — analytics-engineering change management, vendor-review, application security?
- **Every needs-follow-up decision lists the specific missing fields** and the questions the analyst would send back.
- **Boundary-case reasoning is visible.** Vignettes 2, 5, 7, and 10 are all deliberately near a boundary; your triage row for each should explicitly say what would push the decision the other way.
- **No fabricated Article numbers.** Cite from the CELEX text. If a specific sub-article you want to cite is not one you can verify, write `<!-- needs-research: verify Article 5(1)(f) applies to X in Y setting -->` and let the reviewer check it.
- **A short reflection note** — 5–10 sentences at the end of the deliverable — on which vignettes were hardest, where you felt tempted to guess, and one thing you would ask counsel about before publishing the triage row.

## Starter guidance

- Walk the five-step decision tree from chapter 02 in order for each vignette. Do not jump ahead. Vignette 8 tempts you to jump straight to "prohibited"; walk the tree anyway and note explicitly why the specific Article 5 sub-article does or does not fire.
- For vignettes with jurisdictional variation (1, 4, 5, 7, 9), consider whether the EU AI Act applies. Under Article 2, the Act reaches systems whose *output* is used in the Union — an internal-only tool used by US employees on non-EU data may still catch obligations if any of the output touches EU-based deployment. When unsure, note it and route to counsel.
- Vignettes 2, 5, 7, and 10 are the ones where the exercise's real value lives. Spend disproportionate time on those.
- Do not resolve derogations solo. Article 6(3) is one place the analyst *always* routes to legal; note it and move on.
- The internal-tier tag is not derived mechanically from the EU AI Act tier. A system tagged EU AI Act Limited-risk can be internal-tier High if the enterprise decides it has meaningful blast radius. Say so where relevant.

## Acceptance criteria

- A `triage-decisions.md` file with ten triage rows, each conforming to the format above.
- Every tier tag cites a specific Article, Annex item, or residual category; every out-of-scope decision names the receiving track; every needs-follow-up decision lists the missing fields and the questions to send back.
- Boundary-case vignettes (2, 5, 7, 10) each include a one-line "what would flip this" note.
- Any uncertain claim is marked `<!-- needs-research: -->` rather than guessed.
- Reflection note of 5–10 sentences present at the end.

## Stretch goals

- **Author a decision-tree diagram.** Draw the five-step tree from chapter 02 as a diagram (Mermaid, Excalidraw, plain ASCII) suitable to hang in a team's Confluence page. Include the enterprise-internal-tier overlay as a parallel branch.
- **Build a "second-opinion" pair-review protocol.** Take three of your own triage rows and swap them with a peer (or an LLM playing devil's advocate). Log which decisions survived and which you changed after the challenge.
- **Sector-overlay layering.** For vignettes 1, 2, 7, 8, 9, list the *non-EU* obligations that layer on top of the tier tag — NYC LL 144, EEOC Title VII, HIPAA, US state biometric-privacy statutes, GDPR Article 22 — with a one-line note per overlay.
- **Escalation memo.** For vignette 8 (real-time facial recognition), write the escalation memo to legal that a real analyst would send — with the specific sub-article you would cite as the block, the retail-loss-prevention exception you would ask counsel to opine on, and the SLA you would request.
- **Extend the vignette set.** Author three additional vignettes drawn from your target sector (finance / healthcare / public sector / retail) with the answer key hidden in a folded section; give them to a peer for a self-graded run.

## Deliverables

- `mod-102-ex-02-triage-decisions.md` — the ten triage rows.
- Optional `mod-102-ex-02-decision-tree.md` for the diagram.
- Optional `mod-102-ex-02-escalation-memo.md` for the vignette 8 stretch.

## Notes on evaluation

There is a defensible reference answer for each vignette in the paired solutions repo. The vignettes where the reference answer varies (2 and 10 in particular) are the ones where the *reasoning* matters more than the tier tag; a triage row that lands on the "wrong" tag with clean reasoning and clean routing is a stronger deliverable than one that lands on the "right" tag with no citation.
