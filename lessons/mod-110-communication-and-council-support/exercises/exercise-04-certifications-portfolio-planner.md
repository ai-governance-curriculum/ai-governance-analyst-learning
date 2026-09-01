# Exercise 04 — Certifications Portfolio Planner

**Estimated effort:** 2 hours
**Grounding chapters:** [01 — The Analyst's Scope on Communication and Council Support](../01-analyst-scope-on-communication-and-council-support.md), [08 — Certifications: AIGP, CIPP, and ISO/IEC 42001 Lead Implementer / Lead Auditor](../08-certifications-aigp-cipp-and-iso-42001.md), [09 — Delegation Boundary and Escalation Patterns](../09-delegation-boundary-and-escalation-patterns.md).

## Objective

Compose the analyst's own three-year written credential portfolio plan per chapter 08, mapped against the analyst's enterprise context (jurisdictional footprint, industry vertical, promotion-path intent) and the modules' actual coverage of the AIGP / CIPP / ISO-42001 body-of-knowledge overlap. Chapter 08 was explicit that the portfolio plan is a *written* artefact reviewed annually with the analyst's manager; this exercise is where the analyst produces the artefact.

The drill's point is that certification is a *choice*, not an accretion. An analyst who accretes credentials over the course of a role without a written plan ends up with a certification profile shaped by whichever training the enterprise happened to fund in a given year — often peer-role credentials (CISSP, CISM, AWS ML Specialty) that the analyst does not need and that chapter 08 identified as *not the analyst's default targets*. Composing the plan explicitly is how the analyst makes the choice their own.

The plan is also the analyst's negotiation artefact for the annual performance and training-budget conversation. Chapter 08 was explicit: *the analyst discusses the portfolio plan with their manager at the annual performance cycle and secures the training budget in that conversation*.

After this exercise you should have a ready-to-share credential portfolio plan the analyst can present to their manager at the next annual cycle, plus a personal *coverage-gap analysis* mapping the analyst's current fluency to the AIGP body of knowledge and identifying the two or three topics the analyst most needs to study before sitting the exam.

## Prerequisites

- Chapter 01 read; the analyst's role and the module's three tangible outputs fresh in memory.
- Chapter 08 read at depth. Particularly: the AIGP-as-shared-vocabulary framing, the CIPP/US-vs-CIPP/E jurisdictional-choice logic, the ISO/IEC 42001 lead-implementer / lead-auditor path, the peer-role credentials the analyst does *not* pursue (CISSP, CISM, PMP, ML practitioner credentials, PhD-level academic credentials, vendor-specific credentials), the three worked portfolio sequences, and the credential-plus-practice discipline.
- Chapter 09 read; the delegation-boundary rows for certifications and professional development (analyst plans in consultation with manager; enterprise ISO/IEC 42001 certification belongs to `head-of-ai-governance` and `senior-ai-governance-architect`; peer-role credentials belong to peer roles).
- The [IAPP AIGP page](https://iapp.org/certify/aigp/) open — the analyst reads the current body-of-knowledge outline and exam blueprint before composing the plan. Chapter 08 was explicit that the outline changes; the analyst does not plan from a snapshot.
- The enterprise's `JOB_REQUIREMENTS.md` for the analyst role (if the track has one) or the enterprise's own analyst-role posting, so the enterprise-specific credential expectations feed the plan.
- The enterprise's training-budget policy (if you have visibility) — training-budget cycles, per-year training caps, credential-cost-reimbursement rules. If you do not have visibility, note the assumption in the plan.

## Problem statement

The deliverable is a **single Markdown file `mod-110-ex-04-portfolio-plan.md`** containing five sections:

- **§1 Analyst profile.** The analyst's current role context — enterprise industry vertical, jurisdictional footprint, portfolio scale, promotion-path intent, current credentials held.
- **§2 AIGP coverage-gap analysis.** The analyst's honest mapping of current fluency against the current AIGP body-of-knowledge outline, identifying the two or three areas the analyst needs to study most before sitting the exam.
- **§3 Three-year portfolio sequence.** The analyst's plan for the next three years — which credential in year 1, which in year 2, which (if any) in year 3 — with the rationale for the sequence chosen and the enterprise-context justification.
- **§4 Credential-versus-practice loop.** For each credential in the sequence, the specific practice-and-application the analyst commits to running *alongside* the credential preparation so the credential-plus-practice discipline is maintained.
- **§5 Manager-conversation preparation.** The analyst's talking points for the annual performance-and-training-budget conversation with their manager — what the analyst is asking for, why, and the expected return-on-effort.

Plus a short *stretch appendix* section (labelled *§Appendix A — Not-pursued credentials*) explicitly listing peer-role credentials the analyst is *not* pursuing, per chapter 08 and 09, with the reasoning.

### The five sections, in detail

#### §1 Analyst profile

One or two paragraphs plus a short structured block. Cover:

- **Enterprise industry vertical** — e.g., regulated financial services, healthcare, public sector, technology-and-media, professional services. The vertical shapes the credential logic (CIPP/E for EU financial services; ISO/IEC 42001 lead-implementer for standards-and-assurance-focused technology).
- **Jurisdictional footprint** — the enterprise's primary and secondary jurisdictions. The footprint drives the CIPP choice.
- **Portfolio scale** — rough count of AI systems in the enterprise's inventory, roughly what proportion are high-risk under the enterprise's tiering, roughly how many jurisdictions the portfolio spans. Chapter 08 was explicit that credential-planning depends on the *material* scale of the AI portfolio.
- **Promotion-path intent** — the analyst's intended promotion path. The two archetypal paths chapter 08 named: (a) toward the `senior-ai-governance-architect` track (the standards-and-assurance-focused path); (b) toward a privacy-adjacent AI-governance path (the CIPP-heavy path). A third: staying at analyst tier long-term (uncommon; the credential-planning is still worth doing but the pacing is different).
- **Current credentials held** — list any relevant credentials the analyst already holds (AIGP, CIPP variants, ISO/IEC 27001 lead-implementer or similar, security or project-management credentials). Note the year obtained and current status (active / lapsed / renewal-due).
- **Enterprise training-budget position** — the analyst's understanding of the enterprise's per-year training-budget cap, credential-cost-reimbursement rule, and per-year credential-count cap (if any). Note assumptions where visibility is limited.

If your worked-artefacts context has not fixed a specific enterprise profile, use a plausible one — e.g., a UK-headquartered mid-sized financial-services enterprise with an EU footprint, roughly 50 AI systems in the inventory, roughly 8 high-risk, targeting the `senior-ai-governance-architect` promotion path.

#### §2 AIGP coverage-gap analysis

For each of the AIGP body-of-knowledge domains, the analyst rates current fluency (*fluent* / *working knowledge* / *gap*) and identifies the specific `mod-101`–`mod-110` chapter or exercise that most-directly covered the domain from the analyst's own study. Chapter 08 was explicit that the track's `mod-101` (landscape), `mod-103` (risk assessment), `mod-105` (impact assessments), `mod-106` (regulatory tracking), and `mod-108` (controls) cover a large fraction of the AIGP preparation as a by-product; the analyst's honest self-assessment identifies which of the domains the track covered less directly.

The AIGP body of knowledge organises around (per chapter 08): foundational AI concepts (what AI is, what an AI system is, the AI lifecycle stages); the AI legal and regulatory landscape (EU AI Act, US federal and state statutes, sector overlays, cross-jurisdictional variation); the AI risk management landscape (NIST AI RMF, ISO/IEC 23894, ISO/IEC 42001); impact assessments and their variants; the deployment lifecycle (development, testing, deployment, monitoring, incident response); the roles and responsibilities across an AI governance program. Verify the current outline against the [IAPP AIGP page](https://iapp.org/certify/aigp/) at the time of composing — chapter 08 flagged the outline as `<!-- needs-research: -->` because it changes.

The gap-analysis format:

```
| AIGP domain (per current IAPP outline) | Current fluency | Anchored in this track by | Study action (if gap or working knowledge) |
|---|---|---|---|
| [domain 1] | [rating] | [chapter or exercise] | [action] |
| ... | ... | ... | ... |
```

Identify the *two or three domains* the analyst has the deepest gap on. These are the study-prioritisation calls the analyst will make ahead of the exam. Chapter 08 was explicit that the credential is preceded by the practice; if the analyst rates every domain as *fluent* without having done the module work, the assessment is wishful.

#### §3 Three-year portfolio sequence

The analyst's plan for years 1, 2, and 3. Chapter 08 gave three worked sequences (privacy-adjacent enterprise; US-centric enterprise; standards-and-assurance enterprise); use the one that most-closely matches your §1 analyst profile, or compose a fourth-sequence variant with explicit justification.

Format:

```
| Year | Credential | Rationale (why this credential this year) | Enterprise-context justification | Estimated cost | Estimated study effort |
|---|---|---|---|---|---|
| Year 1 (starting [YYYY-MM]) | [e.g., AIGP] | [rationale] | [context] | [cost] | [effort] |
| Year 2 | [e.g., CIPP/E or ISO 42001 LI] | ... | ... | ... | ... |
| Year 3 | [e.g., the other of above, or none / renewal] | ... | ... | ... | ... |
```

For the rationale, cite chapter 08's framing (AIGP as shared vocabulary → sequenced first; CIPP as privacy-adjacent depth extension → sequenced by jurisdictional footprint; ISO/IEC 42001 lead-implementer as standards-and-assurance depth extension → sequenced for the senior-architect promotion path). Estimated cost and estimated study effort should be honest and researched (typically several hundred to a few thousand pounds / dollars per credential; typically 40–100 hours of study effort depending on prior background). Chapter 08 was explicit that these are real budget and time commitments.

Year 3 may legitimately be *no new credential, focus on practice and renewal* if the year-1-and-2 credentials plus the analyst's continuing practice are sufficient for the promotion-path intent. Chapter 08's *three credentials over three years is a reasonable pace; more than that is a signal of credential-collecting* discipline applies.

#### §4 Credential-versus-practice loop

For each credential in the sequence, the analyst names the specific practice-and-application the analyst commits to running alongside the credential preparation. Chapter 08 was explicit that the credential *plus* practice produces competence; the credential alone produces the vocabulary without the ground.

Format per credential:

```
### Year N — [Credential name]
- **Practice paired with study.** [Specific application — e.g., authoring three fresh impact assessments in the impact-assessment domain the AIGP covers; leading a mock council pre-read cycle where the analyst applies AIGP vocabulary in real cross-functional conversation; running a fresh vendor intake using the ISO/IEC 42001 clause-9 audit lens.]
- **Deliverables the analyst commits to.** [Specific artefacts — e.g., three signed IAs, one full council-cycle pack, one worked vendor row.]
- **Success indicator (independent of exam result).** [How the analyst will know the practice-and-credential loop worked — e.g., a specific colleague conversation the analyst is now able to have; a specific artefact the analyst is now able to compose faster.]
```

The practice-and-application must be *distinct* from the analyst's normal role duties. The point is that the analyst uses the credential preparation as a scaffold for deeper engagement with the practice, not that the credential runs on top of the normal work.

#### §5 Manager-conversation preparation

The analyst's talking points for the annual performance-and-training-budget conversation. Chapter 08 was explicit that the manager-conversation is where the plan lands or does not; going into the conversation without prepared talking points is where portfolio plans die.

Cover at minimum:

- **The ask.** Concrete — the specific credential the analyst is proposing for the coming year, the training-budget line the analyst is asking the manager to approve, the study-time accommodation (if any) the analyst is requesting.
- **The rationale.** In the manager's language — how the credential supports the enterprise's AI governance posture, the analyst's promotion-path intent, and the specific practice the analyst will run alongside.
- **The expected return-on-effort.** What the analyst will be able to do six or twelve months after obtaining the credential that the analyst cannot do today. Chapter 08 was explicit that credential-holding without ongoing practice is a snapshot-fluent pattern; the analyst's return-on-effort is credential-plus-practice, not credential alone.
- **The alternative.** What the analyst will do if the manager cannot approve the credential (self-fund? defer to next year? substitute a lower-cost credential?). Preparing the alternative is what makes the conversation an actual negotiation.
- **The follow-through commitment.** How the analyst will report back on the credential (progress updates through the year; a debrief after the exam sit).

#### §Appendix A — Not-pursued credentials

A short section listing peer-role credentials the analyst is *not* pursuing, per chapter 08 and 09, with the reasoning. At minimum:

- **CISSP (ISC²)** — the security credential. Belongs to the `ai-infra-security` peer track. The analyst borrows the vocabulary from the security-audience translations (chapter 02) and from `mod-108`'s control-library work.
- **CISM (ISACA)** — the security-management credential. Belongs to `ai-infra-security` at a management-tier and to `internal-audit` peers.
- **CISA (ISACA)** — the audit credential. Belongs to `internal-audit` peers.
- **PMP / Prince2 (PMI / AXELOS)** — project-management credentials. Useful for project-management-flavoured governance roles; not the analyst's differentiator.
- **AWS Machine Learning Specialty (AWS)** or **Google Professional ML Engineer (Google)** — technical ML-engineering credentials. Belong to `ai-eval-engineer` and `ai-infra-mlops` peer tracks.
- **Vendor-specific responsible-AI or governance-tool certifications** — pursued only where the enterprise is materially committed to the vendor's platform; not pursued speculatively.

For each, name the peer track it belongs to and the vocabulary-borrowing pattern the analyst uses in place of pursuing the credential.

## Requirements

- **The file is a single Markdown file** `mod-110-ex-04-portfolio-plan.md`.
- **All five sections present** (§1 through §5) plus §Appendix A.
- **§1 covers all six items** (industry vertical, jurisdictional footprint, portfolio scale, promotion-path intent, current credentials held, enterprise training-budget position).
- **§2 is an honest coverage-gap analysis**, not a self-congratulatory *fluent-in-everything* pass. At least two or three domains identified as *working knowledge* or *gap* with specific study actions.
- **§3 is a three-year sequence** with per-year credential, rationale, enterprise-context justification, estimated cost, estimated study effort. AIGP is sequenced first (unless the analyst already holds AIGP; in which case the plan opens with the credential the analyst already holds noted in §1). Chapter 08's *AIGP first, then depth extensions* discipline is applied.
- **§4 is per-credential**, with practice paired with study, deliverables the analyst commits to, and success indicators independent of exam result.
- **§5 covers all five items** (the ask, the rationale, the expected return-on-effort, the alternative, the follow-through commitment).
- **§Appendix A explicitly names peer-role credentials the analyst is not pursuing** with the reasoning tied to chapter 08 and 09.
- **The plan does not read as credential-collecting.** Chapter 08 was explicit that more than three credentials over three years is a signal of credential-collecting rather than role-depth. If your plan has five credentials in three years, revisit.
- **The plan respects the peer-role boundary.** Chapter 09 was explicit that the analyst does not compete on peer-role credentials as a substitute for their own portfolio. A plan that has AWS Machine Learning Specialty in year 2 is off-side.
- **The plan is realistic about cost, effort, and enterprise budget.** Not aspirational — the numbers are honest.
- **Facts about credentials (fees, exam length, prerequisites, providers, current outline) are verified against the primary source at the time of composing.** Where verification is not possible, note `<!-- needs-research: ... -->` per chapter 08's flagging discipline.
- **The plan is written to be read by the analyst's manager**, not by the analyst alone. Tone is professional; the ask is explicit.

## Starter guidance

- Read the current AIGP body-of-knowledge outline from the [IAPP AIGP page](https://iapp.org/certify/aigp/) before drafting §2. Chapter 08 flagged the outline as `<!-- needs-research: -->` because it changes; the analyst reads live, does not plan from a snapshot.
- Draft §1 first. The analyst profile shapes every subsequent section — the CIPP variant chosen in §3, the practice pairings in §4, the manager-conversation framing in §5.
- For §2, be honest about which domains you are less fluent in. Chapter 08 was explicit that the credential-plus-practice discipline requires the analyst to identify the gaps and study them. A gap analysis that shows fluency across every domain is the sign the analyst has not yet done the honest assessment.
- For §3, pick the worked sequence from chapter 08 that most-closely matches your §1 profile. Chapter 08's three sequences (privacy-adjacent, US-centric, standards-and-assurance) cover the three archetypal analyst contexts; the analyst's specific case usually maps to one of them with minor variation.
- Estimate the cost and effort honestly. The AIGP exam fee is typically several hundred pounds / dollars for members and slightly higher for non-members; the CIPP exam fees are similar; the ISO/IEC 42001 lead-implementer training is typically several thousand pounds / dollars including exam. Verify against the training provider's current fee schedule.
- Estimate the study effort honestly. For a candidate with the track's `mod-101`–`mod-110` under their belt, the AIGP is typically 30–60 hours of focused preparation. CIPP/E or CIPP/US is typically 50–100 hours (more if the analyst is new to the jurisdiction's privacy statutes). ISO/IEC 42001 lead-implementer training is typically 40 hours of instruction plus 20–40 hours of preparation for the exam.
- For §4, the practice-and-application must be *distinct* from the analyst's normal role duties. If the practice is *"continue doing what I already do"*, the practice-and-application discipline is not being exercised; the credential is running on top of business-as-usual, not scaffolding deeper engagement.
- For §5, the manager conversation is a negotiation. Preparing the alternative (self-fund, defer, substitute) is what makes the ask credible; a manager who hears *"this is the only credential I want and I want it approved"* has less flexibility to say yes than one who hears *"this credential, this cost, this year — and here's the alternative if the budget does not permit."*
- For §Appendix A, chapter 09 was explicit about the peer-role credentials. Do not list every credential in every adjacent domain; list the credentials the analyst has been *asked about* or *tempted by* and explain why they are not on the plan.
- If your enterprise has a specific certification the AI-governance analyst role posting lists as required or preferred (some enterprises name specific ISO/IEC 42001 lead-implementer training providers, some name the AIGP explicitly), reconcile the plan against the requirement. If the plan does not include a credential the role posting lists as required, name the reconciliation explicitly (are you targeting the role in year N; is the requirement flexible; do you already hold an equivalent).
- If you already hold some of the credentials in the sequence, adjust the plan accordingly — §3 opens with the year the credential was obtained (noted in §1) and years 1, 2, 3 sequence the next credentials. Chapter 08's three-credentials-over-three-years pacing applies to *net-new* credentials from where the analyst stands today.

## Acceptance criteria

- Single file `mod-110-ex-04-portfolio-plan.md` filed.
- All five sections plus §Appendix A present.
- §1 covers all six items (industry vertical, jurisdictional footprint, portfolio scale, promotion-path intent, current credentials held, enterprise training-budget position).
- §2 is an honest AIGP coverage-gap analysis with at least two or three domains identified as *working knowledge* or *gap* with specific study actions.
- §3 is a three-year sequence with per-year credential, rationale, enterprise-context justification, estimated cost, estimated study effort. AIGP sequenced first (or noted as already-held). Chapter 08's *AIGP first, then depth extensions* discipline applied. No peer-role credentials in the sequence.
- §4 is per-credential with practice paired with study, deliverables the analyst commits to, and success indicators independent of exam result. The practice is distinct from business-as-usual.
- §5 covers all five items (ask, rationale, expected return-on-effort, alternative, follow-through commitment).
- §Appendix A names at least four peer-role credentials the analyst is not pursuing with the reasoning tied to chapter 08 and 09.
- No more than three credentials in the three-year plan. No peer-role credentials substituted for the analyst's own portfolio.
- Facts about credentials verified against primary sources or noted with `<!-- needs-research: -->`.
- The plan is written to be read by the analyst's manager.

## Stretch goals

- **The five-year extension.** Extend the three-year plan to five years, covering the analyst's continued professional development after the initial three credentials are obtained. Chapter 08's discussion of the professional-network dimension (IAPP membership, ISO/IEC JTC 1/SC 42 mirror-committee engagement, NIST AI Safety Institute Consortium participation) offers non-credential development options for years 4 and 5. The five-year plan is what the analyst reviews at each annual cycle.
- **The peer-role credential-borrow map.** Compose a `mod-110-ex-04-borrow-map.md` file listing, for each peer-role credential the analyst is *not* pursuing (per §Appendix A), the *specific* vocabulary borrowing the analyst uses in practice — which peer role holds the credential, which specific concepts the analyst carries from the credential's body of knowledge without holding the credential themselves, and how the analyst maintains awareness of updates. This exercises chapter 09's *analyst borrows peer-role vocabulary* discipline.
- **The credential-ROI check-in template.** Compose a `mod-110-ex-04-roi-check-in.md` file — a lightweight template the analyst uses six months after obtaining each credential to check whether the credential-plus-practice loop actually worked. Fields: which vocabulary the analyst has actively used, which conversations were shorter because of the credential, which artefacts the analyst has authored differently, which specific claim of return-on-effort from §4 was validated or missed. This is the analyst's internal accountability artefact.
- **The manager-conversation script.** Compose a `mod-110-ex-04-manager-script.md` file with an actual 400–600 word script for the annual performance-and-training-budget conversation. The analyst reads it aloud in preparation; the script exposes any weak claims or unrealistic asks before the actual conversation. Chapter 08 was explicit that the conversation is where portfolio plans land.
- **The alternative-path sketch.** For an analyst on the standards-and-assurance sequence targeting `senior-ai-governance-architect` promotion, sketch a `mod-110-ex-04-architect-track.md` file identifying which additional credentials the *architect* role typically holds that the analyst does not yet have (chapter 09's cross-role discipline). This is not a claim the analyst pursues these credentials at analyst tier; it is preparation for the promotion conversation.

## Deliverables

- `mod-110-ex-04-portfolio-plan.md` — the five-section plan plus §Appendix A.
- Optional stretch files named per the stretch-goals list.

## Notes on evaluation

The paired solutions repo works one reference portfolio plan for one archetypal analyst profile (typically the standards-and-assurance sequence targeting `senior-ai-governance-architect` promotion). The load-bearing calls your draft is expected to match: (a) all five sections plus §Appendix A present; (b) §1 covers the six analyst-profile items honestly; (c) §2 identifies specific AIGP-body-of-knowledge gaps rather than claiming across-the-board fluency; (d) §3 sequences AIGP first (or notes already-held), stays within three credentials over three years, and does not include peer-role credentials; (e) §4 pairs each credential with a distinct-from-business-as-usual practice; (f) §5 prepares the manager conversation with the ask, rationale, return-on-effort, alternative, and follow-through commitment; (g) §Appendix A names peer-role credentials the analyst is not pursuing. The narrower calls — the specific credential chosen in year 2, the specific practice pairing in §4, the specific cost and effort estimates — will differ per your §1 profile. What should not differ is the *AIGP first, depth extensions second, peer-role credentials never* logic and the honest gap analysis in §2. A tight three-year plan that the analyst can actually take into a manager conversation beats a longer five-year plan that reads as aspirational.
