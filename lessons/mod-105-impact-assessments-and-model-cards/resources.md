# Resources — mod-105 Impact Assessments, Model Cards, System Cards, and Datasheets

Primary references for the impact-assessment scaffolds, the canonical model-card / system-card / datasheet literature, and the publication surfaces the module walks. Read the standard or the statute first; blog summaries are one level removed and go stale on the timeline of the regulator, not of the summary author.

## The AI-specific ISO/IEC standard stack

The three interlocking standards behind the shared-template idea in chapter 01.

- [ISO/IEC 42005:2025 — Information technology — Artificial intelligence — AI system impact assessment](https://www.iso.org/standard/44545.html) — the AI-specific impact-assessment standard; the canonical scaffold the analyst adopts. Paywalled; enterprise use needs a licensed copy.
- [ISO/IEC 42001:2023 — Information technology — Artificial intelligence — Management system](https://www.iso.org/standard/81230.html) — the AI management-system standard; Clause 6 requires an AI risk assessment and an AI system impact assessment and points at 23894 and 42005 for their shapes.
- [ISO/IEC 23894:2023 — Information technology — Artificial intelligence — Guidance on risk management](https://www.iso.org/standard/77304.html) — the AI-specific risk-management guidance; sibling standard to 42005 supplying the risk-source lens.
- [ISO/IEC 22989:2022 — Information technology — Artificial intelligence — Artificial intelligence concepts and terminology](https://www.iso.org/standard/74296.html) — vocabulary underneath 42001 / 23894 / 42005.
- [ISO/IEC TR 24028:2020 — Information technology — Artificial intelligence — Overview of trustworthiness in artificial intelligence](https://www.iso.org/standard/77608.html) — trustworthiness overview cited from SC 42 documents that reference 42005.
- [ISO/IEC 27701:2019 — Security techniques — Extension to ISO/IEC 27001 and ISO/IEC 27002 for privacy information management](https://www.iso.org/standard/71670.html) — the ISO privacy-management standard the DPIA cross-references at enterprises that also certify to 27001.
- [ISO/IEC JTC 1/SC 42 (Artificial Intelligence) committee page](https://www.iso.org/committee/6794475.html) — the publishing committee; useful for tracking work items in flight (42005 amendments, new SC 42 publications).

## NIST anchors reused across the module

The MAP output feeding the 42005 canonical document is authored under this stack in `mod-103`.

- [NIST AI RMF 1.0 (AI 100-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf) — the Framework and its four functions (GOVERN / MAP / MEASURE / MANAGE); MAP is the walk whose output the 42005 canonical document re-projects.
- [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) — subcategory-by-subcategory suggested actions and documentation prompts; useful when writing the impact-assessment prompts an intake reviewer will follow.
- [NIST AI RMF Generative AI Profile (AI 600-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) — the GenAI risk-source list referenced from the MAP walk that feeds enumerated impacts in the AIA / FRIA / DPIA.
- [NIST SP 800-53 Rev. 5 — Security and Privacy Controls for Information Systems and Organizations](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final) — the privacy-controls catalogue a mature enterprise DPIA cites for its Section 3 mitigations.
- [NIST Privacy Framework 1.0](https://www.nist.gov/system/files/documents/2020/01/16/NIST%20Privacy%20Framework_V1.0.pdf) — the US analogue to the DPIA structure; useful where enterprise policy adopts it in lieu of a GDPR-shaped DPIA outside EU scope.
- [NIST AI Resource Center (AIRC)](https://airc.nist.gov/) — the hub the RMF, Playbook, and GenAI Profile publish through.

## Canadian algorithmic impact assessment — chapter 02

- [Directive on Automated Decision-Making](https://www.tbs-sct.canada.ca/pol/doc-eng.aspx?id=32592) — Treasury Board of Canada Secretariat directive; requires an AIA before production of automated decision systems and sets the four impact levels.
- [Government of Canada — Algorithmic Impact Assessment tool](https://www.canada.ca/en/government/system/digital-government/digital-government-innovations/responsible-use-ai/algorithmic-impact-assessment.html) — the questionnaire, scoring methodology, and the completed-AIA publication catalogue.
- [`canada-ca/aia-eia-js` on GitHub](https://github.com/canada-ca/aia-eia-js) — the AIA / ÉFA source code (open-source; MIT); useful when the enterprise stands up an internal AIA analogue or wants to see the exact questions in a diffable format.
- [Open Government Portal — completed AIAs](https://open.canada.ca/en/open-government) — the publication surface for federally-completed AIAs; browse for real examples in the analyst's domain before drafting.
- [Privacy Act (Canada)](https://laws-lois.justice.gc.ca/eng/acts/p-21/) — the personal-information companion statute referenced from the AIA where personal information is in scope.

## EU AI Act and the fundamental-rights impact assessment — chapter 03

- [Regulation (EU) 2024/1689 — the EU AI Act](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — consolidated text on EUR-Lex; the authoritative source for Articles 6, 13, 26, 27, and 50 and for Annex III.
- [artificialintelligenceact.eu — Article 6 (Classification rules for high-risk AI systems)](https://artificialintelligenceact.eu/article/6/) — annotated mirror of the Article 6 text.
- [artificialintelligenceact.eu — Annex III (List of high-risk AI systems)](https://artificialintelligenceact.eu/annex/3/) — annotated mirror of the Annex III text; the FRIA scope filter reads point 5(b) (credit / creditworthiness) and 5(c) (life / health insurance).
- [European Commission — European AI Office](https://digital-strategy.ec.europa.eu/en/policies/ai-office) — the AI Act enforcement and template-publishing body; the FRIA notification template comes from here.
- [Charter of Fundamental Rights of the European Union (2012/C 326/02)](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:12012P/TXT) — the Charter rights the FRIA element (4) attaches specific risks of harm to.

## GDPR and the data-protection impact assessment — chapter 04

- [Regulation (EU) 2016/679 — GDPR (consolidated text)](https://eur-lex.europa.eu/eli/reg/2016/679/oj) — the authoritative EUR-Lex text of the GDPR; Articles 35 and 36 are the DPIA anchors.
- [GDPR Article 35 — Data protection impact assessment](https://gdpr-info.eu/art-35-gdpr/) — annotated public copy of Article 35; useful for the four required elements the analyst produces.
- [gdpr-info.eu — GDPR full text](https://gdpr-info.eu/) — annotated hypertext of the whole regulation; the DPIA-authoring analyst references Article 22 (automated individual decision-making) from here.
- [Article 29 Working Party — WP 248 rev.01: Guidelines on Data Protection Impact Assessment](https://ec.europa.eu/newsroom/article29/items/611236) — the nine-criteria filter the analyst runs as the DPIA trigger; endorsed by the EDPB on its inaugural meeting and still the operative guidance.
- [EDPB — Guidelines, Recommendations and Best Practices](https://www.edpb.europa.eu/our-work-tools/general-guidance/gdpr-guidelines-recommendations-best-practices_en) — the ongoing European Data Protection Board publication surface; check for guidelines that update or supplement WP 248 before authoring.
- [CNIL — Deliberation No. 2018-327 (list of processing operations requiring a DPIA)](https://www.cnil.fr/en/deliberations/decision-2018-327) — the French supervisory authority's Article 35(4) mandatory-DPIA list; representative example of member-state DPIA lists.
- [BfDI — Bundesbeauftragte für den Datenschutz und die Informationsfreiheit](https://www.bfdi.bund.de/EN/Home/home_node.html) — the German federal DPA; publishes German mandatory-DPIA guidance.
- [UK ICO — Data protection impact assessments guidance](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/accountability-and-governance/data-protection-impact-assessments-dpias/) — regulator guidance on when a DPIA is required under UK GDPR and how to structure one.

## Sector-specific impact assessments — chapter 05

FDA good machine-learning practice (the module's worked example) plus the neighbouring sector overlays the chapter contrasts against.

- [FDA — Good Machine Learning Practice for Medical Device Development: Guiding Principles](https://www.fda.gov/medical-devices/software-medical-device-samd/good-machine-learning-practice-medical-device-development-guiding-principles) — the ten GMLP guiding principles jointly issued by FDA, Health Canada, and the UK MHRA.
- [FDA — Transparency for Machine Learning-Enabled Medical Devices: Guiding Principles](https://www.fda.gov/medical-devices/software-medical-device-samd/transparency-machine-learning-enabled-medical-devices-guiding-principles) — the transparency guiding principles that map onto the model-card / system-card discipline.
- [FDA — Predetermined Change Control Plans for Machine Learning-Enabled Medical Devices](https://www.fda.gov/medical-devices/software-medical-device-samd/predetermined-change-control-plans-machine-learning-enabled-medical-devices) — the PCCP guidance that reshapes the change-management sections of the impact assessment for medical AI.
- [FDA — Artificial Intelligence and Machine Learning in Software as a Medical Device](https://www.fda.gov/medical-devices/software-medical-device-samd/artificial-intelligence-and-machine-learning-software-medical-device) — hub page linking the AI/ML SaMD action-plan, submissions guidance, and public advisory materials.
- [FDA — Software as a Medical Device (SaMD)](https://www.fda.gov/medical-devices/software-medical-device-samd) — parent programme page for the SaMD framework the AI/ML guidance sits inside.
- **Financial-services model risk** (contrast case). [Federal Reserve SR 11-7 — Guidance on Model Risk Management](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm); [OCC Bulletin 2011-12](https://www.occ.treas.gov/news-issuances/bulletins/2011/bulletin-2011-12.html); [FDIC FIL-22-2017](https://www.fdic.gov/news/financial-institution-letters/2017/fil17022.html). The three-pillar (development, implementation, use) shape differs from the FDA slice.
- **Insurance** (contrast case). [NAIC Model Bulletin on the Use of Artificial Intelligence Systems by Insurers (adopted 2023-12-04)](https://content.naic.org/sites/default/files/inline-files/2023-12-4%20Model%20Bulletin_Adopted_0.pdf) — the state-insurance-regulator model bulletin adopted by NAIC member states.
- **Consumer-finance overlay.** [ECOA / Regulation B](https://www.consumerfinance.gov/rules-policy/regulations/1002/); [CFPB Circular 2022-03 on adverse-action notification for decisions based on complex algorithms](https://www.consumerfinance.gov/compliance/circulars/circular-2022-03-adverse-action-notification-requirements-in-connection-with-credit-decisions-based-on-complex-algorithms/) — cited from AIA / FRIA where credit decisions are in scope.
- **US-state overlay.** [Colorado SB 24-205 — Consumer Protections for Artificial Intelligence](https://leg.colorado.gov/bills/sb24-205) — first US-state comprehensive AI act; consequential-decision-tool obligations that layer on top of federal sector regimes.
- **NYC hiring overlay.** [NYC Local Law 144 — Automated Employment Decision Tools](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page) — the NYC AEDT rule; referenced from AIA / FRIA drafts where hiring is in scope.
- **EU medical devices** (adjacent regime). [Regulation (EU) 2017/745 — Medical Device Regulation (MDR)](https://eur-lex.europa.eu/eli/reg/2017/745/oj); [Regulation (EU) 2017/746 — In Vitro Diagnostic Regulation (IVDR)](https://eur-lex.europa.eu/eli/reg/2017/746/oj) — the EU analogue to the FDA SaMD framework the sector overlay references.
- **US education overlay.** [FERPA — Family Educational Rights and Privacy Act](https://studentprivacy.ed.gov/ferpa) — referenced from datasheet Collection Process fields where a US education dataset is in scope.

## Model cards — chapter 06

- [Mitchell et al. (2019) — "Model Cards for Model Reporting"](https://arxiv.org/abs/1810.03677) — the canonical nine-section paper; the module's reference shape for every model card the analyst produces or reviews.
- [Hugging Face — Model Cards documentation](https://huggingface.co/docs/hub/model-cards) — the dominant publication surface; YAML frontmatter for machine-readable metadata plus Markdown body.
- [Hugging Face — Model Cards Writing Tool](https://huggingface.co/spaces/huggingface/Model_Cards_Writing_Tool) — form-based generator that produces a Hugging Face-formatted model card.
- [Hugging Face Hub Python library — model-card helpers](https://huggingface.co/docs/huggingface_hub/how-to-manage#create-a-model-card) — programmatic model-card creation and editing.
- [Hugging Face](https://huggingface.co) — the wider Hub; useful for browsing peer vendor and community cards as shape exemplars.
- [Google — Model Card Toolkit (TensorFlow)](https://github.com/tensorflow/model-card-toolkit) — the alternative publication surface; a `ModelCard` proto plus HTML/Markdown renderers with the intersectional-evaluation slot the Mitchell paper called for.
- **Vendor exemplars to compare when authoring an enterprise supplement.**
    - [Meta Llama 3.1 model card](https://github.com/meta-llama/llama-models/blob/main/models/llama3_1/MODEL_CARD.md) — well-organised foundation-model card with intended-use, limitations, and eval sections in the Mitchell layout.
    - [Google Gemma model card](https://ai.google.dev/gemma/docs/model_card) — Google-hosted Gemma card; useful for the intended-use / out-of-scope framing.
    - [Anthropic — Claude 3 model card (addendum PDF)](https://www-cdn.anthropic.com/de8ba9b01c9ab7cbabf5c33b80b7bbc618857627/Model_Card_Claude_3.pdf) — public model card supplementing Claude 3; useful for the safety-eval section shape.

## System cards — chapter 07

Public system cards evolve; treat the URLs below as snapshots and verify against the vendor's current listing when citing an audit-facing artefact.

- [OpenAI — GPT-4 System Card](https://cdn.openai.com/papers/gpt-4-system-card.pdf) — the canonical "system card" the popularisation traces to; safety evaluations, red-team findings, and deployment mitigations.
- [OpenAI — GPT-4V(ision) System Card](https://cdn.openai.com/papers/GPTV_System_Card.pdf) — the vision-enabled variant; useful for the multi-modality-specific evaluation sections.
- [OpenAI — o1 System Card (2024-12-05)](https://cdn.openai.com/o1-system-card-20241205.pdf) — reasoning-model system card; representative of the newer disclosure shape. <!-- needs-research: verify against openai.com's current system-card listing before citing; system-card URLs change as new model versions are released. -->

## Datasheets for datasets — chapter 07

- [Gebru et al. (2018) — "Datasheets for Datasets"](https://arxiv.org/abs/1803.09010) — the canonical seven-section paper; the appendix lists roughly fifty questions grouped into Motivation, Composition, Collection Process, Preprocessing / Cleaning / Labeling, Uses, Distribution, and Maintenance.
- [Hugging Face — Dataset Cards documentation](https://huggingface.co/docs/hub/datasets-cards) — the dominant publication surface; loosely aligned with the Gebru sections.
- [Google — Data Cards Playbook](https://sites.research.google/datacardsplaybook/) — Google Research's alternative dataset-documentation framework; broader than the Gebru datasheet and useful as a shape reference on larger datasets.
- [PhysioNet — MIMIC-IV clinical database (v2.2)](https://physionet.org/content/mimiciv/2.2/) — representative example of a de-identified clinical dataset published with a dataset-description artefact; useful as an exemplar of the DPIA hook on Collection Process for sensitive-data cases.

## Deferred-depth references

Depth-owning tracks the analyst hands off to for the sections outside analyst-tier scope.

- [ai-risk-engineer](https://github.com/ml-engineering-curriculum/ai-risk-engineer-learning) — the depth track for eval-methodology, red-team, and mitigation-design work that populates model card sections 4–8 and system card sections 10–12.
- [ai-evaluation-engineer](https://github.com/ai-governance-curriculum/ai-evaluation-engineer-learning) — the eval-methodology depth track that produces the reports Model Card Section 6–7 references.
- [senior-ai-governance-architect](https://github.com/ai-governance-curriculum/senior-ai-governance-architect-learning) — the enterprise-architecture depth track that owns the shared-template design decisions, the tooling choice between Hugging Face and MCT at portfolio scale, and the change-management policy that governs card and impact-assessment supersession.

## What is deliberately not here

- Blog-post walk-throughs of the AI Act, GDPR Article 35, the Canadian Directive, or the FDA GMLP principles — read the primary text. Blog authors do not have standing before the regulator; the analyst does.
- Vendor "trust centre" one-pagers that claim compliance with 42001 / the AI Act / the GDPR without publishing evidence — the analyst-tier discipline is to read the standard's clause or the statute's article against the vendor's documentation, not against the vendor's marketing.
- ISO/IEC 42005 unofficial summaries produced before the 2025 publication — these were drafted against the draft text and often diverge from the published clause numbering. Use only the licensed standard for verbatim quotation in audit-facing artefacts.
- One-shot "AI ethics certification" services that promise a green tick without producing an ISO 42005-shaped or AIA / FRIA / DPIA-shaped artefact — chapter 08 is explicit that the impact assessment is the artefact; a certificate is not a substitute.
