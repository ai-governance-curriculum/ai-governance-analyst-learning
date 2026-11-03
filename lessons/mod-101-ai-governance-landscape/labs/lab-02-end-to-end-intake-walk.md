# Lab 02 — End-to-End Intake Walk Across All Five Frameworks

**Duration:** 2 hours.
**Grounding chapters:** [01](../01-nist-ai-rmf-four-functions.md), [02](../02-genai-profile-twelve-risks.md), [03](../03-iso-iec-42001-clause-walkthrough.md), [04](../04-eu-ai-act-risk-tiers-and-annex-iii.md), [05](../05-international-values-baseline.md), [06](../06-role-scope-and-deferrals.md).
**Difficulty:** Core — threads all six chapters through a single artefact.

## Objective

Take **one** fictional intake and walk it, in order, through every framework the module teaches: EU AI Act tier → NIST AI RMF MAP → NIST AI 600-1 GenAI risks → ISO/IEC 42001 clause touchpoints → international values-baseline check → analyst-tier routing per the deferral map. Produce a single `intake-walk.md` artefact that reads like the first-week work product of a competent analyst.

The exercises in this module each exercise *one* chapter's mechanics on a batch of inputs. This lab is the opposite shape: *one* input, *all six* chapters' mechanics. It is the integration drill — the muscle that turns six separate framework fluencies into a single coherent intake record.

## Prerequisites

- All six chapters read.
- Exercise 03 (EU AI Act tier tagging) and exercise 04 (GenAI risk mapping) completed, or at minimum read, so you are not re-learning the tagging and mapping mechanics here.
- A markdown editor.

## The intake (fixed input)

Use *exactly* this intake description — do not substitute. A fixed input lets you compare your walk to the chapter-anchored expected shape in the checkpoint section.

> **Intake request #INT-2026-0411 — "ClaimScout" first-pass claim-triage assistant**
>
> *Submitter:* Director of Claims Operations, Property & Casualty line.
> *Target go-live:* Q2 2026.
> *Business purpose:* Reduce first-touch claim-triage time for home-insurance claims by routing incoming claim narratives (text + attached photos) to one of three queues: fast-track settlement, standard adjuster review, or special-investigations (potential fraud).
> *System shape:* Hosted frontier LLM reads the claim narrative; a separate vision model scores attached photos for damage severity. A rules layer combines the two scores and selects one of the three queues. A human claims adjuster reviews every routing and can reroute.
> *Data:* Last four years of closed claims from the enterprise warehouse plus two years of fraud-labelled claims from the Special Investigations Unit. Claimant names and addresses are present in training data.
> *Deployment surface:* Internal claims-ops app. Policyholders are notified by email that "an AI-assisted triage" was performed.
> *Jurisdictions in scope:* US (all states) and the Republic of Ireland (EU member state).

## Steps

### Step 1 — Scaffold the artefact (10 min)

Create the working file.

```bash
mkdir -p ~/aicg-labs/mod-101-lab-02
cd ~/aicg-labs/mod-101-lab-02
touch intake-walk.md
```

Open `intake-walk.md` and lay in the six section headers up front:

```markdown
# Intake walk — INT-2026-0411 ClaimScout

## 1. EU AI Act tier
## 2. NIST AI RMF MAP walk
## 3. GenAI Profile risks (NIST AI 600-1)
## 4. ISO/IEC 42001 clause touchpoints
## 5. International values baseline — sanity check
## 6. Analyst-tier routing per the deferral map
## 7. Summary and open questions for the risk owner
```

The scaffolded order matters: tier-tag first (because it drives downstream artefact depth), then the risk work, then the management-system clause touchpoints, then the values floor, then routing. Walking out of order is where real analysts drift — follow the scaffold.

### Step 2 — Tag the EU AI Act tier (20 min)

Walk the chapter 04 decision tree from step 1 to step 5. For each step, write down what matched and why.

Fill section 1 with:

- The tier tag — one of `unacceptable`, `high (Annex I)`, `high (Annex III)`, `limited`, `minimal`, `GPAI provider`, or `needs-follow-up`.
- The anchor citation — the Article and, where applicable, the Annex III area or Annex I product family. For this intake, think carefully about Annex III area 5 (access to essential private services, including *insurance risk assessment*). Check the specific wording in chapter 04 before you commit.
- 2–3 sentences of rationale, including what is uncertain.
- An Article 50 transparency flag — the intake says policyholders are notified, so check whether that notification is sufficient under chapter 04's description of Article 50.
- One question you would send back to the submitter to disambiguate.

Do **not** invoke an Article 6(3) derogation yourself — that is legal territory per chapter 04. If this intake looks like a derogation candidate, note it as a question for legal, not a decision.

### Step 3 — Walk NIST AI RMF MAP (20 min)

Open the RMF (or chapter 01's "MAP — five categories" table) in a second window. Fill section 2 as a short MAP walk, one subsection per category:

```markdown
### MAP 1 — Context
<2–3 sentences on business purpose, stakeholders, deployment surface — drawn from the intake, not invented.>

### MAP 2 — System categorisation
<Task, model family, autonomy level, data provenance. The intake gives you all four — do not improvise additions.>

### MAP 3 — Capabilities, usage, benefits and costs
<The claimed benefit, the stated usage mode, the cost profile.>

### MAP 4 — Risks and benefits, including third-party components
<The hosted LLM, the vision model, the rules layer, the warehouse feed — walk each and name a candidate risk per component.>

### MAP 5 — Impacts to individuals, groups, communities, organisations, society
<Impact on the claimant if misrouted into special-investigations when they should be fast-tracked; impact if a fraud case is routed to fast-track; impact at population level if a protected class is systematically misrouted.>
```

Each subsection stays to a short paragraph — this is a walk, not an impact assessment.

### Step 4 — List the GenAI Profile risks that apply (15 min)

The LLM read-and-score step makes this a generative-AI intake. Fill section 3 as a short per-risk table:

```markdown
| # | Risk | Applies? | Rationale |
|---|---|---|---|
| 1 | CBRN Information or Capabilities | ... | ... |
| 2 | Confabulation | ... | ... |
...
| 12 | Value Chain and Component Integration | ... | ... |
```

Rules:

- Mark each **applies**, **does not apply**, or **needs follow-up**.
- Chapter 02 names three near-universal defaults (Value Chain and Component Integration, Data Privacy, Information Security). Expect all three to apply here unless you can argue otherwise.
- Chapter 02 warns that an intake with fewer than three risks tagged is almost always under-tagged. Target four to seven on this one.
- For every **applies**, add a one-line rationale pointing at the intake details, not at a generic risk description.

### Step 5 — Locate the ISO/IEC 42001 clause touchpoints (15 min)

For an enterprise running an ISO/IEC 27001 ISMS and extending it with an AIMS, where in ISO/IEC 42001 does this intake generate work? Fill section 4 as a short list, drawing on chapter 03's "The 27001 ↔ 42001 mapping in practice":

```markdown
- **Clause 4 (Context):** Confirm ClaimScout is inside the AIMS scope.
- **Clause 5 (Leadership):** Does the enterprise Responsible AI Policy cover this use-case shape? If not — gap.
- **Clause 6 (Planning):** AI risk assessment (ref. ISO/IEC 23894 risk sources) + AI impact assessment (ref. ISO/IEC 42005) are both required for this intake.
- **Clause 7 (Support):** AI-literacy training for the claims-ops users; this is also an EU AI Act Article 4 obligation.
- **Clause 8 (Operation):** Intake questionnaire and risk/impact templates run inside the SDLC.
- **Clause 9 (Performance evaluation):** Register entry feeds the quarterly management-review KPI pack.
- **Clause 10 (Improvement):** Any defect that surfaces post-go-live routes through corrective action.
- **Statement of Applicability:** New AI-section rows for Annex A controls applicable to this system (e.g., model documentation, human oversight, data-quality controls). Do not fabricate specific Annex A control IDs — mark `<!-- needs-research: Annex A A.X.Y -->`.
```

The point is not to be exhaustive; it is to show that an analyst walks the clause structure before filing, rather than only filing the RMF.

### Step 6 — Values-baseline sanity check (10 min)

Fill section 5 as a short checklist against chapter 05's "Positioning against enterprise policy":

```markdown
- OECD Principle 2 (human rights, fairness, privacy): ...
- OECD Principle 3 (transparency and explainability): ...
- CoE Framework Convention — equality and non-discrimination: ...
- CoE Framework Convention — privacy and data protection: ...
- UNESCO — sustainability / environmental impact: ...
- EU AI Act Article 14 — human oversight (because this intake is likely high-risk): ...
```

For each row, write one sentence: *does this intake, as currently described, undercut this baseline? If so, note it as a policy-gap finding.* The analyst-tier finding here is "policy-gap candidates" — the fix routes to the senior architect and head of governance per chapter 06.

### Step 7 — Route per the deferral map (10 min)

Fill section 6 by naming, for each piece of downstream work surfaced in sections 1–5, who the right owner is, drawing from chapter 06. Use this shape:

```markdown
| Downstream work | Owner | Analyst-tier hand-off |
|---|---|---|
| First-draft AI risk assessment | Analyst (self) | Walk NIST AI RMF MAP; file register entry row. |
| First-draft FRIA (Article 27) | Analyst (self) | Author the first draft; route to Senior Architect for cross-jurisdiction reconciliation. |
| Cross-jurisdiction reconciliation (EU FRIA + US state overlays + GDPR DPIA) | Senior AI Governance Architect | Package the three applicable instrument requirements and open a ticket. |
| Bias-eval methodology and release sign-off | AI Evaluation Engineer | Summarise once eval report lands; do not sign off. |
| Harm-model design for the fraud-adjacent routing | AI Risk Engineer | File a request citing the special-investigations routing path. |
| Legal opinion on Article 6(3) derogation candidacy | Legal counsel | Flag the uncertainty; do not interpret the statute yourself. |
| Deep privacy implementation (claimant data, EU/IE residency) | Privacy engineering | AI-specific overlay stays with you; general implementation routes out. |
| Board-pack portfolio view | Head of AI Governance / CAIO | Prepare the data pack; do not present. |
```

Every row names a specific role from chapter 06 and a non-empty analyst-tier hand-off. "Nothing" is never the right hand-off — even for a declined ask, the next person gets a running head start.

### Step 8 — Summarise and list open questions (10 min)

Fill section 7 with:

- A three-sentence summary of the intake, the tier tag, and the three most salient GenAI risks.
- A numbered list of 4–8 open questions to send back to the submitter and the risk owner. Each question should be answerable in one sentence — avoid "please provide more detail" at the open-ended end.

### Step 9 — Self-check (10 min)

Walk the artefact top-to-bottom and verify:

- Every claim about EU AI Act, Annex III area, Article number, ISO clause, Annex A control, or GenAI risk is either cited to the chapter it comes from or marked `<!-- needs-research: -->`.
- No invented RMF subcategory numbers. Where you cannot name a specific subcategory, cite the top-level category (e.g., `MAP 5`) only.
- Every routing row in section 6 names a role that appears in chapter 06's "What defers upward / sideways / out-of-family" lists.
- No "release decision" or "legal opinion" statements in your own voice — any such statement is a scope creep per chapter 06.

## Expected output

A single markdown file `intake-walk.md` with seven filled sections, roughly 800–1500 words total. It should be short enough that a senior architect or head of governance can read it in 10 minutes and either (a) sign off on the routing or (b) push back on specific rows.

## Checkpoint

A mentor, peer, or self-review check — walk the following four questions and answer honestly:

1. **Did you tier it correctly?** The intake describes "insurance risk assessment" in an EU member state. Chapter 04 lists "life-and-health insurance risk assessment" under Annex III area 5 — but ClaimScout is a *claims-triage* assistant, not an underwriting-risk model. There is genuine ambiguity here. If you tagged this as a clear "high (Annex III)" without flagging the ambiguity, you missed the boundary case. If you tagged it as a clear "minimal" or "limited" without flagging the Annex III proximity, same problem. The chapter-anchored right answer is: **tag as high-risk candidate, cite Annex III area 5, flag the "claims triage vs risk assessment" ambiguity as a question for legal, and start the full impact assessment anyway.**
2. **Did you list at least four GenAI risks?** The three defaults (Value Chain, Data Privacy, Information Security) apply. Confabulation applies to the LLM narrative read. Harmful Bias or Homogenization applies to the routing (claimant demographics may correlate with historical adjuster bias). Information Integrity applies at scale if the system mis-triages hundreds of claims per day. Intellectual Property is unlikely here. Human-AI Configuration applies to the human-reviewer step. That is six to seven at minimum. If you listed only three, re-read the intake.
3. **Did you file any ISO 42001 clause content?** It is tempting to only file the RMF walk and forget that an enterprise running an AIMS needs the clause touchpoints too. If section 4 is thin or missing, your analyst's artefact will not survive the Clause 9 management review.
4. **Did you keep release sign-off off your own desk?** Chapter 06's canonical scope-creep failure is accepting release sign-off. Your section 6 should route release sign-off to the AI Evaluation Engineer, with you owning the eval summary — not the sign-off.

If any of the four honest answers is "no", revise *that section* before considering the lab done.

## Why this is a lab, not an exercise

Exercise 03 tags twelve intakes against the EU AI Act. Exercise 04 maps the twelve GenAI risks against twelve use cases. This lab inverts both: it stays on *one* intake and threads *all six* chapters through it. The failure mode a new analyst actually has in production is not "cannot tag one of twelve intakes" — it is "walks one intake into the register with the EU AI Act work done but the ISO 42001 touchpoints forgotten, or the values-baseline check skipped, or routing scoped-crept into the register." This lab exercises the integration directly.
