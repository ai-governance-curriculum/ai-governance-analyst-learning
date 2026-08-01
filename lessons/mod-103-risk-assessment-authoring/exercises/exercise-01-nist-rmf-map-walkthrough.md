# Exercise 01 — NIST AI RMF MAP Walkthrough

**Estimated effort:** 2 hours
**Grounding chapter:** [01 — Walking a Use Case Through NIST AI RMF MAP](../01-nist-rmf-map-walkthrough.md)

## Objective

Take an intake row for a new AI use case and produce a first-draft MAP walk — narrative, cited to the MAP subcategories, and structured as *context / stakeholders / technical framing / value and oversight / third-party components / impacts*. The output has to read as a short case study a reviewer can challenge, not as a subcategory checklist.

After this exercise you should be able to sit down with a triaged intake row and produce a defensible MAP 1–5 narrative in the two-hour window the chapter advertises for a Medium-tier system.

## Prerequisites

- Chapter 01 read; the MCDA worked example fresh in memory.
- The [NIST AI RMF 1.0 (AI 100-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf) MAP function open — you will cite subcategories by number (MAP 1.1 through MAP 5.2).
- The [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) MAP entries as a scanning reference for the "suggested actions" per subcategory.
- Fluency in the intake row shape from `mod-102` — you will not re-triage the intake; you will consume it as given.
- Access to one public incident register — the [AI Incident Database](https://incidentdatabase.ai/) or the [OECD AI Incidents Monitor](https://oecd.ai/en/incidents) — to source MAP 5.1 prior-art evidence.

## Problem statement

Pick **one** of the following triaged intake rows as your starting point. Each one has been through `mod-102` triage; your job is not to re-decide tier or scope, it is to walk MAP 1 through MAP 5 for the system as described.

### Intake A — CareTriage Chat (healthcare)

- **System name.** CareTriage Chat.
- **Owner.** Digital Care Ops (Ana Ruiz).
- **Purpose.** Triage inbound patient portal messages into urgent / routine / administrative buckets and draft a suggested response for the nurse to edit.
- **Users.** Registered nurses in the enterprise's tele-triage line, US only.
- **Affected populations.** Patients messaging the portal; skewed older and lower-digital-literacy.
- **Model family.** Hosted foundation model (Vendor V, model v2025-04) fronted by an internal retrieval layer over the enterprise's clinical-content library.
- **Automation level.** Assistive — nurse always reviews and sends the message; the system never sends unaided.
- **Data.** Message text (PHI); prior message context (PHI); no imaging, no chart notes.
- **Third parties.** Vendor V (LLM); Vendor E (embeddings / retrieval SaaS, HIPAA BAA in place).
- **Triage decision.** In-scope; enterprise-internal-tier High; EU AI Act N/A (US only); jurisdictional overlays HIPAA and state medical-boards guidance.

### Intake B — CreditBoost Explainer (financial services)

- **System name.** CreditBoost Explainer.
- **Owner.** Consumer Lending Product (Marcus Chen).
- **Purpose.** Generate the plain-language explanation attached to an adverse-action notice when the bank's existing credit-decisioning model declines an application.
- **Users.** Applicants receiving the adverse-action notice; internally, the compliance analyst who samples 5% of outputs weekly.
- **Affected populations.** Denied credit applicants across the bank's US footprint.
- **Model family.** Prompted use of a hosted foundation model with structured input drawn from the (separate, non-AI) credit-decisioning model's reason codes.
- **Automation level.** Fully automated on the generation step; the underlying decision is not touched.
- **Data.** Reason codes from the credit model; applicant name and case ID; no full application PII in-prompt.
- **Third parties.** Vendor V (LLM).
- **Triage decision.** In-scope; SR 11-7 model risk tier Medium (explanation is regulatory-required content); ECOA / Regulation B applies; CFPB circular 2022-03 applies.

### Intake C — SkillMatch (workforce / public sector)

- **System name.** SkillMatch.
- **Owner.** State Workforce Development Agency, Employment Services Division.
- **Purpose.** Match unemployed jobseekers on state unemployment insurance to open state-listed jobs and to relevant re-training programs, producing a ranked list a caseworker uses in the intake meeting.
- **Users.** State employment caseworkers.
- **Affected populations.** Unemployment insurance recipients in the state, including groups protected under state and federal civil-rights law.
- **Model family.** Fine-tuned classical ML model (gradient-boosted trees) over structured jobseeker and job-posting features.
- **Automation level.** Advisory — the caseworker reviews and finalises the recommendation.
- **Data.** Jobseeker profile (protected characteristics inferred by proxy in some features); job-posting metadata.
- **Third parties.** External vendor SaaS hosting the model; state-owned data lake for training data.
- **Triage decision.** In-scope; state-internal-tier Critical; EU AI Act N/A; state civil-rights and public-benefits-administration overlays apply; state legislature has flagged the program in a recent report.

## Requirements

Produce a MAP walkthrough for your chosen intake. The deliverable is one Markdown file with these sections, in order:

1. **Header.** System name, intake ID (fabricate one — e.g., `INT-2026-0338`), analyst (you), date, and the chosen intake letter.
2. **MAP 1 — Context.** Two to four paragraphs. Cover MAP 1.1 through MAP 1.6. Cite the enterprise's risk-tolerance statement even if you have to write *"the enterprise's published risk-tolerance statement — cited by reference; not authored here."*
3. **MAP 2 — Technical framing.** MAP 2.1 through MAP 2.3. Name the TEVV owner explicitly; do not design the eval methodology.
4. **MAP 3 — Value and oversight.** MAP 3.1 through MAP 3.5. Distinguish intended purpose from reasonably foreseeable misuse.
5. **MAP 4 — Third-party components.** MAP 4.1 through MAP 4.2. Enumerate the third parties. Flag any dependency that has not been through vendor review.
6. **MAP 5 — Impacts.** MAP 5.1 through MAP 5.2. Enumerate **at least four** distinct impacts. Each impact uses the shape *type of harm × affected population × plausible mechanism × ordinal likelihood × ordinal magnitude*. Cite at least one **public incident** from the AI Incident Database or the OECD AI Incidents Monitor whose mechanism informs one of your impact claims. Do not invent incidents.
7. **Sequence log.** A short list of the passes you actually did — which categories you re-visited after MAP 5 surfaced something. Show the loop the chapter describes.
8. **Deferrals.** A section that lists what you *did not* do at analyst tier and where it lands: harm-model design → `ai-risk-engineer`; quantitative loss estimates → `senior-ai-governance-architect`; release sign-off → `ai-evaluation-engineer`.

Cross-cutting requirements:

- **Narrative voice, not checklist voice.** No "MAP 1.1: yes; MAP 1.2: yes" tables. The subcategory numbers appear as citations inside the narrative — parenthetical or inline.
- **Every impact in MAP 5.1 names the population.** "Patients messaging the portal, skewed older and lower-digital-literacy" is a population claim; "users" is not.
- **Every likelihood or magnitude claim carries a one-line rationale.** No naked ordinals.
- **No fabricated facts.** No made-up regulator names, model version numbers, statute references, or incidents. If uncertain, write `<!-- needs-research: verify X --> `.
- **Length target.** 1,500 to 2,500 words. Longer than that means you have drifted into `mod-105` (impact assessment) or `mod-107` (evaluation) scope; shorter than that means MAP 5 is under-cooked.

## Starter guidance

- Run the passes in the order the chapter recommends: MAP 1 → 2 → 3 → 4 → 5 → re-visit MAP 1 and MAP 3. Do not try to write the file top-to-bottom in a single pass.
- For MAP 5.1, brainstorm impacts in the two-lens shape *before* you tighten prose: GenAI Profile risks (from `mod-101` chapter 02) on one axis, ISO 23894 categories (chapter 02 of this module — you will formalise the overlay in exercise 02) on the other. Not every cell fires; you are enumerating so nothing is left silent.
- For the incident citation, search the AI Incident Database or the OECD monitor for incidents in the same domain — clinical triage, adverse-action notices, workforce matching. Take one incident and quote the summary field plus the incident URL. Do not extrapolate details the source does not carry.
- Where the intake row is thin (owner unavailable; TEVV owner not yet named), write the field with a `needs-follow-up` marker rather than inventing. That is realistic MAP work.
- The MAP walk feeds exercises 02 and 03 directly. Choose an intake you are willing to carry through the next two exercises — you will overlay ISO 23894 on this same system in exercise 02 and score the register entries in exercise 03.

## Acceptance criteria

- A `mod-103-ex-01-map-walkthrough.md` file with the eight sections above, in order, for the chosen intake.
- Every MAP subcategory referenced at least once (MAP 1.1 through MAP 5.2).
- MAP 5.1 enumerates at least four impacts, each in the *type × population × mechanism × likelihood × magnitude* shape, each with a one-line rationale, and at least one carrying a public-incident citation.
- Narrative voice throughout — no checklist tables of "yes / no" per subcategory.
- Sequence log shows at least one re-visit pass to MAP 1 or MAP 3 after MAP 5.
- Deferrals section explicitly names the three downstream tracks.
- Any uncertain factual claim is marked `<!-- needs-research: -->`. No fabricated statutes, regulators, incidents, or version numbers.

## Stretch goals

- **Second-analyst pair review.** Swap files with a peer (or an LLM playing a skeptical reviewer). Log which of your MAP 5 impacts survived challenge and which needed the mechanism or population claim tightened.
- **A jurisdictional-overlay sidebar.** If you chose intake A or B, add a short section that names the jurisdictional overlays MAP already implies — HIPAA breach-notification for A; ECOA adverse-action-notice requirements for B — with a one-line note on which downstream module owns the depth.
- **MAP walk against a second intake.** Do a compressed version (~500 words) of a second intake. This is where the discipline of narrative-not-checklist really tightens.
- **A MAP walk template.** From your worked file, extract a reusable template — headers, prompts, and empty placeholders — that a peer analyst could fill in for a different system. Publish it as `mod-103-ex-01-map-template.md`.
- **Public-incident evidence pack.** Take three incidents from your chosen domain and write a short (100-word) note on each: mechanism, affected population, and which MAP 5.1 subcategory it would be cited under. This is preparation for the ISO 23894 overlay pass in exercise 02.

## Deliverables

- `mod-103-ex-01-map-walkthrough.md` — the eight-section MAP walk.
- Optional `mod-103-ex-01-map-template.md` for the stretch template.
- Optional `mod-103-ex-01-incident-pack.md` for the incident-evidence stretch.

## Notes on evaluation

The paired solutions repo works intake A (CareTriage Chat) as the reference. A strong deliverable against intake B or intake C is *not* penalised — the point is a defensible narrative with cited subcategories and cited incidents. A checklist-voice deliverable, however faithful to the subcategory list, is a fail: the whole exercise is about the shift from checklist to case study.
