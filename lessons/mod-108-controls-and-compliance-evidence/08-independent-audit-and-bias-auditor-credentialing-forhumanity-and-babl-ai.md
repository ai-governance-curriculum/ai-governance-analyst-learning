# Independent-Audit and Bias-Auditor Credentialing — ForHumanity and BABL AI

## Why this chapter

The vendor-intake row (chapter 06) and the crosswalk (chapter 07) both cite *independent audit reports* as an evidence class. The analyst's tagging convention (chapters 04–05) routes security-linked findings; the analyst's report language (chapter 03) distinguishes *the analyst supplies the row* from *internal audit issues the opinion*. Sitting behind all of that is a market of *external, credentialed AI auditors* — practitioners and firms whose engagements produce the independent audit reports the analyst reads, the bias-audit certificates the analyst references, and the certification-scheme documentation the analyst tracks.

Two credentialing / audit bodies come up most often in the analyst's inbox: [ForHumanity](https://forhumanity.center/) and [BABL AI](https://babl.ai/). This chapter positions each — what they are, what shape of work they produce, how their outputs read into the analyst's row set — and states the through-line where they most often intersect the enterprise's operations: [New York City Local Law 144](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page) bias-audit obligations, and the wave of AI-audit obligations that has followed.

The chapter is deliberately narrow. It does not attempt an inventory of every AI-audit firm, credential, or standards body — the market moves too fast for that inventory to remain accurate. It positions the two the analyst is *most likely* to see cited on a vendor's trust site or a customer's questionnaire, and gives the analyst the vocabulary to read what they produce without over-interpreting it.

## The independent-audit landscape at a glance

Independent audits in the AI space fall into four rough shapes; ForHumanity and BABL AI operate primarily in the last two.

- **Management-system certification.** An accredited certification body (a firm like BSI, DNV, TÜV, LRQA, DEKRA, Bureau Veritas, or a national equivalent) certifies the enterprise's management system against a standard such as ISO/IEC 42001. The certifying body must itself be accredited by a national accreditation body signatory to the [IAF Multilateral Recognition Arrangement](https://iaf.nu/en/iaf-mla/). The output is a *certificate*, granted for a defined scope and period, with surveillance audits at intervals.
- **Assurance engagement.** A public-accounting firm (Big Four and equivalents; specialist firms) performs an attestation engagement — typically a [SOC 2 examination](https://us.aicpa.org/interestareas/frc/assuranceadvisoryservices/aicpasoc2report) under [AICPA SSAE 18](https://us.aicpa.org/research/standards/auditattest/ssae) in the US, an [ISAE 3000 engagement](https://www.iaasb.org/publications/international-standard-assurance-engagements-isae-3000-revised-assurance-engagements-other-audits-or) internationally — against a set of criteria. Growing use of AI-specific criteria in this space; the AICPA has published resources supporting SOC-for-AI approaches, and equivalents exist internationally.
- **Independent audit of algorithmic systems.** Non-management-system, non-accounting-firm audits — engagements by AI-specific auditors examining a system against a framework of AI-specific criteria (bias, transparency, accountability, robustness, privacy, safety). ForHumanity's [Independent Audit of AI Systems (IAAIS)](https://forhumanity.center/independent-audit-of-ai-systems/) sits here.
- **Bias audit.** A narrower engagement — often statutorily driven — examining the discriminatory impact of an AI system on protected classes. NYC Local Law 144's *bias audit* requirement is the most-cited instance; the state of Colorado's [Artificial Intelligence Act (SB24-205)](https://leg.colorado.gov/bills/sb24-205) and other jurisdictions are creating analogous obligations.

The analyst reads across all four shapes. Chapter 06's row schema records the independent-audit artefact regardless of shape; this chapter narrows to the two bodies most likely to be behind an AI-specific audit or bias-audit output.

## ForHumanity

[ForHumanity](https://forhumanity.center/) is a US-registered public charity focused on AI, algorithmic, and autonomous-system risk. It maintains a set of publicly available *audit criteria* — the "*[ForHumanity Body of Knowledge](https://forhumanity.center/body-of-knowledge/)*" — which is developed and reviewed by an open community of contributors and organised into audit schemes for specific regulations and standards.

### What ForHumanity produces

- **Audit criteria.** Openly published criteria decks against which independent audits can be performed. Coverage includes the EU AI Act, GDPR, NYC Local Law 144, the [UK ICO's AI-and-data-protection auditing framework](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/artificial-intelligence/), children's privacy, and other jurisdictional AI obligations.
- **The Independent Audit of AI Systems (IAAIS) methodology.** A framework for conducting independent audits against the criteria decks, with defined roles (auditor, quality reviewer, oversight committee) and defined deliverables (audit report, exceptions register, management response).
- **Auditor credentialing.** A tiered credentialing programme — training programmes and examinations that qualify individuals to audit against specific ForHumanity schemes. Named credentials (as public content indicates) include specialist tracks per scheme; the credential set has evolved over time, and the analyst confirms the current credentialing structure on the ForHumanity site before referencing it in an audit-facing artefact.

<!-- needs-research: ForHumanity's specific credential names, training pathways, and current audit-scheme coverage should be verified against https://forhumanity.center/ before an audit-facing citation. The programme has evolved substantially since its inception and the terminology on the ForHumanity site is authoritative. -->

### How ForHumanity-linked work reads onto the analyst's row set

- **On the vendor row (chapter 06 §"Independent audit report").** A vendor whose independent-audit engagement was performed against a ForHumanity audit criteria set, by an auditor holding the corresponding ForHumanity credential, produces a report the analyst records with the auditor, the credential(s), the criteria set (with version), the scope, the period, the opinion, and the exceptions.
- **On the crosswalk (chapter 07 optional column for voluntary framework anchors).** Where the enterprise voluntarily aligns to a ForHumanity audit criteria set, the crosswalk carries a column pointing controls at the specific criteria the enterprise commits to.
- **On the escalation register.** Where a ForHumanity-linked audit report cites an exception, the analyst adds it as a *known-exception* row in the escalation register with the auditor's classification and the enterprise-side remediation status.

### What ForHumanity is *not*

- **Not an accreditation body under the IAF.** ForHumanity's credentialing is programme-specific, not IAF-recognised in the same sense that a national accreditation body accredits certification bodies for ISO management-system certification. This does not diminish the value of a ForHumanity-linked audit report; it changes what the report can be substituted for. A ForHumanity audit is not a substitute for an ISO/IEC 42001 certification from an IAF-accredited body.
- **Not a certification body.** ForHumanity provides the criteria and the methodology; the audits are conducted by third-party auditors holding the credentials. The analyst records both — the criteria origin *and* the auditor's identity and credential.

## BABL AI

[BABL AI](https://babl.ai/) is a US-based AI consultancy and training organisation whose work covers algorithmic auditing, AI risk assessment, and practitioner training. It positions itself in both the *services* market (performing algorithmic audits for enterprise clients) and the *training* market (courses and certification programmes for individual practitioners).

### What BABL AI produces

- **Algorithmic-audit services.** Engagements examining AI systems against a set of criteria — often bias-focused, but extending to broader responsible-AI dimensions. BABL AI has been publicly associated with algorithmic-audit work in employment contexts (including NYC Local Law 144 bias audits) and other regulated domains.
- **Training and credentialing programmes.** Courses covering algorithmic auditing, AI risk assessment, AI ethics, and AI governance, with completion credentials. Course structure and credential names have evolved as the market has matured; the analyst references the current BABL AI course catalogue rather than a memorised list.

<!-- needs-research: BABL AI's specific service offerings, training courses, and credential names should be verified against https://babl.ai/ before an audit-facing citation. The market moves quickly. -->

### How BABL-linked work reads onto the analyst's row set

- **On the vendor row.** A vendor whose bias audit or algorithmic audit was performed by BABL AI (or by a practitioner trained through BABL AI) produces a report the analyst records with the same fields as any independent-audit report — auditor identity, credentials, criteria, scope, period, opinion, exceptions.
- **On the internal-side bias-audit control.** Where the enterprise runs its own bias audits under a statutory obligation (NYC Local Law 144 being the paradigmatic case), and engages BABL AI or a BABL-trained practitioner, the resulting audit is an *enterprise-produced* artefact — evidence for a control in the master library and a row in the eval-evidence set from `mod-107` — and also a *statutory disclosure* under the local law.

### What BABL AI is *not*

- **Not a credentialing body in the IAF sense.** Same distinction as ForHumanity — training-and-certification is programme-specific, not IAF-recognised.
- **Not a substitute for the enterprise's own analysis.** A BABL-conducted audit is an *input* to the enterprise's decision-making; the enterprise still records the audit report, sets the residual-risk decision, and integrates the finding into the control cycle. The auditor's report is not the analyst's report.

## The NYC Local Law 144 through-line

[New York City Local Law 144 of 2021](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page) requires that employers and employment agencies using an *automated employment decision tool* (AEDT) in the hiring or promotion of NYC-based candidates conduct a *bias audit* by an *independent auditor* within one year of use, publish a summary of the audit results on the employer's website, and provide specified notices to candidates.

Both ForHumanity and BABL AI are visible in the ecosystem that grew up around Local Law 144's audit obligation — ForHumanity through its audit criteria and credentialing programme, BABL AI through direct audit services and practitioner training. For the analyst, this is where the two most commonly cross the enterprise's inbox: an enterprise using an AEDT (whether built or bought) has to source a *bias audit* from an *independent auditor*, and the two names show up as candidates when the enterprise builds a shortlist.

The through-line for the analyst's row and report set:

- **On the `mod-102` inventory row.** An AEDT in scope for NYC hiring is a system whose intake triggers a *Local Law 144 applies* obligation; `mod-106` regulatory-tracker holds the `REG-<year>-<sequence>` row for the obligation.
- **On the master control library (`senior-ai-governance-architect` scope).** A control exists — "*For every AEDT used in NYC hiring, an independent bias audit is conducted within the past twelve months and the audit summary is published on the employer's website*" — with an evidence class of *sign-off record + independent audit report link* and an on-event cadence.
- **On the control-status report (chapter 03).** The test row records the audit report identifier, the auditor, the date, and the publication URL.
- **On the vendor row (chapter 06).** Where the AEDT is provided by a vendor, the vendor row records the vendor's own bias-audit posture and whether the enterprise inherits or supplements.
- **On the crosswalk (chapter 07).** The internal control maps to the external obligation (`REG-<year>-<sequence>` from `mod-106`) and to the internal-policy anchor.

Local Law 144 is the paradigmatic case; the pattern generalises to the [Colorado AI Act](https://leg.colorado.gov/bills/sb24-205) and to other jurisdictional AI-audit obligations as they land. The analyst's row shape is the same; the `mod-106` tracker holds the jurisdiction-specific obligation set.

## What the analyst records when reading a ForHumanity- or BABL-linked artefact

The analyst treats a ForHumanity- or BABL-linked audit report the same way as any other independent audit report — with the caveat that the *criteria origin* and the *auditor credentialing* are distinct fields on the row that the analyst does not conflate.

- **Auditor identity.** Individual or firm; contact identity for follow-up.
- **Auditor credentialing / accreditation.** ForHumanity-programme credential name(s); BABL-programme credential name(s); any other credentialing the auditor holds (CIPP, CISA, ISO/IEC 27001 lead-auditor, etc.).
- **Criteria origin.** ForHumanity criteria set (with version), BABL-defined criteria set (with version), enterprise-defined criteria set, statutory criteria (e.g., the Local Law 144 required audit shape as codified by the [NYC Department of Consumer and Worker Protection](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page)).
- **Scope statement.** What was audited — system, deployment context, period.
- **Opinion.** Unqualified, qualified, adverse, disclaimed, or the criteria-set-defined equivalent.
- **Exceptions register.** What the auditor identified and did not close within the engagement.
- **Management response.** The enterprise's (or the vendor's) documented response to exceptions.

The row schema in chapter 06 has fields for each. The analyst populates them all; leaving fields blank is what leads a downstream reader to conflate credentials, criteria, and opinion.

## What the analyst does not do

- **The analyst does not audit.** Even where the analyst holds a ForHumanity or BABL credential personally, the analyst-tier role does not perform independent audits *on the enterprise's own systems* — the independence requirement is not compatible with the analyst's day-to-day control-cycle work. The analyst can *support* audits (supplying documentation, walking auditors through the artefact set) but does not sign as auditor on the enterprise's own systems.
- **The analyst does not commission the audit.** Commissioning an independent audit is `head-of-ai-governance` or `senior-ai-governance-architect` scope, typically with `procurement` handling the engagement contract. The analyst helps scope; the analyst does not sign the engagement letter.
- **The analyst does not opine on auditor selection.** A shortlist of auditors is an ecosystem decision the enterprise makes with `legal`, `procurement`, and the accountable executive. The analyst may note the credential ecosystem (ForHumanity, BABL AI, others) as background; the analyst does not recommend a specific auditor without a broader review.
- **The analyst does not treat a credential as a substitute for the audit report itself.** The credential says the auditor was trained to a defined standard; the report says what the auditor found. The analyst records both.

## Common failure modes

- **Conflating criteria with credential.** Recording *audit against ForHumanity criteria* as the credential, or recording *audit by a BABL-trained auditor* as the criteria. Fix: two fields on the row, populated distinctly.
- **Treating a ForHumanity-linked audit as equivalent to an ISO/IEC 42001 certification.** Different mechanism; different scope; different accreditation. Fix: chapter 06 columns 12 (certification) and 14 (independent audit) are distinct fields; use both.
- **Missing the publication step on Local Law 144 bias audits.** The obligation includes *publish a summary on the employer's website*, not just *conduct the audit*. Fix: the control test records the *published summary URL* in addition to the audit report.
- **Stale credential references.** ForHumanity and BABL AI evolve their credential offerings; a reference to a credential that no longer exists ages badly. Fix: `<!-- needs-research: verify credential name against the body's current site -->` on every specific credential reference in the analyst-facing artefacts.

## What to memorise

- **ForHumanity and BABL AI are the two most-cited AI-audit-adjacent bodies the analyst encounters.** ForHumanity publishes audit criteria and runs an auditor credentialing programme; BABL AI provides audit services and runs training and certification programmes.
- **Neither is a management-system certification body.** ISO/IEC 42001 certification comes from an IAF-accredited certification body; ForHumanity- and BABL-linked audits are a different (and distinct) evidence class.
- **The through-line where they most often cross the analyst's inbox is NYC Local Law 144.** The bias-audit obligation drives shortlist activity where both names commonly appear.
- **Record criteria origin and auditor credentialing as distinct fields.** Conflating them misleads downstream readers.
- **The analyst does not audit the enterprise's own systems.** Even with a credential, the independence requirement is incompatible with the role.

## Summary

Independent audits are one of the evidence-artefact classes chapter 06 records on the vendor-risk-register row, and one of the artefacts internal audit and external stakeholders most often ask the analyst to walk through. Among the growing set of AI-audit-adjacent bodies, ForHumanity and BABL AI are the two the analyst is most likely to see referenced — ForHumanity through its openly published audit criteria decks, its IAAIS methodology, and its auditor credentialing programme; BABL AI through algorithmic-audit services and practitioner training. Neither replaces an IAF-accredited ISO/IEC 42001 certification; both provide distinct, useful evidence when read into the row with criteria origin and auditor credentialing recorded as separate fields. NYC Local Law 144's bias-audit obligation is the through-line where these bodies most often cross the analyst's inbox; the pattern generalises to the wave of AI-audit obligations following it. Chapter 09 closes the module by stating the full delegation boundary and the escalation classes the analyst uses across all preceding chapters.
