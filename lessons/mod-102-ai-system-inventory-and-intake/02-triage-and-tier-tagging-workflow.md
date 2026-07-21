# Intake Triage — In-Scope / Out-of-Scope / Needs-Follow-Up

## Why this chapter

Not every intake is real. Not every intake is even an AI system. Some are one-off spreadsheets that a product manager has re-labelled as "AI" because that is where budget lives this quarter. Some are third-party tools already procured under a different track. Some are experimental notebooks that will never leave a data scientist's laptop.

Triage is how the analyst decides, within an hour or two of receiving an intake, which bucket it falls into: **in-scope** (goes into full risk-and-impact assessment), **out-of-scope** (does not enter the AI governance program — with a documented reason), or **needs follow-up** (missing information; routed back with specific questions).

The three-bucket triage output is the analyst's most visible daily deliverable. Getting the triage right is what keeps the program's capacity trained on the systems that actually deserve it.

## The three buckets

### In-scope

The intake describes a system the enterprise's AI definition covers, in a jurisdiction the program operates in, at a stage of development where governance work is useful (i.e., before production launch or, for existing systems, at a material change). It advances to a first-draft risk assessment (`mod-103`), an impact assessment (`mod-105`), and the inventory row (chapter 03 of this module).

### Out-of-scope

The intake describes something that is not in the program's scope. The analyst records the reason and closes the intake with a routing note. Common reasons:

- **Not AI under the enterprise definition.** A deterministic rules engine that the requester called "AI" is not in scope for a program that scopes to ML / statistical learning / generative AI. Document the exclusion, cite the enterprise's definition, and point the requester at the correct governance track (typically application security, data governance, or engineering change management).
- **Already covered by another program.** A third-party analytics tool acquired through procurement two years ago and running in production. Route the record to the vendor-review track rather than re-running intake.
- **Research / exploration only.** A notebook that will never leave the researcher's laptop and has no production intent within the next six months. Note the exclusion; commit to re-review if scope changes.
- **Duplicate.** Another intake for the same system already exists. Merge with the existing record.

Out-of-scope is not a rejection — it is a routing decision. The analyst records *what the ask was, why it is out of scope, and where it went instead*.

### Needs follow-up

The intake is real but under-specified. Common shapes:

- **Business owner unnamed or a mailbox rather than a person.** Return with "please name an accountable individual — we cannot complete an assessment without one".
- **Purpose statement is a paragraph of vendor marketing.** Return with two or three concrete questions ("what decision does this system inform / take", "who is the user population").
- **Personal data question answered 'no' but the system reads customer records.** Return with a privacy-team joint follow-up.
- **Automated-decision-making about individuals answered 'no' but the deployment surface is external customer-facing.** Return with a joint follow-up — this often unblocks either a re-answer or a legitimate high-risk tag.

Needs-follow-up intakes get a target SLA (typically three to five business days) after which the analyst chases the requester. Follow-up work is analyst-owned; the requester should never feel abandoned.

## The tier-tag overlay

Once an intake is *in-scope*, the analyst adds the tier tag. The tier tag is the single most consequential downstream signal — it drives which impact assessment template is used, which reviewers are looped in, and which controls apply.

The default tier scheme in most large-enterprise programs is a combination of the EU AI Act tier (four tiers plus GPAI overlay — see mod-101 chapter 04) *and* an enterprise-internal tier that adds one or two rungs above "high-risk" for systems the enterprise considers extra-sensitive regardless of what EU AI Act says.

### The EU AI Act tier — the primary hook

Walk the [EU AI Act (Regulation (EU) 2024/1689)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) decision tree from mod-101:

1. Article 5 prohibited practice? → **Unacceptable — block and escalate.**
2. Annex I safety-component route (medical device, machinery, in-vitro diagnostic, etc. with third-party conformity)? → **High-risk (Annex I).**
3. Annex III use-case route (biometrics, critical infrastructure, education, employment, essential services, law enforcement, migration and border, justice and democratic processes)? → **High-risk (Annex III).**
4. Interacts with people / generates synthetic content / does emotion or biometric categorisation / produces deep-fakes? → **Limited-risk (Article 50 transparency).**
5. None of the above? → **Minimal risk.**

Any borderline call — Article 6(3) derogation, "does this really count as biometric categorisation", ambiguity between limited and high-risk — is a **needs-follow-up** with a legal-team ping. The analyst never invokes a derogation solo.

### The enterprise internal tier — the enterprise's own overlay

Most large enterprises publish an internal tier scheme with one or two extra rungs. Typical shapes:

- **Critical.** Systems whose failure would produce a regulator-reportable incident, a safety event, or a headline-grade brand event. Almost always maps to EU AI Act high-risk *plus* additional enterprise scrutiny (e.g., mandatory board-track review).
- **High.** Systems affecting individuals' access to services, employment, credit, or legal rights, or handling regulated data. Maps roughly to EU AI Act high-risk.
- **Medium.** Systems with material operational or reputational exposure but no direct individual-rights impact. Often maps to EU AI Act limited-risk plus a sector overlay.
- **Low.** Internal productivity tools with narrow blast radius.

The two tier schemes are not mutually exclusive — the intake row carries both, and downstream artefacts trace to whichever applies (the impact assessment traces to EU AI Act; the internal review cadence traces to the enterprise tier).

## Triage decision heuristics

Some patterns are worth internalising because they surface at almost every intake.

- **When in doubt on personal data, treat it as "yes".** A follow-up to confirm is cheap. Missing a DPIA trigger is expensive.
- **External customer-facing + generative AI defaults to Article 50 transparency at minimum.** Even if it does not hit Annex III, someone will need to update UX copy to disclose the AI. Note it in the triage.
- **Any system that touches employment, hiring, credit, insurance, education, or public benefits gets a high-risk suspicion by default, and the analyst has to argue *out* of that.** These are the Annex III core areas.
- **Any hosted foundation model brings Value Chain and Component Integration (GenAI Profile risk #12) with it by default.** The triage note flags the vendor as needing third-party review even if the tier tag is limited or minimal.

## The triage decision log — what the analyst records

Whatever the decision, the analyst records:

- **Decision:** in-scope / out-of-scope / needs-follow-up.
- **Reason:** in one paragraph, cite the enterprise definition, the Article, the Annex, or the missing field.
- **Tier tag** (if in-scope): EU AI Act tier + enterprise tier + one-line rationale for each.
- **Routing:** who owns the next step; when the SLA fires.
- **Assumptions:** anything the analyst inferred that the requester did not confirm — flagged so the risk assessment can re-check.

This is a **register-visible artefact**. If a triage decision is challenged three months later, this is what the analyst points to.

## Concrete example — three intakes on a Monday morning

**Intake A: an internal HR team wants to trial a hosted "AI résumé screener".** The purpose statement is honest: rank inbound résumés against a job description to save recruiter time.
- Bucket: **in-scope.**
- EU AI Act tier: **High-risk, Annex III item 4 (employment / recruitment).**
- Enterprise tier: **High.**
- Routing: full risk assessment; FRIA drafted per EU AI Act Article 27 (if the enterprise falls under a deployer obligation — verify with legal); NYC LL 144 bias-audit overlay if any hiring happens for NYC-based roles; EEOC Title VII overlay for the US.

**Intake B: a data engineer requests governance review of a nightly cron that computes a rolling-average dashboard metric.** No ML, no learned parameters, no generative AI — just SQL.
- Bucket: **out-of-scope.**
- Reason: does not meet the enterprise's AI definition (deterministic aggregate, no learned model).
- Routing: closed with note; the requester is pointed at the analytics-engineering change-management process.

**Intake C: a product manager asks about "using AI to help our customer support team", with no purpose statement, no business owner, and no deployment surface named.**
- Bucket: **needs-follow-up.**
- Reason: purpose statement missing, business owner unnamed, deployment surface not specified. The analyst returns the intake with three specific questions and an SLA of three business days.

The Monday-morning triage note captures all three, and by lunchtime the analyst has cleared them.

## What to memorise

- The **three buckets**: in-scope / out-of-scope / needs-follow-up.
- The **five-step EU AI Act decision tree** (Article 5 → Annex I → Annex III → Article 50 → residual).
- The two-scheme structure: **EU AI Act tier + enterprise internal tier**, both carried on the intake row.
- The **default suspicions**: personal-data-yes when unsure; external-generative-AI defaults to Article 50 at minimum; employment / hiring / credit / education / benefits defaults to high-risk suspicion.
- The triage note fields: decision, reason, tier tag, routing, assumptions.

## Summary

Triage is where the analyst decides which intakes deserve the program's capacity. The three buckets — in-scope, out-of-scope, needs-follow-up — each get a documented reason; in-scope intakes carry both an EU AI Act tier and an enterprise-internal tier. Borderline calls, derogations, and legal ambiguity all route out to counsel or a senior architect rather than being resolved silently at the analyst desk. The triage note is a first-class governance record and the audit-facing answer to "why did this system get the review it got?"
