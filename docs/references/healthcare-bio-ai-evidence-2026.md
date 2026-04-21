# Healthcare-Bio AI Evidence (April 2026)

## Purpose

This note collects 2026 evidence on healthcare, hospital, and pharmaceutical AI so that the repository's frameworks — [`../frameworks/cost-taxonomy.md`](../frameworks/cost-taxonomy.md), [`../frameworks/skill-domain-taxonomy.md`](../frameworks/skill-domain-taxonomy.md), [`../frameworks/ai-system-lifecycle.md`](../frameworks/ai-system-lifecycle.md), [`../frameworks/ai-system-operations.md`](../frameworks/ai-system-operations.md), and [`../frameworks/ai-system-economics.md`](../frameworks/ai-system-economics.md) — can be extended to this sector as a special topic rather than as part of the main research spine.

Healthcare-bio AI is not a separate skill domain. It is a collection of subdomains whose mapping onto the existing sales/productization lens is non-uniform, and whose compliance overlay and failure-cost shape are different enough from the sectors already covered that a dedicated evidence cut is warranted. The companion scenario-level analysis lives in [`../reports/healthcare-bio-ai-special-topic.md`](../reports/healthcare-bio-ai-special-topic.md).

The data here is current as of April 2026. Citations in the Sources section are intended to be reused across the special-topic report rather than restated inline.

## 1. Regulatory Landscape

### 1.1 FDA AI/ML-Enabled Medical Devices

- **Authorized device count**: the FDA's public list of AI/ML-enabled medical devices passed approximately 1,250 as of July 2025, up from approximately 950 in August 2024. In December 2025 an additional 56 radiology AI devices were added, bringing imaging-specific AI devices to approximately 1,039 (about 80% of the list). The cumulative count since 1995 exceeds 1,200.
- **PCCP final guidance**: the FDA published final guidance on Predetermined Change Control Plans for AI-enabled device software functions in December 2024 and a broader draft PCCP guidance for all device types in August 2024. A PCCP documents planned modifications, a Modification Protocol, and an Impact Assessment, and lets a manufacturer update an AI-enabled device after clearance without a new marketing submission for changes the plan covers.
- **AI-enabled SaMD lifecycle draft guidance**: on January 6, 2025 the FDA published "Artificial Intelligence-Enabled Device Software Functions: Lifecycle Management and Marketing Submission Recommendations," which proposes lifecycle considerations across premarket, deployment, and postmarket phases.
- **CDS update**: on January 9, 2026 the FDA published key updates to the 2026 General Wellness and Clinical Decision Support Software Guidance, expanding wellness exemptions and adjusting enforcement discretion on CDS.
- **QMSR effective**: ISO 13485-aligned Quality Management System Regulation becomes effective on February 2, 2026. Manufacturers of AI-enabled devices must demonstrate design controls, change control, bias monitoring, and record retention processes compatible with PCCP implementation.

### 1.2 EU AI Act Interaction with MDR/IVDR

- **Entry into force for high-risk systems**: August 2, 2026, with full applicability on August 2, 2027. For regulated digital medical products subject to MDR/IVDR, obligations for AI subsystems apply 36 months after entry into force.
- **Default high-risk classification**: MDR class IIa, IIb, and III devices and IVDR class A-D normally classify as high-risk under the AI Act when the AI is a safety component or is itself the medical device and the device is subject to third-party conformity assessment.
- **Additional compliance surface above MDR/IVDR**: data quality and governance, record-keeping, transparency, accountability, and human oversight. Commission classification guidelines due February 2026 include concrete examples of what counts as high-risk for pharma and devices.
- **Commission December 2025 proposal**: on December 16, 2025 the European Commission published a proposal that would remove medical devices from the high-risk scope of the AI Act and instead harmonize AI requirements through the MDR framework. The proposal is not yet adopted. Treat the high-risk obligation as the operational baseline until the proposal is enacted.
- **Joint Artificial Intelligence Board and MDCG 2025-6**: the Medical Device Coordination Group published guidance (MDCG 2025-6) on interaction between MDR and the AI Act.

### 1.3 FDA/EMA Joint AI Principles (January 2026)

In January 2026 the FDA and EMA jointly published ten guiding principles for good AI practice across the full medicines lifecycle. The principles cover drug discovery, clinical development, pharmacovigilance, real-world evidence analysis, and manufacturing. Key expectations:

- AI-assisted decisions in pharmacovigilance and clinical development must be explainable, traceable, and inspection-ready.
- Human oversight is explicitly required.
- Risk-based data quality and governance assessments must be documented.

### 1.4 EMA GVP 2026 Overhaul (Pharmacovigilance)

The 2026 update to EMA's Good Pharmacovigilance Practices makes AI-powered tools and automated signal detection a regulatory expectation rather than an optional upgrade. Mandatory EudraVigilance integration into internal signal monitoring is also moved from guidance to expectation.

### 1.5 CIOMS Working Group XIV (December 2025)

The CIOMS XIV report provides the first international consensus framework for AI in pharmacovigilance, organized around seven principles: risk-based approach, data quality and governance, transparency, human oversight, validation, monitoring, and accountability.

### 1.6 US State-Level AI Healthcare Laws

- **Colorado AI Act**: the first comprehensive US state AI law, effective February 1, 2026. Applies to high-risk systems including healthcare decision support.
- **California AB 2013**: effective January 1, 2026. Requires disclosures about training data and use cases; analysts treat it as a template for other states.
- **California AI disclosure law for healthcare**: requires generative AI used in patient communications to be disclosed.

### 1.7 HHS OCR Enforcement and the 2026 HIPAA Security Rule Overhaul

- OCR issued more AI-related guidance in 2025 than in the preceding five years combined. AI-specific enforcement actions rose approximately 340% over the same period.
- In 2024 a mid-sized regional hospital network received a $4.75M HIPAA penalty because its AI diagnostics vendor had been processing patient data without a signed Business Associate Agreement.
- A 2026 peer-reviewed study (George Washington University and Yale School of Medicine) reported that only approximately 23% of health systems have BAAs in place with AI vendors despite approximately 66% of physicians using AI tools in some capacity.
- The 2026 HIPAA Security Rule overhaul expands the design controls required on AI data pipelines.

## 2. Clinical / Hospital AI Adoption

### 2.1 Ambient Clinical Scribing Outcomes

Recent controlled evidence across multiple US health systems:

- JAMA multicenter study: AI-powered ambient scribes reduced total EHR time by 13.4 minutes per clinician per day and documentation-specific time by 16.0 minutes. Study covered five academic medical centers.
- 2025 burnout study (263 physicians, six health systems): clinician burnout fell from 51.9% to 38.8% in 30 days with AI scribing. Physicians reported saving 2–3 hours per day on documentation and seeing approximately 15% more patients per hour.
- Abridge quality-improvement study (Feb–Oct 2024, six US health systems): Riverside Health (Virginia) reported an 11% increase in physician work RVUs and a 14% increase in documented Hierarchical Condition Category diagnoses per encounter.
- Northwestern Medicine clinicians using Nuance DAX billed more high-level E/M visits on average.

### 2.2 Ambient Scribing Vendor Pricing Anchors

- Abridge: approximately $208/provider/month for enterprise deployments. Contracts with approximately 150 US enterprise health systems as of 2025.
- Suki: $299–$399+/provider/month. Positioned for health systems of 100+ clinicians.
- Nuance DAX Copilot: enterprise subscription pricing, typically sold through Microsoft. Implementation is 3–6 months for hospital deployments. Deep Epic integration is the benchmark.
- Implementation cost: "3 to 6 months of implementation work and enterprise-level licensing costs" is the standard bracket for Epic-heavy hospital deployments.

### 2.3 AI Medical Coding and Revenue Cycle

- BCBS study (March 9, 2026): hospitals' AI-enabled coding capabilities drove approximately $2.3B in increased spending over three years, split approximately $663M inpatient and approximately $1.67B outpatient.
- AMA 2026 CPT update: the first CPT code set to explicitly recognize AI in medical coding.
- Claimed operational gains (vendor side): approximately 40% reduction in coding time, accuracy above 95%, measurable reduction in claim denials.
- Enforcement exposure: repeated upcoding or unbundling traceable to AI coding tools can trigger False Claims Act investigations. Enforcement actions tied to "knowingly relied on flawed AI tools that generated inaccurate billing codes" have intensified in 2025–2026.

### 2.4 Prior Authorization AI at Payers

- 50+ health plans (UnitedHealthcare, Aetna, Cigna, Blues) committed with CMS to simplify prior authorization by January 1, 2026 and to honor approvals for 90 days when patients switch plans.
- AI-driven overturn rate in Medicare Advantage is approximately 82%, indicating a high denial rate that is reversed upon appeal.
- UnitedHealthcare Medicare Advantage denial rate: approximately 12.8%.
- Cigna PXDX: over a 2-month 2022 window, Cigna doctors denied more than 300,000 claims through an AI-supported review, spending an average of 1.2 seconds per case.
- UnitedHealthcare nH Predict class action: alleged 90% error rate in overriding physician determinations for Medicare Advantage patients in skilled nursing facilities. Broad document discovery ordered March 2025, still active March 2026.
- AHIP first public progress report on the prior-auth commitments expected spring 2026.

### 2.5 Hospital AI Governance Maturity

- 41% of hospitals cite limited documentation from AI vendors (model cards, drift reports) as their top audit barrier.
- 33% cite unclear ownership among IT, quality and safety, and compliance teams as impeding governance.
- The 2026 consensus governance vocabulary includes: cross-functional AI governance committee (data science, clinicians, compliance, ethics), PPTO framework (People, Process, Technology, Operations), PCCP-triggered retraining, real-time drift monitoring, and AI adverse-event reporting.

## 3. Diagnostic AI and Imaging

### 3.1 NHS EDITH Trial (UK)

- Scale: over 700,000 women; five competing AI systems across 30 screening sites. Launched April 2025 with £11M government support.
- Primary question: can AI safely replace one of the two radiologists currently required to analyze a screening mammogram? Potential freed-up clinician time is approximately 100,000 hours/year.
- Preliminary results (Nature Cancer, published 2026, Google / Imperial College London): 125,000-mammogram study — AI identified 25% of interval cancers previously missed. Separate 50,000-woman study — AI reduced workload by approximately 40% when used as second reader.
- **Operational side-effect**: when AI replaced one human reader, arbitration demand surged 142% at one site and 22% at another. Arbitration panels overruled the AI even when it had correctly identified cancer in 93 cases. This is a concrete instance of the human-in-the-loop verifier becoming the bottleneck.

### 3.2 AI Imaging Reimbursement

- As of January 2026, only two CPT Category I payment codes exist for newer AI in radiology, both cardiac:
  - 75580 (FFR-CT analysis) — Category I effective January 2025.
  - 75577 (AI-driven coronary atherosclerotic plaque quantification in CCTA) — Category I effective January 1, 2026.
- AI-assisted lung nodule detection and stroke flagging transitioned from Category III to Category I codes, establishing RVUs.
- Most FDA-cleared imaging AI vendors have not produced the clinical studies required to obtain payment. The gap between clearance and reimbursement remains the dominant adoption constraint.

### 3.3 Korea Medical AI Approvals

- Approval/certification/registration counts: 62 (2023) → 108 (2024) → 157 (2025); approximately 55 additional approvals in Q1 2026 alone. Compound multiple over three years is approximately 2.53x.
- Lunit: approval for Lunit INSIGHT DBT (3D digital breast tomosynthesis AI), 2026 revenue growth target of 40–50% with approximately 20% cost reduction.
- VUNO: VUNO Med-DeepCARS (in-ward cardiac arrest risk prediction within 24 hours) is the flagship product in 2025–2026; VUNO Med-DeepECG Kidney (non-invasive kidney function screening from 12-lead ECG) received 2025 approval.

## 4. Pharmaceutical AI

### 4.1 AI Drug Discovery Pipeline

- Over 173 AI-discovered drug programs are in clinical development globally as of early 2026. 15–20 are set to enter large-scale trials in 2026.
- Insilico Medicine: ISM001-055 (rentosertib), a TNIK inhibitor for idiopathic pulmonary fibrosis, cleared Phase IIa; pivotal trial discussions with global regulators underway; US Phase IIa is actively enrolling. Insilico + Eli Lilly published "From Prompt to Drug: Toward Pharmaceutical Superintelligence" in ACS Central Science (February 2026).
- Recursion (post Exscientia merger): REC-994 (lead AI-discovered compound, pre-merger) discontinued May 2025 after long-term data failed to confirm earlier efficacy trends. Active programs include REC-394 (C. difficile) Phase 2 update Q1 2026 and REC-1245 (RBM39 degrader) Phase 1 data H1 2026.
- Isomorphic Labs: introduced IsoDDE drug design engine (February 2026), claimed to surpass AlphaFold 3 by more than 2x on protein-ligand binding structure prediction. Eli Lilly partnership $1.75B; partnership with Novartis. Targeting first Phase I trials within 2026 in oncology and immunology; no Isomorphic-originated compounds are in the clinic yet.

### 4.2 AlphaFold 3 and Structural AI

- AlphaFold 3 released May 8, 2024. Models protein-protein, protein-ligand, and protein-nucleic-acid complexes.
- Reported effect on the hit-to-lead stage of drug discovery: compressed from years to months for eligible programs.
- AlphaFold Server provides free access to most capabilities for academic and non-commercial use.
- Competing models: Baidu, ByteDance, Chai Discovery, Ligo Biosciences have released proprietary successors. A Columbia-led group is building OpenFold3 as a fully open-source alternative (targeted end of 2026).
- Baseline drug-development economics: approximately $2.5B per approved drug (risk-adjusted for failures); typical 12–15 year timeline from discovery to approval.

### 4.3 AI in Clinical Trial Operations

- Enrollment improvement from AI-driven eligibility matching: up to 65% rate lift; 3x faster candidate identification; reported 96% accuracy in top systems.
- Protocol design with AI: one top-5 pharma reports approximately 10% reduction in patient burden and $5–$10M saved per trial.
- Trial timeline compression: approximately 30–50% (vendor-side claim); 15–30% under more conservative published estimates.
- R&D baseline: approximately $200B/year industry-wide, of which approximately 40% is clinical-trial spend.
- ClinicalReTrial framework (2026) reportedly improved 83.3% of protocols with an average success probability increase of 5.7 percentage points.

### 4.4 Pharmacovigilance

- EMA GVP 2026 overhaul moves AI signal detection into the expected-baseline category (see §1.4).
- CDER Emerging Drug Safety Technology Program continues to be the FDA conduit for AI-enabled pharmacovigilance interaction with sponsors.
- Regulators expect AI-assisted signals to be explainable, traceable, inspection-ready, and reviewed by humans.

## 5. Safety, Liability, and Known Incidents

### 5.1 Epic Sepsis Model

- External validation on approximately 38,500 hospitalizations (JAMA Internal Medicine): missed approximately 67% of sepsis patients; identified only 7% of cases that clinicians missed; generated alerts on approximately 18% of all hospitalizations.
- Consequence: large alert-fatigue burden with limited clinical upside. Epic revamped the model in 2022 in response.
- Repository-relevant pattern: a verifier (the clinician responding to the alert) is expensive and saturates under alert volume; the cost of a false positive is not zero, it is alert fatigue that degrades human response on true positives. Standard FMEA detection scores understate this effect.

### 5.2 UnitedHealthcare nH Predict

- Alleged 90% error rate when overriding physician determinations for skilled-nursing-facility decisions. Class action filed 2023, still active in federal court as of March 2026.

### 5.3 AI Scribe Hallucination Risk

- AI scribe outputs are subject to hallucination: fabricated quotes, omitted complaints, misattributed symptoms. These appear credible inside the chart and can propagate into downstream care.
- Liability framework remains unsettled. Case-by-case judgment on whether the physician, the vendor, or both are liable. California AB 2013, Colorado AI Act, and the FDA/EMA joint principles are the closest to stable anchors in early 2026.

### 5.4 Malpractice and False Claims Act Surface

- False Claims Act enforcement has increased against providers and vendors who relied on flawed AI for billing codes or diagnostic results.
- Malpractice posture in 2026: physicians remain the primary liable party for AI-assisted decisions, with vendor liability possible on a case-by-case basis. AI-specific compliance programs are emerging as the expected standard.

## 6. Medical LLM Benchmarks

- MedQA, 2025–2026: OpenAI GPT-5 reached 95.84% (+4.80% over GPT-4o); Med-Gemini 91.1% with uncertainty-guided search.
- USMLE (GPT-5, all steps average): approximately 95.22%, exceeding typical human passing thresholds.
- Clinical transcription (not MedQA): JSL-LLM 74.9%, GPT-5 72.6%, Gemini 2.5 Pro 72.4%, Claude Sonnet 4 71.6%. Note: transcription is a different and harder task than multiple-choice MedQA; benchmarks that headline MedQA do not generalize.
- Med-Gemini SOTA on 10 of 14 public medical benchmarks; on seven multimodal benchmarks (including NEJM image challenge) outperformed GPT-4 by approximately 44.5% relative margin.
- Implication for cost modeling: medical-LLM scoreboard leaders rotate quickly and per-task ranking varies; do not price a healthcare AI system to one headline score.

## 7. Reporting-Guideline Gaps

- SPIRIT-AI, CONSORT-AI, DECIDE-AI remain the three principal reporting-guideline extensions for AI in clinical research.
- SPIRIT 2025 and CONSORT 2025 (non-AI, general) do not include dedicated AI sections. A May 2025 Lancet comment flagged this as a notable omission; the AI-specific extensions continue to be the operative guidance.
- Practical impact: papers claiming clinical benefit from AI remain hard to compare across studies because reporting is heterogeneous. Health-system procurement for AI should treat vendor-submitted study data as low-standardization evidence unless it explicitly follows CONSORT-AI or DECIDE-AI.

## 8. Vendor Pricing Anchor Table

| Category | Vendor and product | Price anchor | Unit | Note |
| --- | --- | --- | --- | --- |
| Ambient scribe | Abridge | ~$208 | per provider/month | Enterprise; ~150 US health-system contracts |
| Ambient scribe | Suki | $299–$399+ | per provider/month | Enterprise; 100+ clinician systems |
| Ambient scribe | Nuance DAX Copilot | Enterprise | N/A (negotiated) | Through Microsoft; 3–6 month implementation |
| Structural bio | AlphaFold Server (DeepMind) | Free | per run, academic/non-commercial | Commercial alternatives are proprietary |
| Imaging AI | Category I CPT 75580 (FFR-CT) | RVU-based | per exam | Effective January 2025 |
| Imaging AI | Category I CPT 75577 (AI CCTA plaque) | RVU-based | per exam | Effective January 1, 2026 |
| HIPAA-compliant AI platform | Range across vendors | $30–$697 | per user/month or one-time | Wide variance reflects scope and BAA coverage |
| HIPAA non-compliance | OCR penalty example | $4.75M | one-time | 2024 mid-sized network case over missing BAA |

## 9. International Dimension

- **UK**: NHS EDITH screening trial is the world's largest AI-led breast cancer screening evaluation (§3.1). The arbitration surge is the clearest public data point on verifier-saturation cost in a real deployment.
- **Korea**: regulatory-approval cadence accelerating (§3.3); domestic imaging AI (Lunit, VUNO, Samsung) is moving from pilot to revenue-phase deployment. The Korean Ministry of Food and Drug Safety maintains a separate medical AI approval pathway that coexists with CE and FDA routes, and approval numbers per year are now a tracked industry metric.
- **EU**: the Act / MDR interaction and the December 2025 Commission proposal (§1.2) create a moving regulatory surface through 2026–2027.
- **US**: the combination of FDA SaMD lifecycle guidance, state AI laws (Colorado, California), and OCR HIPAA enforcement creates a multi-jurisdictional compliance cost stack that is distinct from any other sector in the repository.

## 10. Pointers to Repository Frameworks

Evidence points link to framework locations as follows:

- §1 regulatory evidence feeds [`../frameworks/skill-domain-taxonomy.md`](../frameworks/skill-domain-taxonomy.md) §7 (compliance overlay as a third cost layer) and [`../frameworks/ai-system-lifecycle.md`](../frameworks/ai-system-lifecycle.md).
- §2–§4 adoption and operational evidence feeds [`../reports/industry-scenarios.md`](../reports/industry-scenarios.md) (healthcare-bio scenarios are added in [`../reports/healthcare-bio-ai-special-topic.md`](../reports/healthcare-bio-ai-special-topic.md)) and [`../frameworks/scenario-cost-assumptions.md`](../frameworks/scenario-cost-assumptions.md).
- §5 safety and liability evidence feeds [`../frameworks/failure-taxonomy.md`](../frameworks/failure-taxonomy.md) and the FMEA practice described in [`../frameworks/ai-system-operations.md`](../frameworks/ai-system-operations.md).
- §6 benchmark evidence feeds evaluation practice in [`../frameworks/evaluation-framework.md`](../frameworks/evaluation-framework.md).
- §8 pricing anchors feed [`../frameworks/scenario-cost-assumptions.md`](../frameworks/scenario-cost-assumptions.md) and [`../frameworks/ai-system-economics.md`](../frameworks/ai-system-economics.md).

## Sources

- [Marketing Submission Recommendations for a Predetermined Change Control Plan for AI-Enabled Device Software Functions — FDA](https://www.fda.gov/regulatory-information/search-fda-guidance-documents/marketing-submission-recommendations-predetermined-change-control-plan-artificial-intelligence)
- [PCCP final guidance final PDF — FDA](https://www.fda.gov/media/166704/download)
- [Predetermined Change Control Plans: Guiding Principles — PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC12577744/)
- [FDA PCCP Guide for AI/ML SaMD — IntuitionLabs](https://intuitionlabs.ai/articles/fda-pccp-implementation-guide-ai-ml-samd)
- [FDA Guidance on AI Medical Devices: PCCP — Medmarc](https://medmarc.com/life-sciences-news-and-resources/blog/fda-guidance-on-ai-medical-devices-predetermined-change-control-plans)
- [AI-Enabled Medical Devices list — FDA](https://www.fda.gov/medical-devices/software-medical-device-samd/artificial-intelligence-enabled-medical-devices)
- [Artificial Intelligence in Software as a Medical Device — FDA](https://www.fda.gov/medical-devices/software-medical-device-samd/artificial-intelligence-software-medical-device)
- [FDA Oversight: Understanding the Regulation of Health AI Tools — Bipartisan Policy Center](https://bipartisanpolicy.org/issue-brief/fda-oversight-understanding-the-regulation-of-health-ai-tools/)
- [FDA Digital Health Technology Guidance Requirements — IntuitionLabs](https://intuitionlabs.ai/articles/fda-digital-health-technology-guidance-requirements)
- [FDA AI/ML SaMD Compliance Guide — IntuitionLabs](https://intuitionlabs.ai/articles/fda-ai-ml-samd-guidance-compliance)
- [EU AI Act and Medical Devices: Navigating High-Risk Compliance — Reed Smith](https://www.reedsmith.com/our-insights/blogs/viewpoints/102kq35/the-eu-ai-act-and-medical-devices-navigating-high-risk-compliance/)
- [AI Act Guidelines for Medical Device Manufacturers 2026 — QuickBird Medical](https://quickbirdmedical.com/en/ai-act-medical-devices-mdr/)
- [EU AI Act High-Risk Compliance: Pharma and Medical Devices — IntuitionLabs](https://intuitionlabs.ai/articles/eu-ai-act-pharma-medical-device-compliance)
- [EU AI Act Has Arrived compliance timeline — Gardner Law](https://gardner.law/news/eu-ai-act-compliance-timeline)
- [Simplification or Back to Square One: EU Medical AI Regulation — Petrie-Flom](https://petrieflom.law.harvard.edu/2026/03/05/simplification-or-back-to-square-one-the-future-of-eu-medical-ai-regulation/)
- [MDCG 2025-6 guidance PDF — European Commission](https://health.ec.europa.eu/document/download/b78a17d7-e3cd-4943-851d-e02a2f22bbb4_en?filename=mdcg_2025-6_en.pdf)
- [FDA and EMA Provide Guiding Principles for AI in Drug Development — McGuireWoods](https://www.mcguirewoods.com/client-resources/alerts/2026/1/fda-and-ema-provide-guiding-principles-for-ai-in-drug-development/)
- [EMA GVP Updates 2026 — DDReg Pharma](https://resource.ddregpharma.com/blogs/drug-safety-just-got-smarter-inside-the-emas-2026-gvp-updates-overhaul/)
- [CIOMS WG XIV draft report — CIOMS](https://cioms.ch/wp-content/uploads/2022/05/CIOMS-WG-XIV_Draft-report-for-Public-Consultation_1May2025.pdf)
- [CDER EDSTP — FDA](https://www.fda.gov/drugs/science-and-research-drugs/cder-emerging-drug-safety-technology-program-edstp)
- [6 Health Systems Enhancing Care Delivery with Ambient AI Scribes — AHA](https://www.aha.org/aha-center-health-innovation-market-scan/2026-04-14-6-health-systems-enhancing-care-delivery-ambient-ai-scribes)
- [Ambient AI scribes and administrative burden — PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC12492056/)
- [Policy brief: ambient AI scribes and the coding arms race — PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC12738533/)
- [Nuance DAX cohort study — PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC10990544/)
- [Nuance DAX Copilot — Nuance](https://www.nuance.com/healthcare/dragon-ai-clinical-solutions/dax-copilot/infographic/move-beyond-scribes-to-automatically-document-care.html)
- [AI medical scribe comparison 2026 — Orbdoc](https://orbdoc.com/compare/ai-medical-scribe-comparison-2025/)
- [Suki pricing 2026 — Healos](https://healos.ai/blog/suki-pricing-features-cost-and-the-best-alternatives-in-2026)
- [BCBS: AI coding tools driving up medical bills — STAT News](https://www.statnews.com/2026/03/09/bcbs-study-hospitals-use-ai-upcoding-drive-up-prices/)
- [AI coding hospital spending study — HFMA](https://www.hfma.org/fast-finance/ai-hospital-coding-costs-study/)
- [AMA 2026 CPT updates for AI-augmented billing — Unislink](https://unislink.com/rcm-best-practices-blog/the-amas-2026-cpt-updates-what-physician-groups-need-to-know-about-ai-augmented-codes/)
- [AI is turning the healthcare revenue cycle into an operating system — STAT News](https://www.statnews.com/sponsor/2026/03/30/ai-is-turning-the-healthcare-revenue-cycle-into-an-operating-system/)
- [7 Prior Authorization Updates for 2026 — Becker's Payer Issues](https://www.beckerspayer.com/payer/5-prior-authorization-updates-for-2026/)
- [AI Prior Authorization 82% Overturn Rate — AI2Work](https://ai2.work/blog/ai-prior-authorization-tools-have-an-82-overturn-rate-and-that-s-the-problem)
- [Medicare Advantage AI prior authorization review — npj Digital Medicine](https://www.nature.com/articles/s41746-026-02387-x)
- [Insurers Pledge to Improve Prior Authorization — Fix Prior Auth](https://fixpriorauth.org/insurers-pledge-improve-prior-authorization)
- [EviCore prior authorization investigation — ProPublica](https://www.propublica.org/article/evicore-health-insurance-denials-cigna-unitedhealthcare-aetna-prior-authorizations)
- [UnitedHealthcare denial rate 2026 — Muni Health](https://muni.health/blog/uhc-denial-rate-statistics-2026)
- [Hospitals face AI governance gaps — Becker's Hospital Review](https://www.beckershospitalreview.com/healthcare-information-technology/ai/hospitals-face-ai-governance-gaps-heading-into-2026-report-finds/)
- [Healthcare AI governance maturity model — npj Digital Medicine](https://www.nature.com/articles/s41746-026-02418-7)
- [AI Governance in Healthcare 2026 Guide — Thinking Company](https://thinking.inc/en/industry-service/healthcare-ai-governance/)
- [Healthcare AI Compliance in 2026 Beyond HIPAA — PiTech](https://pitechsol.com/blog/healthcare-ai-compliance-in-2026/)
- [HIPAA Compliance for AI in Digital Health — Foley and Lardner](https://www.foley.com/insights/publications/2025/05/hipaa-compliance-ai-digital-health-privacy-officers-need-know/)
- [AI in Healthcare: Enforcement Risks and False Claims — Morgan Lewis](https://www.morganlewis.com/pubs/2025/07/ai-in-healthcare-opportunities-enforcement-risks-and-false-claims-and-the-need-for-ai-specific-compliance)
- [AI scribes pose liability risks — MICA Insurance](https://www.mica-insurance.com/blog/posts/ai-scribes-pose-liability-risks/)
- [Medical malpractice 2025: AI and lawsuits — Brandon J Broderick](https://www.brandonjbroderick.com/medical-malpractice-2025-how-ai-healthcare-changing-lawsuits)
- [How physicians might get in trouble using AI — PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC12309835/)
- [Medical hallucination in foundation models — arXiv 2503.05777](https://arxiv.org/html/2503.05777v2)
- [NHS AI breast cancer detection 25% interval cancers — ResultSense](https://www.resultsense.com/news/2026-03-11-google-ai-breast-cancer-detection-nhs)
- [NHS AI cancer screening trust challenge — ResultSense](https://www.resultsense.com/news/2026-03-11-nhs-ai-breast-cancer-trust-challenge)
- [World-leading AI trial to tackle breast cancer — GOV.UK](https://www.gov.uk/government/news/world-leading-ai-trial-to-tackle-breast-cancer-launched)
- [AIMS AI mammography screening — Imperial College London](https://www.imperial.ac.uk/global-health-innovation/what-we-do/research/healthcare-data-value-and-analytics/artificial-intelligence/ai-in-mammography-screening-aims/)
- [AI breast cancer screening feasibility — Nature Cancer](https://www.nature.com/articles/s43018-026-01127-0)
- [Radiology dominates FDA-cleared AI but reimbursement lags — Radiology Business](https://radiologybusiness.com/topics/artificial-intelligence/radiology-dominates-fda-cleared-ai-reimbursement-lags-far-behind)
- [Radiology AI reimbursement 2025 landscape — Ventra Health](https://ventrahealth.com/blog/ai-in-radiology-reimbursement-landscape-2025/)
- [Radiology CPT Code Revisions 2026 — AnnexMed](https://annexmed.com/radiology-cpt-code-updates-2026)
- [CCTA AI-powered plaque analysis reimbursement — Cardiovascular Business](https://cardiovascularbusiness.com/topics/cardiac-imaging/computed-tomography-ct/reimbursement-expected-drive-implementation-ccta-ai-powered-plaque-analysis)
- [AI Drug Discovery 2026 Pipeline — BioMedNexus](https://biomednexus.com/ai-drug-discovery-companies-clinical-candidates-2026/)
- [AI drugs reach Phase III 2026 — Humai](https://www.humai.blog/ai-discovered-drugs-reach-phase-iii-and-2026-will-determine-whether-all-the-promises-were-real/)
- [AI drugs reach the clinic: first large-scale test — Humai](https://www.humai.blog/ai-drugs-reach-the-clinic-2026-is-the-year-of-the-first-large-scale-test/)
- [Isomorphic Labs IsoDDE Drug Design Engine — Isomorphic Labs](https://www.isomorphiclabs.com/articles/the-isomorphic-labs-drug-design-engine-unlocks-a-new-frontier)
- [Isomorphic Labs IsoDDE and Eli Lilly Novartis deals — Deep Signal](https://deepsignal-app.com/en/articles/isomorphic-labs-isdde-alphafold-drug-discovery-2026)
- [AlphaFold 3 blog — Google DeepMind / Isomorphic](https://blog.google/innovation-and-ai/products/google-deepmind-isomorphic-alphafold-3-ai-model/)
- [AlphaFold3 overview and performance — PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC12027460/)
- [AlphaFold is running out of data — Nature](https://www.nature.com/articles/d41586-025-00868-9)
- [Biggest biotech AI fundraise 2026 — PharmaVoice](https://www.pharmavoice.com/news/biggest-biotech-fundraise-ai-capital-isomorphic-insilico/744435/)
- [AI clinical development pipeline — IntuitionLabs](https://intuitionlabs.ai/articles/ai-drug-development-pipeline)
- [AI in clinical trials — Clinion](https://www.clinion.com/insight/ai-in-clinical-trials/)
- [Artificial intelligence for clinical trial design — ESMO RWD Digital Oncology](https://www.esmorwd.org/article/S2949-8201(26)00001-9/fulltext)
- [AI clinical trial optimization — Lifebit](https://lifebit.ai/blog/ai-clinical-trial-optimization-guide-2026/)
- [AI in pharmacovigilance review — PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC12317250/)
- [AI governance in pharmacovigilance 2026 — Clinevotech](https://www.clinevotech.com/blog/ai-governance-pharmacovigilance-2026/)
- [Epic sepsis model external validation — JAMA Internal Medicine](https://jamanetwork.com/journals/jamainternalmedicine/fullarticle/2781307)
- [Epic sepsis model incident — AIAAIC repository](https://www.aiaaic.org/aiaaic-repository/ai-algorithmic-and-automation-incidents/epic-systems-sepsis-prediction-model)
- [Epic sepsis algorithm overhaul — STAT News](https://www.statnews.com/2022/10/03/epic-sepsis-algorithm-revamp-training/)
- [Medical AI approvals surge 2.5-fold in Korea — Seoul Economic Daily](https://en.sedaily.com/technology/2026/04/12/medical-ai-approvals-surge-25-fold-in-3-years-now)
- [Korea digital healthcare medical AI revenue era — Seoulz](https://www.seoulz.com/korea-digital-healthcare-medical-ai-enters-its-revenue-era/)
- [Korea Medical AI Powerhouse — BioSpectrum Asia](https://www.biospectrumasia.com/analysis/27/22930/south-korea-poised-to-become-medical-ai-powerhouse.html)
- [Digital Health Laws Korea 2026 — ICLG](https://iclg.com/practice-areas/digital-health-laws-and-regulations/korea)
- [Regulating AI in medical care South Korea — NCBI](https://www.ncbi.nlm.nih.gov/books/NBK613205/)
- [Medical Korea 2026 $30B bio-health ambition — GeneOnline](https://www.geneonline.com/the-30-billion-bio-health-ambition-south-korea-targets-global-top-three-ai-power-status-as-medical-korea-2026-opens-in-seoul/)
- [SPIRIT-AI extension — Nature Medicine](https://www.nature.com/articles/s41591-020-1037-7)
- [CONSORT-AI extension — Nature Medicine](https://www.nature.com/articles/s41591-020-1034-x)
- [DECIDE-AI reporting guideline — Nature Medicine](https://www.nature.com/articles/s41591-022-01772-9)
- [CONSORT 2025 and SPIRIT 2025 missing AI — The Lancet](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736(25)01268-1/fulltext)
- [Open Medical-LLM Leaderboard — Hugging Face](https://huggingface.co/blog/leaderboard-medicalllm)
- [LLM benchmarks in life sciences — IntuitionLabs](https://intuitionlabs.ai/articles/large-language-model-benchmarks-life-sciences-overview)
- [Med-PaLM research page — Google](https://sites.research.google/gr/med-palm/)
