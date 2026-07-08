# NIST AI RMF Generative AI Profile (AI 600-1) — The Twelve Risks

## Why this chapter

NIST released the [Generative AI Profile (NIST AI 600-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) in July 2024 as a *cross-sectoral profile* of the AI RMF for generative AI. It is the shortest path to a defensible enumeration of "what can go wrong with generative AI" that an enterprise governance program can adopt without arguing with the intake team about definitions.

The Profile is not a new framework. It is a lens over the existing AI RMF that (a) lists a canonical set of generative-AI-specific risks, and (b) reorganises the RMF's suggested actions to focus on those risks. As an analyst you will be asked which of these 12 risks apply to *this* intake — often before the register entry exists — so the twelve names and their intents need to be immediate recall.

## How to read the Profile

The Profile does two things at once. It gives you:

1. A **taxonomy of 12 risks** unique or exacerbated by generative AI.
2. A set of **RMF-aligned actions** — the Profile re-indexes MAP / MEASURE / MANAGE / GOVERN subcategory guidance against those 12 risks.

You use the taxonomy at intake ("which of these applies to this use case?") and you use the actions later, once the register entry needs a mitigation ("what does the Profile suggest for MEASURE 2.7 on Confabulation?").

## The twelve risks

The Profile enumerates 12 risks. Below is a one-line intent and a plausible internal use case for each. The use-case column is illustrative — real intake will surface variants — but the pattern is what to memorise.

| # | Risk | One-line intent | Plausible internal use case |
|---|---|---|---|
| 1 | **CBRN Information or Capabilities** | The model provides eased access to chemical, biological, radiological, or nuclear weapon information or capabilities | Research-lab knowledge assistant that indexes public chemistry papers |
| 2 | **Confabulation** | The model produces confidently stated but unsupported or false content (hallucination) | Customer-support agent-facing assistant summarising policy documents |
| 3 | **Dangerous, Violent, or Hateful Content** | The model produces or facilitates production of violent, hateful, or otherwise dangerous content | Consumer-facing content-generation feature (image or text) |
| 4 | **Data Privacy** | The model discloses, infers, or enables inference of personal data — including through training-data memorisation | Fine-tuned assistant trained on internal CRM transcripts |
| 5 | **Environmental Impacts** | Training and inference carry material energy, water, and materials footprints | Enterprise-wide roll-out of a large-parameter foundation model for internal tooling |
| 6 | **Harmful Bias or Homogenization** | The model produces biased outputs, or homogenises outputs in a way that flattens groups or perspectives | Internal résumé-screening pilot; marketing-copy generator |
| 7 | **Human-AI Configuration** | Interaction design causes over-reliance, anthropomorphism, or unclear handoff between human and model | Clinician decision-support summary in an EHR sidebar |
| 8 | **Information Integrity** | The model produces or amplifies mis- or disinformation at scale | Marketing / social-media content pipeline; deepfake-adjacent voice or image generation |
| 9 | **Information Security** | The model introduces new attack surfaces or is used to lower the cost of an attack (prompt injection, malware generation, credential extraction) | RAG assistant with tool-use over internal APIs |
| 10 | **Intellectual Property** | The model reproduces copyrighted material, memorises trade secrets, or produces outputs of unclear IP status | Marketing-copy generator; code-generation assistant on proprietary repos |
| 11 | **Obscene, Degrading, and/or Abusive Content** | The model produces or facilitates sexual, degrading, or abusive content — including CSAM adjacency | Any consumer-facing generation feature; internal image-generation pilot |
| 12 | **Value Chain and Component Integration** | Risks accrue from opaque data provenance, third-party components, and downstream integrations you cannot inspect | Any hosted-model application, fine-tune on a purchased dataset, or agentic pipeline chaining vendor tools |

<!-- needs-research: verify the canonical spelling and ordering of each of the 12 risks against the current published PDF of NIST AI 600-1 before citing this list in an audit-facing document; NIST sometimes revises phrasing between versions and the analyst-facing citation should track the latest published edition. -->

## Two patterns worth internalising

**Every intake touches more than one risk.** A résumé-screening pilot is not *just* Harmful Bias — it is Harmful Bias (6) + Data Privacy (4) + Human-AI Configuration (7, over-reliance on a screening score) + Value Chain (12, if the model is hosted). Train yourself to list at least three risks per intake before you commit to a shortlist.

**Some risks are almost universal.** Value Chain and Component Integration (12), Data Privacy (4), and Information Security (9) show up on virtually every enterprise generative-AI intake. Treat them as *default candidates* — the analyst who omits them will be sent back to redo the register entry.

## Matching risks to trustworthy-AI characteristics

The Profile aligns each risk back to the RMF's trustworthy-AI characteristics (safe; secure and resilient; valid and reliable; privacy-enhanced; fair with bias managed; accountable and transparent; explainable and interpretable). A quick heuristic when you need to cross-reference:

- Confabulation → Valid and reliable
- CBRN, Dangerous Content, Obscene Content → Safe
- Information Security → Secure and resilient
- Data Privacy → Privacy-enhanced
- Harmful Bias or Homogenization → Fair with harmful bias managed
- Information Integrity, Human-AI Configuration → Accountable and transparent
- Value Chain and Component Integration → Cross-cutting; usually Accountable and transparent + Secure and resilient
- Environmental Impacts → Not neatly one; treated as its own concern

The Profile itself is the authoritative source for these mappings — use the table above as a scaffold, verify against the PDF for anything you cite externally.

## Working with the Profile — analyst pattern

When an intake questionnaire arrives with a "yes" to "involves generative AI":

1. Read the purpose statement and the deployment surface.
2. Walk the 12 risks and mark each **applies / does not apply / needs follow-up**.
3. For anything marked *applies*, open the Profile's action guidance for that risk and pull the two or three suggested MEASURE / MANAGE actions closest to your enterprise's shape.
4. Cite the risk name and the RMF subcategory in the register entry (e.g., "Confabulation — MEASURE 2.9").
5. Route MEASURE actions to the ML / evaluation team; route MANAGE actions to the system owner.

The Profile is *sufficient* for a first-draft register entry. It is not sufficient for a domain-specific deep dive — a healthcare intake will additionally reach for [Good ML Practice](https://www.fda.gov/medical-devices/software-medical-device-samd/good-machine-learning-practice-medical-device-development-guiding-principles) and clinical-validation literature; a financial-services intake will reach for [SR 11-7](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm). Those overlays live in later modules.

## Concrete example — an internal marketing-copy generator

An intake proposes an internal tool that generates first-draft marketing copy from a product brief, using a hosted frontier model.

- **Confabulation (2)** — Applies. Copy might state features the product does not have.
- **Harmful Bias or Homogenization (6)** — Applies. Persona-targeted copy risks stereotyping; and homogenised style across campaigns may weaken brand voice.
- **Intellectual Property (10)** — Applies. Copy may reproduce copyrighted phrasing; provenance of training data is unclear.
- **Information Integrity (8)** — Applies at scale — mis-stated claims could reach thousands of customers.
- **Data Privacy (4)** — Applies if the product brief includes unreleased data; the hosted model's data-handling terms need review.
- **Value Chain and Component Integration (12)** — Applies. Hosted model, hosted vector store, third-party analytics.
- **Human-AI Configuration (7)** — Applies. Over-reliance on the generator by copywriters is a plausible operational risk.
- CBRN, Dangerous / Violent / Hateful, Obscene, Environmental, Information Security — mark *does not apply* or *needs follow-up* and note why.

That is seven risks on a single intake — realistic, and the shape reviewers will expect.

## What to memorise

- The **12 risks** by name — even the awkward ones (Value Chain and Component Integration is often forgotten in interviews).
- The three near-universal defaults: **Value Chain, Data Privacy, Information Security**.
- Where to find the Profile: the [NIST AI 600-1 PDF](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) and the [GenAI Profile page on the AI Resource Center](https://airc.nist.gov/AI_RMF_Knowledge_Base/AI_RMF/Uses/GenAI-Profile).

## Summary

The Generative AI Profile gives you a 12-risk taxonomy that is defensible, cross-sectoral, and grounded in the RMF you already use. Use it as the intake lens for any generative-AI use case, always list Value Chain / Data Privacy / Information Security as defaults, and cite the specific RMF subcategory in the register entry so the reviewer can trace your reasoning.
