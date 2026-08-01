# Exercise 01 — Intake Questionnaire Design

**Estimated effort:** 2 hours
**Grounding chapter:** [01 — The AI Use-Case Intake Questionnaire — Fields Employers Actually Populate](../01-intake-questionnaire-design.md)

## Objective

Design a working AI use-case intake questionnaire for a named enterprise scenario, and prove the design by filling it in for two very different use cases. The goal is not a beautiful form. The goal is a form that a non-ML requester can actually complete, that captures every field a downstream risk assessment and inventory row needs, and that routes correctly the first time.

You should finish this exercise able to hand your questionnaire to a product manager who has never heard of the NIST AI RMF and get a usable intake back.

## Prerequisites

- Chapter 01 read.
- A pass over the intake-relevant sections of the [NIST AI RMF 1.0 (AI 100-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf) MAP function and the [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) entries for MAP 1 through MAP 4.
- Skim of [EU AI Act Article 5, Article 6, Annex III, and Article 50](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32024R1689) enough to know what the tier-tag question is asking.
- A drafting surface of your choice — a Google Form, an Airtable form, a Notion database, a Markdown table, or a filled `intake.yaml`. Pick the one closest to what your target employer runs.

## Problem statement

Pick **one** of the following enterprise scenarios as the context for the questionnaire — the field list changes at the margins per sector, and picking a real context forces you to defend concrete design choices:

1. A mid-market **retail bank** (US and EU operations) with a growing pipeline of internal ML models and a first hosted GenAI use case in draft.
2. A **hospital system** running a mix of vendor-supplied clinical decision-support tools and internally-developed operational-analytics ML.
3. A **B2B SaaS** company (~2,000 employees) rolling out internal LLM assistants across support, sales, and engineering, and one external customer-facing AI feature.
4. A **public-sector agency** (national or state) with a mix of legacy rules-based systems being rebranded as "AI" and a new predictive-analytics initiative.

Then produce:

1. **A field-by-field questionnaire spec.** For each field: name, plain-English question text, answer type (short text / long text / single-select / multi-select / date / yes-no-unsure), controlled-vocabulary values where applicable, whether it is required, and the framework anchor(s) it maps to.
2. **A routing / conditional-logic annotation.** Which fields are business-facing (requester fills), which are technical (requester fills with help or ML partner completes after routing), and which are governance-fill (analyst completes at triage). Any conditional logic ("if personal data = yes, then show DPIA-follow-up fields") is called out.
3. **Two filled examples.** Populate the questionnaire for two use cases within your chosen scenario that stress the form in different directions — for example:
   - A **hosted-LLM assistive tool** with no personal data and internal-only deployment (like the MCDA example from the chapter).
   - A **classical-ML decisioning tool** with personal data, external-facing use, and a plausible high-risk tier tag (e.g., credit-underwriting for the bank scenario, admissions-triage for the hospital scenario, resume-screening for the SaaS scenario, benefits-eligibility for the public-sector scenario).

## Requirements

- **The canonical field set is covered.** At minimum every field named in chapter 01's business, technical, and governance-fill tables appears — system name, business owner, purpose statement, users, decision affected, autonomy level, deployment surface, sector, geographies, personal data, automated decision-making, target go-live date, model family, model provider, training / grounding data sources, retrieval sources, tools / APIs, third-party dependencies, integration surfaces, human oversight, intake tier assessment, EU AI Act tier tag, applicable sector regulator, applicable framework anchor, intake decision, assigned analyst. You may add sector-specific fields (SR 11-7 model risk tier for banking; SaMD class for healthcare; NYC bias-audit flag for hiring); if you *remove* any canonical field, justify the removal in a one-line comment on the spec.
- **Every field has a plain-English question text** distinct from the field name. "Autonomy level" is the field; the question text is "How much of the final decision does the tool take on its own?" with the four options defined.
- **Every field with a controlled vocabulary uses one.** Sector, model family, deployment surface, autonomy level, framework anchor, tier tags — enumerate the choices.
- **"Unsure" is a first-class answer** on every question where the requester might not know (personal data, automated decision-making, jurisdictions, model provider, third-party dependencies).
- **Framework anchors are cited** at the field level — NIST RMF subcategory, ISO/IEC 42001 clause, EU AI Act article. The requester does not see these, but the analyst-facing metadata does.
- **The two filled examples are internally consistent.** The autonomy level, deployment surface, and personal-data answers should logically imply the tier tag the analyst assigns; if they do not, the filled example is contradicting itself and needs to be reworked.
- **No fabricated regulator names or article numbers.** If you are not sure whether a specific sector regulator applies, write `<!-- needs-research: verify X regulator applies to Y sector in Z jurisdiction -->` rather than guessing.

## Starter guidance

- Start from the three field-group tables in chapter 01 and copy them into your drafting surface as a starting spec. Then rewrite each field's question text into language a non-ML PM in your chosen sector would understand.
- If your drafting surface is a real form tool (Google Forms, Airtable, ServiceNow, Jira Forms), export a link or a JSON representation and commit it in the workspace next to the spec — the reviewer wants to see the shape, not screenshots.
- For the two filled examples, do not use the MCDA case verbatim from the chapter — pick a use case actually plausible in your chosen scenario. This is where the exercise's teeth are.
- On the tier-tag question, cite the specific Article or Annex III area that drove your answer. "Article 6 + Annex III item 5 (credit-scoring)" is what the analyst-fill field should look like — not "high risk".
- If you notice you cannot answer one of the fields on your own filled example, that is real. Note it, and specify how the questionnaire would route to get the answer (e.g., "personal data = unsure → routes to privacy analyst joint follow-up"). That is *the* signal that the form is doing its job.

## Acceptance criteria

- A `questionnaire-spec.md` (or equivalent — `questionnaire.yaml`, `questionnaire.json`, or a linked shareable form URL committed as a README pointer) with the field list, question text, answer types, controlled vocabularies, and framework anchors.
- A `routing.md` (or an annotated section of the spec) that separates business-facing, technical, and governance-fill sections and calls out the conditional logic.
- Two filled example intakes — `example-a-hosted-llm.md` and `example-b-classical-ml-decisioning.md` (or similar) — each with every required field populated and a governance-fill section that assigns the tier tag with a cited rationale.
- Every canonical field from chapter 01 is present unless justified as removed.
- Every controlled-vocabulary field enumerates its choices; every "unsure"-eligible field allows it.
- No fabricated regulator names, article numbers, or framework subcategories; any uncertain claim is marked `needs-research`.

## Stretch goals

- **Progressive-disclosure design.** Sketch a two-page form where page 1 is the twelve business-facing fields and page 2 unlocks only after a triage decision. Include the transition prompt.
- **A rejection template.** Write the one-paragraph message the analyst returns when an intake is bounced as needs-follow-up — with placeholders for the specific missing fields.
- **A public-tool build.** Publish the questionnaire as an actual Google Form / Airtable / Typeform link that a peer can fill in. Get one peer to complete an intake for a fictional use case and log the friction they hit.
- **A sector-overlay pack.** For the sector you chose, produce a second file listing the additional fields required by the sector regulator (e.g., SR 11-7 model tier, SaMD device class, NYC LL 144 bias-audit disclosure) and where each would slot into the form.
- **A "definitions" microsite.** For the two hardest fields to explain — autonomy level and decision affected — write a 100-word plain-English gloss with three worked examples each, so the form tooltip has real substance.

## Deliverables

- `mod-102-ex-01-questionnaire-spec.md` (or equivalent artefact) with fields, question text, vocabularies, anchors.
- `mod-102-ex-01-routing.md` (or embedded section) with the field grouping and conditional logic.
- `mod-102-ex-01-example-a.md` and `mod-102-ex-01-example-b.md` — the two filled intakes.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The reference solution in the paired `ai-governance-analyst-solutions` repo picks the retail-bank scenario and produces one worked questionnaire against it. Your questionnaire will differ — the point is to defend your field choices and your two filled examples with reference to the framework anchors, not to converge on the reference cut.
