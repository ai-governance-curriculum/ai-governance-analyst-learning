# Resources — mod-102 AI System Intake and Inventory Maintenance

Primary references. Prefer these over blog-post summaries or vendor whitepapers when writing governance records.

## Framework and standards anchors used at intake

- [NIST AI RMF 1.0 (AI 100-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf) — MAP 1 through MAP 4 subcategories drive most intake fields; GOVERN 6 drives the third-party fields.
- [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) — the day-to-day operational companion; look up specific subcategory questions here.
- [NIST AI RMF Generative AI Profile (AI 600-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) — the 12 GenAI risks the intake should surface.
- [ISO/IEC 42001:2023 — Artificial Intelligence Management System](https://www.iso.org/standard/81230.html) — Clause 6 planning and Clause 8 operation set the shape of intake, inventory, and material-change triggers.
- [ISO/IEC 23894:2023 — AI Risk Management Guidance](https://www.iso.org/standard/77304.html) — risk-source taxonomy the intake should be prepared to route into.
- [ISO/IEC 22989:2022 — AI Concepts and Terminology](https://www.iso.org/standard/74296.html) — the terms behind the intake vocabulary.

## Regulatory tier-tagging references

- [Regulation (EU) 2024/1689 — EU AI Act, OJ text](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — Article 5 (unacceptable), Article 6 + Annex I / Annex III (high risk), Article 50 (transparency), Chapter V (GPAI).
- [Consolidated CELEX view of Regulation 2024/1689](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32024R1689) — includes Annex I, Annex III, Annex IV.
- [EU AI Act Article 12 — record-keeping](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the obligation the inventory helps evidence.
- [EU AI Act Article 71 — EU database registration](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the workflow inventory surfaces gaps against.
- [GDPR Article 35 — Data Protection Impact Assessment](https://gdpr-info.eu/art-35-gdpr/) — DPIA trigger surfaced at intake.
- [GDPR Article 22 — Automated Individual Decision-Making](https://gdpr-info.eu/art-22-gdpr/) — automated-decision-making flag at intake.

## Sector overlays the intake routes to

- [US Federal Reserve SR 11-7 — Guidance on Model Risk Management](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) — the intake sector-regulator field maps here for financial services.
- [FDA / Health Canada / MHRA — Good Machine Learning Practice Guiding Principles](https://www.fda.gov/medical-devices/software-medical-device-samd/good-machine-learning-practice-medical-device-development-guiding-principles) — healthcare overlay.
- [EEOC — AI in Employment Selection Procedures](https://www.eeoc.gov/laws/guidance/select-issues-assessing-adverse-impact-software-algorithms-and-artificial) — hiring overlay.
- [NYC Local Law 144 — Automated Employment Decision Tools](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page) — NYC hiring overlay.
- [Colorado AI Act (SB 24-205)](https://leg.colorado.gov/bills/sb24-205) — Colorado consumer-protection overlay.

## GRC-for-AI platforms — vendor pages

Read the vendor pages to know the analyst-facing feature set; do not use vendor whitepapers as framework citations.

- [Credo AI](https://www.credo.ai/)
- [Holistic AI](https://www.holisticai.com/)
- [ModelOp](https://www.modelop.com/)
- [ServiceNow AI Control Tower](https://www.servicenow.com/products/ai-control-tower.html)
- [IBM watsonx.governance](https://www.ibm.com/products/watsonx-governance) — increasingly encountered in interviews. <!-- needs-research: confirm the current product name and feature scope. -->
- [Fairly AI](https://fairly.ai/) — an emerging option; verify presence in the shortlist for your enterprise before citing.

## Model registry references (analyst-tier awareness)

The analyst does not run these — the ML team does — but knowing the shape of a registry export makes reconciliation faster.

- [MLflow Model Registry](https://mlflow.org/docs/latest/model-registry.html)
- [Weights & Biases Model Registry](https://docs.wandb.ai/guides/registry)
- [Vertex AI Model Registry](https://cloud.google.com/vertex-ai/docs/model-registry/introduction)
- [Amazon SageMaker Model Registry](https://docs.aws.amazon.com/sagemaker/latest/dg/model-registry.html)
- [Azure Machine Learning model registry](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-manage-models)

## Documentation references reused at inventory time

- [Mitchell et al. 2019 — Model Cards for Model Reporting](https://arxiv.org/abs/1810.03993) — the inventory row references the model card.
- [Gebru et al. 2018 — Datasheets for Datasets](https://arxiv.org/abs/1803.09010) — the inventory row references the datasheet.
- [Hugging Face Model Cards Guide](https://huggingface.co/docs/hub/model-cards) — publishing surface.

## pandas / Excel

- [pandas documentation](https://pandas.pydata.org/docs/) — the core reference.
- [pandas merging, joining, and concatenating](https://pandas.pydata.org/docs/user_guide/merging.html) — the reconciliation join is a `merge` and a pair of `isin` filters.
- [Excel XLOOKUP function reference](https://support.microsoft.com/en-us/office/xlookup-function-b7fd680e-6d10-43e6-84f9-88eae8bf5929) — Excel-only fallback.

## What is deliberately not here

- Blog-post summaries of the EU AI Act, NIST AI RMF, or ISO/IEC 42001 — read the primary text.
- Vendor whitepapers describing a product's "responsible AI framework" as if it were a standard — cite the standard, not the vendor's paraphrase.
- Certification cram materials — the certifications page in `mod-101/resources.md` covers the awarding bodies.
