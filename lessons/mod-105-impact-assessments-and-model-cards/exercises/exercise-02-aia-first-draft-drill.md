# Exercise 02 — AIA First Draft Drill

**Estimated effort:** 2 hours
**Grounding chapter:** [02 — The Algorithmic Impact Assessment — Canadian AIA Shape](../02-algorithmic-impact-assessment-canadian-aia.md)

## Objective

Author a first-draft Canadian AIA for a Canadian-federal variant of an internal AI system, rendered from the canonical 42005-shaped document produced in exercise 01. The drill covers the whole AIA questionnaire, the impact-level derivation, the publication-shape discipline, and the analyst-tier gaps the canonical document does not populate on its own.

After this exercise you should be able to open the AIA questionnaire tool for a new federal deployment, populate every section from an existing canonical document plus a small set of AIA-specific extras, and defend the resulting impact level to a Treasury Board Secretariat reviewer.

## Prerequisites

- Chapter 02 read; the four impact levels, the questionnaire areas, and the publication obligation fresh in memory.
- Exercise 01 completed — you have `mod-105-ex-01-canonical-impact-assessment-mcda.md` on disk (or you have populated a canonical document for a use case of your choice).
- The [Directive on Automated Decision-Making](https://www.tbs-sct.canada.ca/pol/doc-eng.aspx?id=32592) open — you will cite the directive by section for the process obligations that attach to your impact level.
- The [Algorithmic Impact Assessment tool page](https://www.canada.ca/en/government/system/digital-government/digital-government-innovations/responsible-use-ai/algorithmic-impact-assessment.html) open — you may complete the questionnaire directly against the tool, or work against a local copy from the [github.com/canada-ca/aia-eia-js](https://github.com/canada-ca/aia-eia-js) source repository.
- A worked example of a published AIA from the [Open Government Portal](https://open.canada.ca/en/open-government) as a shape reference. Pick one federal AIA whose subject-matter is close to your use case if you can find it; otherwise pick any recently-published AIA for the shape.

## Problem statement

The deliverable is a single Markdown file — the first-draft AIA — plus a short retrospective note.

Pick the use case:

- **Default.** Use the MCDA-Federal variant described in chapter 02 — the Canadian federal service-intake standard-response drafting use case. Reuse the canonical document you authored in exercise 01 as the source; add federal-specific narrative for the change of deployment context.
- **Alternative.** Substitute a different federal-deployment scenario if you have one that fits — a benefits-eligibility triage tool, an application-processing prioritiser, a public-service scheduling optimiser, etc. Constraints: the system is an *automated decision system* per the directive, deployed by a federal institution subject to the *Financial Administration Act*, affecting the rights / interests / privileges of clients.

Produce `mod-105-ex-02-aia-<system>-draft.md` shaped as the AIA the enterprise would publish on the Open Government Portal (subject to the redactions the enterprise would apply in an internal draft).

### Section-by-section shape

Cover every AIA questionnaire area from chapter 02:

- **Project details.** System name, sponsoring institution, business owner, contact. Cite the enterprise canonical document ID.
- **Business drivers and risk profile.** Purpose, business drivers, the decision the system makes, populations affected.
- **Impact assessment.** Reversibility, duration, populations, right / economic / health / ecosystem impact. Score each impact question honestly and record the score derivation in a short sub-note (the questionnaire tool computes an impact level from the answer-set — record that computation, not just the answers).
- **About the system.** Automation level, model family, transparency of the algorithm.
- **About the algorithm.** Explainability, auditability, testing regime, bias-review status. Cite the bias-review note from `mod-104` where relevant.
- **About the decision.** Human review, appeal mechanism, notice to the affected individual. Cross-reference to the FRIA if any applies (or note that none applies for a purely Canadian federal deployment).
- **About the data.** Data source, quality-assurance process, retention.
- **Consultations.** Legal, privacy, security, indigenous consultation where relevant. Record dates and outcomes; do not leave dates blank.
- **De-risking and mitigation measures.** The mitigations that reduce the raw impact score. Cite the register entries by identifier.

At the head of the document, place the cross-reference block from chapter 08 (canonical document ID, register entries, model card ID, etc.).

### The retrospective note

At the tail of the document, a 200–400 word retrospective note covering:

- The impact level the AIA landed on and one sentence on why (the load-bearing questionnaire answers).
- The process obligations the directive attaches to that level (peer-review, notice, human-in-the-loop, monitoring, training-data quality — as applicable at that level).
- Any AIA question you could not answer confidently from the canonical document, and what evidence you had to go find (this catches the *gaps* the canonical template does not cover).
- The single most likely regressive-drift point — the questionnaire answer that would change if the system evolved in a plausible way, forcing an AIA re-draft.

## Requirements

- **Every AIA questionnaire area is present**, in order, populated from the canonical document plus the AIA-specific extras (reversibility per decision, duration per impact, consultation record).
- **The impact level is derived, not asserted.** The AIA text includes the impact-level result and cites the questionnaire answers that produced it. A statement of "Level II" without the derivation is not the deliverable.
- **The cross-reference block at the head resolves.** Every identifier cited points to an artefact you have — or that you would file — in the enterprise repository. If a downstream artefact does not yet exist, mark the identifier `TBD-<placeholder>` and note it in the retrospective.
- **The publication discipline is applied.** No internal-only shorthand in the body of the AIA. No unresolved `<!-- needs-research: -->` markers left in the final artefact — either the fact is researched, or the AIA cannot be published. If a fact remains unresolved, park the AIA as a *draft not for publication* and note the blocker in the retrospective.
- **Consultation records carry dates.** A consultation entry without a date is not a record.
- **Nothing is fabricated.** No made-up sponsoring institution; no invented incidents; no fake vendor names. If the exercise reuses the MCDA-Federal variant, treat "[redacted for pedagogic example]" as the sponsoring-institution field per chapter 02.

## Starter guidance

- Start from the canonical document — do not re-author the underlying facts. The AIA is a *view*, per chapter 01. If you find yourself re-writing the system description from scratch, stop and copy from the canonical document.
- The three AIA-specific extras from chapter 02 — reversibility per decision, duration per impact, consultation record — are what you author net-new. Everything else is a projection. Prove to yourself that you have not projected the canonical wording verbatim into the AIA; the questionnaire's phrasing differs.
- The impact-level computation is deterministic. Answer honestly and let the tool compute. If the derived level surprises you, revisit the answers — do not tune the answers to hit an expected level. Recording an inconsistent answer to hit a lower tier is the fastest route to an audit finding.
- The public exemplars on the Open Government Portal are your best shape reference. Read two before you author your first section. Note how the published AIAs frame the *decision* — that framing is the load-bearing question the analyst most often answers loosely.
- On consultations, resist writing "consultation planned". Either the consultation happened and the date and outcome go in, or the AIA is not ready to publish. The directive expects consultations to have happened before deployment.
- If you land at Level III or higher, the retrospective should be honest about whether the enterprise is ready to meet the attached obligations — independent peer review, senior official approval, ongoing training, monitoring. Landing at a high level is not a fault; being unprepared for the obligations is.

## Acceptance criteria

- `mod-105-ex-02-aia-<system>-draft.md` with the cross-reference block and every AIA questionnaire area populated.
- The impact level is stated with the derivation from the questionnaire answers.
- Consultation records carry dates and outcomes.
- No unresolved `<!-- needs-research: -->` markers in the AIA body; any unresolved fact is either researched or the AIA is marked *draft not for publication* with the blocker named in the retrospective.
- Retrospective note of 200–400 words covering impact level, attached obligations, AIA questions not answerable from the canonical document, and the most likely regressive-drift point.
- No fabricated institutions, vendors, incidents, or statutes.

## Stretch goals

- **A regenerate-from-canonical script.** Sketch (in pseudocode or a short Python snippet) how a downstream tool would read the canonical-document YAML front-matter and render the AIA questionnaire answers. The manual mapping in chapter 02 becomes a `dict` in the script; the AIA-specific extras become the fields the script prompts a human for.
- **A second impact-level scenario.** Re-author the same AIA under a plausible *scope expansion* — e.g., the same system extended to a scenario where it makes a low-stakes decision autonomously without human review. Compare the impact-level derivations; document what shifts.
- **An AIA-to-FRIA gap analysis.** For the same system, list the fields the AIA covers that the FRIA (exercise 03) does not, and vice versa. This is preview work for exercise 04.
- **A publication-readiness checklist.** Compress the "no unresolved markers, dated consultations, cited derivations" discipline into a short pre-publication checklist a colleague would run before filing an AIA to the Open Government Portal.
- **A stakeholder-consultation record template.** Author the shape of the *consultation record* artefact the AIA references — meeting date, attendees, questions asked, outcomes, follow-ups. Route back to `mod-110` where stakeholder-consultation-artefact framing lives.

## Deliverables

- `mod-105-ex-02-aia-<system>-draft.md` — the AIA first draft plus retrospective.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works one reference draft against the MCDA-Federal variant. Yours will differ in tone and in the specific consultation and mitigation content; what should not differ is (a) every questionnaire area is populated, (b) the impact level is derived not asserted, (c) the AIA reads from a canonical document rather than duplicating it, (d) the publication discipline is respected — no internal shorthand, no unresolved research markers in the body. A short, publish-ready AIA that lands cleanly at Level II beats a longer, richer one that fabricates a consultation date to look complete.
