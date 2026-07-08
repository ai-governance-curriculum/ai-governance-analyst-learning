# EU AI Act — Risk Tiers and Annex III

## Why this chapter

The [EU AI Act (Regulation (EU) 2024/1689)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) is the first comprehensive horizontal AI regulation. It reaches enterprises far beyond the EU: any AI system placed on the EU market, or whose outputs are used in the Union, is in scope. For an analyst, that turns "which EU AI Act tier is this?" into a triage question you will answer *at intake*, before the risk assessment even opens.

The Act is not a values statement. It is *product-safety-style regulation* for AI, built around a risk-tier scheme with hard obligations attached to each tier. Getting the tier wrong at intake means the wrong obligations flow downstream — the wrong impact assessment, the wrong documentation depth, the wrong deployment gate.

You do not become a lawyer for this. You become fluent enough to *tag* an intake against the tier scheme and route to counsel any case that sits close to a tier boundary.

## The four risk tiers

The Act sorts AI systems into four tiers of increasing regulatory intensity. Two are defined by *what the system does* (unacceptable, high-risk); the other two are defined by *how the system interacts with people* (transparency-obligated, minimal).

| Tier | Article anchor | Regulatory posture | Analyst-tier tag |
|---|---|---|---|
| **Unacceptable risk** | Article 5 | Prohibited on the EU market | Stop; escalate to legal / compliance leadership |
| **High risk** | Article 6 (via Annex I safety-component route or Annex III use-case route) | Allowed only with a documented set of obligations: risk-management system, data-governance, technical documentation, logging, transparency, human oversight, accuracy / robustness / cybersecurity, conformity assessment, registration, post-market monitoring | Full impact assessment; treat as flagship deliverable |
| **Limited risk (transparency obligations)** | Article 50 | Allowed with transparency obligations — disclose AI use, label synthetic / manipulated content, disclose to natural persons that they are interacting with an AI system where not obvious | Note the disclosure obligation; verify UX text and content labels exist |
| **Minimal risk** | (No specific article; residual category) | No specific obligations under the Act | Standard governance record; no EU-specific overlay |

There is also a distinct set of obligations for **General-Purpose AI (GPAI) models** (Article 51 onward, plus systemic-risk designation), which apply to the *providers* of foundation models. Most enterprise use cases will consume a GPAI model rather than provide one — but if your employer is the provider, GPAI obligations dominate.

## What Article 5 prohibits

Unacceptable-risk practices under Article 5 include (paraphrased — check the article text for exact wording):

- Manipulative or deceptive techniques that materially distort behaviour and cause significant harm.
- Exploiting vulnerabilities of specific groups (age, disability, socio-economic situation) causing significant harm.
- Social scoring by public authorities producing detrimental treatment.
- Real-time remote biometric identification in public spaces for law-enforcement (with narrowly-scoped exceptions).
- Untargeted scraping of facial images from the internet or CCTV to build facial-recognition databases.
- Emotion inference in workplaces and educational institutions (with medical / safety exceptions).
- Biometric categorisation inferring sensitive attributes.
- Predictive policing based solely on profiling.

If an intake description matches one of these, the analyst does not "tier" — the analyst files a *hard block* and routes to compliance leadership. Do not paraphrase Article 5 from memory when issuing that block; cite the sub-article.

## What Article 6 and Annex III cover — high risk

An AI system is high-risk under Article 6 if either:

1. It is a **safety component** of a product covered by EU harmonisation legislation listed in **Annex I** (medical devices, machinery, toys, radio equipment, in-vitro diagnostics, and others), and the underlying product is subject to third-party conformity assessment; **or**
2. It falls under an area listed in **Annex III**.

Annex III lists eight areas (paraphrased — cite the Annex text for the definitive list):

1. **Biometrics** — remote biometric identification, biometric categorisation, emotion recognition (in domains not already prohibited).
2. **Critical infrastructure** — safety components in road traffic, water, gas, heating, electricity, and digital infrastructure.
3. **Education and vocational training** — determining access, admission, evaluation, and detecting exam-cheating.
4. **Employment, workers management, and access to self-employment** — recruitment, promotion, task allocation, monitoring and evaluation.
5. **Access to and enjoyment of essential private services and essential public services and benefits** — public benefit eligibility, credit-scoring / creditworthiness, life-and-health insurance risk assessment, emergency-service dispatch.
6. **Law enforcement** — victim / crime risk assessments, polygraphs, evidence reliability assessment, profiling.
7. **Migration, asylum, and border-control management** — polygraphs, migration-risk assessment, application examination.
8. **Administration of justice and democratic processes** — assisting judicial authorities in researching and interpreting facts and the law, and (added scope) systems intended to influence electoral outcomes or voting behaviour.

Analyst-tier drill: for a new intake, work through Annex III area-by-area and ask *"could a reasonable person say this system's intended purpose falls into this area?"* If yes, tag as high-risk and start the full impact assessment.

There are narrow **derogations** in Article 6(3) — an Annex III system may not be high-risk if it performs a narrow procedural task, improves a completed human activity, detects deviations from decision patterns without replacing prior human assessment, or performs a preparatory task. When you invoke a derogation, document *which one*, and expect legal review.

## High-risk obligations — what the analyst files

For a system tagged high-risk, the enterprise obligations (Articles 8–15 for providers; Article 26 for deployers; and others) drive a large downstream artefact list. From the analyst desk, the flow looks like:

- **Risk-management system** (Article 9) — a rolling AI-risk-management process. This maps directly to NIST AI RMF MAP + MEASURE + MANAGE work already discussed.
- **Data and data governance** (Article 10) — training / validation / test data provenance, quality, and bias-relevance checks. This lands in `mod-105` (dataset documentation) and `mod-104` (bias review).
- **Technical documentation** (Article 11 and Annex IV) — an artefact list the analyst helps assemble.
- **Record-keeping and logging** (Article 12) — logs enabling post-market monitoring and traceability. Analyst work: verify the log-retention policy is documented.
- **Transparency and provision of information to deployers** (Article 13) — the provider-facing information sheet.
- **Human oversight** (Article 14) — design and organisational measures for meaningful human oversight. Analyst work: verify the oversight design is stated in the impact assessment.
- **Accuracy, robustness, and cybersecurity** (Article 15) — testing and evidence requirements. Analyst work: read the evidence into the governance record.
- **Fundamental Rights Impact Assessment (FRIA)** (Article 27) — required for certain deployers (public bodies, and providers of essential services such as banking or insurance) before first use. Analyst work: author the first draft (see `mod-105`).
- **Registration in the EU database** (Article 71) — for high-risk systems.
- **Post-market monitoring** (Article 72) and **serious-incident reporting** (Article 73) — analyst work: file the monitoring summaries and incident notes (`mod-109`).

That is a lot. Your job at intake is not to *deliver* all of it. It is to *tag the tier correctly* so the machinery downstream produces the right list of deliverables.

## Limited-risk transparency obligations

Article 50 applies to systems that interact with people or generate synthetic content. Paraphrased obligations:

- Systems that interact directly with natural persons must inform them they are dealing with an AI system, unless it is obvious.
- Providers of generative-AI systems must ensure outputs are marked as machine-readable synthetic content (with narrow exceptions).
- Deployers of emotion-recognition or biometric-categorisation systems must inform exposed persons.
- Deployers of deep-fake content must disclose it as artificially generated or manipulated (with exceptions for law-enforcement and clearly artistic / satirical use).

At analyst level: check the UX copy, check the content-labelling pipeline, note the obligation in the register.

## GPAI and systemic-risk models

Chapter V of the Act imposes obligations on providers of general-purpose AI models — including technical documentation, information for downstream providers, copyright / training-data summaries, and, for models designated as systemic risk, additional evaluation, adversarial-testing, incident-reporting, and cybersecurity obligations. If your employer *provides* a GPAI model, this is the deep track. If your employer *uses* one, the [EU AI Office GPAI Code of Practice](https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice) tells you what your provider's obligations look like and what evidence you can expect from them.

## Timeline — when the obligations bite

The Act entered into force on 1 August 2024, and its obligations phase in over roughly the next 36 months:

- **Prohibitions** (Article 5) — applicable from 2 February 2025.
- **GPAI obligations** (Chapter V) — applicable from 2 August 2025.
- **Most other obligations, including high-risk systems under Annex III** — applicable from 2 August 2026.
- **High-risk systems that are safety components of Annex I products** — applicable from 2 August 2027.

<!-- needs-research: verify each dated milestone above against the current published consolidated text of Regulation (EU) 2024/1689 before citing it externally; the phase-in schedule has been the subject of multiple published corrigenda and any date used in an audit-facing document should be pinned to the specific Article and effective date in the consolidated text. -->

At analyst level, the practical read is: prohibitions and GPAI are already live; high-risk-under-Annex-III bites in 2026; treat any 2027 exceptions as legal-review territory.

## Tagging heuristic — a quick decision tree

Use this at intake:

1. Does the system's intended purpose match any Article 5 prohibited practice? → **Unacceptable — block and escalate.**
2. Is the system a safety component of an Annex I product with third-party conformity assessment? → **High-risk (Annex I route).**
3. Does the intended purpose fall in any Annex III area? → **High-risk (Annex III route).** Consider Article 6(3) derogations only with legal review.
4. Does the system directly interact with people, generate synthetic content, do emotion recognition / biometric categorisation, or produce deep fakes? → **Limited-risk (Article 50 transparency).** Note it can also be high-risk if step 3 hit.
5. None of the above? → **Minimal risk.** Standard governance record; no EU-specific overlay.

Any answer that is "close to a boundary" gets tagged **needs-follow-up** and routed to legal.

## What to memorise

- Four tiers: **unacceptable / high / limited / minimal**, with their anchor articles.
- The two high-risk routes: **Annex I safety component** vs **Annex III use-case list**.
- The **eight Annex III areas** (biometrics; critical infrastructure; education; employment; essential services; law enforcement; migration and border; justice and democratic processes).
- The three phase-in dates (2 Feb 2025; 2 Aug 2025; 2 Aug 2026) — verify against the latest consolidated text before citing externally.

## Summary

The EU AI Act sorts AI systems into unacceptable / high / limited / minimal risk, with a distinct track for GPAI and systemic-risk models. High-risk is triggered either by being a safety component of an Annex I product or by falling into one of the eight Annex III areas. Analyst work at intake is a tier-tag, not a legal opinion — tag correctly, route boundary cases to counsel, and let the downstream artefact list follow from the tier.
