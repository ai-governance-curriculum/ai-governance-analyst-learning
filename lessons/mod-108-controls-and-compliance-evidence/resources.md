# Resources — mod-108 Controls, Compliance Evidence, and Third-Party AI Vendor Review

Primary references for every control class, evidence-artefact class, threat-taxonomy reference, vendor-intake artefact, crosswalk framework, and independent-audit / bias-auditor body this module walks. Read the primary source (the standard's authoritative text, the regulator's official page, the vendor's own trust portal, the framework's authoring organisation's canonical URL) first; practitioner briefings and law-firm client alerts are useful for *noticing* a change quickly but do not sit in a control-status report row's *source-artefact link* column — the analyst chases the primary reference before writing the row.

## Frameworks and standards this module sits inside

Chapters 01, 03, and 07 orientation references.

- [NIST AI Risk Management Framework 1.0 (NIST AI 100-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf) — the foundational AI RMF; the GOVERN / MAP / MEASURE / MANAGE structure frames the control-cycle vocabulary chapters 02 and 03 use.
- [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) — the RMF Playbook; the sub-category-level actions the crosswalk column B cites directly.
- [NIST AI RMF Generative AI Profile (NIST AI 600-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) — the twelve GenAI risk categories the security-linked control-tagging (chapters 04 and 05) and the crosswalk optional-column (chapter 07) reference.
- [NIST AI Resource Center (AIRC)](https://airc.nist.gov/) — the RMF resource hub; crosswalks, playbook updates, and Generative AI Profile companion material land here.
- [NIST AI 100-2e2025 — Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations](https://csrc.nist.gov/pubs/ai/100/2/e2025/final) — NIST's normative reference on AML attack classification; the four families (evasion, poisoning, privacy, abuse) chapter 05 anchors on. Cite the edition.
- [ISO/IEC 42001:2023 — Information technology — Artificial intelligence — Management system](https://www.iso.org/standard/81230.html) — the AI management-system standard chapters 06 and 07 anchor on. Clauses 4–10 are the body; Annex A is the AI-specific control set (paywalled; verify identifiers against a licensed copy).
- [ISO/IEC 23894:2023 — Information technology — Artificial intelligence — Guidance on risk management](https://www.iso.org/standard/77304.html) — AI risk-management guidance; complements the AI RMF and, as an optional column, complements the analyst crosswalk.
- [ISO/IEC 42005:2025 — Information technology — Artificial intelligence — AI system impact assessment](https://www.iso.org/standard/44545.html) — the ISO AI-system impact-assessment standard cited from `mod-105` and referenced when the vendor-intake row from chapter 06 needs to name the enterprise's impact-assessment posture on inherited artefacts.
- [ISO/IEC JTC 1/SC 42 (Artificial Intelligence)](https://www.iso.org/committee/6794475.html) — the SC 42 committee page; work items on AI evaluation, testing, assurance, and controls in development.
- [ISO/IEC 27001:2022 — Information security management systems — Requirements](https://www.iso.org/standard/27001) — the information-security management-system standard the analyst records as an *adjacent attestation* on vendor rows.
- [ISO/IEC 27701:2019 — Extension to ISO/IEC 27001 and ISO/IEC 27002 for privacy information management](https://www.iso.org/standard/71670.html) — the privacy information management extension; another common adjacent attestation on vendor rows.
- [AICPA SOC 2 — System and Organization Controls 2](https://us.aicpa.org/interestareas/frc/assuranceadvisoryservices/aicpasoc2report) — the US audit-firm-issued security / availability / processing-integrity / confidentiality / privacy attestation the analyst records for hosted-service vendors.
- [AICPA SSAE 18 (Statements on Standards for Attestation Engagements No. 18)](https://us.aicpa.org/research/standards/auditattest/ssae) — the standard SOC 2 examinations are conducted under.
- [IAASB ISAE 3000 (International Standard on Assurance Engagements 3000)](https://www.iaasb.org/publications/international-standard-assurance-engagements-isae-3000-revised-assurance-engagements-other-audits-or) — the international attestation-engagement standard; SOC 2's non-US equivalent shape.
- [International Accreditation Forum (IAF)](https://iaf.nu/) — the international accreditation body whose Multilateral Recognition Arrangement (MLA) member accreditation bodies attest certification bodies. Chapter 06 was explicit that ISO/IEC 42001 certification claims must trace to an IAF-accredited certifying body.
- [IAF Members](https://iaf.nu/en/iaf-members/) — the member list; how the analyst verifies a claimed accreditation is real.

## Control-testing cycle and evidence-artefact discipline — chapters 02, 03

Practitioner references on the mechanics of control operation.

- [ISACA — IT Audit Framework (ITAF)](https://www.isaca.org/resources/itaf) — the audit-framework reference many enterprise internal-audit functions use; the audit-side vocabulary the control-status report's readers bring with them.
- [ISACA COBIT 2019 framework](https://www.isaca.org/resources/cobit) — the enterprise-governance-of-IT framework whose control-classification vocabulary many GRC platforms adopt.
- [The Open Group — Open FAIR (Factor Analysis of Information Risk) body of knowledge](https://www.opengroup.org/open-fair) — a risk-quantification reference the enterprise's residual-risk paragraphs (chapter 06 column 17) may adopt.
- [OECD.AI Policy Observatory — AI Incidents Monitor](https://oecd.ai/en/incidents) — the incident monitor the analyst references when a control-status finding needs cross-industry context.
- [MLCommons AILuminate benchmark and Safety Working Group](https://mlcommons.org/working-groups/ai-safety/ai-safety/) — the MLCommons AI Safety benchmark suite; a shared reference for safety-eval categories that eval-cadence control tests cite.

## GRC platforms the analyst runs the cycle in

The GRC-platform landscape. `mod-102` chapter 04 walked the AI-inventory-in-GRC discipline; this module adds the control-testing-in-GRC layer. No endorsement implied; the enterprise uses whichever tool is licensed.

- [OneTrust](https://www.onetrust.com/) — a widely adopted privacy and GRC platform with AI-governance modules.
- [Vanta](https://www.vanta.com/) — a compliance-automation platform popular with growth-stage enterprises.
- [Drata](https://drata.com/) — a compliance-automation platform.
- [RSA Archer](https://www.archerirm.com/) — a long-standing enterprise GRC platform.
- [ServiceNow GRC](https://www.servicenow.com/products/governance-risk-and-compliance.html) — the ServiceNow GRC surface.
- [MetricStream](https://www.metricstream.com/) — an enterprise GRC platform.
- [LogicGate](https://www.logicgate.com/) — a risk-cloud GRC platform.
- [Diligent (formerly Galvanize / HighBond)](https://www.diligent.com/) — an audit / GRC platform.
- [Whistic](https://www.whistic.com/) — a vendor-security trust-portal / questionnaire-exchange platform.
- [SecurityScorecard](https://securityscorecard.com/) — a third-party-risk platform with attack-surface scoring.
- [BitSight](https://www.bitsight.com/) — a third-party-risk rating platform.

## OWASP LLM Top 10 — chapter 04

The primary LLM-application threat catalogue.

- [OWASP Top 10 for LLM Applications](https://genai.owasp.org/llm-top-10/) — the current canonical list; chapter 04 walks the 2025 edition. Version-cite (`LLM01:2025`) rather than bare (`LLM01`).
- [OWASP GenAI Security Project — hub](https://genai.owasp.org/) — the umbrella OWASP project; publishes the Top 10 plus the AI Security Solutions Landscape and practitioner deep-dive guides.
- [OWASP AI Security & Privacy Guide](https://owasp.org/www-project-ai-security-and-privacy-guide/) — an OWASP guide covering AI-security controls, threats, and privacy considerations.
- [OWASP Foundation](https://owasp.org/) — the parent foundation.
- [OWASP Risk Rating Methodology](https://owasp.org/www-community/OWASP_Risk_Rating_Methodology) — OWASP's severity × likelihood shape, referenced in chapter 04's guidance that severity is `ai-infra-security`'s call, not the analyst's.

## MITRE ATLAS — chapter 05

The AI-system adversarial-tactics-and-techniques knowledge base.

- [MITRE ATLAS](https://atlas.mitre.org/) — the *Adversarial Threat Landscape for Artificial-Intelligence Systems* knowledge base; the analyst carries technique identifiers forward from source artefacts that name them.
- [MITRE ATLAS matrix](https://atlas.mitre.org/matrices/ATLAS) — the tactic-and-technique matrix; ATLAS is a living matrix and the tactic/technique set evolves.
- [MITRE ATLAS case studies](https://atlas.mitre.org/studies) — a growing set of case studies drawn from public incidents and research; how the analyst builds pattern recognition.
- [MITRE ATT&CK](https://attack.mitre.org/) — the parent adversarial-behaviour framework the ATLAS ML-specific overlay sits alongside.
- [MITRE — AI Assurance program](https://www.mitre.org/focus-areas/artificial-intelligence) — MITRE's AI-assurance work; source of AI-security and red-team methodology beyond ATLAS.
- [MITRE Sensible Regulatory Framework for AI Security](https://www.mitre.org/news-insights/publication/sensible-regulatory-framework-ai-security) — MITRE's regulatory framing on AI security.

## Google Secure AI Framework (SAIF) — chapter 05

The defender-oriented programme framework the control library anchors against.

- [Google Secure AI Framework (SAIF)](https://safety.google/cybersecurity-advancements/saif/) — the SAIF hub; the six defence-programme elements chapter 05 anchors on.
- [Google — SAIF risk assessment](https://saif.google/) — an interactive assessment surface for practitioners.
- [Coalition for Secure AI (CoSAI)](https://www.coalitionforsecureai.org/) — the industry-and-community coalition Google, IBM, Anthropic, OpenAI, Microsoft and others formed around AI-security practice; SAIF-adjacent content lands here.

## Adjacent AI-security references

Threat catalogues and defensive references beyond the four chapter 05 walks.

- [ENISA — Multilayer Framework for Good Cybersecurity Practices for AI](https://www.enisa.europa.eu/publications/multilayer-framework-for-good-cybersecurity-practices-for-ai) — ENISA's AI-cybersecurity framework; the EU-side counterpart to SAIF-family references.
- [ENISA — Cybersecurity of AI and Standardisation](https://www.enisa.europa.eu/publications/cybersecurity-of-ai-and-standardisation) — ENISA's mapping of the AI-cybersecurity standards landscape.
- [UK NCSC — Guidelines for secure AI system development](https://www.ncsc.gov.uk/collection/guidelines-secure-ai-system-development) — the UK NCSC guidelines, co-published with CISA and multiple national agencies.
- [US CISA — AI at CISA](https://www.cisa.gov/ai) — CISA's AI-security guidance hub.
- [Microsoft — Failure Modes in Machine Learning](https://learn.microsoft.com/en-us/security/engineering/failure-modes-in-machine-learning) — Microsoft's taxonomy of intentional and unintentional ML failure modes; a widely cited practitioner reference.
- [MLSecOps community](https://mlsecops.com/) — the MLSecOps community hub.
- [`leondz/garak` on GitHub](https://github.com/leondz/garak) and [`nvidia/garak` — NVIDIA-maintained fork](https://github.com/NVIDIA/garak) — an open-source LLM vulnerability scanner useful for automating parts of a security-linked control test.

## EU AI Act and EU regulatory infrastructure — chapters 03, 07

The EU AI Act and the AI Office instruments the crosswalk column C cites.

- [Regulation (EU) 2024/1689 — the EU Artificial Intelligence Act (consolidated text on EUR-Lex)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the AI Act.
- [European Commission — Regulatory framework proposal on artificial intelligence](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai) — the Commission's AI-Act hub; the phased-entry-into-application timeline.
- [European Commission — European AI Office](https://digital-strategy.ec.europa.eu/en/policies/ai-office) — the AI Office; the enforcement and template-publishing body for the EU AI Act.
- [EU AI Office — Code of Practice hub](https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice) — the general-purpose AI Code of Practice hub.
- [EU AI Office — Final General-Purpose AI Code of Practice (July 2025)](https://digital-strategy.ec.europa.eu/en/library/final-general-purpose-ai-code-practice) — the final GPAI Code of Practice.
- [EU AI Act — Article 26 deployer obligations (via EUR-Lex)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the deployer-side obligation cluster the crosswalk cites when the enterprise is a deployer of a high-risk system.
- [European Data Protection Board (EDPB) — Guidance on personal data processing and AI](https://edpb.europa.eu/) — the EDPB hub; guidance on personal-data-processing obligations layered onto AI systems the analyst records on vendor rows (column 11).
- [European Commission — EU-U.S. Data Privacy Framework](https://commission.europa.eu/law/law-topic/data-protection/international-dimension-data-protection/eu-us-data-transfers_en) — the transfer mechanism the analyst records on the vendor DPA column.
- [EDPB — Standard Contractual Clauses (SCCs)](https://commission.europa.eu/law/law-topic/data-protection/international-dimension-data-protection/standard-contractual-clauses-scc_en) — the DPA transfer-mechanism reference.

## SR 11-7 and financial-services model-risk-management supervisory guidance — chapter 07

The SR 11-7 pillars column and adjacent financial-services supervisory guidance.

- [Board of Governors of the Federal Reserve System — SR Letter 11-7 (Guidance on Model Risk Management)](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) — the US supervisory guidance; three pillars (development, validation, governance).
- [OCC Bulletin 2011-12](https://www.occ.treas.gov/news-issuances/bulletins/2011/bulletin-2011-12.html) — the OCC parallel guidance.
- [FDIC — Adoption of Supervisory Guidance on Model Risk Management](https://www.fdic.gov/news/financial-institution-letters/2017/fil17022.html) — the FDIC adoption.
- [ECB — Guide to internal models (2019)](https://www.bankingsupervision.europa.eu/legalframework/publiccons/pdf/internal_models_guide/ssm.guidetointernalmodels_consolidated_201910.en.pdf) — the ECB internal-models guide.
- [PRA Supervisory Statement SS1/23 — Model risk management principles for banks](https://www.bankofengland.co.uk/prudential-regulation/publication/2023/may/model-risk-management-principles-for-banks-ss) — the UK PRA supervisory statement.
- [MAS — Consultation Paper on Model Risk Management](https://www.mas.gov.sg/) — MAS's model-risk-management materials.

## Sector-specific overlays the crosswalk optional columns cite — chapter 07

Sector references the crosswalk uses as optional columns.

- **Healthcare.**
    - [US FDA — Good Machine Learning Practice for Medical Device Development: Guiding Principles](https://www.fda.gov/medical-devices/software-medical-device-samd/good-machine-learning-practice-medical-device-development-guiding-principles) — the joint FDA / Health Canada / MHRA guiding principles.
    - [US FDA — Artificial Intelligence and Machine Learning in Software as a Medical Device](https://www.fda.gov/medical-devices/software-medical-device-samd/artificial-intelligence-and-machine-learning-software-medical-device) — the FDA AI/ML-SaMD hub.
    - [HHS Office for Civil Rights — HIPAA](https://www.hhs.gov/hipaa/index.html) — the HIPAA hub.
- **Hiring / employment.**
    - [NYC Department of Consumer and Worker Protection — Automated Employment Decision Tools (Local Law 144)](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page) — the Local Law 144 hub.
    - [US EEOC — Artificial Intelligence and Algorithmic Fairness Initiative](https://www.eeoc.gov/ai) — EEOC AI-and-employment guidance.
- **Public sector.**
    - [Canadian Directive on Automated Decision-Making](https://www.tbs-sct.canada.ca/pol/doc-eng.aspx?id=32592) — the Canadian federal directive.
    - [Canada — Algorithmic Impact Assessment tool](https://open.canada.ca/aia-eia-js/?lang=en) — the tool referenced in the AIA the Directive requires.
    - [UK — Algorithmic Transparency Recording Standard](https://www.gov.uk/government/collections/algorithmic-transparency-recording-standard-hub) — the UK's ATRS.
- **Consumer / state-level US.**
    - [Colorado SB24-205 — Consumer Protections for Artificial Intelligence (Colorado AI Act)](https://leg.colorado.gov/bills/sb24-205) — the Colorado AI Act.
    - [California Consumer Privacy Act (CCPA) and CPRA — CPPA](https://cppa.ca.gov/regulations/) — California privacy regulation the crosswalk cites for consumer-facing AI systems.

## Third-party AI vendor intake — chapter 06

Vendor-side evidence and trust-portal references. Vendor URLs move; the row records both the live URL and a snapshot.

- **Hosted foundation-model providers.**
    - [OpenAI — Trust portal](https://trust.openai.com/) — OpenAI's trust and security surface.
    - [OpenAI — Usage policies](https://openai.com/policies/usage-policies/) — the deployment-constraint reference.
    - [OpenAI — Enterprise privacy](https://openai.com/enterprise-privacy/) — enterprise-tier data-usage terms (no-training-use guarantees).
    - [OpenAI — Business terms](https://openai.com/policies/business-terms/) — the enterprise-facing contract terms.
    - [Anthropic — Trust Center](https://trust.anthropic.com/) — the Anthropic trust-and-security surface.
    - [Anthropic — Usage Policy (AUP)](https://www.anthropic.com/legal/aup) — the acceptable-use policy.
    - [Anthropic — Commercial Terms of Service](https://www.anthropic.com/legal/commercial-terms) — the commercial contract terms.
    - [Anthropic — Sub-processors](https://www.anthropic.com/subprocessors) — the sub-processor list surface.
    - [Google Cloud — Trust Center](https://cloud.google.com/security/compliance/trust-center) — Google Cloud's trust surface.
    - [Google Cloud — Vertex AI generative-AI documentation](https://cloud.google.com/vertex-ai/generative-ai/docs) — the Vertex AI documentation the analyst reads on Gemini-family deployments.
    - [Microsoft — Azure OpenAI Service documentation](https://learn.microsoft.com/en-us/azure/ai-services/openai/) — the Azure OpenAI documentation.
    - [Microsoft — Trust Center](https://www.microsoft.com/en-us/trust-center) — the Microsoft trust-center surface.
    - [Amazon — AWS Trust Center](https://aws.amazon.com/security/) — the AWS trust-center surface.
    - [Amazon — Bedrock foundation-model catalog](https://docs.aws.amazon.com/bedrock/latest/userguide/models-supported.html) — the Bedrock model catalog.
    - [Mistral — Trust Center / documentation](https://docs.mistral.ai/) — Mistral's documentation surface.
    - [Cohere — Trust and security](https://cohere.com/security) — Cohere's trust surface.
    - [IBM — watsonx security and compliance](https://www.ibm.com/watsonx) — IBM's watsonx hub.
- **Self-hosted / open-weights model publishers.**
    - [Meta — Llama models repository](https://github.com/meta-llama/llama-models) — Llama model cards live here.
    - [Meta AI — Acceptable Use Policy](https://llama.meta.com/use-policy/) — the Meta AI AUP.
    - [Meta Llama Community License](https://llama.meta.com/llama-community-license/) — the Llama Community License text.
    - [Mistral — Model overview](https://docs.mistral.ai/getting-started/models/) — Mistral model list.
    - [DeepSeek — Model releases (Hugging Face collection)](https://huggingface.co/deepseek-ai) — DeepSeek releases.
    - [Hugging Face — Model card creation guide](https://huggingface.co/docs/hub/model-cards) — the model-card scaffold Hugging Face applies.
    - [Hugging Face — Security](https://huggingface.co/docs/hub/security) — Hugging Face's security surface.
- **Vendor-questionnaire standards.**
    - [Cloud Security Alliance — Consensus Assessments Initiative Questionnaire (CAIQ)](https://cloudsecurityalliance.org/artifacts/consensus-assessments-initiative-questionnaire-v4/) — the CAIQ.
    - [Shared Assessments — SIG](https://sharedassessments.org/sig/) — the Standardized Information Gathering (SIG) questionnaire.
    - [HITRUST CSF](https://hitrustalliance.net/product-tool/hitrust-csf/) — the HITRUST framework often referenced on healthcare-vendor questionnaires.
    - [EDUCAUSE HECVAT](https://library.educause.edu/topics/cybersecurity/higher-education-community-vendor-assessment-toolkit-hecvat) — HECVAT for higher-education-vendor assessment.
- **Data-protection instruments.**
    - [ICO — Data Processing Agreement (UK guidance)](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/contracts-and-data-sharing/) — the UK ICO guidance.
    - [European Commission — Standard Contractual Clauses (2021 revision)](https://commission.europa.eu/law/law-topic/data-protection/international-dimension-data-protection/standard-contractual-clauses-scc_en) — the 2021 SCCs.

## Independent-audit and bias-auditor bodies — chapter 08

The two credentialing bodies the analyst most often encounters, plus the surrounding assurance-market references.

- [ForHumanity — Homepage](https://forhumanity.center/) — ForHumanity's hub.
- [ForHumanity — Body of Knowledge](https://forhumanity.center/body-of-knowledge/) — the openly published audit criteria decks.
- [ForHumanity — Independent Audit of AI Systems (IAAIS)](https://forhumanity.center/independent-audit-of-ai-systems/) — the audit methodology.
- [ForHumanity — Certified Auditor programme](https://forhumanity.center/certified-auditor/) — the credentialing surface. Verify current credential names against the site.
- [BABL AI — Homepage](https://babl.ai/) — BABL AI's hub.
- [BABL AI — Algorithm Audit services](https://babl.ai/algorithm-audit/) — the services surface.
- [BABL AI — Training courses](https://babl.ai/courses/) — the training-and-certification surface. Verify current course names against the site.
- [ISACA — Certified in the Governance of Enterprise IT (CGEIT)](https://www.isaca.org/credentialing/cgeit) — the ISACA credential the analyst may see on auditor CVs.
- [ISACA — Certified Information Systems Auditor (CISA)](https://www.isaca.org/credentialing/cisa) — the ISACA audit credential.
- [IAPP — Certified Information Privacy Professional (CIPP)](https://iapp.org/certify/cipp/) — the IAPP privacy-professional credential.
- [IEEE — CertifAIEd program](https://engagestandards.ieee.org/ieeecertifaied.html) — IEEE's AI ethics assessment certification programme; another AI-adjacent credentialing surface.
- [OECD.AI — AI tools & metrics catalogue (assurance references)](https://oecd.ai/en/catalogue) — the OECD.AI catalogue of tools and metrics; a scan-list for the assurance ecosystem.
- [World Privacy Forum — Risks and harms of AI audits (2023)](https://www.worldprivacyforum.org/2023/12/risks-and-harms-in-the-ai-audit-ecosystem/) — a critical read of the AI-audit market landscape; useful for reading vendor bias-audit posture claims critically.

## Voluntary codes and regulator-adjacent guidance the control library aligns to

Chapter 07 optional-column references overlapping with `mod-106`'s voluntary-code references; kept narrow to what the control library cites for coverage.

- [OECD AI Principles](https://oecd.ai/en/ai-principles) — the OECD principles.
- [OECD AI — Catalogue of Tools and Metrics for Trustworthy AI](https://oecd.ai/en/catalogue) — the tools catalogue.
- [G7 Hiroshima Process — International Code of Conduct for Organizations Developing Advanced AI Systems](https://digital-strategy.ec.europa.eu/en/library/hiroshima-process-international-code-conduct-advanced-ai-systems) — the G7 voluntary code.
- [Council of Europe — Framework Convention on AI, Human Rights, Democracy and the Rule of Law](https://www.coe.int/en/web/artificial-intelligence/the-framework-convention-on-artificial-intelligence) — the CoE Framework Convention.
- [UNESCO — Recommendation on the Ethics of Artificial Intelligence](https://unesdoc.unesco.org/ark:/48223/pf0000381137) — the UNESCO ethics recommendation.
- [Bletchley Declaration (November 2023)](https://www.gov.uk/government/publications/ai-safety-summit-2023-the-bletchley-declaration/the-bletchley-declaration-by-countries-attending-the-ai-safety-summit-1-2-november-2023) — the AI Safety Summit declaration.
- [Seoul Declaration (May 2024)](https://www.gov.uk/government/publications/seoul-declaration-for-safe-innovative-and-inclusive-ai-ai-seoul-summit-2024) — the AI Seoul Summit declaration.
- [Frontier AI Safety Commitments (Seoul, May 2024)](https://www.gov.uk/government/publications/frontier-ai-safety-commitments-ai-seoul-summit-2024) — the sixteen-signatory safety-commitments text.

## Deferred-depth references

Depth-owning tracks the analyst hands off to for work outside analyst-tier scope. Chapter 09's delegation-boundary references.

- [senior-ai-governance-architect](https://github.com/ai-governance-curriculum/senior-ai-governance-architect-learning) — the enterprise-architecture depth track that owns the master control library, the control-library revision workflow, and the class-1 library-design-fix escalation resolution.
- [head-of-ai-governance](https://github.com/ai-governance-curriculum/head-of-ai-governance-learning) — the accountable-role track that owns Class-4 governance-council decisions and external-audit engagement leadership.
- [ai-infra-security](https://github.com/ai-infra-security-curriculum/ai-infra-security-learning) — the depth track for AI-specific security threat analysis, exploit reproduction, pentest, and mitigation code that chapters 04 and 05 route Class-2 escalations to.
- [ai-red-team-engineer](https://github.com/ai-governance-curriculum/ai-red-team-engineer-learning) — the depth track for red-team engagement design and adversarial-prompt discovery; the source of ATLAS technique identifiers the analyst carries forward.
- [ai-evaluation-engineer](https://github.com/ai-governance-curriculum/ai-evaluation-engineer-learning) — the depth track for eval-methodology and release-assurance sign-off; where control-tests citing eval-report links (chapter 02) resolve their supporting evidence from.
- [ai-incident-responder](https://github.com/ai-governance-curriculum/ai-incident-responder-learning) — the depth track for incident-response engagement; the `mod-109` post-market-surveillance control re-test trigger flows through here.
- [ai-model-risk-manager](https://github.com/ml-engineering-curriculum/ai-model-risk-manager-learning) — the depth track for quantitative model-risk management the SR 11-7 pillars 1 and 2 anchor on for financial-services enterprises.

## What is deliberately not here

- Consultancy trend reports, vendor "trust centre" one-pagers not paired with a specific artefact class from chapter 06, and marketing-adjacent framings of vendor safety work — useful for *noticing* a change quickly, but the vendor row's evidence columns carry the primary published artefact.
- Snapshots of a threat catalogue's documentation taken more than one release cycle ago — OWASP LLM Top 10, MITRE ATLAS, NIST AI 100-2, and Google SAIF all revise on a rolling basis. Cite against the current published documentation, not against an older summary, and record the edition / version per row.
- Cross-vendor certification-badge tables that plot ISO/IEC 42001 certification claims against SOC 2 Type II claims against ForHumanity independent-audit claims — chapter 06 was explicit that these are distinct evidence classes and columns 12 (ISO/IEC 42001), 13 (adjacent attestations), and 14 (independent audit) sit apart on the row. A cross-vendor arithmetic table blurs the distinction.
- Case dockets, plaintiff-bar filings, and enforcement-action press coverage — relevant to counsel's risk-management view, not to the control-status report's or the vendor row's primary-source columns. Where an enforcement action turns on control evidence, `mod-106`'s regulator-tracker row holds the regulator's own bulletin; this module's rows cite the underlying artefact.
- Vendor-produced certification "attestation" pages that do not cite the certifying body's accreditation — chapter 06 was explicit that a certification claim without an IAF-accredited certifying body is not equivalent to an accredited certification. A vendor page that names *"self-attested"* or names a certifying body not in the [IAF Members](https://iaf.nu/en/iaf-members/) list is a residual-risk contributor, not evidence of certification.
- Practitioner cheat-sheets that treat OWASP LLM Top 10, MITRE ATLAS, NIST AI 100-2, and Google SAIF as interchangeable — chapter 05 was explicit that the four references do different work (risk / attack / technique / defence-programme area) and the analyst's tagging convention carries whichever the source artefact provides without conflating.
- Snapshots of ForHumanity and BABL AI credential offerings — chapter 08 was explicit that both bodies revise their credentialing over time and that specific credential names age poorly. Reference the current [ForHumanity site](https://forhumanity.center/) and [BABL AI site](https://babl.ai/) at read time; do not cite a credential name from a snapshot.
- Sponsor-produced "AI-audit-ready" attestations that do not cite the framework's specific commitments and evidence classes — an adherence claim without a per-commitment citation is a marketing statement, not evidence for the analyst's row.
