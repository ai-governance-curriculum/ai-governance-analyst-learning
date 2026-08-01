# Exercise 03 — FRIA First Draft Drill

**Estimated effort:** 2 hours
**Grounding chapter:** [03 — The Fundamental-Rights Impact Assessment — EU AI Act Article 27](../03-fundamental-rights-impact-assessment-eu-article-27.md)

## Objective

Author a first-draft Article 27 FRIA for an EU-deployment variant of an internal AI system, rendered from the canonical 42005-shaped document. The drill covers the scoping filter, the six required elements, the Article 13 provider-information dependency, the Charter-right tagging, and the market-surveillance authority notification record.

After this exercise you should be able to open the AI Office's FRIA notification template (as it becomes available) or the enterprise's internal FRIA template, populate every element from a canonical document plus the FRIA-specific extras, and hand the draft to counsel and the DPO for review with a clear sense of what is analyst-tier and what is not.

## Prerequisites

- Chapter 03 read; the Article 27 scoping filter, the six required elements, and the Article 13 dependency fresh in memory.
- Exercise 01 completed — you have a populated canonical document; you have a MAP walk with register entries to reuse.
- Chapter 04 skimmed — the FRIA / DPIA overlap is preview work here; exercise 04 develops it.
- The [EU AI Act consolidated text at EUR-Lex](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) open — you will cite Article 27 (and Articles 26, 13, and 6 / Annex III as needed) by article number.
- The [Charter of Fundamental Rights of the European Union](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:12012P/TXT) open — you will tag each identified risk with the Charter article it engages.
- Optional: the [European Commission's AI Office](https://digital-strategy.ec.europa.eu/en/policies/ai-office) page for updates on the FRIA notification template, and any enterprise-adopted FRIA template from a national-supervisory-authority or industry-body publication.

## Problem statement

The deliverable is a single Markdown file — the first-draft FRIA — plus a short scoping-and-hand-off note.

Pick the use case:

- **Default.** Use the MCDA-Benefits variant from chapter 03 — a public-body deployer using a high-risk system that determines access to essential public benefits (Annex III point 5(a)). This *does* trigger Article 27.
- **Alternative.** Substitute another Article-27-triggering use case if you have one that fits — a credit-scoring deployment by a private lender (Annex III point 5(b)), a public employment agency's job-matching system (Annex III point 4 plus the deployer-is-a-public-body test), a public infrastructure risk-management system (Annex III point 2), etc. Constraints: the system is high-risk under Article 6 / Annex III *and* the deployer is one of the four Article-27-scoped classes.

Produce `mod-105-ex-03-fria-<system>-draft.md`.

### Section-by-section shape

Cover every one of the Article 27(1) required elements, in order, each labelled with the sub-article citation:

- **(1) Deployer processes using the system.** From the canonical System description + treatment plan.
- **(2) Period and frequency of use.** From the canonical System description + review-triggers section.
- **(3) Categories of natural persons and groups affected.** From the canonical Affected-stakeholder inventory. Include the sub-groups (protected classes, vulnerable populations) explicitly — do not compress to *general public*.
- **(4) Specific risks of harm** — with the Charter-right tag on each risk. For each register entry, name the risk, the mechanism, the affected sub-population, the inherent and residual claim, and the Charter article the risk engages. Cite the provider's Article 13 instructions-for-use as an input (or note that the provider has not supplied Article 13 information and flag the gap).
- **(5) Human-oversight implementation.** From the canonical Treatment plan (oversight controls). Do not compress; name the specific human roles and their moments of oversight.
- **(6) Response to materialised risk** — internal governance and complaint mechanisms. From the canonical Treatment plan + related-artefact reference to the incident-response plan.

At the head, place the cross-reference block from chapter 08 (canonical document ID, register entries, model card, related DPIA if any, provider's Article 13 document by identifier).

At the head, also include a short **scoping-filter narrative** — three or four sentences — that shows the three tests from chapter 03 (high-risk system + Article-27-scoped deployer + not sufficiently covered by an existing DPIA) applied to your use case with cited outcomes. This is the analyst's answer to *why does this system need a FRIA*.

### The scoping-and-hand-off note

At the tail, a 200–400 word note covering:

- The Article 6 / Annex III basis on which the system is high-risk, cited to the article and Annex point.
- The Article 27 scoping-class basis on which the deployer is in scope.
- Any Article 13 information gap and how you would close it.
- The Charter articles you tagged and one line each on why (name the article, name the harm mechanism).
- The market-surveillance-authority notification status — filed / drafted / pending template. Do not fabricate a filing acknowledgement.
- The next-step hand-off to counsel and the DPO — what you are asking them to opine on, in one sentence each.

## Requirements

- **The scoping filter is applied at the head.** The FRIA does not exist without the three-test filter answered. If the answer is *not in scope*, the deliverable is a scoping memo, not a FRIA.
- **Every Article 27(1) element is present**, in order, with the sub-article citation.
- **Every identified risk carries a Charter-right tag** naming the specific article (e.g., *Article 21 — non-discrimination*), not the generic label (*non-discrimination*). If a risk engages more than one Charter article, tag each.
- **The Article 13 provider-info reference is resolved or the gap is flagged.** No FRIA without the provider's instructions-for-use, per Article 27(1)(d). If the provider has not supplied Article 13 information, the FRIA is a *draft pending provider input* and the gap is named at the head.
- **The human-oversight section names specific roles and specific oversight moments.** *A human reviews the output* is not the deliverable; *the caseworker reviews and endorses each draft before dispatch, per the caseworker training programme run quarterly* is.
- **The complaint mechanism reference resolves.** Either the enterprise has an existing complaint mechanism the FRIA cites, or the gap is flagged.
- **No fabricated notification acknowledgements.** The notification status is filed / drafted / pending honestly.
- **No unresolved `<!-- needs-research: -->` markers in the FRIA body.** Where a claim depends on a not-yet-published AI Office template or a not-yet-clarified Article 27 sub-scope, the FRIA carries the marker in the scoping-and-hand-off note, not in the FRIA body.
- **Nothing is fabricated** — no invented supervisory-authority correspondence, no invented case-law citations, no fake vendor names.

## Starter guidance

- Read Article 27 in the consolidated text once before authoring. It is short — about a page. The sub-articles are precise; the analyst-tier work is to answer each sub-article literally.
- The scoping filter is where most first-draft FRIAs fail. The private-sector deployer of an Annex III point 4 (employment) system is *not* in Article 27 scope unless the deployer provides a public service. Do not skip the filter to get to the six-element authoring — a FRIA for a system not in scope is not a FRIA; it is unnecessary work.
- The Charter-right tagging is the FRIA's most analyst-distinctive move. Do not compress. Non-discrimination (Article 21) is not the same as data protection (Article 8) is not the same as good administration (Article 41). When two rights are engaged, tag both.
- The Article 13 dependency is real. Vendor foundation-model providers have started publishing high-risk-system instructions-for-use as separate documents; the FRIA cites them by document identifier. If the vendor has not published one, the analyst-tier action is to *request it* — do not shrug and continue.
- The market-surveillance-authority notification template is under development at time of writing. Enterprises are preparing based on the Article 27 text alone. If the template is published by the time you author, use it; otherwise, structure the FRIA to the six-element shape and note the pending-template dependency in the scoping-and-hand-off note.
- The FRIA is a legal-adjacent artefact. The analyst produces the draft; counsel and the DPO opine. The hand-off note is what makes the draft *reviewable* — do not skip it.

## Acceptance criteria

- `mod-105-ex-03-fria-<system>-draft.md` with the cross-reference block, the scoping-filter narrative, every Article 27(1) element populated with sub-article citations, and the scoping-and-hand-off note.
- Every identified risk in element (4) carries a specific Charter-article tag.
- The Article 13 provider-info reference is either resolved (by identifier) or flagged as a gap in the scoping-and-hand-off note.
- The human-oversight section names specific roles and specific oversight moments.
- The market-surveillance-authority notification status is honestly stated.
- No fabricated notification acknowledgements, statutes, incidents, or vendor documents.
- No unresolved research markers in the FRIA body itself.

## Stretch goals

- **A Charter-right reference sheet.** Compile a one-page reference of the Charter articles most commonly engaged by AI systems — Articles 1, 8, 21, 24, 25, 41, 47, and any others you tag — with a one-line summary of the right each protects. This becomes a reusable analyst artefact across FRIAs.
- **A FRIA-to-DPIA overlap table draft.** Fill the overlap table from chapter 04 for your specific system — which concerns the DPIA covers, which the FRIA covers, which both cover. This is preview work for exercise 04.
- **A provider-info request template.** Author the shape of the request the analyst sends to the provider when Article 13 instructions-for-use are not on file. Include the specific sub-fields the FRIA needs from the provider.
- **A residual-risk-triggered-authority-consultation memo.** If your FRIA lands with any residual risk *High* after mitigation, author a short memo for counsel walking whether Article 36 GDPR-style prior consultation applies (the FRIA does not carry this mechanism; the DPIA does) and whether the AI Act's serious-incident reporting under Article 73 is a live concern.
- **A cross-reference to a public-sector deployment example.** If you can find a published FRIA or FRIA-shaped assessment from an EU public-sector deployer, cite it as a shape reference. Do not fabricate one.

## Deliverables

- `mod-105-ex-03-fria-<system>-draft.md` — the FRIA first draft plus scoping-and-hand-off note.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works one reference draft against the MCDA-Benefits variant. Yours will differ in the specific harm and Charter-tagging content; what should not differ is (a) the scoping filter is applied and cited before the six-element authoring, (b) every Article 27(1) element is present with sub-article citations, (c) every risk carries a specific Charter-article tag, (d) the Article 13 provider-info dependency is resolved or explicitly flagged, (e) counsel and the DPO have a hand-off note that lets them review efficiently. A short, hand-off-ready FRIA that flags an Article 13 gap beats a longer one that quietly fills the gap with a plausible-sounding paraphrase.
