# The Analyst's Scope on Eval, Red-Team, and Audit Evidence

## Why this chapter

By this point in the track the analyst has an inventory (`mod-102`), a risk register (`mod-103`), a fairness-review note per relevant system (`mod-104`), an impact-assessment corpus (`mod-105`), and a rolling regulatory tracker (`mod-106`). The next question every one of those artefacts silently asks is: *what is the evidence that the mitigations we listed actually work?*

That evidence comes from evaluations — capability evals, safety evals, fairness evals, RAG-quality evals, red-team engagements, external audits, and (for hosted foundation models) the vendor's own system-card disclosures. Producing that evidence is not analyst-tier work. **Reading** it and turning it into a governance-record row that a council, an auditor, and a downstream release-assurance engineer can use *is*.

This module is the discipline that closes the loop. Chapters 02–04 walk the anatomy of the three most common eval / adversarial-eval report shapes the analyst encounters. Chapter 05 defines the row shape the analyst extracts. Chapters 06–08 cover the public references (system cards, Responsible Scaling Policies, Preparedness Frameworks) that the analyst uses to benchmark internal artefacts. Chapter 09 is the hand-off packet to `ai-evaluation-engineer` for release-assurance sign-off. Chapter 10 is the delegation boundary and the escalation protocol when the evidence is not there.

## What the analyst does with eval evidence

The analyst-tier verbs, in order:

1. **Reads** the eval report, red-team report, or system-card disclosure end-to-end at least once.
2. **Locates** the three load-bearing claims inside it: the residual-risk claim, the threshold-decision rationale, and the unresolved-findings list.
3. **Summarises** those three claims into the governance-record row shape (chapter 05).
4. **Links** the row to the source artefact (the report itself, versioned, with a stable URL or repository path).
5. **Benchmarks** the internal artefact against the relevant public references — the vendor's system card, an Anthropic-style Responsible Scaling Policy, an OpenAI Preparedness-Framework disclosure, a DeepMind Frontier-Safety-Framework update, or the [NIST AI 600-1 Generative AI Profile](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) risk actions.
6. **Composes** a review packet — analyst-tier summary, source-artefact link, open follow-ups — and hands it to `ai-evaluation-engineer` for release-assurance sign-off.
7. **Escalates** any under-evidenced claim, mis-scoped eval, or stale eval to the ML / product owner and the governance council.

None of these verbs *authors the evaluation itself*. That distinction is the module's spine.

## What the analyst does not do

The analyst does not:

- **Design or run the evaluation.** Choosing tasks, writing scorers, executing runs, tuning prompts, and computing metric distributions is `ai-evaluation-engineer` / `model-evaluation-engineer` scope. Where the enterprise has an internal safety-eval function or contracts an external evaluator (an AI Safety Institute engagement, an academic collaboration, a commercial safety-testing vendor), that team runs the eval.
- **Run the red-team engagement.** Adversarial prompt discovery, multi-turn attack construction, jailbreak methodology, tool-use exploitation, and multi-model transfer testing is `ai-red-team-engineer` scope.
- **Author the residual-risk-acceptable decision.** The analyst summarises the *rationale* the eval owner published; the decision itself belongs to the accountable model / product owner (often with a governance-council sign-off overlay). This mirrors the NIST AI RMF *Govern-1.1* accountability roles and the ISO/IEC 42001 Clause 5 leadership-commitment shape.
- **Interpret novel benchmark metrics.** If an eval reports a metric the analyst has not seen — an unfamiliar RAG-quality score, a bespoke deception-eval score, a proprietary jailbreak-robustness index — the analyst records the metric, notes that it is unfamiliar, and asks the eval owner to characterise it. The analyst does not silently guess.
- **Sign off release-assurance.** Release-assurance is `ai-evaluation-engineer` scope with (depending on the enterprise) a `principal-ai-engineer` or `head-of-ai-governance` counter-sign. The analyst-tier review packet is an *input* to that sign-off, not the sign-off itself.

Chapters 09 and 10 return to this boundary in operational detail. The point at this stage: the analyst is a *reader-and-summariser* here, not a producer.

## The three load-bearing claims

Every eval, red-team, or audit report the analyst reads carries three load-bearing claims. If any of the three is missing or unlocatable, the report is not evidence — it is a document.

- **The residual-risk claim.** What risk remains *after* the mitigations described in the report. Expressed as a plain-language sentence plus (where the report provides them) the metric values that support it. Example shape: *After applying refusal-training pass A and system-prompt guardrail set B, the model refuses 92% of CBRN-uplift prompts in the internal harm suite v3.2; the residual 8% is characterised as [description] and is judged [acceptable / requiring further mitigation] against the internal threshold.*
- **The threshold-decision rationale.** *Why* the residual number is (or is not) acceptable. This is usually a reference to an internal risk threshold, a Responsible Scaling Policy commitment, an OpenAI-Preparedness-Framework capability threshold, or a regulator-recognised benchmark. If the report says *we consider this acceptable* without pointing at the threshold that made it acceptable, the threshold-decision rationale is missing.
- **The unresolved-findings list.** What findings the report explicitly did not close. A red-team report that finds five jailbreaks and mitigates three but leaves two open must list the two open ones with severity, reproducibility, and (ideally) a proposed follow-up owner and date. Same for eval reports — a coverage gap that the eval owner acknowledges but does not close belongs in this list.

The analyst's row is exactly these three fields plus provenance and link fields. Chapter 05 details the schema.

## Where this module sits in the arc

- **Inputs.** The eval / red-team / audit reports themselves (produced by others); the enterprise's inventory (`mod-102`); the enterprise's risk register (`mod-103`); the enterprise's impact-assessment corpus (`mod-105`); the enterprise's regulatory tracker (`mod-106`).
- **Outputs.** A per-system evaluation-evidence row set in the governance repository; a review packet handed to `ai-evaluation-engineer`; escalation notes to the ML / product owner and the governance council where warranted.
- **Downstream consumers.** `mod-108` (controls-and-compliance-evidence) references these rows as the evidence for any `evaluated-and-below-threshold` control assertion. `mod-109` (incident-response-and-continuous-monitoring) reads the *unresolved findings* column to prioritise post-market surveillance. `mod-110` (communication-and-council-support) reads the row set for council briefings.

The module does not produce the evaluations. It is the connective tissue that turns *someone ran an eval* into *the governance record cites that eval and knows what it says*.

## The vocabulary the analyst needs

- **Eval.** A structured task run against a model or system to measure a specific capability or behaviour. Modern practice standardises around task specifications, scorers, and datasets. The [UK AI Security Institute's Inspect framework](https://inspect.aisi.org.uk/) formalises this shape.
- **Capability eval.** Measures whether the model *can* do something (translate, summarise, code, reason about biology). Higher scores usually mean *more* capability.
- **Safety eval.** Measures whether the model *does not* do something it should not (produce CBRN uplift, output disallowed content, comply with jailbreak prompts, hallucinate under grounding). Lower scores on *harm* usually mean *safer*; framings vary.
- **RAG-triad eval.** Three-metric family for retrieval-augmented systems, popularised by TruLens and TruEra: *context relevance*, *groundedness*, and *answer relevance*. Chapter 03 walks the shape.
- **Red-team engagement.** A structured adversarial exercise, often multi-turn, seeking to elicit unsafe behaviour that standard evals would not catch. Deliverable is an engagement report, not a metric table.
- **System card.** A public artefact describing a deployed system — model + prompts + tools + guardrails + safety evaluation coverage + known limitations. Chapter 06 walks the shape.
- **Responsible Scaling Policy (RSP).** A public commitment from a frontier model developer that names capability thresholds and the safety commitments that trigger at each. [Anthropic's RSP](https://www.anthropic.com/rsp) is the canonical instance; [OpenAI's Preparedness Framework](https://openai.com/preparedness/) and [DeepMind's Frontier Safety Framework](https://deepmind.google/discover/blog/introducing-the-frontier-safety-framework/) are the two other frontier-lab exemplars. Chapter 07 walks them.
- **Threshold decision.** The named threshold and the yes-or-no call against it. A residual-risk number without a threshold is a metric; with a threshold it is a decision.
- **Release-assurance sign-off.** The final go / no-go decision to deploy or ship, informed by the eval evidence. `ai-evaluation-engineer` owns; the analyst supplies the packet.

## The delegation map — preview

The delegation map for eval and audit evidence, previewed here and re-established explicitly in chapter 10:

| Artefact / action | Role that produces | Role that reads and summarises |
|---|---|---|
| Inspect-style capability / safety eval report | `ai-evaluation-engineer` (or external evaluator such as an AI Safety Institute) | `ai-governance-analyst` |
| Internal RAG-triad eval report | `ai-evaluation-engineer` / `ml-engineer` | `ai-governance-analyst` |
| Red-team engagement report | `ai-red-team-engineer` (or contracted third party) | `ai-governance-analyst` |
| Internal risk-quantification / robustness study | `ai-risk-engineer` | `ai-governance-analyst` |
| Public system card | Vendor (OpenAI, Anthropic, Google DeepMind, Meta, Mistral, etc.) | `ai-governance-analyst` |
| Public Responsible Scaling Policy / Preparedness Framework disclosure | Vendor | `ai-governance-analyst` |
| Governance-record eval-evidence row | `ai-governance-analyst` | `ai-evaluation-engineer` (as consumer for release-assurance sign-off), governance council |
| Review packet to release-assurance | `ai-governance-analyst` | `ai-evaluation-engineer` |
| Release-assurance sign-off | `ai-evaluation-engineer` (with counter-sign per enterprise policy) | Model / product owner |

The row in the middle — *governance-record eval-evidence row* — is the analyst's tangible output for this module. The row shape is chapter 05.

## What to memorise

- **The analyst reads eval evidence; specialists produce it.** Design, run, and interpretation of novel metrics stay with `ai-evaluation-engineer`, `ai-red-team-engineer`, and `ai-risk-engineer`.
- **The three load-bearing claims** — residual-risk claim, threshold-decision rationale, unresolved-findings list — are what the analyst extracts from every report.
- **The row is the output.** The analyst's tangible artefact for this module is a governance-record row per evaluated system, with the three claims summarised and the source artefact linked.
- **The review packet is the hand-off.** Analyst summary + source-artefact link + open-follow-up list → `ai-evaluation-engineer` for release-assurance sign-off.
- **Escalation is a first-class output too.** An under-evidenced claim, a mis-scoped eval, or a stale eval is escalated to the ML / product owner and the governance council; it is not silently filed.

## Summary

This module turns the *someone ran an eval* signal into the governance record that a council, an auditor, and a release-assurance engineer can act on. The analyst is a reader-and-summariser, not a producer. The three load-bearing claims — residual-risk, threshold-decision rationale, unresolved findings — populate a per-system row that links back to the source artefact and is packaged into a review packet handed to `ai-evaluation-engineer`. Chapters 02–04 walk the three most common report shapes (Inspect-style eval, RAG-triad, red-team). Chapter 05 fixes the row schema. Chapters 06–08 cover the public references — system cards, Responsible Scaling Policies, Preparedness Frameworks — that the analyst uses to benchmark internal artefacts. Chapter 09 is the packet hand-off. Chapter 10 is the delegation boundary and the escalation protocol.
