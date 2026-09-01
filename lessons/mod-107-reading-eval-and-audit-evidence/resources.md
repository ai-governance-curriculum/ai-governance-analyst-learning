# Resources — mod-107 Reading Eval, Red-Team, and Audit Evidence into Governance Records

Primary references for every report shape, benchmarking axis, and delegation-boundary artefact this module walks. Read the primary source (the eval framework's docs, the vendor's own published card, the standard's authoritative text) first; practitioner briefings and law-firm client alerts are useful for *noticing* a change quickly but do not sit in the eval row's *source-artefact link* column — the analyst chases the primary reference before writing the row.

## Frameworks and standards this module sits inside

Chapter 01 and chapter 05 orientation references.

- [NIST AI Risk Management Framework 1.0 (AI 100-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf) — the AI RMF; the Measure and Manage functions frame the eval-and-mitigation loop the analyst reads evidence from.
- [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) — the RMF Playbook; specific Measure-family actions map directly to the report shapes chapters 02–04 walk.
- [NIST AI RMF Generative AI Profile (AI 600-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) — the twelve GenAI risk categories the red-team methodology (chapter 04) and the benchmark categories (chapter 08) reference.
- [NIST AI Resource Center (AIRC)](https://airc.nist.gov/) — the RMF resource hub; publishes crosswalks, playbook updates, and Generative AI Profile companion material.
- [ISO/IEC 42001:2023 — Information technology — Artificial intelligence — Management system](https://www.iso.org/standard/81230.html) — the AI management-system standard. Clause 9 (performance evaluation) is where an internal audit reads the eval-row register against; clause 8 (operational planning and control) is where release-assurance sits.
- [ISO/IEC 23894:2023 — Information technology — Artificial intelligence — Guidance on risk management](https://www.iso.org/standard/77304.html) — AI risk-management guidance; complements the AI RMF and the eval-evidence discipline.
- [ISO/IEC 42005:2025 — Information technology — Artificial intelligence — AI system impact assessment](https://www.iso.org/standard/44545.html) — the ISO AI-system impact-assessment standard cited from `mod-105` and from the impact-assessment refresh triggers this module's rows fire.
- [ISO/IEC JTC 1/SC 42 (Artificial Intelligence)](https://www.iso.org/committee/6794475.html) — the SC 42 committee page; useful for tracking work items on AI evaluation, testing, and assurance in development.
- [OECD.AI Policy Observatory — AI Incidents Monitor](https://oecd.ai/en/incidents) — the OECD's incident monitor, useful for cross-referencing red-team findings and post-market surveillance signals to a broader landscape.
- [MLCommons AILuminate benchmark and Safety Working Group](https://mlcommons.org/working-groups/ai-safety/ai-safety/) — the MLCommons AI Safety benchmark suite; a growing shared reference for safety-eval categories across the industry.

## Eval frameworks — chapter 02

Inspect and the open-source eval-framework landscape.

- [UK AI Security Institute — Inspect framework documentation](https://inspect.aisi.org.uk/) — the canonical reference for Inspect's task / dataset / solver / scorer / model / sample / log / metric vocabulary.
- [`UKGovernmentBEIS/inspect_ai` on GitHub](https://github.com/UKGovernmentBEIS/inspect_ai) — the Inspect framework source code.
- [`UKGovernmentBEIS/inspect_evals` on GitHub](https://github.com/UKGovernmentBEIS/inspect_evals) — the Inspect evaluations catalogue; MMLU, ARC, GPQA, HumanEval, and safety-oriented tasks the enterprise's eval-engineering function may draw from.
- [UK AI Security Institute — homepage](https://www.aisi.gov.uk/) — the AISI hub; publishes safety research, evaluation methodology notes, and the [Advanced AI Evaluations May 2024 update](https://www.aisi.gov.uk/work/advanced-ai-evaluations-may-update) and successor briefings.
- [US AI Safety Institute (NIST)](https://www.nist.gov/aisi) — the US-AISI hub; publishes evaluation guidance and the [ARIA (Assessing Risks and Impacts of AI)](https://ai-challenges.nist.gov/aria) programme.
- [METR (Model Evaluation and Threat Research)](https://metr.org/) — METR's evaluation methodology on autonomy and dangerous capabilities; a named external evaluator on many vendor cards.
- [Apollo Research](https://www.apolloresearch.ai/) — Apollo's deception and scheming evaluations; another named external evaluator on vendor cards.
- [EleutherAI `lm-evaluation-harness`](https://github.com/EleutherAI/lm-evaluation-harness) — the open-source eval harness; predates and complements Inspect; still widely used for capability-benchmark reproduction.
- [BIG-bench (Beyond the Imitation Game)](https://github.com/google/BIG-bench) — the community capability-benchmark suite.
- [HELM (Holistic Evaluation of Language Models)](https://crfm.stanford.edu/helm/) — Stanford CRFM's evaluation platform; a shared reference for capability and safety benchmarking.
- [Anthropic — Challenges in evaluating AI systems](https://www.anthropic.com/news/evaluating-ai-systems) — a candid write-up of the difficulties in producing robust safety evaluations; useful context for reading vendor eval sections critically.

## RAG-triad and retrieval-quality evaluation — chapter 03

The RAG-eval tooling landscape.

- [TruLens documentation](https://www.trulens.org/) — the TruEra project that popularised the RAG triad (context relevance, groundedness, answer relevance).
- [`truera/trulens` on GitHub](https://github.com/truera/trulens) — the TruLens source repository.
- [RAGAS documentation](https://docs.ragas.io/) — an alternative RAG-eval framework; introduces *faithfulness*, *context precision*, *context recall*, and *answer correctness* extensions.
- [`explodinggradients/ragas` on GitHub](https://github.com/explodinggradients/ragas) — the RAGAS source repository.
- [DeepEval documentation](https://docs.confident-ai.com/) — Confident AI's LLM eval framework covering RAG metrics alongside broader LLM-eval scaffolding.
- [`confident-ai/deepeval` on GitHub](https://github.com/confident-ai/deepeval) — the DeepEval source repository.
- [LangChain evaluation documentation](https://python.langchain.com/docs/guides/productionization/evaluation/) — LangChain's RAG-eval helpers; often the shape enterprise RAG-eval reports are authored against.
- [LlamaIndex evaluation guide](https://docs.llamaindex.ai/en/stable/module_guides/evaluating/) — LlamaIndex's RAG-eval helpers; another common shape.
- [OpenAI Evals framework](https://github.com/openai/evals) — the OpenAI-published evals framework; still used for many enterprise capability and RAG evals.
- [Hugging Face — Evaluate library](https://huggingface.co/docs/evaluate/) — general-purpose evaluation library; used across many enterprise eval pipelines.

## Red-team engagements and adversarial-eval taxonomies — chapter 04

The threat-catalogue and adversarial-methodology landscape.

- [OWASP LLM Top 10 (2025)](https://genai.owasp.org/llm-top-10/) — the canonical LLM threat catalogue; LLM01 prompt injection through LLM10 unbounded consumption. The [OWASP Gen AI Security Project hub](https://genai.owasp.org/) is the umbrella.
- [MITRE ATLAS](https://atlas.mitre.org/) — the ML-system adversarial-tactic taxonomy; tactics and techniques red-team reports map findings against.
- [MITRE ATLAS matrix](https://atlas.mitre.org/matrices/ATLAS) — the tactic-and-technique matrix; useful for reading a red-team report's methodology section.
- [MITRE ATT&CK](https://attack.mitre.org/) — the parent adversarial-behaviour framework the ATLAS ML-specific overlay sits alongside.
- [NIST AI 600-1 Generative AI Profile](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) — the twelve GenAI risk categories a red-team report scopes coverage against.
- [NIST AI 100-2e2025 — Adversarial Machine Learning taxonomy](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-2e2025.pdf) — NIST's taxonomy of adversarial-ML attacks; useful for characterising red-team findings in categories the AI RMF references.
- [CVSS 4.0 specification](https://www.first.org/cvss/v4-0/specification-document) — the CVSS severity-scoring specification; some enterprise red-team severity rubrics adapt CVSS's exploitability / impact / scope shape.
- [OWASP Risk Rating Methodology](https://owasp.org/www-community/OWASP_Risk_Rating_Methodology) — OWASP's severity × likelihood risk-rating shape; another common source for red-team rubrics.
- [MLSecOps community](https://mlsecops.com/) — the MLSecOps community hub; publishes AI red-teaming resources.
- [`leondz/garak` on GitHub](https://github.com/leondz/garak) — an open-source LLM vulnerability scanner useful for automating parts of the red-team engagement's exploratory pass.
- [`nvidia/garak` — NVIDIA-maintained fork](https://github.com/NVIDIA/garak) — NVIDIA's maintained fork.
- [Anthropic — Red-teaming language models to reduce harms](https://arxiv.org/abs/2209.07858) — Anthropic's early red-team paper; foundational methodology.
- [Anthropic — Challenges in red-teaming AI systems](https://www.anthropic.com/news/challenges-in-red-teaming-ai-systems) — Anthropic's operational write-up on red-team practice.
- [OpenAI — Red-teaming network](https://openai.com/blog/red-teaming-network) — OpenAI's external red-team-network programme.
- [DEF CON AI Village](https://aivillage.org/) — the DEF CON AI Village; publishes the Generative Red Team competition materials the enterprise's red-team function may reference for crowdsourced-adversarial methodology.

## Public system cards — chapter 06

Load-bearing exemplars per vendor family. Vendor URLs move; the row records both the live URL and a snapshot.

- **OpenAI.**
    - [OpenAI research index](https://openai.com/research/) — the OpenAI research page; the canonical entry point for current system cards.
    - [GPT-4 System Card (2023, PDF)](https://cdn.openai.com/papers/gpt-4-system-card.pdf) — the first widely-cited system card.
    - [GPT-4V(ision) System Card (2023, PDF)](https://cdn.openai.com/papers/GPTV_System_Card.pdf) — the modality-extended shape.
    - [GPT-4o System Card](https://openai.com/index/gpt-4o-system-card/) — the omnimodal shape.
    - [OpenAI o1 System Card (2024, PDF)](https://cdn.openai.com/o1-system-card-20241205.pdf) — the reasoning-model shape.
    - <!-- needs-research: verify current OpenAI system-card URLs (o3, GPT-4.5, GPT-5, and successor releases) against the OpenAI research index at time of use; system-card URLs change per release and older cards are moved or superseded. -->
    - [OpenAI usage policies](https://openai.com/policies/usage-policies/) — the deployment-constraint reference that pairs with the system cards.
- **Anthropic.**
    - [Anthropic model overview](https://www.anthropic.com/claude) — the Claude models overview; entry point for current model cards.
    - [Anthropic news page](https://www.anthropic.com/news) — the announcements page; new model releases and card revisions land here.
    - [Claude 3 Model Card (PDF)](https://www-cdn.anthropic.com/de8ba9b01c9ab7cbabf5c33b80b7bbc618857627/Model_Card_Claude_3.pdf) — the Claude 3 model card.
    - <!-- needs-research: verify current Anthropic model-card URLs for the Claude 3.5, Claude 4, and successor releases against the Anthropic news page at time of use. -->
    - [Anthropic Usage Policy](https://www.anthropic.com/legal/aup) — the acceptable-use policy the card's deployment-constraint sections reference.
    - [Anthropic Trust Center](https://trust.anthropic.com/) — the trust-and-security surface that supplements the model card on security controls.
- **Google DeepMind.**
    - [DeepMind publications page](https://deepmind.google/research/) — the publications hub; entry point for current Gemini technical reports.
    - [Gemini 1.5 technical report (arXiv 2403.05530)](https://arxiv.org/abs/2403.05530) — the Gemini technical-report shape.
    - <!-- needs-research: verify current Gemini technical-report URLs (arXiv identifiers and DeepMind publications page) for Gemini 2.x, Gemini 3.x, and successor releases at time of use. -->
- **Meta.**
    - [Meta Llama models repository](https://github.com/meta-llama/llama-models) — the Llama models source; model cards live here.
    - [Llama 2 model card](https://github.com/meta-llama/llama-models/blob/main/models/llama2/MODEL_CARD.md) — the Llama 2 card.
    - [Llama 3 model card](https://github.com/meta-llama/llama-models/blob/main/models/llama3/MODEL_CARD.md) — the Llama 3 card.
    - <!-- needs-research: verify current Llama model-card URLs for Llama 4 and successor releases against the Meta Llama models repository at time of use. -->
    - [Meta AI acceptable use policy](https://llama.meta.com/use-policy/) — the deployment-constraint reference.
- **Other frontier providers.** [Mistral model overview](https://docs.mistral.ai/getting-started/models/), [Cohere model cards](https://docs.cohere.com/docs/models), and [Amazon Bedrock foundation-model catalog](https://docs.aws.amazon.com/bedrock/latest/userguide/models-supported.html) — the vendor-neutral / reseller surface that carries model-provider documentation where the enterprise consumes models via a hosted platform.
- **Foundational reading on the model-card shape.** [Mitchell et al., *Model Cards for Model Reporting* (2019)](https://arxiv.org/abs/1810.03993) — the foundational model-card paper; the shape from which system cards derive.
- **Foundational reading on the datasheet shape.** [Gebru et al., *Datasheets for Datasets* (2018)](https://arxiv.org/abs/1803.09010) — the foundational datasheet paper; cited from RAG-triad corpora and from training-data-summary sections of system cards.

## Responsible Scaling Policies and Preparedness Frameworks — chapter 07

The RSP-family disclosure landscape. Frameworks revise; the analyst records the exact version identifier per row.

- [Anthropic Responsible Scaling Policy](https://www.anthropic.com/rsp) — Anthropic's RSP with the AI Safety Levels (ASL) framing.
- [Anthropic news — RSP updates](https://www.anthropic.com/news) — Anthropic's news page; RSP revisions are announced here.
- [OpenAI Preparedness Framework](https://openai.com/preparedness/) — OpenAI's Tracked Categories × Risk Levels grid (Cybersecurity, CBRN, Persuasion, Model Autonomy, scored Low / Medium / High / Critical).
- [OpenAI Safety Evaluations Hub](https://openai.com/safety/) — OpenAI's safety hub; Safety Scorecards and Preparedness updates land here.
- [Google DeepMind Frontier Safety Framework — introduction (May 2024)](https://deepmind.google/discover/blog/introducing-the-frontier-safety-framework/) — the DeepMind FSF with the Critical Capability Levels (CCLs) framing.
- [Google DeepMind — publications and safety pages](https://deepmind.google/discover/) — the DeepMind hub; FSF revisions and successor documents are indexed here.
- [Frontier Model Forum](https://www.frontiermodelforum.org/) — the industry forum; publishes on RSP practice and cross-lab safety-eval alignment.
- [AI Governance Alliance (World Economic Forum)](https://initiatives.weforum.org/ai-governance-alliance/home) — WEF's AI-governance initiative; RSP and Preparedness-Framework references appear in AGA reports.
- [Partnership on AI](https://partnershiponai.org/) — cross-industry AI-governance body; publishes framework references and multi-stakeholder guidance.
- [METR — Responsible Scaling Policies reference](https://metr.org/rsp) — METR's public reference on RSP practice; useful for cross-vendor context.
- **Foundational reading on the RSP idea.** [Anthropic — Anthropic's Responsible Scaling Policy (September 2023)](https://www-cdn.anthropic.com/1adf000c8f675958c2ee23805d91aaade1cd4613/responsible-scaling-policy.pdf) — the original RSP document; useful for reading against the current version to see how the framework has evolved.

## Vendor evaluation collaborations and external evaluators — chapter 08

Named externals the card and RSP sections reference.

- [UK AI Security Institute — homepage](https://www.aisi.gov.uk/) — the UK AISI; a common named external evaluator on frontier cards.
- [UK AISI publications and briefings](https://www.aisi.gov.uk/work) — AISI publications, including the Advanced AI Evaluations briefings.
- [US AI Safety Institute (NIST)](https://www.nist.gov/aisi) — the US AISI; the US analogue of UK AISI, publishes evaluation-programme materials.
- [US AISI Consortium](https://www.nist.gov/aisi/artificial-intelligence-safety-institute-consortium-aisic) — the consortium the US AISI convenes; the enterprise's participation, if any, is a first-class external-evaluator line.
- [METR](https://metr.org/) — evaluation methodology and reports on autonomy and dangerous capabilities.
- [Apollo Research](https://www.apolloresearch.ai/) — deception and scheming evaluations.
- [MITRE — AI Assurance program](https://www.mitre.org/focus-areas/artificial-intelligence) — MITRE's AI-assurance work; a source of AI-security and red-team methodology beyond ATLAS.
- [Alignment Research Center (ARC Evals — now METR)](https://evals.alignment.org/) — the legacy ARC Evals name (folded into METR); still cited in older vendor cards.
- [Redwood Research](https://www.redwoodresearch.org/) — safety-research organisation cited in some vendor eval collaborations.
- [Stanford Center for Research on Foundation Models (CRFM)](https://crfm.stanford.edu/) — CRFM's HELM and foundation-model research surface.

## Voluntary codes and regulator-adjacent guidance the eval evidence feeds into

Chapter 07 and chapter 08 downstream references. Overlaps with `mod-106`'s voluntary-code references and is deliberately narrow to the artefacts that consume eval evidence directly.

- [EU AI Office — Code of Practice hub](https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice) — the AI Office's General-Purpose AI Code of Practice hub.
- [EU AI Office — Final General-Purpose AI Code of Practice (July 2025)](https://digital-strategy.ec.europa.eu/en/library/final-general-purpose-ai-code-practice) — the final GPAI Code of Practice; adopting general-purpose AI providers publish safety-and-security reports referencing this document.
- [European Commission — European AI Office](https://digital-strategy.ec.europa.eu/en/policies/ai-office) — the AI Office hub; the enforcement and template-publishing body for the EU AI Act.
- [G7 Hiroshima Process — International Code of Conduct for Organizations Developing Advanced AI Systems](https://digital-strategy.ec.europa.eu/en/library/hiroshima-process-international-code-conduct-advanced-ai-systems) — G7 voluntary code that references red-team and eval commitments.
- [Bletchley Declaration (November 2023)](https://www.gov.uk/government/publications/ai-safety-summit-2023-the-bletchley-declaration/the-bletchley-declaration-by-countries-attending-the-ai-safety-summit-1-2-november-2023) — the AI Safety Summit declaration; cited from RSP and Preparedness-Framework context.
- [Seoul Declaration (May 2024)](https://www.gov.uk/government/publications/seoul-declaration-for-safe-innovative-and-inclusive-ai-ai-seoul-summit-2024) — the AI Seoul Summit declaration; successor to Bletchley.
- [Frontier AI Safety Commitments (Seoul, May 2024)](https://www.gov.uk/government/publications/frontier-ai-safety-commitments-ai-seoul-summit-2024) — the sixteen-signatory safety-commitments text; a companion reference to individual vendor RSPs.

## Deferred-depth references

Depth-owning tracks the analyst hands off to for work outside analyst-tier scope. Chapter 10's delegation-boundary references.

- [ai-evaluation-engineer](https://github.com/ai-governance-curriculum/ai-evaluation-engineer-learning) — the depth track for the eval-methodology, scorer-design, judge-model calibration, and release-assurance sign-off work chapter 09 hands the packet to.
- [model-evaluation-engineer](https://github.com/ml-engineering-curriculum/model-evaluation-engineer-learning) — near-synonym of `ai-evaluation-engineer` in many enterprise structures; depth on model-specific evaluations.
- [ai-red-team-engineer](https://github.com/ai-governance-curriculum/ai-red-team-engineer-learning) — the depth track for red-team engagement design, adversarial-prompt discovery, jailbreak methodology, and multi-turn attack construction that produces the reports chapter 04 walks.
- [ai-risk-engineer](https://github.com/ml-engineering-curriculum/ai-risk-engineer-learning) — the depth track for quantitative-risk modelling, robustness studies, and adversarial-perturbation analyses that produce internal risk-quantification artefacts the analyst reads.
- [senior-ai-governance-architect](https://github.com/ai-governance-curriculum/senior-ai-governance-architect-learning) — enterprise-architecture depth track that owns eval-programme tooling choices at portfolio scale, release-gating policy, and the enterprise's eval-cadence policy that governs row refresh.
- [head-of-ai-governance](https://github.com/ai-governance-curriculum/head-of-ai-governance-learning) — accountable-role track that owns release-gating threshold policy, Class-4 escalations, and the enterprise's eval-programme maturity.
- [ai-incident-responder](https://github.com/ai-governance-curriculum/ai-incident-responder-learning) — the depth track for incident-response engagement chapter 10 routes SCN-06-shaped scenarios to (`mod-109` in this track carries the reader-summariser view).

## What is deliberately not here

- Vendor benchmarks that are not accompanied by a system card or an RSP-family disclosure — a leaderboard entry without an accompanying safety-and-eval disclosure is not evidence of the *residual-risk* / *threshold-decision* / *unresolved-findings* shape the row schema requires. Chapter 06 was explicit that vendor rows are pairs (card + RSP).
- Consultancy trend reports, vendor "trust centre" one-pagers not paired with a specific eval or a specific card, and marketing-adjacent framings of vendor safety work — useful for *noticing* a change quickly, but the eval row's *source-artefact link* column carries the primary published artefact.
- Snapshots of an eval framework's documentation taken more than one release cycle ago — Inspect, TruLens, RAGAS, DeepEval, and the vendor cards revise on a rolling basis. Cite against the current published documentation, not against an older summary, and record the version identifier per row.
- Cross-vendor threshold-comparison tables that plot Anthropic ASL, OpenAI Preparedness Levels, and DeepMind CCLs on a common axis. Chapter 07 was explicit that these thresholds are not directly comparable; a cross-vendor arithmetic table is chapter 07's *threshold-arithmetic trap* and does not sit in the primary-source register.
- Case dockets, plaintiff-bar filings, and enforcement-action press coverage — relevant to counsel's risk-management view, not to the eval-evidence register's primary-source column. Where an enforcement action turns on eval evidence, the analyst records the regulator's own bulletin (per `mod-106`); the eval row itself cites the underlying eval report.
- Sponsor-produced RSP-family "compliance" attestations that do not cite the framework's specific commitments and thresholds — an adherence claim without a per-commitment citation is a marketing statement, not evidence for the row.
