# Quiz 01 — Reading Eval and Audit Evidence, Row Schema, Benchmarks, Packet Hand-Off, and the Delegation Boundary

**Format:** 12 multiple-choice questions, one correct answer each.
**Grounding chapters:** [01](../01-analyst-scope-on-eval-and-audit-evidence.md), [02](../02-inspect-style-eval-report-anatomy.md), [03](../03-rag-triad-and-quality-eval-reports.md), [04](../04-red-team-engagement-reports.md), [05](../05-summarising-eval-evidence-into-a-governance-row.md), [06](../06-reading-public-system-cards.md), [07](../07-responsible-scaling-policies-and-preparedness-frameworks.md), [08](../08-benchmarking-internal-artifacts-against-public-references.md), [09](../09-composing-and-handing-off-the-review-packet.md), [10](../10-delegation-boundary-and-escalation-patterns.md).
**Rules:** Open-book against the chapters themselves — this quiz tests fluency, not look-up. Closed-book against anything else.

---

## Questions

### 1. The analyst's stance

Chapter 01 names the analyst's stance across the module and lists the seven analyst-tier verbs that follow from it. Which statement captures the chapter's framing?

- A. The analyst's stance is producer — designing eval tasks, authoring scorers, running red-team engagements, and signing off release-assurance; the module teaches those production skills.
- B. The analyst's stance is reader-and-summariser — reading the eval, red-team, and audit reports; locating the three load-bearing claims; summarising them into a governance-record row; linking to the source artefact; benchmarking against public references; composing a review packet; escalating under-evidenced claims. Design, execution, and interpretation of novel metrics stay with `ai-evaluation-engineer`, `ai-red-team-engineer`, and `ai-risk-engineer`.
- C. The analyst's stance is release-manager — the analyst's row IS the sign-off, and `ai-evaluation-engineer` reads the row as record of the decision already made.
- D. The analyst's stance is optional — some enterprises assign the row authoring to counsel, others to the product owner, others to the platform team.

### 2. The three load-bearing claims

Chapter 01 names three load-bearing claims the analyst extracts from every report, and chapter 05 wires them into the row schema. Which statement matches both chapters?

- A. The three claims are *accuracy*, *fairness*, and *latency*; without all three the report is not evidence.
- B. The three claims are *vendor name*, *model version*, and *eval date*; the row's identity columns record them.
- C. The three claims are *residual-risk claim* (what risk remains after mitigations, with the per-slice disaggregation where a headline aggregate hides a subset failure), *threshold-decision rationale* (the named internal / vendor / regulator threshold and the yes-or-no call; without a named threshold the field reads *no threshold cited — follow-up filed* and the row is a Class-1 escalation trigger), and *unresolved-findings list* (itemised with severity, likelihood, status, owner, target closure). All three populate the row; a missing claim is a gap, not a silently-omitted field.
- D. The three claims are *coverage*, *depth*, and *calibration*; the analyst is expected to score the report against each on a 1-5 scale.

### 3. Inspect-style anatomy and the per-sample breakdown

Chapter 02 names a specific aggregate-only reading trap and ties it to one of the fourteen expected sections. Which statement captures the chapter's framing?

- A. The analyst reads only section 7 (aggregate metrics) because downstream consumers only care about the headline; section 8 (per-sample breakdown) is optional.
- B. The analyst reads both the aggregate (section 7) and the per-sample breakdown (section 8); the latter is where a safe-looking aggregate — say a 92% refusal rate — can hide an unsafe subset, so the row's residual-risk claim records the disaggregation, and the exact solver and scorer configuration (sections 5 and 6) is recorded in the row's provenance fields so a downstream reader knows the regime (temperature, best-of-N, tool use, judge-model identity) the number came from.
- C. The analyst reads only the change log (section 13) because the headline aggregates are summarised there.
- D. The analyst may ignore sections 5 (solver) and 6 (scorer) because solver and scorer choices do not materially shape the numeric result.

### 4. The RAG triad and the negative-query subset

Chapter 03 fixes the three TruLens RAG-triad metrics and names a load-bearing query subset. Which statement matches the chapter?

- A. The RAG triad is a single composite score that averages three internal numbers; the analyst records only the composite in the row.
- B. The triad is *latency*, *token cost*, and *user satisfaction*; negative queries are the queries a user rates unfavourably.
- C. The triad is *context relevance* (is retrieved context relevant to the query?), *groundedness* (is the generated answer supported by the retrieved context?), and *answer relevance* (does the answer address the question?); all three are recorded separately in the row because a composite can hide a failed component (e.g., 0.98 groundedness, 0.98 answer relevance, 0.3 context relevance is a very different governance story than 0.98 across all three). Negative queries — where the correct answer is a refusal or explicit uncertainty because the corpus does not contain the information — are the load-bearing subset: without them the eval cannot measure over-confident hallucination, and the analyst flags the absence as a scope gap.
- D. Groundedness is treated as a *safety* metric and can substitute for a separate safety eval on a RAG system.

### 5. Red-team evidence shape and the mitigation-without-retest distinction

Chapter 04 characterises red-team evidence shape and names a specific status-field discipline. Which statement captures the chapter?

- A. Red-team evidence is numeric and aggregate-shaped; the analyst reads leaderboard-style metric tables and records a single pass/fail per engagement.
- B. Red-team evidence is narrative and finding-shaped. Each finding is the atomic unit (identifier, title, category mapped to a public taxonomy like OWASP LLM Top 10 / MITRE ATLAS / NIST AI 600-1, severity with rubric name and version, likelihood or exploitability, reproduction, impact, status, mitigation, owner, target closure). A mitigation that was *proposed* but not re-tested is not a validated mitigation; the row's status field must reflect the distinction, and *absence of evidence* is not *evidence of absence* — a red-team that did not find a given attack within scope and budget has not proven the attack does not exist.
- C. A red-team's *no findings* conclusion can be taken as evidence the system is safe; absence of evidence is evidence of absence for adversarial testing.
- D. Severity rubrics for red-team findings on AI systems are fully standardised under CVSS; the rubric name and version are therefore not recorded on the row.

### 6. The `EVAL-<year>-<sequence>` row schema

Chapter 05 fixes the row schema. Which statement matches the chapter?

- A. The row is a free-text memo with no fixed columns; its usefulness is the analyst's written judgment, not a structured record.
- B. The row has nineteen columns across six groups — identity and provenance, system under evaluation (including the inventory row ID, which is mandatory because an eval that cannot be tied to an inventoried system is an eval of nothing), the three load-bearing claims, cross-artefact references (`RSK-`, `IA-`, `REG-`, related `EVAL-` rows), provenance for the eval configuration, and status / review / cadence plus governance-package fields. Identifiers follow `EVAL-<year>-<sequence>`, are never re-used, and a new report produces a new row rather than an update in place. Where a column genuinely does not apply the value is `Not applicable — [one-line reason]`; blank is not a valid value.
- C. One row covers all versions of a system — the analyst updates the single row as new reports arrive, overwriting the prior residual-risk claim.
- D. The row omits the inventory row ID when the system is new, filling it in later when the inventory row is created.

### 7. Reading a public system card

Chapter 06 lists the sections that recur across public system cards and names where the three load-bearing claims live. Which statement captures the chapter?

- A. Public cards are hundreds of pages but contain no shape the analyst can rely on; each card has to be read from scratch with no transferable structure.
- B. Across the public exemplars (OpenAI GPT-4 / GPT-4V / o1 / GPT-4o, Anthropic Claude 3 and successors, DeepMind Gemini technical reports, Meta Llama model cards) a twelve-section shape recurs — overview, training-data summary, safety-training methodology, capability evaluations, safety evaluations, frontier / catastrophic-risk evaluations, red-team summary, known limitations, mitigations, deployment considerations, external evaluation collaborations, change log. The residual-risk claim lives in sections 5 and 6 synthesised with section 8 (known limitations); the threshold-decision rationale lives in section 6 (the vendor's own RSP / Preparedness-Framework classification call); unresolved findings live in section 8 (known limitations) and section 10 (deployment considerations that constrain use). The vendor card row is *supplement*, not *substitute* — internal system-card and internal-eval rows still populate.
- C. The vendor card is independent third-party evidence; where an external collaborator (UK AISI, US AISI / NIST, METR, Apollo Research) is named the analyst can collapse vendor self-report and external-collaborator lines into a single provenance entry.
- D. Model-identifier version suffixes are cosmetic — `claude-3-5-sonnet-20240620` and `claude-3-5-sonnet-20241022` can be treated as the same model when reading cards.

### 8. RSP / Preparedness-Framework vocabulary and cross-vendor comparison

Chapter 07 covers Anthropic's RSP, OpenAI's Preparedness Framework, and DeepMind's Frontier Safety Framework and attaches a specific discipline to cross-vendor comparison. Which statement matches the chapter?

- A. Anthropic's ASL-3, OpenAI's *High* for CBRN, and DeepMind's biosecurity CCL-1 are measured on a common scale; the analyst can build a direct cross-vendor arithmetic table.
- B. The three exemplars share one underlying shape — named risk categories, named thresholds per category, named commitments that trigger at each threshold, named evaluation methodology (internal plus named externals), named governance mechanism, named change process — expressed in three vocabularies (Anthropic AI Safety Levels, OpenAI Tracked Categories × Risk Levels grid, DeepMind Critical Capability Levels). Thresholds are not cross-vendor comparable, so the analyst does not build cross-vendor arithmetic without explicit methodology notes. RSPs are voluntary commitments (not regulations), they revise regularly, and the analyst records both the framework version a paired system card cites and the currently-published version, flagging divergence. The vendor rows come in pairs — *vendor-system-card* plus *vendor-rsp-disclosure* — and reading one without the other loses context.
- C. An RSP is a regulatory instrument that binds the vendor under law; its commitments can be enforced directly by regulators.
- D. An RSP is static; once an initial version is published the analyst does not re-read it.

### 9. The benchmark's four axes and its output

Chapter 08 defines the `BENCH-<year>-<sequence>` row's four axes and names what the benchmark's *output* is. Which statement captures the chapter?

- A. The benchmark is a conformance check that certifies the enterprise against the vendor's framework as a standard; the output is a pass / fail stamp.
- B. The benchmark is a cross-vendor leaderboard the analyst publishes to compare vendors; the output is a vendor ranking.
- C. The benchmark is a structured comparison between the internal `EVAL-<year>-<sequence>` rows and the paired vendor-system-card and vendor-rsp-disclosure rows for the underlying model, walked along four axes — *category coverage* (does the internal eval cover what the vendor's safety-eval categories cover?), *threshold alignment* (does the internal control library match the vendor's stated classification tier?), *deployment-consideration honour* (does the enterprise's deployment honour the vendor's stated deployment considerations?), and *external-evaluator alignment* (does the enterprise have a corresponding line of evidence per each named external — UK AISI, US AISI / NIST, METR, Apollo Research — the vendor relied on?). The output is a gap list with per-gap ID, severity, owner, and target closure date — not a scorecard; every *not applicable* carries a one-line justification. Benchmarks are required for any system whose base model has a public card and RSP disclosure, and are revised when either artefact revises or when the internal system changes materially.
- D. The benchmark produces a composite single-number score that the council quotes in briefings.

### 10. The review packet — structure and hand-off protocol

Chapter 09 fixes the packet's eight sections and the six-step hand-off protocol. Which statement matches the chapter?

- A. The packet is an email to the receiver summarising the eval evidence; filing a copy in a shared drive constitutes hand-off.
- B. The packet is a per-release-decision artefact with eight sections (header plus analyst-tier summary rolling up residual-risk / threshold-decision / unresolved findings / benchmark gap list; evidence table; benchmark row and gap list inline; cross-artefact linkages across `INV-` / `RSK-` / `IA-` / `REG-` / `CTRL-` and prior packets; provenance with a row-set commit / version pin and vendor-artefact snapshot references; open follow-ups for `ai-evaluation-engineer`; escalation hooks; change log). Hand-off runs an explicit six-step protocol: pre-hand-off completeness check against an eleven-point checklist, notification to `ai-evaluation-engineer`, receiver acknowledgement, review, sign-off decision, post-decision packet closure. Tensions between cited rows are *stated, not resolved* — an optimistic summary that silently reconciles a safety-eval pass with an open red-team Medium finding is a broken packet. Every cited stale row is called out explicitly; the correct pattern for an in-flight escalation is to hand off with the escalation entry inline, not to delay the packet waiting for closure.
- C. The packet is a slide deck the analyst walks `ai-evaluation-engineer` through verbally; written version is optional.
- D. The analyst's packet IS the release-assurance sign-off; `ai-evaluation-engineer` counter-signs it as a formality.

### 11. The four escalation classes

Chapter 10 defines four escalation classes with specific triggers, routing, and templates. Which statement captures the chapter?

- A. There is one general escalation flow — the analyst emails `head-of-ai-governance` whenever something looks wrong; class distinctions are not part of the discipline.
- B. There are four classes — *Class 1 under-evidenced claim* (the residual-risk / threshold / unresolved-findings claim is not supported by the evidence cited; routes to the eval owner and ML / product owner, copying `ai-evaluation-engineer`), *Class 2 mis-scoped eval* (the eval measured cleanly but scope does not match the deployed system — model version drift, solver mismatch, category not covered; routes to the eval owner and ML / product owner), *Class 3 stale eval* (the report is beyond its refresh cadence or the evaluated system has drifted; routes to the eval owner and ML / product owner), and *Class 4 packet-cannot-be-handed-off* (rare — material evidence gap cannot be closed in the release window; routes to `head-of-ai-governance` and the governance council, with `ai-evaluation-engineer` notified that the packet is being held). Filing an escalation is the analyst doing the job correctly — silence is the failure mode (the *silent-launder*, the *version-drift silence*, the *stale-refresh silence*, the *packet-shipped-anyway silence*); each escalation is itself a first-class row in a discoverable escalation register (`ESC-<year>-<sequence>`) that auditors read.
- C. Escalations route exclusively to counsel for a legal opinion before any other action.
- D. The analyst resolves Class 4 cases themselves by authoring the residual-risk-acceptable decision in place of the accountable product owner.

### 12. Reading SCN-08 — the reverse hand-off from `ai-evaluation-engineer`

Chapter 10 is explicit about one thing the analyst does not do, and chapter 05 and chapter 09 reinforce it. When `ai-evaluation-engineer` sends the review packet back asking for *the analyst's view on whether the residual-risk claim is actually acceptable given a category-specific miss*, which response matches the chapter's discipline?

- A. The analyst authors a risk-acceptability opinion on the packet so that `ai-evaluation-engineer` can counter-sign it; this is the point of the packet hand-off.
- B. The analyst records the opinion as a new residual-risk claim in the row and updates the packet summary to match, resolving the tension in favour of the deployed system.
- C. The analyst does *not* author the residual-risk-acceptable decision — the eval owner's threshold-decision rationale is quoted in the row; the accept-or-not call belongs to the accountable model / product owner (with governance-council sign-off per enterprise policy on council-relevant rows). The correct response to `ai-evaluation-engineer`'s question is either *additional context quoted from the source report, the impact assessment, or the threshold policy* that helps the receiver's own decision, or a re-routing to the accountable ML / product owner or the governance council for the policy question. The analyst does not substitute their own judgement for either the specialist's or the accountable owner's.
- D. The analyst declines to respond and marks the packet *held* indefinitely; `ai-evaluation-engineer` must resolve the question alone.

---

## Answer key

| # | Answer | Why |
|---|---|---|
| 1 | **B** | Chapter 01's "What the analyst does with eval evidence" enumerates the seven verbs (read / locate / summarise / link / benchmark / compose / escalate) and the "What the analyst does not do" section fixes the delegation boundary (not design / run / sign off / interpret novel metrics / author the residual-risk-acceptable decision). The reader-and-summariser framing is the module's spine; the chapter is explicit that none of the analyst-tier verbs *authors the evaluation itself*. |
| 2 | **C** | Chapter 01's "The three load-bearing claims" section defines each of the three (residual-risk, threshold-decision rationale, unresolved findings) and chapter 05's "The three load-bearing claims" field group wires them into the row. Chapter 05 is explicit that the threshold-decision rationale must cite a named threshold (internal policy, RSP, Preparedness-Framework, regulator benchmark); absence is populated as *no threshold cited in report — follow-up filed [ID]* and the row is flagged for escalation, which chapter 10 names as Class 1. |
| 3 | **B** | Chapter 02's "Common failure modes when reading Inspect-style reports" lists *aggregate-only reading* as the first failure mode and uses the 92% / 8% worked example. The chapter is explicit that solver configuration (temperature, best-of-N, tool use) and scorer configuration (judge model identity, judge prompt version) must go into the row's provenance fields because *a number without its regime is a number, not evidence* (the "What to memorise" bullet). |
| 4 | **C** | Chapter 03's "The three metrics of the RAG triad" names the three verbatim; its "Failure modes specific to RAG-triad reading" section lists *reading the composite RAG-triad score* and *ignoring the negative-query subset* as named traps; and its "What to memorise" bullet is explicit that a composite score is not evidence and that negative queries are the load-bearing subset for measuring over-confident hallucination. The groundedness-is-not-safety discipline is also a "What to memorise" bullet. |
| 5 | **B** | Chapter 04's "What red-teaming is (and is not)" frames the evidence as narrative; "The finding record shape" section enumerates the atomic finding fields; "Severity rubrics — what the analyst should expect" is explicit that rubrics are not standardised and the rubric name / version is recorded on the row; "Reading traps specific to red-team reports" names *absence of evidence isn't evidence of absence* and *the mitigation-without-retest trap*; and "What to memorise" closes with the same four disciplines. |
| 6 | **B** | Chapter 05's "The row schema" section lists the nineteen columns across the six groups verbatim; "The row is a register entry, not a memo" fixes the `EVAL-<year>-<sequence>` identifier convention and the never-re-used rule; "Failure modes when populating the row" lists *the one-row-many-versions row* as a named failure mode; and the inventory-row-ID-is-mandatory rule is the first bullet of the "System under evaluation" field group and the "What to memorise" section. |
| 7 | **B** | Chapter 06's "The load-bearing sections common across public system cards" enumerates the twelve sections; "Where the three claims live in a public system card" names the sections the three claims sit in; "Populating a *vendor-system-card* row" has the mapping table; "Reading traps specific to public system cards" names the *self-published-metric trap* (external-collaborator evidence stays on its own line of provenance), the *version-drift trap* (exact model-identifier version suffixes matter), and the *composition-not-in-card trap* (card is supplement, not substitute). |
| 8 | **B** | Chapter 07's "The three exemplars share a shape" section lists the six shape elements; the three sub-sections (Anthropic, OpenAI, DeepMind) show the three vocabularies against the same shape; "Reading traps specific to RSP-family documents" names the *threshold-arithmetic trap* (thresholds not cross-vendor comparable) and the *version-in-flight trap*; "What the analyst reads for" and "The connection to internal governance artefacts" wire the RSP row to the paired vendor-system-card row; and the "What to memorise" bullets close with *RSPs are voluntary commitments, not regulations* and *vendor rows come in pairs*. |
| 9 | **C** | Chapter 08's "What the benchmark is (and is not)" opens with the gap-analysis framing and names *conformance check* and *cross-vendor comparison* as explicit non-descriptions; "The four benchmark axes" names each axis with its load-bearing question; "Failure modes when benchmarking" lists *the scorecard trap* (the output is a gap list, not a scorecard) and *the silent-not-applicable trap* (every *not applicable* carries a one-line justification); and "What to memorise" states that the benchmark is required for any system whose base model has a public system card and RSP disclosure. |
| 10 | **B** | Chapter 09's "The packet structure" enumerates the eight sections; "The hand-off protocol" numbers the six steps; "The pre-hand-off completeness checklist" lists the eleven checks; "Failure modes" names *the optimistic-summary packet* (tensions stated, not resolved), *the stale-row packet* (every cited stale row called out), *the waiting-on-escalation packet* (hand off with the entry inline — do not delay), and *the silent-file-in-repo hand-off* (notification is explicit). The analyst-is-not-the-signer discipline is in "What the packet is (and is not)". |
| 11 | **B** | Chapter 10's "The four escalation classes" section walks each class with definition, trigger examples, route, and template. The per-class routing (Class 1/2/3 to eval owner + ML / product owner; Class 4 to `head-of-ai-governance` + governance council) is named per class. "Escalation is a first-class output, not a failure mode" lists the four silence failure modes (silent-launder, version-drift silence, stale-refresh silence, packet-shipped-anyway silence); "The register of escalations" fixes the `ESC-<year>-<sequence>` row shape and marks it as a first-class artefact auditors read. |
| 12 | **C** | Chapter 10's "`ai-governance-analyst` does *not*" list is explicit that the analyst *does not author the residual-risk-acceptable decision* — the accept-or-not call belongs to the accountable model / product owner. Chapter 05's "What the analyst does not second-guess" sub-sections across report shapes reinforce the same boundary; chapter 09's "What the packet is (not)" states that *the packet is not the analyst's opinion on whether the system should ship*. The correct response to a reverse-hand-off question for a risk-acceptability view is additional context from source materials or a re-route to the accountable role — not an analyst-authored opinion and not a silent packet-hold. |

## Scoring

- **11–12 correct:** Fluent — ready to read an Inspect-style, RAG-triad, or red-team report and file a defensible `EVAL-<year>-<sequence>` row inside an hour; ready to benchmark against a vendor's card and RSP and produce a gap list; ready to compose and hand off a review packet that `ai-evaluation-engineer` can use as release-assurance input; ready to file an escalation of the correct class rather than silently absorb an evidence gap.
- **9–10 correct:** Solid. Re-read the chapters anchoring any missed questions before `mod-108` (controls-and-compliance-evidence cites eval-evidence rows), `mod-109` (incident-response reads unresolved-findings and stale-eval signals), and `mod-110` (council briefings quote the analyst-tier summary and the benchmark gap list) start leaning on this fluency.
- **7–8 correct:** Partial. Re-read chapters 02 / 03 / 04 (the three report shapes), chapter 05 (the row schema), and chapter 10 (the delegation boundary and the four escalation classes) end-to-end; those five chapters are the module's integration muscle.
- **≤6 correct:** Re-read the module. The downstream modules (`mod-108`, `mod-109`, `mod-110`, `project-101`) assume this material at recall speed, not look-up speed.
