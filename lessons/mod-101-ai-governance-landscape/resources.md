# Resources — mod-101 AI Governance Landscape

Every reference below is either a primary standards / regulatory document or an official companion to one. Prefer these over blog-post summaries when writing governance records.

## NIST AI Risk Management Framework

- [NIST AI RMF 1.0 (AI 100-1) — full PDF](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf) — the framework document. Read cover-to-cover once; keep tab-open for reference.
- [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) — the day-to-day operational companion; suggested actions per subcategory.
- [NIST AI RMF Generative AI Profile (AI 600-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) — the 12 generative-AI risks and RMF-aligned actions.
- [NIST AI Resource Center (AIRC) Knowledge Base](https://airc.nist.gov/AI_RMF_Knowledge_Base) — the umbrella hub NIST keeps updated.
- [NIST AI 100-2 — Adversarial ML Taxonomy](https://csrc.nist.gov/publications/detail/nistir/8269/draft) — the security-adjacent taxonomy the analyst needs at recognition level (deeper coverage in `mod-108`).

## ISO/IEC standards

- [ISO/IEC 42001:2023 — Artificial Intelligence Management System](https://www.iso.org/standard/81230.html) — the AIMS standard; the core reference for chapter 03.
- [ISO/IEC 27001:2022 — Information Security Management System](https://www.iso.org/standard/27001) — the ISMS the AIMS layers on top of.
- [ISO/IEC 23894:2023 — AI — Guidance on Risk Management](https://www.iso.org/standard/77304.html) — AI-specific risk-source taxonomy referenced by ISO 42001 Clause 6.
- [ISO/IEC 23053:2022 — Framework for AI Systems Using ML](https://www.iso.org/standard/74438.html) — an AI-system reference framework.
- [ISO/IEC 22989:2022 — AI Concepts and Terminology](https://www.iso.org/standard/74296.html) — the shared-vocabulary standard.
- [ISO/IEC 42005:2025 — AI Impact Assessment Guidance](https://www.iso.org/standard/44545.html) — the AI-specific IA standard; deeper coverage in `mod-105`.
- [ISO/IEC 38507:2022 — Governance Implications of the Use of AI by Organizations](https://www.iso.org/standard/56641.html) — governance-body vocabulary; deeper coverage in `mod-110`.

## EU AI Act and companion instruments

- [Regulation (EU) 2024/1689 — EU AI Act, official OJ text](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the regulation itself.
- [Consolidated CELEX view of Regulation 2024/1689 with Annexes](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32024R1689) — includes Annex I, Annex III, and Annex IV; cite these for the tier-tagging drill.
- [EU AI Office — General-Purpose AI Code of Practice](https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice) — the code that operationalises GPAI obligations under Chapter V.
- [EU Commission — Shaping Europe's Digital Future: AI Act hub](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai) — official summaries and explanatory materials.

## International values baseline

- [OECD AI Principles](https://oecd.ai/en/ai-principles) — the five value-based principles and five recommendations to governments.
- [OECD.AI Policy Observatory](https://oecd.ai/) — the country- and topic-level dashboards.
- [Council of Europe Framework Convention on Artificial Intelligence and Human Rights, Democracy and the Rule of Law (CETS 225)](https://www.coe.int/en/web/artificial-intelligence/the-framework-convention-on-artificial-intelligence) — the first legally binding international treaty on AI.
- [UNESCO Recommendation on the Ethics of Artificial Intelligence](https://www.unesco.org/en/artificial-intelligence/recommendation-ethics) — the 193-state consensus recommendation.

## Sector- and jurisdiction-specific regulation used as examples

The materials below are the ones referenced or alluded to in this module. Deeper cross-jurisdiction work lives in `mod-106-regulatory-tracking-and-jurisdictions`.

- [US Federal Reserve SR 11-7 — Guidance on Model Risk Management](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) and [OCC Bulletin 2011-12](https://www.occ.gov/news-issuances/bulletins/2011/bulletin-2011-12.html) — the financial-services baseline for model risk.
- [Canada — Directive on Automated Decision-Making + Algorithmic Impact Assessment tool](https://www.canada.ca/en/government/system/digital-government/digital-government-innovations/responsible-use-ai/algorithmic-impact-assessment.html) — the AIA lineage.
- [EU AI Act Article 35 / GDPR Article 35 — Data Protection Impact Assessment](https://gdpr-info.eu/art-35-gdpr/) and [GDPR Article 22 — Automated Individual Decision-Making](https://gdpr-info.eu/art-22-gdpr/) — the privacy overlays.
- [Colorado AI Act (SB 24-205)](https://leg.colorado.gov/bills/sb24-205) — the first US-state comprehensive AI law.
- [NYC Local Law 144 — Automated Employment Decision Tools](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page) — bias-audit precedent for hiring AI.
- [EEOC — AI in Employment Selection Procedures](https://www.eeoc.gov/laws/guidance/select-issues-assessing-adverse-impact-software-algorithms-and-artificial) — Title VII adverse-impact overlay.
- [FDA / Health Canada / MHRA — Good Machine Learning Practice Guiding Principles](https://www.fda.gov/medical-devices/software-medical-device-samd/good-machine-learning-practice-medical-device-development-guiding-principles) — the healthcare overlay.
- [UK — Algorithmic Transparency Recording Standard](https://www.gov.uk/government/publications/algorithmic-transparency-recording-standard-hub) — the UK public-sector transparency instrument.

## AI security threat taxonomies (awareness-level)

Deeper coverage in `mod-108-controls-and-compliance-evidence`. The analyst needs recognition-level awareness at this stage.

- [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
- [MITRE ATLAS — Adversarial Threat Landscape for AI Systems](https://atlas.mitre.org/)
- [Google SAIF — Secure AI Framework](https://safety.google/cybersecurity-advancements/saif/)

## Documentation practice

Deeper coverage in `mod-105-impact-assessments-and-model-cards`.

- [Mitchell et al. 2019 — Model Cards for Model Reporting](https://arxiv.org/abs/1810.03993)
- [Gebru et al. 2018 — Datasheets for Datasets](https://arxiv.org/abs/1803.09010)
- [Hugging Face Model Cards Guide](https://huggingface.co/docs/hub/model-cards)
- [Google Model Card Toolkit](https://github.com/tensorflow/model-card-toolkit)
- [Partnership on AI — ABOUT ML documentation guidance](https://partnershiponai.org/paper/about-ml/)

## Certifications relevant to this module

Threaded through `mod-101` and `mod-110`.

- [IAPP AIGP — Artificial Intelligence Governance Professional](https://iapp.org/certify/aigp/) — the most-cited certification for this role; body of knowledge overlaps this module substantially.
- [IAPP CIPP/US and CIPP/E](https://iapp.org/certify/) — privacy-adjacent add-ons.
- ISO/IEC 42001 Lead Implementer / Lead Auditor — offered by several accredited training bodies; content aligns with chapter 03. <!-- needs-research: cite one or two specific ISO/IEC 42001 LI/LA training providers once vetted; the market is still consolidating. -->

## What is deliberately not here

- Blog-post summaries of the NIST AI RMF, the EU AI Act, or ISO/IEC 42001. Read the primary text instead.
- Vendor whitepapers on "AI governance" that describe a product rather than a standard. Vendor coverage lives in `mod-102` and `mod-108`.
- Certification cram materials. The certifications page above links to the awarding bodies; syllabi are on their sites.
