# Lab 01 — Intake-to-Inventory Walk on One Fixed Vignette

**Duration:** 2 hours.
**Grounding chapters:** [01](../01-intake-questionnaire-design.md), [02](../02-triage-and-tier-tagging-workflow.md), [03](../03-inventory-row-and-registry-sync.md).
**Difficulty:** Core — threads three chapters through a single artefact.

## Objective

Take **one** fixed intake vignette and walk it in order through the three artefacts chapters 01–03 produce: the intake row (requester-filled business fields plus a governance-fill section), the triage decision with EU AI Act tier tag and enterprise-internal tier tag, and the inventory row — all three populated for the same system and cross-referenced.

The module's exercises each exercise *one* chapter on a batch of inputs: exercise-01 asks you to design a whole questionnaire; exercise-02 asks you to triage ten vignettes; exercise-03 asks you to design a schema and populate three rows across three lifecycle states. This lab is the opposite shape — *one* vignette, *three* chapters' mechanics, chained. It is the muscle an analyst actually uses on their first day: walk one new intake all the way to an inventory row that downstream teams can draw from, without dropping a field or a citation.

## Prerequisites

- Chapters 01, 02, and 03 read at least once.
- Exercise 01 (intake questionnaire design) and exercise 02 (tier triage) completed, or at minimum read, so you are not re-learning the intake-schema and tier-tagging mechanics here.
- A markdown editor.

## The intake (fixed input)

Use *exactly* this intake description — do not substitute. A fixed input lets you compare your walk to the chapter-anchored expected shape in the checkpoint section.

> **Intake request #INT-2027-0029 — "ServiceLens" first-touch support-ticket classifier**
>
> *Submitter:* Head of Customer Support Operations.
> *Target go-live:* 2027-04-01.
> *Business purpose:* When a customer submits a support ticket through the web form, ServiceLens reads the free-text description and attached screenshots and classifies the ticket into one of six queues (billing, account, outage, feature request, bug report, abuse) so the ticket lands on the right team without a human triager in between. Volume is ~12,000 tickets per week across US, UK, EU, and Canada customer bases.
> *System shape:* A hosted frontier LLM reads the ticket text; a vision model scores attached screenshots; a rules layer combines the two and assigns a queue. A human team lead reviews a 5% random sample post-routing for quality-control, but a given individual ticket is not reviewed before routing.
> *Data:* Three years of previously closed support tickets (text + screenshots) labelled by the human triage team. Customer names, email addresses, and account IDs are present in the training data; screenshots sometimes contain PII incidentally (an account page showing the customer's name).
> *Deployment surface:* Internal support-tooling (agents see the classification), plus a customer-facing "we received your ticket and routed it to our [billing] team" confirmation email.
> *Jurisdictions:* US (all states), UK, EU (France, Germany, Ireland, Netherlands, Spain), Canada (all provinces).
> *Third-party dependencies:* Hosted LLM vendor (not yet selected — requester lists two candidates); hosted vision model vendor (same vendor as LLM); prompt-management SaaS; the enterprise's internal data warehouse for training data.

## Steps

### Step 1 — Scaffold the artefact (10 min)

Create the working folder and files:

```bash
mkdir -p ~/aicg-labs/mod-102-lab-01
cd ~/aicg-labs/mod-102-lab-01
touch intake-row.md triage-decision.md inventory-row.md
```

Open each file and lay in a top-of-file title and the section scaffold for that artefact. Use the exact headers below so the cross-references between the three files line up.

`intake-row.md`:

```markdown
# Intake row — INT-2027-0029 ServiceLens

## 1. Business-facing fields (requester-filled)
## 2. Technical fields (requester-filled with help, or ML-partner-completed)
## 3. Governance-fill fields (analyst-completed)
```

`triage-decision.md`:

```markdown
# Triage decision — INT-2027-0029 ServiceLens

## 1. Decision (in-scope / out-of-scope / needs-follow-up)
## 2. EU AI Act tier walk (five-step decision tree)
## 3. Enterprise-internal tier tag
## 4. Routing and SLA
## 5. Assumptions
```

`inventory-row.md`:

```markdown
# Inventory row — AI-2027-0029 ServiceLens

## 1. Identity and ownership
## 2. Classification
## 3. Artefact cross-references
## 4. Lifecycle and status
```

The scaffolded order matters: chapter 01's intake sections first, then chapter 02's triage output, then chapter 03's inventory row. Walking out of order is where real analysts drift — follow the scaffold.

### Step 2 — Fill the intake row (35 min)

Open `intake-row.md`. Work the three sections in order against chapter 01's "Field-by-field — the canonical intake row" tables.

**Section 1 — business-facing fields.** Populate every field in chapter 01's business-facing table:

- System name; business owner; purpose statement; users; decision affected; autonomy level; deployment surface; sector or line of business; geographies; personal data involved; automated decision-making about individuals; target go-live date.

For each field, write the answer **as the submitter would** — do not skip ahead to governance judgement. The submitter is the Head of Customer Support Operations, not an ML engineer. Two field-level tripwires to watch:

- **Autonomy level.** Chapter 01 gives four verbatim definitions (advisory / assistive / semi-autonomous / autonomous). ServiceLens routes tickets automatically; a 5% sample is reviewed *after* the routing happens. Which of the four is this? Read the chapter 01 definitions before you commit.
- **Automated decision-making about individuals.** The classification decision does not change a customer's rights (a billing ticket going to the billing team is not a GDPR Art. 22 call). But the field has three answers (yes / no / unsure) — pick deliberately and write a one-line rationale.

**Section 2 — technical fields.** Populate every field in chapter 01's technical table. The intake names two candidate LLM vendors but no final pick; chapter 01 says the right move is to mark provider as *requester unsure — flag for ML partner*, not to guess. Do the same for any other field where the requester cannot commit.

**Section 3 — governance-fill fields.** Leave these blank for now — they will be filled from `triage-decision.md` in step 4 and cross-copied back.

At the bottom of `intake-row.md`, add a one-line `Date / analyst:` entry so the row is time-stamped like chapter 01's example.

### Step 3 — Triage the intake (30 min)

Open `triage-decision.md`. Walk chapter 02's five-step EU AI Act decision tree in order and record what you found at each step.

**Section 1 — decision.** ServiceLens is a real AI system that matches the enterprise's AI definition, has a named business owner, has a purpose statement, and has a stated jurisdiction set. Which of the three buckets is it? Write the decision with a one-paragraph reason that cites the enterprise definition and at least one field from `intake-row.md`.

**Section 2 — EU AI Act tier walk.** Author the five-step walk as:

```markdown
1. Article 5 (prohibited practice)? ...
2. Annex I (safety-component route)? ...
3. Annex III (use-case route)? ...
4. Article 50 (interaction / synthetic content / biometric categorisation / deep-fakes)? ...
5. Residual minimal? ...
```

For each step, write `yes / no / unsure` and the citation that drove the answer. For this intake, two steps deserve extra care:

- **Annex III step 3.** The intake is customer *support* ticket triage — not *access to essential services*. Is the classification a routing-shape decision or an essential-service-access decision? The chapter 02 heuristic is: anything that touches employment, hiring, credit, insurance, education, or public benefits gets a high-risk suspicion; support triage is *not* on that list, but if a misroute materially delays a safety-critical outage ticket, the blast-radius argument may push back. Note the ambiguity rather than resolving it silently.
- **Article 50 step 4.** The system is reading free-text (and writing a classification), and the customer receives a confirmation email that names the routed team. Does that email say "an AI classified this" explicitly? If the chapter 02 heuristic ("external customer-facing + generative AI defaults to Article 50 transparency at minimum") fires, note it as a UX-copy ask.

**Section 3 — enterprise-internal tier tag.** Walk chapter 02's enterprise-internal tiers (Critical / High / Medium / Low). The two schemes are not derived mechanically from each other — a system can be EU AI Act limited-risk and enterprise-tier High if the volume (12,000 tickets per week across four jurisdictions) gives it meaningful blast-radius. Write one sentence of rationale.

**Section 4 — routing and SLA.** Who owns the next step (risk assessment author, FRIA drafter if Annex III fires, privacy team joint review, legal on any derogation question)? When does the SLA fire? Follow chapter 02's "triage decision log" field list.

**Section 5 — assumptions.** Any field in `intake-row.md` you had to infer — a provider name, a jurisdiction interpretation, a personal-data answer — goes here, flagged so the risk assessment can re-check.

### Step 4 — Copy governance-fill back to the intake row (10 min)

Return to `intake-row.md` section 3. Fill the governance-fill fields from chapter 01's table — intake tier assessment, EU AI Act tier tag, applicable sector regulator(s), applicable framework anchor(s), intake decision, assigned analyst — directly from the matching entries in `triage-decision.md`. A field that is in both places must be identical in both places; if they drift, the intake row is already stale.

### Step 5 — Scaffold the inventory row (20 min)

Open `inventory-row.md`. Work the four sections against chapter 03's "The inventory row — canonical schema" tables.

**Section 1 — identity and ownership.** Populate every field from chapter 03's identity-and-ownership table: system ID; system name; version / release; business owner; technical owner; governance owner; status; first deployed date; last material change date. For a system still at intake-acceptance stage, several fields are legitimately empty — mark them `pending` with a target date and owner, not blank, per chapter 03's expectation of a complete-looking row. `Status` is `proposed` at this stage (chapter 03's enum: proposed / in-development / in-production / retired).

**Section 2 — classification.** Populate every field from chapter 03's classification table: model family; model provider; data sources; autonomy level; deployment surface; EU AI Act tier; enterprise tier; sector regulator(s); applicable framework. Every one of these fields is sourced from the intake and the triage — if any field here does not match the matching entry in the earlier two artefacts, you have drift to fix *now*, before the row goes into the register.

**Section 3 — artefact cross-references.** For each row in chapter 03's artefact cross-reference table, write either a placeholder ID (`RA-2027-0029`, `IA-2027-0029`, `VR-2027-0029`, etc.) with a `not yet authored` note, or an explicit "not applicable at intake-acceptance stage". No blanks.

**Section 4 — lifecycle and status.** Populate `Next review due` (the program cadence + tier-driven multiplier your triage picked); `Continuous monitoring dashboard link` (`not yet provisioned — pending ML partner`); `Retirement plan` (not applicable at proposed status).

### Step 6 — Cross-check the three artefacts (10 min)

Walk the three files side-by-side and verify that **every value that appears on more than one artefact is identical on all of them**. The high-tripwire fields:

- **EU AI Act tier.** Appears on `intake-row.md` section 3, `triage-decision.md` section 2, and `inventory-row.md` section 2.
- **Enterprise-internal tier.** Appears on `triage-decision.md` section 3 and `inventory-row.md` section 2.
- **Business owner.** Appears on `intake-row.md` section 1 and `inventory-row.md` section 1.
- **Autonomy level.** Appears on `intake-row.md` section 1 and `inventory-row.md` section 2.
- **Deployment surface.** Appears on `intake-row.md` section 1 and `inventory-row.md` section 2.
- **Personal data involvement.** Appears on `intake-row.md` section 1 and drives routing in `triage-decision.md` section 4.

Any mismatch is a bug — fix it before the row is considered complete. Chapter 03's "Why it matters" line (the audit answer to "how do I trace everything about this system?") depends on this cross-artefact consistency.

### Step 7 — Self-check (5 min)

Walk the three artefacts top-to-bottom and verify:

- Every EU AI Act Article, Annex item, NIST RMF subcategory, or ISO 42001 clause referenced is either sourced from the chapter it appears in or marked `<!-- needs-research: ... -->`. Do not invent Article 5 sub-items, Annex III area numbers, or NIST subcategory codes from memory.
- Every field defined in chapter 01's business, technical, and governance-fill tables appears somewhere on `intake-row.md`. Missing fields are a bug, not a style preference.
- Every section defined in chapter 03's inventory schema appears somewhere on `inventory-row.md`.
- No "risk-register entry", "impact-assessment finding", or "control-testing result" is *written* on any of the three artefacts — those belong on downstream artefacts the inventory row *points at*, not on the row itself. Chapter 03's "What the inventory is *not*" section is the anchor.

## Expected output

Three markdown files in `~/aicg-labs/mod-102-lab-01/`:

- `intake-row.md` — three populated sections, one timestamp, one named analyst.
- `triage-decision.md` — five populated sections with the five-step EU AI Act walk visible and the enterprise-tier rationale written.
- `inventory-row.md` — four populated sections, every cross-reference resolving to a placeholder ID or an explicit `not yet authored` note.

Total length across the three files: roughly 1,000–1,800 words. A senior architect or governance lead should be able to read all three in ten minutes and either sign off on the routing or push back on specific rows.

## Checkpoint

A mentor, peer, or self-review walk. Answer honestly:

1. **Did the autonomy level survive from intake to inventory unchanged?** Chapter 01 defines *semi-autonomous* as "the system acts by default; a human can override before the action commits". ServiceLens routes a given ticket without pre-review (post-routing 5% QC sample does not count as pre-commit override on that ticket). The autonomy-level answer should be *semi-autonomous* on both `intake-row.md` and `inventory-row.md`. If you wrote *assistive* on intake and *semi-autonomous* on inventory (or vice versa), the three artefacts are already inconsistent before downstream teams see them.
2. **Did you flag the Article 50 transparency question?** The customer receives a confirmation email naming the routed team. Chapter 02's default-suspicion rule for external-customer-facing + generative-AI points at Article 50 at minimum. If the triage row does not note it, the UX-copy ask never gets filed and a transparency obligation goes uncovered.
3. **Did you flag the Annex III ambiguity rather than resolving it?** Chapter 02 is explicit that boundary cases go to legal. Customer-support routing is not clearly on the Annex III list, but it is near enough to "access to services" that the chapter-02 heuristic says *flag and route to counsel, do not interpret solo*. If your tier tag landed on a confident call without the ambiguity note, revise.
4. **Does the inventory row distinguish itself from a model-registry row?** The row names model family and provider (classification fields) but should not list hyperparameters, training-run IDs, or evaluation metric values — those are chapter 03's "what the inventory is *not*" list, owned by the ML team's model registry and *referenced* from the inventory via the cross-reference section. If any of those slipped onto the inventory row, move them.
5. **Does every cross-reference resolve?** Chapter 03's rule: broken cross-references silently rot the row. Every line in section 3 of `inventory-row.md` points at either a placeholder ID or an explicit `not yet authored` note, with no blanks.

If any of the five is "no", revise *that artefact section* before considering the lab done.

## Why this is a lab, not an exercise

Exercise-01 designs a whole intake questionnaire with two filled examples. Exercise-02 triages ten vignettes against the EU AI Act tier scheme. Exercise-03 builds an inventory schema and three lifecycle-state rows. All three exercises exercise one chapter's mechanics on a batch of inputs.

This lab is the inverted drill: *one* intake, *three* chapters chained, with every value forced to match across the three artefacts. The failure mode a new analyst actually has in production is not "cannot design an intake questionnaire" or "cannot triage one of ten vignettes" — it is "walks one intake all the way to an inventory row where the autonomy level, the tier tag, and the business owner each drifted silently between the intake, the triage, and the inventory". This lab exercises the cross-artefact consistency that chapter 03 requires and the exercises do not directly test.
