# Exercise 01 — Eval Report Reading Drill

**Estimated effort:** 2 hours
**Grounding chapters:** [02 — Inspect-Style Eval Report Anatomy](../02-inspect-style-eval-report-anatomy.md), [03 — RAG-Triad and Retrieval-Quality Eval Reports](../03-rag-triad-and-quality-eval-reports.md), [04 — Red-Team Engagement Reports](../04-red-team-engagement-reports.md), [05 — Summarising Eval Evidence into a Governance-Record Row](../05-summarising-eval-evidence-into-a-governance-row.md).

## Objective

Read three eval-family reports covering the three shapes the analyst encounters most often — an Inspect-style capability / safety eval, a RAG-triad retrieval-quality eval, and a red-team engagement report — and turn each into a governance-record row against the `EVAL-<year>-<sequence>` schema fixed in chapter 05. The drill's point is not to *pick* the reports but to *read* them: locate the three load-bearing claims (residual-risk, threshold-decision rationale, unresolved findings), capture the provenance in enough detail that a downstream reader knows the regime the number came from, and file each row with cross-artefact linkages back to the inventory rows the track has already been carrying.

After this exercise you should be able to sit down with any eval, RAG-triad, or red-team report the enterprise's eval-engineering function hands you and produce a defensible row inside an hour without help.

## Prerequisites

- Chapters 02, 03, 04, 05 read; the three load-bearing claims (residual-risk / threshold-decision rationale / unresolved findings) fresh in memory; the nineteen-column row schema open in a second tab.
- The MCDA (`INV-2026-0088`) and MCDA-Benefits (`INV-2026-0311` or your equivalent) inventory rows from `mod-102` and the paired impact-assessment corpus entries from `mod-105`. If you swapped in a different pair of systems on earlier exercises, use the same pair here.
- The regulatory-tracker rows from `mod-106` for the jurisdictions and sector overlays that attach to the pair of systems (at minimum: EU AI Act, Colorado AI Act, NYC LL 144 where applicable, and — for MCDA-Benefits — any healthcare / benefits sector overlay).
- The [UK AISI Inspect framework docs](https://inspect.aisi.org.uk/) open for reference on the task / dataset / solver / scorer vocabulary. The [Inspect Evals repository](https://github.com/UKGovernmentBEIS/inspect_evals) open for a concrete example of what task and scorer implementations look like end-to-end.
- The [TruLens RAG-triad documentation](https://www.trulens.org/) and the [RAGAS metrics reference](https://docs.ragas.io/) open for the RAG-triad metric definitions.
- The [OWASP LLM Top 10](https://genai.owasp.org/llm-top-10/), [MITRE ATLAS](https://atlas.mitre.org/), and [NIST AI 600-1 Generative AI Profile](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) open for the red-team taxonomies the engagement report will reference.

## Problem statement

The deliverable is a **single Markdown file, `mod-107-ex-01-eval-rows.md`**, containing three governance-record rows populated against the chapter-05 schema. One row per report shape.

### Step 1 — Pick or generate the three reports

Two acceptable modes for each of the three shapes. Pick whichever combination is most realistic for your enterprise context; mixing modes across the three shapes is fine.

- **Mode A — real report.** Use a public or lightly-redacted internal report of the target shape. Acceptable public examples:
  - For the Inspect-style shape: any of the eval implementations shipped in the [Inspect Evals repository](https://github.com/UKGovernmentBEIS/inspect_evals) walked as if a run report had been produced against it, or (for a real published run) the [UK AISI Advanced AI Evaluations May 2024 update](https://www.aisi.gov.uk/work/advanced-ai-evaluations-may-update) or an [Apollo Research evaluation](https://www.apolloresearch.ai/research) covering a shape close to the one the enterprise runs.
  - For the RAG-triad shape: a [TruLens example notebook](https://www.trulens.org/trulens_eval/getting_started/quickstarts/) or [RAGAS example](https://docs.ragas.io/en/latest/getstarted/) rendered as a written report against a hypothetical enterprise RAG system.
  - For the red-team shape: the red-team summary section of the [OpenAI GPT-4 System Card](https://cdn.openai.com/papers/gpt-4-system-card.pdf) or the [Anthropic Claude 3 Model Card](https://www-cdn.anthropic.com/de8ba9b01c9ab7cbabf5c33b80b7bbc618857627/Model_Card_Claude_3.pdf), extended into a standalone engagement-report shape for the drill.
- **Mode B — analyst-authored synthetic.** Author a report yourself against the shape chapter 02 / 03 / 04 walks. Use MCDA / MCDA-Benefits as the system under evaluation. This is the mode the paired solutions repo assumes as a fallback.

Whichever mode you pick per shape, the deliverable is not the report itself — it is the row derived from reading it. The report only needs to exist in a form you can cite from the row.

### Step 2 — Populate the three rows

For each of the three reports, author one row in `mod-107-ex-01-eval-rows.md` populated against the chapter-05 schema. Nineteen columns across six groups: identity and provenance, system under evaluation, three load-bearing claims, cross-artefact references, provenance for the eval configuration, status and review and cadence, governance-package fields.

Row identifiers follow the `EVAL-<year>-<sequence>` convention — for this exercise, `EVAL-2026-EX01-01`, `-02`, `-03`.

### Step 3 — Write a short reading-notes block per row

Underneath each row, a short **Reading notes** block (no more than half a page) that captures:

- Which sections of the report populated which columns of the row (mapping table from chapter 05).
- Any ambiguity or absence you had to work through — a missing threshold, an unnamed scorer calibration, an out-of-scope area that surfaced a finding.
- Which row column, if any, you had to populate as `Not applicable — [reason]` versus which you had to escalate (chapter 10 preview — the escalation itself is exercise 04's deliverable, but flag the trigger here).

The reading-notes block is what a peer reviewer or a downstream auditor uses to check your row against the report; without it the row is opaque.

## Requirements

- **All three report shapes are covered** — one Inspect-style, one RAG-triad, one red-team. A three-row file where all three are red-team reports does not meet the drill's coverage requirement.
- **Every row populates every column of the chapter-05 schema.** Where a column genuinely does not apply, the value is `Not applicable — [one-line reason]` (parallel to the `mod-106` convention). Blanks are not permitted.
- **The three load-bearing claims are quoted verbatim from the source report** where language exists in the report. Paraphrasing is only acceptable to compress; it must not sharpen or soften the claim. If the report uses hedged language (*generally acceptable*, *in most tested cases*) the row uses the same hedged language.
- **The provenance columns are populated at the level of the report's regime.** Model identifier and version, exact solver configuration (temperature, best-of-N, tool inventory), scorer type and — for LLM-as-judge scorers — the judge model and judge-prompt version, dataset identifier and sample count. A row that reads *temperature 0-ish* is not defensible; the exact value goes in.
- **Every row's inventory row ID is populated.** An eval that cannot be tied to an `INV-<year>-<sequence>` row is filed against nothing; use the MCDA or MCDA-Benefits inventory row (or the equivalent pair) that has carried across the track.
- **Cross-artefact reference fields are populated for every row.** At minimum: `RSK-<year>-<sequence>` rows updated in the register (`mod-103`); `IA-<year>-<sequence>` refresh triggers fired (`mod-105`); `REG-<year>-<sequence>` rows linked (`mod-106`). Where none apply, mark `None` with a one-line reason.
- **The RAG-triad row records all three metrics separately.** A composite RAG-triad score alone is not evidence per chapter 03. Record context relevance, groundedness, and answer relevance as three values with per-metric threshold-decision rationale.
- **The red-team row records the taxonomy referenced.** Which OWASP LLM Top 10 items, which MITRE ATLAS techniques, which NIST 600-1 categories the engagement scoped against.
- **Report-type field uses the controlled vocabulary from chapter 05.** *capability-eval* / *safety-eval* / *fairness-eval* / *rag-triad-eval* / *red-team* / *external-audit* / *vendor-system-card* / *vendor-rsp-disclosure*. Not free-text.
- **The reading-notes block per row is populated** — sections-to-columns mapping, ambiguities encountered, escalation triggers flagged.
- **No fabricated numbers, benchmarks, or vendor claims.** If you author a synthetic report, mark the header of that synthetic explicitly as `<!-- illustrative — not a real report -->` and prefer illustrative-shaped numbers (*hypothetical refusal rate 96.4%*) over vendor-branded ones. If you cite a real published report, the numbers come from the report verbatim; where a specific piece of data you would have wanted is not in the published source, mark that row's cell `<!-- needs-research: source of X -->` rather than filling it.

## Starter guidance

- Read each report end-to-end before you start populating the row. Populating fields as you read on the first pass produces rows that get shape wrong — you cannot summarise a residual-risk claim from section 10 while you are still reading section 4. One-pass read, then structured extraction.
- The chapter-02 mapping table (section *Populating the row from an Inspect-style report*) is the mechanical guide for the first row. The chapter-03 table walks the RAG-triad populator. The chapter-04 mapping is the red-team populator. If you find yourself deviating from these tables, note *why* in the reading-notes block.
- For the Inspect-style row, the trap chapter 02 called out is *aggregate-only reading*. If the report has a per-sample breakdown, quote both the aggregate and the disaggregated result in the residual-risk claim — a system whose 96% refusal-rate collapses to 89% on one protected-class subset has a residual-risk claim with two parts, not one.
- For the RAG-triad row, the trap chapter 03 called out is *composite RAG-triad score reading*. Record the three metrics separately. Also check that the report has a **negative-query** subset; if not, the *unresolved findings* column names this as a scope gap the analyst is filing.
- For the red-team row, the trap chapter 04 called out is *mitigation-without-retest*. A finding whose mitigation was proposed but not re-tested is not a closed finding; the row's status column reads *evidence-current* only if the mitigations that were re-tested cover the release-gating criteria.
- If the report you are reading does not name a threshold, the *threshold-decision rationale* field is populated with `no threshold cited in report — follow-up filed [ID]` per chapter 05, and the row is a Class-1 escalation trigger for exercise 04. Do not manufacture a threshold from the metric.
- The *counsel-flag* column is often the hardest to populate honestly. Ask: does anything in this report change what counsel should know about the system's regulatory posture — a category-specific failure in a Colorado or NYC-covered use case, a fairness signal, a hallucination pattern on a healthcare-adjacent MCDA-Benefits use case? If yes, populate the field with the specific one-line question and the linked `REG-<year>-<sequence>` tracker row.
- The *council-relevant* and *release-assurance-relevant* boolean flags govern which downstream artefacts (the council briefing per `mod-110` and the review packet per chapter 09) will cite the row. Any Critical or High unresolved finding is council-relevant by default; any row on a system approaching a release gate is release-assurance-relevant.

## Acceptance criteria

- `mod-107-ex-01-eval-rows.md` filed with three complete `EVAL-<year>-<sequence>` rows — one Inspect-style, one RAG-triad, one red-team — and one reading-notes block per row.
- Every row populates every one of the nineteen columns across six groups. `Not applicable — [reason]` is a valid value; blank is not.
- The residual-risk claim quotes the report; the threshold-decision rationale cites a named threshold (or explicitly flags its absence); the unresolved-findings list is itemised with severity, owner, and target closure date.
- The provenance columns record the exact model identifier and version, solver configuration, scorer configuration, dataset identifier and sample count.
- The cross-artefact reference columns are populated with `RSK-`, `IA-`, `REG-` identifiers (or `None` with a reason).
- The RAG-triad row records all three metrics separately; a composite-only row is not accepted.
- The red-team row names the taxonomy references (OWASP LLM Top 10 / MITRE ATLAS / NIST 600-1) the engagement scoped against.
- The reading-notes block per row maps sections to columns, names ambiguities encountered, and flags any Class-1 / Class-2 / Class-3 escalation triggers (exercise 04 handles the escalations themselves).
- No fabricated numbers, benchmarks, or vendor claims. Synthetic reports are marked as such; real reports are cited to source; uncertain fields are marked `<!-- needs-research: -->`.

## Stretch goals

- **A fourth row of type *external-audit*.** Read a public external-audit-shaped artefact — for example a [Big-Three assurance-report engagement over a public AI-management-system implementation](https://www.aicpa-cima.com/topic/audit-assurance/audit-and-assurance-greater-than-service-organization-smaller-than-soc-suite-of-services) or the audit sections of a public system card — and populate a fourth `EVAL-<year>-<sequence>` row. This exercises the schema's coverage of the *external-audit* report type not otherwise covered by the three main reports.
- **A same-system multi-report row set.** Instead of three unrelated reports, produce three rows against the same inventory row (e.g., all three against MCDA — Inspect-style safety eval, RAG-triad eval if MCDA is retrieval-augmented, red-team engagement). The stretch is not the reading; it is the *cross-referencing* — the three rows link to each other via the *related eval rows* column, and their residual-risk claims should be coherent when read together. If they are not coherent, that is a chapter-09 packet-composition issue you will meet again in exercise 03.
- **A same-model multi-system row set.** Take one underlying frontier model your enterprise uses on two or more inventoried systems and produce one row per system for a safety eval on that model. This surfaces where the same model produces different residual risks in different deployment contexts and prepares the ground for the benchmark chapter 08 works.
- **A rubric-catalogue mini-artefact.** For the red-team row, extract the severity rubric the report used and file it as a standalone reference (e.g., `mod-107-ex-01-severity-rubric-catalogue.md`) that names the rubric, its version, its tier definitions, and how it compares to CVSS and to OWASP's risk-rating methodology. Chapter 04 called this out as an enterprise gap; extracting it once means the analyst is not chasing it every time.
- **A machine-readable projection.** Render the three rows as YAML or JSON alongside the Markdown, using field names that match the chapter-05 schema exactly. GRC platforms increasingly ingest structured evidence rows; a machine-readable projection makes the row usable downstream without re-authoring.

## Deliverables

- `mod-107-ex-01-eval-rows.md` — three complete governance-record rows, one per report shape, each with a reading-notes block.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works one reference row set shaped around MCDA / MCDA-Benefits with the three report shapes authored in Mode B (analyst-authored synthetic). Yours will differ in the specific reports chosen, the specific numbers quoted, and the specific ambiguities encountered. What should not differ is (a) all three shapes are covered, (b) every row populates every column of the schema, (c) the three load-bearing claims are quoted verbatim from the source rather than paraphrased into abstractions, (d) the RAG-triad row keeps all three metrics separate, (e) the red-team row names the taxonomy the engagement mapped to, and (f) the reading-notes block per row maps sections to columns. A three-row file with every column populated honestly and every claim traceable to the source beats a ten-row file where half the columns are pending or paraphrased away from the report's own language.
