# Resources — mod-109 AI Incident Response and Continuous Monitoring at the Analyst Tier

Primary references for the AI-incident taxonomy the analyst files against, the continuous-monitoring platforms the analyst reads dashboards on, the EU AI Act post-market surveillance and serious-incident-reporting obligations the analyst drafts against, the AI-specific incident corpora the analyst cross-references, and the framework and specialist-role hand-offs the module's escalations route to. Read the primary source (the Regulation's authoritative text, the standard's authoring body, the tool project's canonical documentation, the reporting corpus's own methodology page) first; consultancy briefings and law-firm alerts are useful for *noticing* a change quickly but do not sit in an `INC-<year>-<sequence>` record's cross-reference column — the analyst chases the primary reference before writing the record.

## EU AI Act — Articles 72 and 73, and the surrounding infrastructure — chapter 07

The Regulation, the AI Office, and the market-surveillance instruments the PMS summary and Article 73 notification anchor on.

- [Regulation (EU) 2024/1689 — the EU Artificial Intelligence Act (consolidated text on EUR-Lex)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the AI Act. Article 3(49) definition of *serious incident*; Article 6 and Annex III high-risk classification; Article 9 risk-management system; Article 11 technical documentation; Article 26 deployer obligations; Article 27 fundamental-rights impact assessment; Article 72 post-market monitoring; Article 73 serious-incident reporting.
- [European Commission — Regulatory framework proposal on artificial intelligence](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai) — the Commission's AI-Act hub; the phased-entry-into-application timeline; the Commission's implementing acts and delegated acts as they publish.
- [European Commission — European AI Office](https://digital-strategy.ec.europa.eu/en/policies/ai-office) — the AI Office; the enforcement and template-publishing body for the EU AI Act. Watch this page for the Commission implementing act on the Article 72 post-market monitoring plan template and the Article 73 notification format.
- [EU AI Act — Article 72 — Post-market monitoring by providers and post-market monitoring plan (EUR-Lex)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the Article the PMS summary reports against. Verify the current text against the published OJ before drafting.
- [EU AI Act — Article 73 — Reporting of serious incidents (EUR-Lex)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the Article the notification draft implements. Verify the 15-day / 10-day / 2-day timeline structure and any corrigendum against the published OJ.
- [EU AI Act — Article 26 — Obligations of deployers of high-risk AI systems (EUR-Lex)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the deployer-side obligation cluster the analyst records on the PMS summary when the enterprise's customers are deployers.
- [EU AI Act — Article 27 — Fundamental rights impact assessment for high-risk AI systems (EUR-Lex)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the FRIA obligation the analyst re-opens per chapter 04.
- [European Commission — AI Act: enforcement authorities](https://digital-strategy.ec.europa.eu/en/policies/ai-act-enforcement) — the enforcement architecture; the Member-State-designated market surveillance authorities the Article 73 notification is submitted to. Different Member States are designating different authorities.
- [European Data Protection Board (EDPB)](https://edpb.europa.eu/) — the EDPB hub; the personal-data-processing obligations that layer onto AI systems the analyst cross-references on the Article 73 draft's coordination-with-other-authorities section.
- [European Commission — Standard Contractual Clauses (2021 revision)](https://commission.europa.eu/law/law-topic/data-protection/international-dimension-data-protection/standard-contractual-clauses-scc_en) — the SCCs the DPA transfer-mechanism references for cross-border deployer relationships.
- [ENISA — Multilayer Framework for Good Cybersecurity Practices for AI](https://www.enisa.europa.eu/publications/multilayer-framework-for-good-cybersecurity-practices-for-ai) — the EU cybersecurity agency's AI-cybersecurity framework; useful for the *coordination with other authorities* section when a serious incident has both a fundamental-rights and a cybersecurity dimension.

## AI incident corpora — chapters 02, 03

Public references the incident record's *external-corpus reference* field carries.

- [AI Incident Database (AIID) — Homepage](https://incidentdatabase.ai/) — the community-maintained catalogue of publicly reported AI incidents, with per-incident `AIID Incident nnn` identifiers, a common data schema, and cross-references to sources.
- [AI Incident Database — Discover incidents](https://incidentdatabase.ai/apps/discover) — the searchable index; how the analyst finds the *closest-match* AIID entry when an internal incident mirrors a public one.
- [AI Incident Database — Editors' summaries](https://incidentdatabase.ai/summaries/incidents/) — the editors' summaries page; useful for the intake-triage pattern-recognition work chapter 02 called out.
- [Partnership on AI — AI Incident Database governance](https://partnershiponai.org/workstream/ai-incidents-database/) — the governance surface for the AIID.
- [OECD.AI Policy Observatory — AI Incidents Monitor (AIM)](https://oecd.ai/en/incidents) — the OECD's real-time feed of AI incidents drawn from global news reporting, structured by principle (safety, fairness, privacy, transparency, accountability).
- [OECD.AI — Defining AI incidents](https://oecd.ai/en/wonk/defining-ai-incidents-and-related-terms) — the OECD's definition work on *AI incident*, *AI hazard*, and related terms; useful for aligning the enterprise's internal definition with the international vocabulary.
- [OECD.AI — Catalogue of Tools and Metrics for Trustworthy AI](https://oecd.ai/en/catalogue) — a scan-list of assurance tools, useful when the analyst's monitoring-reading note flags a missing metric.
- [MIT AI Risk Repository](https://airisk.mit.edu/) — a taxonomy of AI risks the analyst may cross-reference on class-4 (biased-outcome escalation) and class-5 (hallucination-driven harm) incident records; useful for the escalation-register class-4 (governance-council decision) pattern narrative.
- [Stanford HAI — AI Index Report](https://aiindex.stanford.edu/report/) — the AI Index; the *technical performance*, *responsible AI*, and *policy and governance* sections track incident and monitoring trends the analyst reads against.
- [AI, Algorithmic, and Automation Incidents and Controversies (AIAAIC) — Repository](https://www.aiaaic.org/aiaaic-repository) — an independently maintained incident repository; a secondary corpus for cross-reference beyond the AIID and OECD monitor.

## Continuous-monitoring platforms and tooling — chapter 05

Vendor platforms, open-source projects, and open-standard references the analyst reads dashboards on. No endorsement implied; the enterprise uses whichever tool `ai-eval-engineer` and `ai-infra-mlops` have adopted.

- **Vendor observability platforms.**
    - [Arize AI — Homepage](https://arize.com/) — a widely deployed ML / LLM observability platform.
    - [Arize AI — Documentation](https://docs.arize.com/) — the docs; useful for the analyst's tour of the four-family panel shapes.
    - [Fiddler AI — Homepage](https://www.fiddler.ai/) — an AI observability platform with explainability and monitoring modules.
    - [WhyLabs — Homepage](https://whylabs.ai/) — an ML monitoring platform with LLM security features.
    - [Datadog LLM Observability](https://www.datadoghq.com/product/llm-observability/) — Datadog's LLM observability surface.
    - [New Relic AI Monitoring](https://newrelic.com/platform/ai-monitoring) — New Relic's AI monitoring surface.
    - [Grafana Labs — AI Observability](https://grafana.com/solutions/ai-observability/) — Grafana's AI observability positioning.
    - [Aporia — Homepage](https://www.aporia.com/) — an ML observability platform.
    - [Truera (acquired by Snowflake) — Truera Observability](https://www.snowflake.com/en/data-cloud/ai/truera/) — the observability tool now integrated into Snowflake's AI stack.
- **Open-source monitoring frameworks.**
    - [Evidently AI — Documentation](https://docs.evidentlyai.com/) — open-source drift, quality, and monitoring reports for ML and LLM systems.
    - [Evidently AI on GitHub](https://github.com/evidentlyai/evidently) — the project repository.
    - [DeepEval — Documentation](https://docs.deepeval.com/docs/getting-started) — an open-source LLM-evaluation framework; useful for the quality-panel metric taxonomy.
    - [DeepEval on GitHub](https://github.com/confident-ai/deepeval) — the project repository.
    - [Ragas — Documentation](https://docs.ragas.io/) — an open-source RAG-evaluation framework; the RAG-triad (context precision, context recall, answer relevance) the analyst reads on RAG-system quality panels.
    - [Ragas on GitHub](https://github.com/explodinggradients/ragas) — the project repository.
    - [TruLens — Documentation](https://www.trulens.org/) — an open-source LLM-evaluation framework with feedback-function abstractions.
    - [Arize Phoenix — Documentation](https://docs.arize.com/phoenix) — an open-source LLM tracing and evaluation tool.
    - [Langfuse — Documentation](https://langfuse.com/docs) — an open-source LLM observability and tracing platform.
    - [Langfuse on GitHub](https://github.com/langfuse/langfuse) — the project repository.
    - [OpenLLMetry](https://www.traceloop.com/openllmetry) — an OpenTelemetry-based LLM observability convention.
    - [OpenTelemetry — Semantic conventions for Generative AI](https://opentelemetry.io/docs/specs/semconv/gen-ai/) — the emerging OpenTelemetry semantic conventions for GenAI systems; the standard the LLM-observability tools are aligning around.
- **Drift and distribution-shift references.**
    - [Alibi Detect — Documentation](https://docs.seldon.io/projects/alibi-detect/en/stable/) — an open-source outlier / drift / adversarial detection library.
    - [River — Concept-drift detection](https://riverml.xyz/dev/user-guide/concept-drift/) — a streaming-ML library with concept-drift primitives.
    - [Population Stability Index (PSI) — Wikipedia overview](https://en.wikipedia.org/wiki/Population_stability_index) — the PSI metric the drift panels commonly use.
    - [KL divergence — Wikipedia overview](https://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence) — the KL-divergence metric drift panels also use.

## Model risk management and incident-response practice — chapters 03, 08

Practitioner references on incident-response mechanics and post-incident evidence discipline.

- [Google SRE — Incident Response chapter](https://sre.google/sre-book/managing-incidents/) — the SRE-book chapter on managing incidents; the classical-incident-response vocabulary the analyst's *both-at-once* pattern cross-references.
- [Google SRE — Postmortem Culture chapter](https://sre.google/sre-book/postmortem-culture/) — the SRE-book chapter on postmortem culture; the practice the analyst reads the engineering team's post-mortem against.
- [Google SRE — The Incident Response section](https://sre.google/workbook/incident-response/) — the workbook chapter with additional patterns.
- [PagerDuty — Incident Response documentation](https://response.pagerduty.com/) — PagerDuty's open-source incident-response documentation; the industry-widespread on-call vocabulary the analyst records against.
- [Atlassian — Incident Management Handbook](https://www.atlassian.com/incident-management/handbook) — Atlassian's incident management handbook; another practitioner reference.
- [FIRST — CVSS specification](https://www.first.org/cvss/) — the Common Vulnerability Scoring System; the specialist's severity taxonomy on the classical-security side of both-at-once records.
- [MITRE ATT&CK — Homepage](https://attack.mitre.org/) — the parent adversarial-behaviour framework.
- [MITRE ATLAS — Homepage](https://atlas.mitre.org/) — the *Adversarial Threat Landscape for Artificial-Intelligence Systems* knowledge base; the ML-specific overlay whose technique identifiers land on class-3 (prompt-injection exploitation) and class-2 (jailbreak) incident records where the source artefact provides them.
- [MITRE ATLAS — Case studies](https://atlas.mitre.org/studies) — a growing set of case studies; useful for the analyst's pattern recognition on repeat-incident classes.
- [NIST AI 100-2e2025 — Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations](https://csrc.nist.gov/pubs/ai/100/2/e2025/final) — NIST's normative reference on AML attack classification (evasion, poisoning, privacy, abuse); the taxonomy chapter 02's class-3 (prompt-injection exploitation) and class-6 (unauthorised model use) incidents may cross-reference on the technical-detail block. Cite the edition.

## Frameworks, standards, and voluntary codes the module sits inside — chapters 01, 07

Foundational frameworks the analyst carries context from into the module.

- [NIST AI Risk Management Framework 1.0 (NIST AI 100-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf) — the foundational AI RMF; the MEASURE and MANAGE functions map to continuous monitoring and incident response; the MANAGE 4 sub-function on incident response is the direct anchor.
- [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) — the RMF Playbook; the sub-category-level actions the analyst's monitoring-reading note and incident record cross-reference.
- [NIST AI RMF Generative AI Profile (NIST AI 600-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) — the twelve GenAI risk categories chapter 02's AI-specific class definitions align with (confabulation → class 5; harmful bias and homogenisation → class 4; obscene, degrading, and abusive content → class 2; information security → class 3; etc.).
- [NIST AI Resource Center (AIRC)](https://airc.nist.gov/) — the RMF resource hub.
- [ISO/IEC 42001:2023 — Information technology — Artificial intelligence — Management system](https://www.iso.org/standard/81230.html) — the AI management-system standard whose Annex A contains AI-specific controls including on incident-response and post-market monitoring.
- [ISO/IEC 23894:2023 — Information technology — Artificial intelligence — Guidance on risk management](https://www.iso.org/standard/77304.html) — AI risk-management guidance; complements the AI RMF for the risk-and-incident interaction.
- [ISO/IEC 42005:2025 — AI system impact assessment](https://www.iso.org/standard/44545.html) — the ISO AI-system impact-assessment standard cited from `mod-105`; the shape the FRIA re-open on incident trigger (chapter 04) aligns to.
- [ISO/IEC 27035:2023 — Information security incident management](https://www.iso.org/standard/78973.html) — the ISO information-security incident-management standard; the practitioner reference the enterprise's classical-security incident process the analyst cross-references on both-at-once records is often anchored to.
- [ISO/IEC 27001:2022 — Information security management systems — Requirements](https://www.iso.org/standard/27001) — the ISMS standard.
- [OECD AI Principles](https://oecd.ai/en/ai-principles) — the OECD principles; the OECD AI Incidents Monitor structures its per-incident classifications against these.
- [G7 Hiroshima Process — International Code of Conduct for Organizations Developing Advanced AI Systems](https://digital-strategy.ec.europa.eu/en/library/hiroshima-process-international-code-conduct-advanced-ai-systems) — the G7 voluntary code; the *report vulnerabilities and misuse* commitment cross-references the module's incident-and-monitoring practice.
- [UNESCO — Recommendation on the Ethics of Artificial Intelligence](https://unesdoc.unesco.org/ark:/48223/pf0000381137) — the UNESCO ethics recommendation.
- [Council of Europe — Framework Convention on AI, Human Rights, Democracy and the Rule of Law](https://www.coe.int/en/web/artificial-intelligence/the-framework-convention-on-artificial-intelligence) — the CoE Framework Convention; the *effective remedy* obligation the biased-outcome-escalation class-4 record on some Member States' implementations may cross-reference.

## Sector-specific incident and post-market obligations — chapter 07

Sector-adjacent obligations the PMS summary and Article 73 notification cross-reference when the affected system carries a sector regime.

- **Healthcare / medical devices.**
    - [US FDA — Artificial Intelligence and Machine Learning in Software as a Medical Device](https://www.fda.gov/medical-devices/software-medical-device-samd/artificial-intelligence-and-machine-learning-software-medical-device) — the FDA AI/ML-SaMD hub.
    - [US FDA — Medical Device Reporting (MDR)](https://www.fda.gov/medical-devices/postmarket-requirements-devices/medical-device-reporting-mdr-how-report-medical-device-problems) — the US medical-device incident-reporting obligation the PMS summary cross-references when the enterprise's system is an SaMD.
    - [European Commission — Medical Device Regulation (MDR)](https://health.ec.europa.eu/medical-devices-sector/new-regulations_en) — the EU MDR hub; Article 87 vigilance reporting and Article 88 trend reporting the PMS summary cross-references.
    - [European Commission — In Vitro Diagnostic Medical Devices Regulation (IVDR)](https://health.ec.europa.eu/medical-devices-sector/new-regulations_en) — the EU IVDR hub.
- **Financial services / model risk.**
    - [Board of Governors of the Federal Reserve System — SR Letter 11-7 (Guidance on Model Risk Management)](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) — the US model-risk-management supervisory guidance; the model-monitoring practice cited on chapter 05's quality panels.
    - [OCC Bulletin 2011-12 — Sound practices for model risk management](https://www.occ.treas.gov/news-issuances/bulletins/2011/bulletin-2011-12.html) — the OCC parallel guidance.
    - [PRA Supervisory Statement SS1/23 — Model risk management principles for banks](https://www.bankofengland.co.uk/prudential-regulation/publication/2023/may/model-risk-management-principles-for-banks-ss) — the UK PRA supervisory statement; the model-monitoring principle is Principle 4.
- **Hiring / employment.**
    - [NYC Department of Consumer and Worker Protection — Automated Employment Decision Tools (Local Law 144)](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page) — the Local Law 144 hub; the annual bias-audit publication obligation the incident-response for a class-4 (biased-outcome escalation) on a NYC-scope AED tool cross-references.
    - [US EEOC — Artificial Intelligence and Algorithmic Fairness Initiative](https://www.eeoc.gov/ai) — the EEOC AI-and-employment guidance.
- **Public sector automated decision-making.**
    - [Canadian Directive on Automated Decision-Making](https://www.tbs-sct.canada.ca/pol/doc-eng.aspx?id=32592) — the Canadian federal directive; the ongoing-monitoring section the analyst cross-references for Canadian-federal deployments.
    - [UK — Algorithmic Transparency Recording Standard](https://www.gov.uk/government/collections/algorithmic-transparency-recording-standard-hub) — the UK ATRS; the operating-updates section.
- **Consumer privacy and personal data.**
    - [Regulation (EU) 2016/679 — General Data Protection Regulation (GDPR)](https://eur-lex.europa.eu/reg/2016/679/oj) — GDPR; Article 22 automated decision-making, Article 33 personal-data breach notification (72-hour), Article 34 communication to the data subject, Article 35 DPIA.
    - [Article 29 Working Party (now EDPB) — Guidelines on Automated individual decision-making and Profiling](https://ec.europa.eu/newsroom/article29/items/612053) — the DPO's reference for the Article 22 pattern chapter 02 class 4 records may cross-reference.

## LLM-specific security taxonomies — chapter 02 classes 2 and 3

The taxonomies the class-2 (jailbreak) and class-3 (prompt-injection exploitation) records cite.

- [OWASP Top 10 for LLM Applications](https://genai.owasp.org/llm-top-10/) — the current canonical list. LLM01:2025 Prompt Injection is the direct anchor for class-3 records; LLM06:2025 Excessive Agency and LLM07:2025 System Prompt Leakage cross-reference on class-3 sub-variants; LLM09:2025 Misinformation cross-references on class-5 (hallucination-driven harm) records. Version-cite (`LLM01:2025`) rather than bare (`LLM01`).
- [OWASP GenAI Security Project — Hub](https://genai.owasp.org/) — the umbrella OWASP project; publishes the Top 10 plus practitioner guides.
- [OWASP AI Security & Privacy Guide](https://owasp.org/www-project-ai-security-and-privacy-guide/) — an OWASP guide covering AI-security controls, threats, and privacy considerations.
- [Google Secure AI Framework (SAIF)](https://safety.google/cybersecurity-advancements/saif/) — Google's defender-oriented programme framework; the *detect and respond* and *observability* elements map to chapter 05 and chapter 03 respectively.
- [Coalition for Secure AI (CoSAI)](https://www.coalitionforsecureai.org/) — the industry-and-community coalition; SAIF-adjacent content.
- [Anthropic — Responsible Scaling Policy](https://www.anthropic.com/rsp) — the Anthropic RSP; a reference the analyst may cross-reference for provider-side incident practice.
- [OpenAI — Preparedness Framework](https://openai.com/safety/preparedness/) — OpenAI's preparedness framework; a reference for provider-side incident practice.
- [UK NCSC — Guidelines for secure AI system development](https://www.ncsc.gov.uk/collection/guidelines-secure-ai-system-development) — the UK NCSC guidelines co-published with CISA and multiple national agencies.
- [US CISA — AI at CISA](https://www.cisa.gov/ai) — CISA's AI-security guidance hub.

## Model and system cards — chapter 03 governance-follow-through

The reference on system-card / model-card update triggers post-incident.

- [Hugging Face — Model card creation guide](https://huggingface.co/docs/hub/model-cards) — the model-card scaffold.
- [Google — Model Cards for Model Reporting (2019 paper)](https://arxiv.org/abs/1810.03993) — the original model-cards paper.
- [Datasheets for Datasets (2018 paper)](https://arxiv.org/abs/1803.09010) — the companion datasheets pattern.
- [OpenAI — System cards](https://openai.com/index/gpt-4-system-card/) — an example of a provider-side system card; useful as a template for enterprise-side system cards on hosted-model integrations.
- [Anthropic — Claude model cards](https://www.anthropic.com/claude/sonnet) — provider-side model documentation.

## Delegated-depth references — chapter 09 escalation targets

Depth-owning tracks the analyst hands off to for work outside analyst-tier scope.

- [ai-eval-engineer](https://github.com/ai-governance-curriculum/ai-eval-engineer-learning) — the depth track for eval-methodology, monitoring-metric choice, threshold tuning, and dashboard design; where the analyst's Class-1 model-behaviour escalations on quality-panel signals land.
- [ai-infra-mlops](https://github.com/ai-infra-mlops-curriculum/ai-infra-mlops-learning) — the depth track for MLOps and monitoring operation; where the analyst's coordination on cost-panel signals and dashboard-instrumentation gaps lands.
- [ai-infra-security](https://github.com/ai-infra-security-curriculum/ai-infra-security-learning) — the depth track for AI-specific security threat analysis, exploit reproduction, and mitigation code; where the analyst's Class-2 security escalations on class-2 (jailbreak) and class-3 (prompt-injection) incidents land.
- [ai-risk-engineer](https://github.com/ai-governance-curriculum/ai-risk-engineer-learning) — the depth track for AI-risk quantification and register-residual-risk re-scoring; where the analyst's Class-1 model-behaviour escalations on drift-panel and biased-outcome signals land.
- [ai-red-team-engineer](https://github.com/ai-governance-curriculum/ai-red-team-engineer-learning) — the depth track for red-team engagement and adversarial-prompt discovery; the source of ATLAS technique identifiers on class-2 and class-3 incident records.
- [ai-incident-responder](https://github.com/ai-governance-curriculum/ai-incident-responder-learning) — the depth track for AI-incident-response engagement; the receiving track for the technical containment work the analyst records on the incident record's *containment actions* field.
- [head-of-ai-governance](https://github.com/ai-governance-curriculum/head-of-ai-governance-learning) — the accountable-role track; where the analyst's Class-4 governance-council escalations land.
- [senior-ai-governance-architect](https://github.com/ai-governance-curriculum/senior-ai-governance-architect-learning) — the enterprise-architecture track; where the analyst's `mod-108` library-design-fix escalations land.
- [data-protection-officer](https://github.com/data-protection-officer-curriculum/data-protection-officer-learning) — the DPO track; the coordination target on GDPR / DPIA cross-referenced obligations.

## What is deliberately not here

- Vendor "AI-observability platform comparison" reports and analyst-firm quadrants — chapter 05 was explicit that the analyst reads whatever tool the enterprise runs; the four-family taxonomy is what carries across tools. A comparison table plotting Arize against Fiddler against WhyLabs is marketing-adjacent; the analyst's fluency is in the panel-shape, not the tool brand.
- Consultancy-produced *AI-incident-response-maturity models* that assign a score to the enterprise on a five-level scale — a scored maturity narrative is not the analyst's artefact; the analyst's artefact is the incident record, the monitoring-reading note, and the PMS summary. Maturity assessments belong upstream (`senior-ai-governance-architect`) if they belong anywhere.
- Snapshots of the AI Incident Database or the OECD AI Incidents Monitor taken more than one release cycle ago — both corpora are actively updated; the analyst reads the live URL, records the *closest-match* identifier at read time, and does not cite a snapshot dated a year prior.
- Vendor product pages that assert *"AI-Act-ready"* or *"Article-72-compliant"* without linking to the specific evidence class the product provides for the enterprise's PMS summary — a vendor readiness claim is not evidence for the analyst's PMS summary section §2; the specific artefact (a config export, a log sample, an eval-report link, a signed-off record) is.
- Practitioner blog posts that treat *hallucination*, *confabulation*, *bullshit*, and *fabrication* as interchangeable — chapter 02 was explicit that the class field is a filing decision anchored on the effect (harm reaching a person or a downstream system) rather than a philosophical stance on the model's epistemic state. The analyst's class assignment cites chapter 02's working definition, not the current fashionable framing.
- Case dockets, plaintiff-bar filings, and enforcement-action press coverage — relevant to counsel's risk-management view, not to the incident record's or PMS summary's primary-source columns. Where an enforcement action turns on incident evidence, the `mod-106` regulator-tracker row holds the regulator's own bulletin; the incident record and PMS summary cite the underlying artefact.
- Snapshots of the EU AI Office's implementing-act workstreams — chapter 07 was explicit that the analyst tracks the Commission's page live and marks any cited item `<!-- needs-research: -->` where the current status is not verified against a live check. A snapshot dated at the time chapter 07 was authored is not evidence of the current template.
