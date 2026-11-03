# Lab 01 — One-Page Framework Cheatsheet for a Product Team

**Duration:** 90 minutes (reading + authoring + self-check).
**Grounding chapters:** [01](../01-nist-ai-rmf-four-functions.md), [02](../02-genai-profile-twelve-risks.md), [03](../03-iso-iec-42001-clause-walkthrough.md), [04](../04-eu-ai-act-risk-tiers-and-annex-iii.md), [05](../05-international-values-baseline.md).
**Difficulty:** Introductory — guided authoring.

## Objective

Produce a **single-page, stakeholder-facing cheatsheet** that a product team can keep at the top of their intake channel. It should answer, in one printed page, the four questions a PM or engineering lead actually asks the week they put up a new AI system:

1. *"Which frameworks do we care about here?"*
2. *"How do I tell if the EU AI Act makes this high-risk?"*
3. *"If this is generative AI, what risks should I pre-list before intake?"*
4. *"What values commitments is our policy already on the hook for?"*

Unlike exercise 01 (your personal flashcards) and exercise 02 (your analyst-tier ISO 42001 clause map), this artefact is **external-facing**. Scannability wins over completeness. If a stakeholder cannot find the answer in 30 seconds, the cheatsheet failed.

## Prerequisites

- Chapters 01, 02, 03, 04, and 05 read at least once.
- A markdown editor and a way to render markdown (VS Code preview, pandoc, a static-site preview — anything).
- About 30 minutes to be uninterrupted for the drafting pass.

## Context

Your head of AI governance has asked for an onboarding one-pager to pin inside the Product org's intake Slack channel. The audience is **product and engineering**, not fellow analysts. Treat the cheatsheet as a sticky note the team can glance at when a new AI system goes into intake — not a reference manual.

## Steps

### Step 1 — Set up the workspace (5 min)

Create a working folder and open an empty markdown file. From a terminal:

```bash
mkdir -p ~/aicg-labs/mod-101-lab-01
cd ~/aicg-labs/mod-101-lab-01
touch cheatsheet.md
```

Open `cheatsheet.md` in your editor and add a top-of-file title:

```markdown
# AI System Intake — One-Page Framework Cheatsheet

_Audience: Product + Engineering._ _Owner: AI Governance Team._ _Last reviewed: <YYYY-MM-DD>._
```

### Step 2 — Draft the four-panel skeleton (10 min)

A one-pager wants a predictable shape so readers' eyes land in the right place. Add four section headers under the title, in this order:

```markdown
## 1. The frameworks we operate against
## 2. EU AI Act — quick tier check
## 3. If it's generative AI — risks to pre-list
## 4. The values baseline our policy stands on
```

Do not fill them yet — the skeleton locks the shape so you do not spend 20 minutes on panel 1 and 2 minutes on panel 4.

### Step 3 — Fill panel 1: the frameworks we operate against (15 min)

The product team does not need the full RMF or 42001. They need to know what the governance team *cites* when it files a record, so they can anticipate the asks.

Author a short table in panel 1. Suggested shape — adapt the wording for your voice:

```markdown
| Instrument | What it is | When it shows up on your intake |
|---|---|---|
| NIST AI RMF 1.0 | Voluntary US framework — four functions (GOVERN, MAP, MEASURE, MANAGE), seven trustworthy-AI characteristics | Every intake: tier-tag → MAP → MEASURE evidence → MANAGE register entry |
| NIST AI 600-1 (GenAI Profile) | 12 generative-AI risks layered on top of the RMF | Any intake that touches generative AI (see panel 3) |
| ISO/IEC 42001:2023 | Certifiable AI management-system standard; layers onto an ISO/IEC 27001 ISMS via the shared Annex L structure | Intake adds a Statement of Applicability row and feeds AI KPIs into Clause 9 management review |
| EU AI Act (Reg. 2024/1689) | Horizontal EU regulation with four risk tiers plus GPAI | Any system placed on the EU market or whose outputs are used in the Union — see panel 2 |
```

Verify every claim against chapters 01 and 03 before moving on. If a cell cannot be verified, replace it with `<!-- needs-research: ... -->` rather than guessing.

### Step 4 — Fill panel 2: the EU AI Act tier check (15 min)

The product team wants to know *before* they open intake whether this is going to be a heavy or light lift. Give them the four-step tagging heuristic from chapter 04 ("Tagging heuristic — a quick decision tree"), in their own vocabulary.

Author the panel as a numbered mini-flow:

```markdown
Walk this list top-down. The first match wins.

1. **Does the system's intended purpose match an Article 5 prohibited practice?** Examples: manipulative techniques causing significant harm, social scoring by public authorities, emotion inference in workplaces or schools (outside narrow medical/safety exceptions), untargeted scraping of facial images, biometric categorisation inferring sensitive attributes. → **Stop. Do not open intake. Message the AI Governance team directly.**
2. **Is the system a safety component of an Annex I product with third-party conformity assessment?** (Medical devices, machinery, in-vitro diagnostics, radio equipment, toys, and others.) → **High-risk (Annex I route). Flag at intake.**
3. **Does the intended purpose fall under one of the eight Annex III areas?** (Biometrics; critical infrastructure; education and vocational training; employment and worker management; access to essential private or public services; law enforcement; migration, asylum, and border control; administration of justice and democratic processes.) → **High-risk (Annex III route). Flag at intake.**
4. **Does the system interact directly with people, generate synthetic content, perform emotion recognition or biometric categorisation, or produce deep fakes?** → **Limited risk — an Article 50 transparency disclosure applies. Flag at intake.**
5. **None of the above?** → **Minimal risk — standard intake row, no EU-specific overlay.**

**When in doubt, flag it.** Boundary cases go to legal — the cost of a flag is low, the cost of a mistier is high.
```

Verify each Annex III area against the chapter 04 list before shipping. Do not paraphrase Article 5 from memory in a stakeholder-facing document; link to the OJ text.

### Step 5 — Fill panel 3: the GenAI pre-list (15 min)

For any generative-AI intake, the product team can self-serve a first pass through the 12 risks before they even hit the intake queue. Give them the list with one-liners and the three defaults called out.

```markdown
If the system uses a generative model, walk this list. Mark each **applies / unsure / does not apply** and note why. The three in **bold** are near-universal defaults — expect them to apply unless you can argue otherwise.

1. CBRN Information or Capabilities — eased access to chemical, biological, radiological, or nuclear information.
2. Confabulation — confidently stated but unsupported outputs ("hallucination").
3. Dangerous, Violent, or Hateful Content.
4. **Data Privacy** — personal data disclosed, inferred, or memorised in training.
5. Environmental Impacts — energy / water / materials footprint of training and inference.
6. Harmful Bias or Homogenization.
7. Human-AI Configuration — over-reliance, anthropomorphism, unclear handoff.
8. Information Integrity — mis- or disinformation at scale.
9. **Information Security** — new attack surface (prompt injection, malware generation, credential extraction).
10. Intellectual Property — copyrighted material, trade-secret memorisation, unclear IP status of outputs.
11. Obscene, Degrading, and/or Abusive Content.
12. **Value Chain and Component Integration** — opaque data provenance, third-party components, downstream integrations you cannot inspect.

The intake form will ask you to list at least three applicable risks. **If you can only list the three defaults in bold, add one more** — a real generative-AI use case virtually always touches a fourth.
```

The "add one more" nudge is a cheatsheet-ism that comes from chapter 02's observation that intakes are always multi-risk and that an analyst who omits a plausible fourth risk gets sent back.

### Step 6 — Fill panel 4: the values baseline (10 min)

The product team should know what the enterprise is already on the hook for publicly, so they do not propose features that would require the enterprise to walk back a published commitment.

```markdown
Our Responsible AI Policy commits at least to what these three international instruments already put on paper. If a product proposal would require us to undercut any of them, raise it early.

- **OECD AI Principles** (soft-law, ~50 states): inclusive growth and well-being; respect for human rights and democratic values including fairness and privacy; transparency and explainability; robustness, security and safety; accountability.
- **Council of Europe Framework Convention on AI** (first legally binding international AI treaty, opened for signature 5 September 2024): human dignity and autonomy; equality and non-discrimination; privacy and data protection; transparency and oversight; accountability and effective remedies; reliability; safe innovation.
- **UNESCO Recommendation on the Ethics of AI** (adopted by all 193 member states, November 2021): includes an explicit environmental anchor (sustainability, environment and ecosystems) and introduces the Ethical Impact Assessment instrument.

If your proposal introduces a trade-off against any of these (e.g., "we'd save latency by not explaining the decision"), that trade-off is a governance conversation, not an implementation detail.
```

Verify the dates and the "first legally binding treaty" claim against chapter 05 before shipping.

### Step 7 — Compress to one page (10 min)

Render the file to one physical page (print preview, PDF export, or pandoc to A4 / US Letter). If it overruns, cut — do not shrink the font. Rules of thumb for cutting:

- Panel 1: four rows is the ceiling. If you added a fifth, drop it or merge it.
- Panel 2: the five-step heuristic is the ceiling. If you added sub-bullets under each step, cut them to parentheticals.
- Panel 3: the list stays at 12; the bolded defaults stay bolded; the "add one more" nudge stays.
- Panel 4: three bullets. Cut the sub-explanations before you cut a bullet.

Suggested render command (adjust for your toolchain):

```bash
pandoc cheatsheet.md -o cheatsheet.pdf \
  -V geometry:margin=0.75in -V fontsize=10pt
```

### Step 8 — Self-check (10 min)

Read the rendered one-pager cold, as if you were a product manager who has never seen it. For each of the four questions in the Objective section, time yourself finding the answer. Each should be ≤ 30 seconds.

Mark any panel that fails the 30-second rule and revise *that panel only* — do not rewrite the whole page.

## Expected output

A single markdown file `cheatsheet.md` plus a one-page rendered PDF `cheatsheet.pdf` in your workspace. The markdown file should:

- Fit on one page at 10–11pt in a readable serif or sans-serif.
- Carry a visible `Last reviewed:` date in the subtitle.
- Cite the governing instruments by their canonical names (NIST AI RMF 1.0; NIST AI 600-1; ISO/IEC 42001:2023; Regulation (EU) 2024/1689; OECD AI Principles; Council of Europe Framework Convention on AI; UNESCO Recommendation on the Ethics of AI).
- Contain no fabricated clause numbers, Annex A control IDs, Article 5 sub-items, or risk names. Any uncertain claim is marked `<!-- needs-research: ... -->` and dropped from the printed version.

## Checkpoint

Hand your cheatsheet to a non-governance colleague (a product manager, an engineer, a non-AI-expert friend) and ask them these three questions. If they can answer each in under 30 seconds using *only* your sheet, you have hit the mark:

1. "Our EU customers are going to use the outputs of this system. Where do I look first?" → They should land on panel 2.
2. "This is a generative-AI assistant. What should I pre-list before I open intake?" → They should land on panel 3 and name the three defaults in bold.
3. "Why does our policy insist on explainability?" → They should land on panel 4 and point at OECD Principle 3, the UNESCO transparency principle, or the CoE Convention's transparency-and-oversight commitment.

If any of the three takes longer than 30 seconds, revise that panel.

## Why this is a lab, not an exercise

Exercise 01 builds your personal flashcard deck (closed-book recall). This lab builds an **external-facing artefact for a stakeholder audience**. They draw from the same chapters but produce different deliverables with different audiences, different compression rules, and different failure modes. Keep both — the flashcards for your head, the cheatsheet for the Product org.
