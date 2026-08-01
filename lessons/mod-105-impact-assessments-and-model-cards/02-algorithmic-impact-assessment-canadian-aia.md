# The Algorithmic Impact Assessment — Canadian AIA Shape

## Why this chapter

The Canadian algorithmic impact assessment (AIA) is the oldest widely-adopted government-mandated AI impact assessment in force — the [Directive on Automated Decision-Making](https://www.tbs-sct.canada.ca/pol/doc-eng.aspx?id=32592) has required it of federal institutions since April 2019. Enterprises that supply Canadian federal customers meet the AIA whether or not they operate in Canada.

Beyond the Canadian federal deployment, the AIA is influential as a shape. Its four-tier impact level, its questionnaire-driven scoring, and its publication-of-completed-assessment obligation have been reused by other jurisdictions and by enterprises that want a machinery for internal ranking. Knowing the AIA shape gives the analyst a template even where the Canadian directive does not directly apply.

This chapter walks the directive's scope, the AIA tool's structure, how the analyst maps a canonical 42005-shaped document (chapter 01) into an AIA questionnaire, and where the AIA stops.

## Where the AIA sits

- **Governing instrument.** [Directive on Automated Decision-Making](https://www.tbs-sct.canada.ca/pol/doc-eng.aspx?id=32592) issued by the Treasury Board of Canada Secretariat (TBS). Applies to federal government institutions subject to the *Financial Administration Act* when they deploy an *automated decision system* affecting the rights, interests, or privileges of clients.
- **The AIA instrument itself.** The [Algorithmic Impact Assessment tool](https://www.canada.ca/en/government/system/digital-government/digital-government-innovations/responsible-use-ai/algorithmic-impact-assessment.html) — an open-source questionnaire that federal institutions complete before deploying an automated decision system.
- **Publication obligation.** Completed AIAs are published on the [Open Government Portal](https://open.canada.ca/en/open-government) so the public can read the assessment before the system deploys. This is a load-bearing detail — the AIA is written to be read.
- **Tooling.** [github.com/canada-ca/aia-eia-js](https://github.com/canada-ca/aia-eia-js) hosts the SurveyJS-based questionnaire source; the enterprise can host a local instance or complete via the federal tool. The output is a JSON blob plus a scored impact-level (I–IV).

## The four impact levels

The AIA yields an **impact level** on a I–IV scale from a scored questionnaire. Each level carries progressively stronger process obligations under the directive — peer review requirements, notice obligations, human-in-the-loop requirements, monitoring requirements, and training-data quality requirements all scale with the level.

- **Level I — little to no impact.** Reversible and brief impact on rights, health, economic interests, or ecosystem. Lightest process obligations.
- **Level II — moderate impact.** Likely reversible; short-term impact.
- **Level III — high impact.** Difficult to reverse; ongoing impact.
- **Level IV — very high impact.** Irreversible or perpetual impact. Heaviest process obligations, including senior official approval and independent peer review.

<!-- needs-research: verify the current version of the Directive's Appendix C requirements-by-impact-level table before quoting the exact process obligations attached to each level in an audit-facing artefact; the directive has been amended (2020, 2023) and process obligations have shifted between revisions. -->

The scoring is deterministic — the questionnaire's answers combine into a raw impact score and a mitigation score, which yield the impact level. The analyst-tier discipline: fill the questionnaire honestly, do not tune answers to hit a lower tier, and record the score derivation in the canonical document so a reader can reproduce it.

## The questionnaire — what it asks

The AIA questionnaire covers roughly the following topical areas (paraphrased headings; consult the tool for the current instrument):

- **Project details.** System name, sponsoring institution, business owner, contact.
- **Business drivers and risk profile.** Purpose of the system, business drivers, the decision it makes, populations affected.
- **Impact assessment.** Reversibility of the decision, duration of the impact, populations affected, right/economic/health/ecosystem impact scoring.
- **About the system.** Automation level (recommendation vs. decision), model family, transparency of the algorithm.
- **About the algorithm.** Explainability, auditability, testing regime, bias-review status.
- **About the decision.** Human review, appeal mechanism, notice to the affected individual.
- **About the data.** Data source, quality-assurance process, retention.
- **Consultations.** Legal, privacy, security, indigenous consultation where relevant.
- **De-risking and mitigation measures.** The mitigations that reduce the raw impact score.

<!-- needs-research: verify the current section headings and question counts of the AIA questionnaire against the live instrument at canada.ca before quoting section names verbatim; the questionnaire has been revised across the directive's amendments. -->

Two features distinguish the AIA from the FRIA and DPIA covered in later chapters:

- **The questionnaire is scored.** There is a numeric output. That number drives the process obligations, so the analyst can defend a claim of *this system is Level II* with a specific answer-set.
- **The output is public.** Completed AIAs are published. That constrains what the analyst writes — no internal-only shorthand, no unresolved needs-research markers left in the final artefact, no references to internal ticket numbers a reader outside the enterprise cannot resolve.

## Mapping the 42005 canonical document into the AIA

The AIA sections align with the canonical 42005 elements from chapter 01. The mapping the analyst uses:

| AIA questionnaire area | Sourced from 42005 canonical section |
|---|---|
| Project details | System description |
| Business drivers and risk profile | System description + treatment plan (business value) |
| Impact assessment (reversibility, duration, populations) | Enumerated impacts + analysis |
| About the system, algorithm, decision | System description + data description |
| About the data | Data description |
| Consultations | Related-artefact references (legal review, privacy review, security review) |
| De-risking and mitigation measures | Treatment plan |

The gaps the analyst fills in on top of the canonical document to complete the AIA:

- **Reversibility per decision.** The 42005 impact analysis records magnitude; the AIA asks specifically whether a given decision can be reversed. The analyst notes this alongside each register entry.
- **Duration per impact.** Similar — the analyst adds a duration claim (brief / short-term / ongoing / perpetual) to each register entry when preparing the AIA view.
- **Consultation record.** The AIA asks whether specific consultations occurred. The analyst records the meeting date, participants, and outcome — this is bookkeeping the canonical document usually holds by reference; the AIA needs the reference resolved.

## Concrete example — the MCDA AIA view

Suppose a variant of the MCDA (chapter 01) is deployed to draft standard-response text for Canadian federal service intake — a Canadian federal deployment, so the directive applies.

The AIA view derived from the MCDA canonical document:

- **Project details.** MCDA-Federal — Marketing Copy Draft Assistant, federal-service-intake variant. Institution: [redacted for pedagogic example]. Business owner: Service Delivery Ops.
- **Business drivers.** Reduce standard-response drafting time; support consistency across service centres.
- **Populations affected.** Members of the public interacting with the federal service.
- **Impact assessment.** The system produces *draft* text reviewed by a service officer before release. Reversibility: high (the officer can rewrite or discard). Duration: brief (a single response). Impact: economic and rights impact are low because the draft does not itself constitute a decision on the individual's file.
- **About the system.** Assistive — recommendation not decision. Hosted foundation model with retrieval grounding. Not fully explainable at the token level; the analyst notes the vendor's model card link.
- **About the algorithm.** Explainability: the enterprise supplies rationale text alongside each draft; auditability: prompt-plus-output pairs logged to an audit store. Bias review: pending — the analyst notes a `needs-research: bias-review dependency on `mod-104` bias-review note` marker to resolve before publication.
- **About the decision.** Human review is mandatory. Appeal mechanism follows standard federal-service appeal channels (system is assistive, not decisional).
- **About the data.** Prompts contain personal information at the service-intake tier; retention follows the enterprise records schedule; retrieval store contains only past-response templates, not personal data.
- **Consultations.** Legal (dd/mm), Privacy (dd/mm), Security (dd/mm) — dates and outcomes filled in from the canonical document.
- **De-risking and mitigation measures.** Human review, PII prompt-scanning, retrieval-only grounding on approved template store, audit logging, vendor review sign-off.

Scored, that answer-set lands at Level II (paraphrased — the actual level depends on the questionnaire computation). The AIA is published in that shape; the canonical document is retained internally.

## Where the AIA stops for the analyst

- **Not a legal opinion.** The AIA is a process artefact, not legal advice. Whether the deployment meets the directive is a legal-review determination; the AIA supports that determination but does not replace it.
- **Not a substitute for the DPIA.** Personal-information handling has its own legal instrument (in Canada, the [Privacy Act](https://laws-lois.justice.gc.ca/eng/acts/p-21/) for federal institutions; provincially, PIPA/PIPEDA-equivalents). The AIA references the privacy review; the privacy review sits alongside it.
- **Not an evaluation report.** The AIA cites evaluation results; it does not produce them. Evaluation is `mod-107` and `ai-evaluation-engineer` scope.
- **Not a monitoring plan.** The directive requires monitoring at higher impact levels; the plan itself is `mod-109` scope. The AIA references the plan by artefact ID.

## What to memorise

- **The instrument.** Directive on Automated Decision-Making (TBS), AIA questionnaire tool, publication on the Open Government Portal.
- **The four impact levels** — I (little to no) through IV (very high, irreversible). Process obligations scale with the level.
- **The score-driven, publish-by-default shape** — the AIA is written to be read publicly and the impact level is deterministic from the answer-set.
- **The canonical-to-AIA mapping table** — each AIA section maps to a 42005 documentary element plus a small set of AIA-specific extras (reversibility, duration, consultation record).

## Summary

The Canadian AIA is a scored, publish-by-default questionnaire mandated by the TBS Directive on Automated Decision-Making for federal automated decision systems. It yields an impact level I–IV that drives process obligations. The analyst-tier authoring pattern is to derive the AIA from the 42005-shaped canonical document, filling only the AIA-specific extras (reversibility, duration, consultation record) on top. The AIA is a process artefact — it supports but does not replace legal review, DPIA, evaluation, or the monitoring plan.
