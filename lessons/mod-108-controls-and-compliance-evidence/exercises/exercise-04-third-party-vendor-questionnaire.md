# Exercise 04 — Third-Party Vendor Questionnaire

**Estimated effort:** 2 hours
**Grounding chapters:** [06 — Third-Party AI Vendor, Model, and Dataset Intake](../06-third-party-ai-vendor-and-model-intake.md), [08 — Independent-Audit and Bias-Auditor Credentialing — ForHumanity and BABL AI](../08-independent-audit-and-bias-auditor-credentialing-forhumanity-and-babl-ai.md), [09 — Delegation Boundary and Escalation Patterns](../09-delegation-boundary-and-escalation-patterns.md).

## Objective

Run the third-party AI vendor intake end to end on three plausible vendor dependencies and produce the paired artefacts: the analyst's *vendor-side questionnaire* (the request the analyst sends to the vendor to elicit missing evidence), the `VND-<year>-<sequence>` vendor-risk-register row per vendor (chapter 06's twenty-two-column schema), and the escalation-register spine for any chapter-09 class-3 vendor / contract actions the row surfaces. The drill's point is not to *find* the vendor evidence — the vendor's trust site and the vendor account team supply that — but to *shape* the request pack, *read* the responses honestly, and *row* the resulting posture in a form procurement, legal, DPO, and vendor-management-office can act on.

After this exercise you should be able to open a new vendor intake and, within the first working day, ship a vendor-side questionnaire that names every artefact the analyst needs, a pre-populated row shell with the fields the public evidence sweep already populates, and a class-3 escalation queue for the gaps the response has to close.

## Prerequisites

- Chapter 06 read; the six vendor-evidence artefact classes (model card, sub-processor list, DPA, ISO/IEC 42001 certification letter, adjacent attestations + independent audit report, security questionnaire response), the twenty-two-column `VND-<year>-<sequence>` row schema, the ten-step intake sequence, the three inheritance decisions (*inherit*, *inherit-with-compensating-controls*, *do-not-inherit*), and the reading-emphasis shifts across dependency classes (hosted foundation model, self-hosted-model artefact, dataset, tooling / audit / monitoring vendor) fresh in memory.
- Chapter 08 read; ForHumanity and BABL AI, the four independent-audit shapes (management-system certification, assurance engagement, independent audit of algorithmic systems, bias audit), the IAF Multilateral Recognition Arrangement, and the NYC Local Law 144 through-line.
- Chapter 09 read; the class-3 vendor / contract action escalation shape.
- The MCDA (`INV-2026-0088`) and MCDA-Benefits (`INV-2026-0311` or equivalent) inventory rows from `mod-102` open — the vendor rows the exercise produces attach to these systems.
- The [OpenAI trust portal](https://trust.openai.com/) and [OpenAI usage policies](https://openai.com/policies/usage-policies/), the [Anthropic Trust Center](https://trust.anthropic.com/) and [Anthropic Usage Policy](https://www.anthropic.com/legal/aup), the [Google Cloud Trust Center](https://cloud.google.com/security/compliance/trust-center) and the [Vertex AI generative-AI documentation](https://cloud.google.com/vertex-ai/generative-ai/docs), the [Azure OpenAI Service documentation](https://learn.microsoft.com/en-us/azure/ai-services/openai/), the [Meta Llama models GitHub repository](https://github.com/meta-llama/llama-models) and the [Meta AI acceptable use policy](https://llama.meta.com/use-policy/), and the [ISO/IEC 42001 abstract](https://www.iso.org/standard/81230.html) plus the [IAF Members list](https://iaf.nu/en/iaf-members/) open — the exercise references these as the public-evidence-sweep sources.
- If your enterprise has ever run a CAIQ, SIG, VSA, or HECVAT vendor security questionnaire, keep the local template open for reference. Otherwise, use the public [Cloud Security Alliance CAIQ](https://cloudsecurityalliance.org/artifacts/consensus-assessments-initiative-questionnaire-v4/) as a reference shape.

## Problem statement

The deliverable is a **single Markdown file, `mod-108-ex-04-vendor-intake.md`**, containing three per-vendor sections plus a cross-vendor summary. Author the intake as if procurement has just notified the analyst that these three vendor dependencies are being renewed or newly evaluated this quarter.

### The three vendors

Pick the vendors from the three dependency classes below. For each, name a plausible specific artefact (do not invent a vendor name that is not real — either use the real vendor or use a bracket placeholder like `[hosted-foundation-model-vendor-X]` if you cannot honestly cite the real trust site):

- **Vendor A — hosted foundation model.** OpenAI (GPT-4o via the enterprise API tier), Anthropic (Claude Sonnet 4.5 via the API), or Google (Gemini 2.x via Vertex AI). Choose one; the exercise scoping is per your enterprise's actual dependency where possible.
- **Vendor B — self-hosted-model artefact.** A Meta Llama release (Llama 3.1 or Llama 4 depending on the release wave at the exercise date), a Mistral release, or a DeepSeek release, pulled from a public source (Hugging Face, the vendor's GitHub, the vendor's own hosting) and fine-tuned inside the enterprise.
- **Vendor C — bias-audit service.** A BABL AI engagement, a ForHumanity-linked audit, or a specialist bias-audit vendor. Where the enterprise's actual bias-audit vendor is not one of these, name it and use the exercise as the analyst's *first* pass at the intake row.

### Per-vendor section shape

Each per-vendor section carries the following sub-sections. Use `## Vendor A — <name>` as the header and mirror the structure for B and C.

#### §A.1 Public-evidence sweep (chapter 06 Step 3)

Author a table with:

- **Artefact class.** One of the six from chapter 06.
- **Source URL.** Live URL the analyst pulled from.
- **Snapshot date.** The date of the sweep (use a plausible date within the last week).
- **Version-of-record.** The specific version, revision, or effective date the artefact declares.
- **Summary.** One or two sentences the analyst can quote later.
- **Gap notes.** Anything missing, ambiguous, or requiring a follow-up.

Cover every artefact class the vendor's dependency class calls for per chapter 06's *reading emphasis* shifts. A hosted foundation model expects all six; a self-hosted-model artefact expects model card + license + supply-chain scan and often skips sub-processor list, DPA, and independent audit; a bias-audit service expects the vendor's own methodology description, their independent-audit posture, and the credentialing of the individuals or teams performing the work (chapter 06's *Evaluation tooling / bias-audit service / monitoring platform* bucket, plus chapter 08's discussion of ForHumanity / BABL AI credentialing).

#### §A.2 Vendor-side questionnaire (chapter 06 Step 4)

Author the request the analyst sends to the vendor's account team for the evidence not available in the public sweep. Structure as a Markdown-rendered email or ticket, with:

- **Header block.** Vendor name, engagement type, enterprise systems affected, `procurement` contract owner cc'd, `data-protection-officer` cc'd (where personal data is in scope), `ai-infra-security` cc'd (where security is in scope), deadline (choose a plausible date five to ten working days out).
- **Body — numbered questions.** Between fifteen and twenty-five questions per vendor, grouped under headers:
  - *Contractual instruments and data protection*
  - *Certifications and accredited attestations*
  - *Independent audit and bias audit*
  - *Sub-processors and supply chain*
  - *Security programme and vulnerability management*
  - *Model / artefact provenance and versioning*
  - *Evaluation, safety, and responsible-use disclosures*
  - *Incident notification and communication*

Every question has a single, unambiguous ask. *Please provide the current DPA text and effective date* is a question; *tell us about your data protection* is not. Every question that references a standard, framework, or credential cites the reference (ISO/IEC 42001, ISO/IEC 27001, ISO/IEC 27701, SOC 2 Type II, ForHumanity IAAIS, BABL AI credential name, IAF-accredited certification body, NYC Local Law 144, GDPR Article 28, etc.). Where the question has a *known-answer* shape (e.g., the vendor's model card is already public and the analyst is asking about a specific gap), the question references the source URL the analyst is asking against.

Vendor B's questionnaire will differ substantially — self-hosted-model artefacts do not have sub-processors, but do have license and provenance questions (upstream URL, verified hash, fine-tune methodology, RAIL / community-license restrictions, etc.). Vendor C's questionnaire will differ again — the bias-audit vendor's own independent-audit posture, their auditor credentialing (ForHumanity, BABL AI, other), their engagement scope shape, and their alignment to NYC Local Law 144 or the Colorado AI Act if applicable.

#### §A.3 `VND-<year>-<sequence>` row (chapter 06 Step 6–8)

Populate the twenty-two-column row from chapter 06. Columns dependent on the vendor's response to the questionnaire (columns 12 ISO/IEC 42001 certification, 14 independent audit, 15 security questionnaire, and — depending on the vendor — column 11 DPA) are populated with *TBD-<reason>-<deadline>*. Columns populatable from the public evidence sweep (identity, dependency class, named artefact, enterprise-side integration, data classification, contract owner, technical owner, model card, sub-processor list, adjacent attestations, OWASP / ATLAS / AI 100-2 / SAIF tags) are populated in full.

Column 17 (residual-risk assessment) is populated as a *draft* — the analyst writes what the residual-risk paragraph *would look like* if the vendor's response confirms the current public evidence, and marks the paragraph *draft — pending vendor response*. Column 18 (inheritance decision) is populated as *draft: inherit-with-compensating-controls — subject to Q<n>, Q<m> resolution* or the analogous shape. Chapter 06 was explicit that the analyst does not skip to the inheritance decision without the residual-risk paragraph; the exercise reinforces the discipline.

#### §A.4 Class-3 escalations

Author the chapter-09 class-3 escalations any gap in the row surfaces. Class-3 covers vendor / contract action escalations — sub-processor in new jurisdiction, DPA needs re-negotiation, certification lapse, questionnaire inconsistency, personal-data processing purpose not covered by contract. Each escalation carries the chapter-09 row shape (rationale, requested action, escalation owner, target date, status) plus the vendor row identifier and the specific column that surfaced the gap.

Where a gap is not a class-3 (the response has not landed; the gap is a *pending* rather than a *class-3*), do not force one; note it in the row as *TBD-<reason>* and hold the escalation until the response lands. Chapter 09's file-up threshold governs.

### Cross-vendor summary section

After the three per-vendor sections, add a **§4 Cross-vendor summary** section. Author a short (half-page) summary covering:

- **The three inheritance decisions.** Draft decisions per vendor with their conditional-on-response qualifiers.
- **The recurring patterns.** Any two-or-more vendors whose intake surfaces the same class of gap (e.g., two vendors with expired ISO/IEC 27001 certifications; two vendors with sub-processor lists that lack jurisdiction detail; two vendors whose bias-audit posture is unclear). Chapter 09's *pattern language for library-level policy work* section governs the pattern classification.
- **The `procurement` / `legal` / DPO / `ai-infra-security` routing summary.** One paragraph per addressee summarising what the analyst is handing off, what the addressee is being asked to act on, and by when. This is the artefact the analyst sends as the cover note when shipping the three rows.

## Requirements

- **Three vendors covered, one per dependency class.** All three (hosted-foundation-model, self-hosted-model artefact, bias-audit service) are present. A three-vendor deliverable where all three are hosted foundation models does not exercise the *reading emphasis shifts with dependency class* discipline chapter 06 called out.
- **Each vendor's public-evidence sweep covers every artefact class the dependency class calls for.** Missing artefact classes are marked *not-published* or *not-applicable-<reason>* on the row — chapter 06 was explicit that recording *no sub-processor list published* is more useful than omitting the artefact class altogether.
- **Each vendor's questionnaire has fifteen to twenty-five questions organised under the section headers above.** Each question is single, unambiguous, and cites the relevant standard, framework, or credential where applicable.
- **Each questionnaire header block copies the correct roles.** `procurement`, `data-protection-officer` (where personal data is in scope), `ai-infra-security` (where security is in scope). Vendor A (hosted foundation model) copies all three by default; Vendor B (self-hosted artefact) copies `ai-infra-security` and possibly `procurement`; Vendor C (bias-audit service) copies `procurement` and possibly `legal`.
- **Each vendor's `VND-<year>-<sequence>` row populates all twenty-two columns.** Columns populatable from the public sweep are populated in full; columns dependent on the vendor's response are marked *TBD-<reason>-<deadline>*. Blanks are not permitted.
- **Column 17 (residual-risk assessment) is a paragraph, not a phrase.** Chapter 06's discipline: the analyst does not skip to the inheritance decision.
- **Column 18 (inheritance decision) is one of the three chapter-06 values.** *inherit*, *inherit-with-compensating-controls*, *do-not-inherit*. A conditional draft (*subject to Q<n> resolution*) is acceptable; a fourth or fifth value is not.
- **Class-3 escalations are opened only where chapter 09's file-up threshold is met.** A questionnaire question the analyst is waiting on the vendor to answer is not a class-3 escalation; a jurisdiction-out-of-approved-footprint sub-processor addition *is*.
- **Adjacent attestations (column 13) name specific certifications and their attesting bodies.** ISO/IEC 27001, ISO/IEC 27701, SOC 2 Type II, SOC 2 Type I, and any others. Chapter 06 and chapter 08 were explicit that the analyst distinguishes IAF-accredited certifications from ForHumanity / BABL-linked audits.
- **The cross-vendor summary identifies at least one recurring pattern.** Chapter 09's pattern language is the reference — recurring inheritance-with-compensating-controls decisions across multiple vendors may suggest a control-library gap; recurring DPA gaps may suggest a procurement model-DPA revision is needed.
- **No fabricated vendor evidence.** Where the vendor's public evidence is genuinely missing (not just gated), the row records *not-published* rather than inventing content. Where the analyst is uncertain about a specific vendor claim (e.g., the exact date of an ISO/IEC 42001 certification), mark `<!-- needs-research: verify against vendor trust portal on <date> -->`.

## Starter guidance

- Start with the public-evidence sweep on all three vendors before drafting any questionnaires. The sweep tells you what the questionnaire needs to ask — questions that would have been answered by the vendor's own published evidence are wasted vendor time and inflate the response deadline.
- For Vendor A (hosted foundation model), the sweep should recover the model card, the acceptable-use policy, the DPA boilerplate (usually available on the trust portal), the ISO/IEC 27001 certification claim, and any published SOC 2 or ISO/IEC 42001 posture. What the analyst asks for privately: the current DPA text (not the boilerplate; the enterprise's actual contract instrument), the current ISO/IEC 42001 certification letter with the IAF-accredited certifying body, the current sub-processor list snapshot, and the CAIQ / SIG response.
- For Vendor B (self-hosted-model artefact), the sweep should recover the model card, the license, the release-note history, and any known-vulnerabilities disclosures. What the analyst asks for privately: the model publisher's response to the enterprise's specific fine-tune methodology, the supply-chain-scan artefact against the enterprise's model registry, and the model publisher's incident-notification protocol. The DPA and sub-processor questions are usually not applicable; do not force them.
- For Vendor C (bias-audit service), the sweep should recover the vendor's methodology description, their auditor credentialing (per chapter 08 — ForHumanity, BABL AI, other), their engagement-scope shape, and any published bias-audit reports. What the analyst asks for privately: the specific auditor to be assigned, their specific credentialing (with `<!-- needs-research: -->` markers where credential names or programme structures cannot be verified from the vendor's current site), the engagement scope for the enterprise's specific AEDT / high-risk system, and their alignment to NYC Local Law 144's *bias audit* and *published summary URL* requirements.
- Vendor A's row will typically end up *inherit-with-compensating-controls* (the enterprise's own guardrail, monitoring, and access-control layers compensate for what the hosted vendor cannot inherit); Vendor B's row will typically end up *inherit-with-compensating-controls* with the compensating controls sitting at the ML platform layer (supply-chain-scan on every model pull, weight-hash pinning, restricted-registry policy); Vendor C's row will typically end up *inherit* with a note on the auditor's credentialing — the audit either meets the enterprise's independence and criteria requirements or it does not.
- Chapter 06's ten-step sequence is the discipline: do not skip from public sweep to inheritance decision. Steps 5 (questionnaire consistency check), 6 (residual-risk draft), and 7 (compensating-controls draft) are what makes the row honest.
- Chapter 08's independence discipline governs the bias-audit vendor. A BABL AI-affiliated auditor is *not* a substitute for the enterprise's own control-cycle work — the audit report is one evidence input; the enterprise's control-cycle still runs.
- The class-3 escalation shape is chapter-09's row shape, not an ad-hoc note. Rationale + requested action + escalation owner + target date + status. Do not shortcut the shape.

## Acceptance criteria

- `mod-108-ex-04-vendor-intake.md` filed with three per-vendor sections and one cross-vendor summary section.
- Each per-vendor section has §A.1 public-evidence sweep, §A.2 vendor-side questionnaire, §A.3 `VND-<year>-<sequence>` row, §A.4 class-3 escalations.
- Public-evidence sweep tables have URL, snapshot date, version-of-record, summary, and gap notes per row.
- Questionnaires have between fifteen and twenty-five questions organised under the eight section headers, each question single and unambiguous, each standard / framework / credential citation explicit.
- Header blocks copy the correct roles (`procurement`, `data-protection-officer`, `ai-infra-security`) with deadline set five to ten working days out.
- `VND-<year>-<sequence>` rows populate all twenty-two columns; TBD-<reason>-<deadline> is used for response-dependent columns; column 17 is a paragraph; column 18 is one of the three inheritance-decision values.
- Class-3 escalations use the chapter-09 template with rationale, requested action, escalation owner, target date, status; escalations are opened only where the file-up threshold is met.
- Adjacent attestations (column 13) name specific certifications with attesting bodies; the ISO/IEC 42001 column and the independent-audit column are distinct (chapter 08).
- Cross-vendor summary identifies at least one recurring pattern and routes to `procurement` / `legal` / `data-protection-officer` / `ai-infra-security` with per-addressee actions.
- No fabricated vendor evidence; `<!-- needs-research: -->` markers used for uncertain claims; not-published / not-applicable recorded honestly.

## Stretch goals

- **A vendor-side response mock.** For one of the three vendors, author a plausible response to your questionnaire — including one *inconsistency* the analyst has to catch. Update the `VND-<year>-<sequence>` row with the response and open the class-3 escalation the inconsistency triggers. This exercises chapter 06's Step 5 (questionnaire consistency check) discipline and the class-3 escalation shape.
- **A compensating-controls cross-reference.** For Vendor A (hosted foundation model), name the specific `CTL-<year>-<sequence>` identifiers of the enterprise controls that compensate for what the vendor cannot inherit (guardrail-classifier, PII-DLP filter, rate-limit, access-log, incident-response playbook). Cross-reference to exercise 01's runbook where those controls sit in scope for the period. This closes the loop between the vendor intake and the internal control cycle.
- **A bias-audit criteria-versus-credential separation table.** For Vendor C, author a short table separating the *criteria origin* (ForHumanity criteria set, BABL-defined criteria set, statutory criteria per Local Law 144, enterprise-defined criteria set) from the *auditor credentialing* (ForHumanity-programme credentials, BABL-programme credentials, CIPP / CISA / ISO 27001 lead-auditor, other). Chapter 08 was explicit that conflating criteria with credential misleads downstream readers; the table is the discipline.
- **A vendor-portfolio roll-up.** After the cross-vendor summary, add a `## Vendor portfolio` block that would sit on the analyst's dashboard: the count of vendors per dependency class, the count of inheritance-decision-draft values, the count of open class-3 escalations, the count of vendors with certifications expiring in the next 90 days. This is the artefact the vendor-management-office reads at the standing council slot; the drill's real value shows the day the roll-up lands on the standing agenda.
- **A cross-reference to `mod-107` vendor-system-card rows.** For Vendor A specifically, link the `VND-<year>-<sequence>` row's model-card column to the `EVAL-<year>-<sequence>` *vendor-system-card* row from `mod-107` exercise 02 (comparative reading of vendor system cards). The two rows are two views of the same vendor artefact — one from the eval-evidence perspective, one from the vendor-intake perspective — and their claims should be coherent when read together.

## Deliverables

- `mod-108-ex-04-vendor-intake.md` — three per-vendor sections (each with §A.1 public sweep, §A.2 questionnaire, §A.3 row, §A.4 escalations) plus the cross-vendor summary.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works one reference intake shaped around Anthropic Claude via the API (Vendor A), a Meta Llama release pulled from Hugging Face (Vendor B), and a BABL AI-affiliated bias-audit engagement (Vendor C), with public-evidence sweeps against the current trust portals, questionnaires of ~20 questions per vendor, twenty-two-column rows with response-dependent columns marked TBD, and two class-3 escalations across the batch. Yours will differ in the specific vendors chosen, the specific evidence pulled, the specific questions asked, and the specific escalations opened. What should not differ is (a) three vendors across the three dependency classes, (b) public-evidence sweep covering every applicable artefact class per chapter 06, (c) questionnaires organised under the eight section headers, (d) rows populating all twenty-two columns with TBD for response-dependent, (e) inheritance decisions from the three chapter-06 values only, (f) class-3 escalations using the chapter-09 template only where the file-up threshold is met, and (g) adjacent attestations distinguished from independent audit distinguished from ISO/IEC 42001 certification. A tight intake pass that gets the chapter-06 discipline right beats a longer pass that inflates the questionnaire and blurs the artefact class distinctions.
