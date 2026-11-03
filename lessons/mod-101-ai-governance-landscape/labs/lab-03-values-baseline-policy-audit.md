# Lab 03 — Values-Baseline Audit of a Draft Responsible AI Policy

**Duration:** 90 minutes.
**Grounding chapters:** [05](../05-international-values-baseline.md), with cross-references to [01](../01-nist-ai-rmf-four-functions.md), [04](../04-eu-ai-act-risk-tiers-and-annex-iii.md), and [06](../06-role-scope-and-deferrals.md).
**Difficulty:** Core — analyst-tier policy-draft review.

## Objective

Audit a short draft Responsible AI Policy against the international values baseline chapter 05 names: the **OECD AI Principles**, the **Council of Europe Framework Convention on AI**, and the **UNESCO Recommendation on the Ethics of AI**. Produce an analyst-tier gap-finding memo that the head of AI governance can read in five minutes before routing the fixes to the senior architect.

Chapter 05 explicitly flags this as the analyst's role in the policy stack: *"The failure mode you are guarding against: a Responsible AI Policy that says less than what the country already signed onto is a public-relations and audit liability. The analyst is often the first person to notice."* This lab builds that noticing muscle.

Note the deferral boundary from chapter 06: analysts do not *rewrite* the policy. They **find and flag gaps**; architect and head of governance **own the fix**. Hold that line throughout the lab.

## Prerequisites

- Chapter 05 read.
- Chapter 06 read (so you keep the gap-finding scope boundary straight).
- A markdown editor.
- About 20 uninterrupted minutes to read the draft policy critically.

## The draft policy (fixed input)

Create the file `draft-policy-v0.1.md` in your workspace and paste this draft verbatim. **Do not improve it as you paste it in** — the gaps are the point of the lab.

```markdown
# Draft Responsible AI Policy — v0.1
_Draft shared by: VP Product. Reviewed by: nobody yet._

## 1. Our commitment
We will develop and deploy AI systems that drive business value for our customers and shareholders, while taking a thoughtful approach to risk.

## 2. Principles
We commit to the following principles, where feasible and cost-effective:

- **Accuracy.** Our AI systems will produce accurate outputs.
- **Fairness.** Our AI systems will treat users fairly, where measurable fairness metrics are available and cost-justified.
- **Privacy.** Our AI systems will handle personal data in accordance with applicable law.
- **Security.** Our AI systems will be secured per our existing security standards.

## 3. Governance
AI risk decisions are made by the Product Risk Committee. The committee reviews AI projects quarterly.

## 4. Transparency
We will inform customers that AI is used in our products when required by law.

## 5. Oversight
Humans will remain in the loop for high-stakes AI decisions, as determined by product management.

## 6. Scope
This policy applies to AI systems developed in-house. Third-party AI systems are governed by the Procurement Policy.
```

Yes, this draft is deliberately bad. That is the shape policy drafts actually arrive in before governance sees them.

## Steps

### Step 1 — Set up the workspace (5 min)

```bash
mkdir -p ~/aicg-labs/mod-101-lab-03
cd ~/aicg-labs/mod-101-lab-03
touch draft-policy-v0.1.md
touch audit-memo.md
```

Paste the draft policy above into `draft-policy-v0.1.md`. The audit memo goes in `audit-memo.md`.

Open `audit-memo.md` and lay in the scaffold:

```markdown
# Audit memo — draft Responsible AI Policy v0.1

## 1. Baselines used
## 2. Findings — OECD AI Principles
## 3. Findings — Council of Europe Framework Convention
## 4. Findings — UNESCO Recommendation on the Ethics of AI
## 5. Findings — EU AI Act (named law we are already on the hook for)
## 6. Framework-citation gaps
## 7. Scope and ownership findings (analyst-tier)
## 8. Prioritised ask for the senior architect
```

### Step 2 — Record the baselines (5 min)

Fill section 1 with a short table — this is the citation your findings reference.

```markdown
| Baseline | Instrument | Where it binds |
|---|---|---|
| Soft-law intergovernmental principles | OECD AI Principles (2019, updated 2024) | Adopted by ~50 countries incl. OECD + G20 members |
| Rights-and-democracy treaty | CoE Framework Convention on AI (CETS 225, opened for signature 5 September 2024) | Legally binding on parties once ratified |
| Broadest consensus recommendation | UNESCO Recommendation on the Ethics of AI (2021) | Adopted by all 193 UNESCO Member States |
| Domestic regulation (named example) | EU AI Act (Reg. 2024/1689) | Legally binding on EU-market activity |
```

### Step 3 — Audit against OECD Principles (15 min)

Walk the five OECD value-based principles from chapter 05, one by one. For each, write a finding row:

```markdown
| OECD Principle | Draft policy coverage | Finding |
|---|---|---|
| 1. Inclusive growth, sustainable development, well-being | ... | ... |
| 2. Human rights and democratic values, incl. fairness and privacy | ... | ... |
| 3. Transparency and explainability | ... | ... |
| 4. Robustness, security and safety | ... | ... |
| 5. Accountability | ... | ... |
```

Fill the "Finding" column with one of: `covered`, `partial — <why>`, `gap — <why>`, or `undercut — <why>`. Chapter 05's analyst-tier heuristic ("Does it caveat fairness with 'where feasible and cost-effective'? That is a red flag") applies here directly — the draft does exactly that in section 2. Flag it.

Expect at least three findings in the `gap` or `undercut` column. If you flag fewer than three, re-read the draft.

### Step 4 — Audit against the CoE Framework Convention (10 min)

Walk the seven CoE commitments chapter 05 names (human dignity and autonomy; equality and non-discrimination; privacy and data protection; transparency and oversight; accountability and effective remedies; reliability; safe innovation). Use the same finding-table shape.

Specific triggers to watch for in this draft:

- Does the policy mention human dignity or autonomy *anywhere*?
- Does the policy mention equality / non-discrimination, or only "fairness where measurable"?
- Does the policy commit to **effective remedies** — i.e., can a person meaningfully challenge an AI decision?
- Is the oversight commitment at section 5 strong enough to count as the CoE "oversight tailored to context" commitment, or is it a hand-wave?

### Step 5 — Audit against UNESCO (10 min)

Walk the UNESCO values and principles. Three specific chapter-05 points to apply:

- UNESCO is the strongest single instrument on the **environmental anchor** (sustainability, environment and ecosystems). Does the draft policy mention environmental impact at all? If not, `gap`.
- UNESCO names **awareness and literacy** as a principle (this also aligns with EU AI Act Article 4 AI-literacy obligations). Does the draft address AI literacy for employees?
- UNESCO is the broadest consensus — 193 states. The analyst finding here is that *silence against UNESCO is a defensible-ness problem*, not merely a stylistic one.

### Step 6 — Audit against the EU AI Act (10 min)

Chapter 05 names domestic regulation as a required layer. For the EU AI Act specifically — this employer's jurisdiction almost certainly includes the EU for any non-trivial product — check:

- Does the draft commit to Article 14 **human oversight** language strong enough to anchor a high-risk-system oversight design, or is section 5 ("as determined by product management") too vague?
- Does the draft acknowledge Article 50 **transparency obligations** for generative-AI and deep-fake outputs, or is section 4 ("when required by law") too narrow?
- Does the draft commit to Article 4 **AI literacy** obligations for staff dealing with AI systems?

Each is a chapter-04-anchored finding you can file.

### Step 7 — Framework-citation gaps (5 min)

Fill section 6 of the audit memo with findings on *which frameworks the draft fails to name*:

- Does the policy name **NIST AI RMF**? (Chapter 05 names it as a typical "framework of choice" in the enterprise stack.) If not, `gap`.
- Does the policy name **ISO/IEC 42001**? Same shape of finding.
- Does the policy name the specific **jurisdictions** the enterprise operates in and the laws it commits to comply with? Chapter 05's stack-layer table makes this a stack-cleanness requirement.

### Step 8 — Scope and ownership findings (10 min)

Fill section 7. Two chapter-6 anchored findings to look for:

- Section 3 of the draft puts AI risk decisions in the **Product Risk Committee** and reviews projects **quarterly**. Chapter 06 names a separate AI governance council with analyst-tier council support — the draft silently reorganises the governance structure. Analyst-tier finding: `ownership question — route to Senior Architect and Head of Governance`.
- Section 6 of the draft puts third-party AI under the **Procurement Policy** entirely. Chapter 06's owned-scope list includes "third-party AI vendor review with an AI-specific due-diligence questionnaire," and NIST AI RMF GOVERN 6 is specifically about AI supply-chain risk. Analyst-tier finding: `gap — the AI-specific overlay for third-party AI is missing`.

### Step 9 — Package the ask (10 min)

Fill section 8 with a **prioritised** ask for the senior architect. Target 5–8 bullets. Order them: most-defensible-public-finding first, most-ambiguous last.

Example shape (your findings will differ in specifics):

```markdown
In order of urgency to resolve before this policy is published:

1. **Remove "where feasible and cost-effective" caveat on fairness.** This undercuts OECD Principle 2 and UNESCO's fairness-and-non-discrimination principle. (Chapter 05 flags this exact pattern as the analyst's canonical red flag.)
2. **Add an environmental-impact commitment.** UNESCO (193 states) names this explicitly; silence is defensible-ness problem.
3. **Strengthen oversight language in section 5.** Current wording ("as determined by product management") is too vague to anchor EU AI Act Article 14 for a high-risk system.
4. **Add effective-remedies language.** CoE Framework Convention requires it; current draft is silent.
5. **Name the frameworks the enterprise operates against.** NIST AI RMF and ISO/IEC 42001 at minimum.
6. **Clarify third-party AI scope.** Current section 6 dumps all third-party AI into the Procurement Policy; add an AI-specific overlay citing NIST AI RMF GOVERN 6.
7. **Clarify governance ownership.** Section 3 puts decisions in the Product Risk Committee; reconcile with the AI governance council expected by the ownership map in chapter 06.
```

Each bullet is one analyst-tier finding; the fix routes to the senior architect and head of governance per chapter 06.

### Step 10 — Self-check (10 min)

Walk the memo top-to-bottom and verify:

- No bullet proposes a specific **policy rewrite in your voice**. Analysts find and flag; architect writes. If you wrote a sentence that starts with *"The policy should say..."*, soften to *"Gap against <baseline>; proposed resolution is architect scope."*
- Every finding cites the baseline instrument by name.
- The memo is readable in five minutes — if it is longer than ~800 words, cut.
- No fabricated OECD / CoE / UNESCO clause numbers. Any specific sub-article you cannot verify against the published instrument is marked `<!-- needs-research: -->`.

## Expected output

Two files in the workspace:

1. `draft-policy-v0.1.md` — the draft policy as pasted (do not edit).
2. `audit-memo.md` — the eight-section audit memo, roughly 500–900 words.

## Checkpoint

Hand `audit-memo.md` to a mentor, peer, or (self-review) your senior architect persona. Answer the following four questions honestly:

1. **Does the memo find the "where feasible and cost-effective" caveat on fairness?** This is the chapter 05 canonical red flag. If you missed it, re-read chapter 05's "sanity-checking a draft AI policy" section.
2. **Does the memo include the environmental-impact gap?** UNESCO is the strongest single source and the draft is silent on it. If you missed it, you under-weighted UNESCO.
3. **Does the memo stay inside analyst scope — flag, do not rewrite?** If any finding reads like a policy edit in your own voice, you crossed the deferral boundary chapter 06 draws. The right rewrite verb is "flag," not "fix."
4. **Does the memo cite each finding to a specific baseline instrument?** A finding that is not pinned to an instrument is a stylistic opinion, not an audit finding. If a bullet has no instrument name, pin it or cut it.

If any of the four is "no," revise *that part* before considering the lab done.

## Why this is a lab, not an exercise

Exercise 05 drills the deferral map on fifteen incoming asks. This lab drills a specific slice of that deferral map on a single artefact: the analyst's role in sanity-checking an enterprise AI policy against the international values floor. The failure mode in production is not "cannot route fifteen hallway asks" — it is "reads a draft policy, feels something is off, cannot name *what*, and lets it ship." This lab builds the muscle for naming *what*.
