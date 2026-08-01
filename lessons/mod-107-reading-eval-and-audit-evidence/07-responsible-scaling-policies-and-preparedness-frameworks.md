# Responsible Scaling Policies and Preparedness Frameworks

## Why this chapter

A vendor system card (chapter 06) usually says *the model scored below the CBRN Medium threshold* or *classified at Cybersecurity Uplift Low*. Those threshold names are not free-floating — they refer back to a **Responsible Scaling Policy (RSP)** or **Preparedness Framework** the vendor published separately. The RSP is where the capability-threshold definitions live, where the commitments the vendor makes at each tier are enumerated, and where the analyst can trace a card's *classified at Medium* claim back to *what does Medium mean and what did the vendor commit to at Medium?*

Frontier-lab RSP-family documents have converged on a common shape. The three most-cited exemplars, all publicly available:

- **[Anthropic's Responsible Scaling Policy (RSP)](https://www.anthropic.com/rsp)** — first published September 2023, revised through multiple versions. Introduced the *AI Safety Levels* (ASL-2, ASL-3, ASL-4) framing that has anchored the field's vocabulary.
- **[OpenAI's Preparedness Framework](https://openai.com/preparedness/)** — first published December 2023 (Beta), revised. Uses a Tracked Categories × Risk-Levels grid (Cybersecurity, CBRN, Persuasion, Model Autonomy, each scored Low / Medium / High / Critical, with named commitments at each level).
- **[Google DeepMind's Frontier Safety Framework (FSF)](https://deepmind.google/discover/blog/introducing-the-frontier-safety-framework/)** — first published May 2024, revised. Uses *Critical Capability Levels* (CCLs) as tripwires for named mitigations.

<!-- needs-research: verify current published versions of each vendor's RSP / Preparedness Framework / FSF against the linked pages at time of use; these documents revise on a rolling basis and version numbers, category definitions, and threshold numbers change between revisions. Cite the exact version identifier in every row and briefing. -->

The [Frontier Model Forum](https://www.frontiermodelforum.org/) has separately published on RSP practice, and the [AI Governance Alliance](https://initiatives.weforum.org/ai-governance-alliance/home) and [Partnership on AI](https://partnershiponai.org/) have referenced RSP-family commitments in cross-industry work.

This chapter walks the RSP-family document shape, the specific vocabulary the three exemplars use, and the analyst-tier discipline for populating a `EVAL-<year>-<sequence>` row of type *vendor-rsp-disclosure* and using it in the benchmarking chapter 08 covers.

## What an RSP / Preparedness Framework is (and is not)

An RSP-family document is a *conditional* commitment from a frontier-model developer. Its structure:

1. **A set of capability categories** — the frontier risks the developer takes seriously (CBRN, cyber-offense, model autonomy, persuasion, deception, and successor categories as they emerge).
2. **A set of capability thresholds within each category** — evaluated by the developer's own eval suite plus (usually) named external evaluators.
3. **Commitments that trigger at each threshold** — training-time interventions, deployment-time interventions, security controls, and (at the highest tiers) commitments to pause or restrict deployment.
4. **A governance mechanism** — how commitments are held to (internal review boards, external oversight, board-level approval).
5. **A change process** — how the RSP itself is updated, and what the developer's own oversight of those updates looks like.

An RSP is **not**:

- A regulatory instrument. It is a *voluntary* commitment. Its bindingness on the vendor is the vendor's word, the vendor's governance mechanism, and (increasingly) the market and regulator scrutiny of whether the vendor honours it.
- A safety guarantee. It is a *risk-management* framework — it names risks, thresholds, and commitments, but it does not claim the model is safe below the threshold.
- Static. Every published RSP has revised; the analyst records the specific version identifier and re-reads on the vendor's revision cadence.

## Anthropic's RSP — the AI Safety Levels shape

Anthropic's RSP structures around **AI Safety Levels (ASL)**. The shape (structural summary — verify current definitions against the [current RSP](https://www.anthropic.com/rsp)):

- **ASL-2** — the level current-generation frontier models are typically deployed at. Requires standard safety-and-security controls (see the [Anthropic Trust Center](https://trust.anthropic.com/)), Responsible Disclosure Policy participation, and Acceptable Use Policy enforcement.
- **ASL-3** — triggered by models that show *significant* uplift in autonomous capabilities or in a specific catastrophic-risk category. Requires substantially more stringent security and deployment controls, including hardened access to model weights.
- **ASL-4** — triggered by more advanced capability tripwires. Requires further-strengthened controls; the published RSP names commitments that scale accordingly.

The Anthropic RSP names its capability threshold assessment methodology and the specific categories evaluated (CBRN uplift, cyber-offense uplift, autonomous replication and adaptation, and successor categories as the framework evolves). The RSP explicitly commits to pausing training or deployment of models that would cross the highest ASL thresholds without proportionate mitigations in place.

<!-- needs-research: verify the current ASL definitions, threshold criteria, and commitments enumerated in Anthropic's RSP against the current version at time of use; the ASL boundaries and the commitments at each level have been revised since the September 2023 initial publication. -->

## OpenAI's Preparedness Framework — the Tracked Categories × Risk-Levels grid

OpenAI's Preparedness Framework structures around **Tracked Risk Categories** scored against **Risk Levels**. The shape (structural summary — verify against the [current Preparedness Framework](https://openai.com/preparedness/) and OpenAI's *Preparedness* research index):

- **Tracked risk categories.** Cybersecurity, CBRN, Persuasion, Model Autonomy (as of published versions to date). The framework commits to updating the category list as new risks emerge.
- **Risk levels per category.** Low / Medium / High / Critical, with named threshold criteria per level. Evaluations are run pre-mitigation and post-mitigation.
- **Deployment and development commitments.** The framework commits to specific deployment gating at each level — e.g., no deployment of a model at *High* in a tracked category without specific safeguards; no further training beyond *High* pre-mitigation without a specific review; no deployment at *Critical* pre-mitigation.
- **Preparedness team and Safety Advisory Group.** Named internal governance mechanisms, with board-level oversight escalations documented.

The Preparedness Framework's Safety Scorecards (part of the published-version updates) show a per-model per-category grid of pre- and post-mitigation scores. The system-card frontier-eval section (chapter 06 section 6) references the scorecard.

<!-- needs-research: verify OpenAI's current Preparedness Framework version, the categories tracked, the exact risk-level definitions, and the Safety Scorecard shape against the current published Framework at time of use; category and threshold definitions have been revised across published versions. -->

## Google DeepMind's Frontier Safety Framework — the Critical Capability Levels shape

DeepMind's FSF structures around **Critical Capability Levels (CCLs)**. The shape (structural summary — verify against the [current FSF](https://deepmind.google/discover/blog/introducing-the-frontier-safety-framework/) and DeepMind's publications page):

- **Critical Capability Levels per category.** Autonomy, biosecurity, cybersecurity, and machine-learning-R&D categories (as of published versions to date), each with named CCLs the framework treats as safety-critical tripwires.
- **Evaluation cadence.** Early-warning evaluations run during training; CCLs are re-evaluated at specific compute or capability milestones.
- **Mitigation commitments.** Deployment mitigations and security mitigations that trigger at each CCL. The framework commits to a *response* when a CCL is reached, including deployment restrictions and further access controls.

<!-- needs-research: verify current FSF version, CCL definitions per category, and the specific mitigation commitments against the current published FSF at time of use; the framework has been revised since the May 2024 initial publication. -->

## The three exemplars share a shape

Despite different vocabularies (ASL vs Risk Levels vs CCL), the three exemplars share a shape the analyst can extract from any RSP-family document:

- **Named risk categories** the framework tracks.
- **Named thresholds** per category.
- **Named commitments** that trigger at each threshold.
- **Named evaluation methodology** (internal + named externals).
- **A governance mechanism** for holding the developer to the commitments.
- **A change process** for revising the framework itself.

A framework that does not name all six is under-specified. The analyst records the framework's shape verbatim into the *vendor-rsp-disclosure* row; where a shape element is missing, the row's notes field flags it.

## Populating a *vendor-rsp-disclosure* row

Chapter 05's schema accommodates RSP disclosures under report-type = *vendor-rsp-disclosure*. The mapping:

| Row field | Source in an RSP-family document |
|---|---|
| Report title / date / author | Header — vendor, framework title, version identifier, publication date |
| Report type | *vendor-rsp-disclosure* |
| Inventory row(s) | Foreign key list to every internal `INV-<year>-<sequence>` row using a model that the framework covers |
| System version(s) | The framework version and, if the disclosure includes per-model classifications, the specific model identifiers classified |
| Deployment configuration snapshot | *N/A — RSP disclosure is at framework level; per-model classifications are captured in the paired vendor-system-card row* |
| Task / dataset | *N/A — RSP disclosure describes the framework, not a single eval* |
| Solver / scorer | *N/A at framework level; framework's stated evaluation methodology and named external evaluators recorded in the notes field* |
| Aggregate result | *N/A at framework level* |
| Per-slice breakdown | *N/A at framework level* |
| Residual-risk claim | The framework's own summary of what commitments apply at what threshold, and where the vendor has classified the current model families (typically drawn from the paired system card) |
| Threshold-decision rationale | The framework's named thresholds and (where the paired system card names them) the classification calls made against them |
| Unresolved findings | The framework's own change log and any acknowledged limitations of the framework itself — the developer's own statement of what the framework does not yet cover |
| Cross-artefact links | Foreign key to the paired vendor-system-card row(s) (chapter 06) and to every internal `EVAL-<year>-<sequence>` row on systems using a covered model |
| Row status | *evidence-current* until the vendor revises the framework |
| Refresh cadence | Per vendor's stated revision cadence; recommend annual re-read at minimum |

An RSP row is companion to the vendor-system-card row: the card carries the *classification*, and the RSP carries the *framework the classification is against*. Reading one without the other loses context; the row set carries both.

## What the analyst *reads for* in an RSP-family document

- **Which categories does the framework track that are relevant to the enterprise's use cases?** A framework's CBRN category is relevant to any enterprise using a model for scientific-content generation; the persuasion category is relevant to any enterprise using a model for customer-facing content; the model-autonomy / autonomous-replication category is relevant to any enterprise using a model in an agentic context.
- **What commitments trigger at each threshold?** The framework's threshold commitments constrain what the vendor will make available to the enterprise (weights, API access, fine-tuning access) as the model's capability increases. The enterprise's deployment plan needs to account for the possibility of a downstream commitment (e.g., a security control the vendor will require).
- **What external evaluators does the framework name?** The presence of a named external evaluator (UK AISI, US AISI / NIST, METR, Apollo Research, academic groups) is load-bearing for downstream regulator scrutiny.
- **What is the change process?** How does the vendor revise the framework, and how does the analyst know when a revision has landed? The refresh cadence in the row derives from the framework's own change process.

## Reading traps specific to RSP-family documents

- **The version-in-flight trap.** RSPs revise regularly. A framework version cited in a system card released in 2024 may not be the framework version in force in 2026. The analyst records both — the framework version the card cites and the framework version currently published — and flags any material divergence.
- **The self-oversight trap.** RSP governance mechanisms are usually internal-to-the-vendor governance mechanisms (a Safety Advisory Group, a Responsible Scaling Officer, a board committee). These are the vendor's own accountability structures; they are meaningful but not equivalent to external oversight. The analyst records the mechanism verbatim without silently promoting it into external-oversight status.
- **The threshold-arithmetic trap.** Different vendors' thresholds are not directly comparable. Anthropic's ASL-3, OpenAI's *High* for CBRN, and DeepMind's biosecurity CCL-1 are not measured on a common scale; each is scored against the vendor's own eval suite. The analyst does not build a cross-vendor comparison table without explicit methodology notes.
- **The unenumerated-category trap.** Frameworks tend to lag emerging risks. A framework that does not enumerate a category the enterprise is exposed to (an agentic-AI-specific category, a multi-model-orchestration category, a specific bio-risk sub-category) leaves an evidence gap. The analyst records the gap in the row's notes field.
- **The pause-commitment trap.** An RSP commitment to *pause training or deployment* at a specific threshold is meaningful in principle. The analyst records the commitment verbatim and does not silently promote *would pause if* into *has paused*.

## The connection to internal governance artefacts

The RSP row is one of the two vendor rows (the other being the system-card row). Together they populate the *vendor-baseline* side of the benchmark chapter 08 works. Specifically:

- The internal `EVAL-<year>-<sequence>` rows for a system using a specific model reference *both* the vendor-system-card row and the vendor-rsp-disclosure row for that model. This creates a three-way linkage: internal-eval → vendor-card → vendor-RSP.
- The impact-assessment corpus (`mod-105`) cites the vendor's threshold classification in the residual-risk section of the impact assessment for any system using that model. A model classified at CBRN Medium by the vendor is a Medium-tier CBRN residual on any downstream enterprise system using it in a CBRN-relevant context.
- The regulatory tracker (`mod-106`) links RSP disclosures to regulatory obligations that reference them — the EU AI Office's General-Purpose AI Code of Practice, US federal reporting requirements on frontier models, and any UK / Canada trajectory that names Responsible Scaling commitments explicitly. The tracker row for the GPAI Code of Practice, for example, cross-references the RSP rows for the models the enterprise uses that fall under GPAI scope.
- The control library (`mod-108`) uses RSP commitments as a baseline for the enterprise's own controls. An enterprise deploying a model at Anthropic's ASL-2 or OpenAI's Medium-tier categorises its own required controls at least at that baseline; going below the vendor's stated commitment is an evidence gap.

## What to memorise

- **RSPs are voluntary commitments, not regulations.** Recorded verbatim, not silently promoted.
- **Three exemplars, one shape.** Named risk categories, named thresholds, named commitments, named evaluation methodology, named governance mechanism, named change process.
- **Vendor rows come in pairs.** System card (chapter 06) plus RSP disclosure (this chapter) together form the vendor-baseline for any model.
- **Thresholds are not cross-vendor comparable.** ASL-3 ≠ OpenAI High ≠ DeepMind CCL. Do not build cross-vendor arithmetic without explicit methodology.
- **RSPs revise.** Record the exact framework version cited by the system card and the currently-published version, and flag divergence.
- **The RSP is a baseline, not a ceiling.** Enterprise controls should not fall below the vendor's own stated commitments for the model the enterprise deploys.

## Summary

Responsible Scaling Policies, OpenAI's Preparedness Framework, and Google DeepMind's Frontier Safety Framework are the load-bearing companion documents to vendor system cards. They name the risk categories the vendor tracks, the thresholds within each, and the commitments that trigger at each. Anthropic's AI Safety Levels, OpenAI's Tracked Categories × Risk Levels grid, and DeepMind's Critical Capability Levels are three vocabularies for the same underlying structure. The analyst populates a `EVAL-<year>-<sequence>` row of type *vendor-rsp-disclosure* per framework version and links it to the paired vendor-system-card rows (chapter 06) and to every internal `EVAL-<year>-<sequence>` row on a covered system. Chapter 08 works the benchmark step — how the internal artefacts compare to what the vendor card and the RSP disclosure jointly represent.
