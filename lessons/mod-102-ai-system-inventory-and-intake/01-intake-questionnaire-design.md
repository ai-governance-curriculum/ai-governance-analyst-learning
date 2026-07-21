# The AI Use-Case Intake Questionnaire — Fields Employers Actually Populate

## Why this chapter

The intake questionnaire is the first artefact in the governance program that carries information about a specific AI use case. Everything downstream — the risk register row, the tier tag, the impact assessment, the inventory row, the control-testing plan — draws its fields from what intake captured. A weak intake ("we want to use AI to help our support team") produces a weak assessment. A well-designed intake makes the rest of your work almost mechanical.

At level 15 in the Governance family, you own the intake questionnaire — its shape, its fields, its routing. This chapter enumerates the fields employers actually populate in production programs, why each field is there, and how to design the form so requesters can actually fill it in.

## The audience problem

The person filling in an intake is almost never an ML engineer. They are a product manager, a business owner, a procurement lead, or a line manager. If your form asks for "model family and quantisation strategy" as a first field, they will abandon it, or worse, guess. If your form asks for "what the tool is supposed to do and who owns it", they will answer.

The design principle is: **capture the business-facing fields first; capture the technical fields separately** — filled either by the requester with visible help, or by the requester's ML partner after routing.

## Field-by-field — the canonical intake row

The list below is the intake schema most large-enterprise governance programs converge on. It maps against fields that the NIST AI RMF Playbook MAP-1 through MAP-4 subcategories ask about, the [ISO/IEC 42001:2023](https://www.iso.org/standard/81230.html) Clause 6 planning requirements, and the [EU AI Act (Regulation (EU) 2024/1689)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) tier-tagging inputs. Cite these anchors on the form so the requester sees why you are asking.

### Business-facing fields (requester fills)

| Field | What good looks like | Framework anchor |
|---|---|---|
| **System name** | Short, human-readable, unique within the org | Inventory primary key |
| **Business owner** | A named individual accountable for the outcome — not a team mailbox | NIST GOVERN 2; ISO 42001 Clause 5 |
| **Purpose statement** | One paragraph, plain English: "what is this tool supposed to do, for whom, and why now" | NIST MAP 1.1 |
| **Users** | The people who interact with the system — employees, customers, partners, the general public | NIST MAP 1.6; EU AI Act deployer disclosure |
| **Decision affected** | The concrete decision the system informs or makes (e.g., "which candidate to interview", "which claim to auto-approve") | NIST MAP 5; EU AI Act Art. 6 / Annex III tagging |
| **Autonomy level** | Advisory / assistive / semi-autonomous / autonomous — with a definition next to each choice | NIST MAP 2.1; EU AI Act Article 14 (human oversight) |
| **Deployment surface** | Internal-only / internal user-facing / external customer-facing / public | EU AI Act Article 50 (transparency); NIST MAP 1.6 |
| **Sector or line of business** | Retail / healthcare / financial services / HR / marketing / operations / other | Routes to sector-specific overlays (SR 11-7, GMLP, HIPAA, EEOC) |
| **Geographies where it will operate** | Countries / states / regions where users interact with the system | Routes to jurisdictional overlays (EU AI Act, Colorado SB 24-205, NYC LL 144) |
| **Personal data involved** | Yes / no / unsure — with a follow-up prompt for special-category data (health, biometrics, minors, etc.) | Routes to privacy team; GDPR Article 35 DPIA trigger |
| **Automated decision-making about individuals** | Yes / no / unsure | GDPR Article 22; EU AI Act Annex III item 5 |
| **Target go-live date** | Requester's date; NOT a governance commitment | Program capacity planning |

### Technical fields (requester fills with help, or ML partner completes after routing)

| Field | What good looks like | Framework anchor |
|---|---|---|
| **Model family** | Foundation model (hosted or self-hosted), fine-tune, classical ML, rules-based system, agentic pipeline | NIST MAP 2.2 |
| **Model provider** | For hosted: named vendor and specific model version. For self-hosted: base model + fine-tune train details. For classical: framework and library version | GOVERN 6; third-party review trigger |
| **Training / grounding data sources** | Enumerated: internal dataset names, public corpora, vendor-provided data, synthetic data | NIST MAP 2.2; EU AI Act Article 10 |
| **Retrieval sources (RAG)** | Which internal knowledge stores the system reads from | Access-control review; data-classification check |
| **Tools / APIs the system can call** | For agentic systems: enumerated tool list and blast radius | NIST MAP 4; OWASP LLM Top 10 (excessive agency) |
| **Third-party dependencies** | Model provider, vector store, orchestration framework, observability stack, evaluation tooling | GOVERN 6; ISO 42001 Annex A supplier controls |
| **Integration surfaces** | Which internal systems it reads from or writes to | Change-management overlap |
| **Human-in-the-loop / oversight design** | Who reviews outputs, when, and how they can override | EU AI Act Article 14; NIST GOVERN 3 |

### Governance-fill fields (analyst / governance owner completes)

| Field | What good looks like | Framework anchor |
|---|---|---|
| **Intake tier assessment** | In-scope / out-of-scope / needs-follow-up against the enterprise's own AI definition | Program scope |
| **EU AI Act tier tag** | Unacceptable / high-risk / limited-risk (Article 50) / minimal — with rationale | EU AI Act Article 5 / Annex III / Article 50 |
| **Applicable sector regulator(s)** | FDA / SR 11-7 (Federal Reserve) / EEOC / CFPB / HIPAA / state DFR / other | Sector overlay |
| **Applicable framework anchor(s)** | NIST AI RMF (default), ISO 42001 (if certified), SR 11-7 (financial services), GMLP (medical device) | Routes to correct assessment template |
| **Intake decision** | Approve to enter risk assessment / return to requester for clarification / reject with reason | Program decision |
| **Assigned analyst / owner** | Named governance-team owner going forward | RACI |

## Why the field split matters

A common failure mode is a *single* long form that mixes business fields (which the requester can answer today) with technical and governance fields (which they cannot). Requesters bounce off. A better pattern is a **progressive intake**:

1. Requester submits business-facing fields.
2. Governance triage happens in hours, not days — an analyst assigns the intake tier and routes.
3. ML partner or governance owner fills technical and governance fields in a second pass.

The intake questionnaire lives in a form tool (ServiceNow / Jira / Airtable / a dedicated GRC platform) with the business fields as the visible short form and the technical / governance fields on separate sections that render conditionally or after routing.

## Field definitions matter more than field count

Every field on the form needs a short definition sitting next to it. Requesters do not know what "decisioning autonomy" means. They *do* know what "does the system just suggest an answer, or does it act on its own?" means. Put the plain-English gloss on the form; put the framework anchor in the analyst-facing metadata.

Two examples of definitions worth pasting verbatim:

- **Autonomy level.** *Advisory:* the system produces a suggestion that a human always sees and always decides. *Assistive:* the system drafts something a human edits before it goes out. *Semi-autonomous:* the system acts by default; a human can override before the action commits. *Autonomous:* the system acts and commits without human intervention on the specific instance.
- **Decision affected.** *The specific decision this system informs or takes, phrased in the language the business already uses.* Examples: "which resumes go through to the recruiter", "which customer support ticket routes to which team", "whether to run a marketing email pipeline for a segment", "which invoice to auto-approve for payment".

## Field patterns that fail in production

- **Free-text where a controlled vocabulary is possible.** "Sector" as free text produces "Retail", "retail", "eCommerce", "Consumer Goods" for the same thing. Use a controlled list.
- **Yes/no where "unsure" is the correct third option.** Personal data, automated decision-making, jurisdiction — all warrant "unsure — please help me confirm" so the intake routes rather than the requester guessing wrong.
- **Requiring artefacts that do not exist yet.** Do not require a model card at intake. Require the *promise* of a model card by a stated milestone.
- **Not versioning the intake row.** An intake evolves. Store it as an append-only history so a later reader can see what was known when.

## Concrete example — a hosted-model marketing-copy generator

An intake for an internal tool that drafts marketing copy from product briefs, using a hosted frontier model. Filled by the marketing PM:

- **System name:** Marketing Copy Draft Assistant (MCDA)
- **Business owner:** Priya Nair (Head of Marketing Operations)
- **Purpose statement:** Reduce the time to first-draft marketing copy for a new product launch from three days to four hours by drafting copy from the product brief and prior campaign assets.
- **Users:** Marketing copywriters (internal, ~40 people)
- **Decision affected:** Which draft copy the copywriter starts from
- **Autonomy level:** Assistive
- **Deployment surface:** Internal user-facing
- **Sector:** Marketing / Consumer Goods
- **Geographies:** US, UK, EU
- **Personal data involved:** No (product briefs, no customer PII)
- **Automated decision-making about individuals:** No
- **Target go-live date:** 2026-09-01
- **Model family:** Hosted foundation model (LLM)
- **Model provider:** *Requester unsure — flag for ML partner*
- **Training / grounding data sources:** Product briefs (internal), prior campaigns (internal), no external corpora
- **Tools / APIs:** None — text-in / text-out
- **Third-party dependencies:** Model provider + prompt-management SaaS
- **Human oversight:** Copywriter reviews and edits every output before it enters review workflow

Governance fill would then add: intake tier *in-scope*; EU AI Act tier *Article 50 limited-risk* (deployer of generative AI needs to mark synthetic content; internal-only mitigates some obligations); applicable framework *NIST AI RMF*; assigned analyst *you*.

That single row now anchors the risk assessment, the impact assessment, the inventory entry, and the control matrix.

## What to memorise

- The **three field groups**: business-facing (requester), technical (with help), governance-fill (analyst).
- The **twelve core business-facing fields** — you can recite them cold.
- The definitions of **autonomy level** and **decision affected** — the two fields most often filled badly.
- The rule: **capture "unsure" as a first-class answer**; it routes correctly, guessing does not.

## Summary

The intake questionnaire is the analyst's most-leveraged artefact — every downstream governance artefact draws its fields from it. Split the form into business-facing, technical, and governance-fill sections; give every field a short plain-English definition; use controlled vocabulary where possible; and treat "unsure" as a first-class routing signal, not a validation failure. A well-designed intake makes the tier tag, the risk assessment, and the inventory row almost fall out.
