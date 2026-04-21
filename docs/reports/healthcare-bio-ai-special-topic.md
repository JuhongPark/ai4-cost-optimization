# Healthcare-Bio AI Special Topic

## Purpose and Positioning

This report is a **special topic**, not a new spine of the research. It applies the repository's existing frameworks — [`../frameworks/cost-taxonomy.md`](../frameworks/cost-taxonomy.md), [`../frameworks/skill-domain-taxonomy.md`](../frameworks/skill-domain-taxonomy.md), [`../frameworks/ai-system-architecture.md`](../frameworks/ai-system-architecture.md), [`../frameworks/ai-system-lifecycle.md`](../frameworks/ai-system-lifecycle.md), [`../frameworks/ai-system-operations.md`](../frameworks/ai-system-operations.md), [`../frameworks/ai-system-economics.md`](../frameworks/ai-system-economics.md) — to healthcare, hospital, and pharmaceutical AI, and reports back what the frameworks handle cleanly, what they need to extend for this sector, and what becomes a genuinely open question.

Concrete 2026 data points behind every claim here live in [`../references/healthcare-bio-ai-evidence-2026.md`](../references/healthcare-bio-ai-evidence-2026.md). This report cites that note rather than restating numbers.

The main research spine (direct-vs-indirect cost, seven optimization strategies, productization-vs-sales domains, five industry scenarios) is unchanged by this special topic. Healthcare-bio AI enters as an additional evidence cut that stresses the framework in ways the existing sectors do not.

## 1. How the Two-Domain Lens Maps to Healthcare-Bio Subdomains

The sales-vs-productization split in [`../frameworks/skill-domain-taxonomy.md`](../frameworks/skill-domain-taxonomy.md) does not collapse under healthcare. It maps, but non-uniformly: different healthcare subdomains land on different points of the existing lens, and one cluster lands outside the two-domain plane because its binding property is clinical-harm exposure, not domain membership.

| Healthcare-bio subdomain | Closest existing domain | Fit quality | Dominant departure |
| --- | --- | --- | --- |
| Pharma medical affairs, KOL comms, payer market-access materials | Sales | Good | Regulated content review adds to human review cost |
| Payer contract and rebate negotiation | Sales | Good | Near-standard sales-domain profile |
| Drug-discovery structural bio (AF3-class protein-ligand prediction, generative chemistry) | Productization | Good | Verifier is a slow biological assay, not a test suite |
| Clinical trial protocol drafting and regulatory submission writing | Productization (conceptual-docs cluster §5 of the skill-domain taxonomy) | Medium | Audit-grade traceability; slow verifier |
| Medical coding / AI revenue cycle | Productization (document extraction analogue) | Medium | False Claims Act tail; payer-side upcoding signal |
| Ambient clinical scribing | Hybrid (productization-operated, expensive verifier, regulated output) | Poor with either domain alone | Clinician-verifier saturation; clinical-harm tail |
| AI clinical decision support (sepsis alerting, triage) | Hybrid | Poor | Alert fatigue; verifier *degrades* with volume |
| Diagnostic imaging AI second reader | Hybrid | Poor | SaMD-regulated; verifier arbitration cost spikes |
| AI prior authorization (payer side) | Hybrid leaning sales-domain fat-tail | Medium | Fat-tailed regulatory tail, appealed-overturn cycle |
| Pharmacovigilance signal detection | Hybrid (investment-domain-like scrutiny + ops-like volume) | Medium | GVP-mandated; human sign-off expected |
| Patient-facing chat (symptom checker, adherence coach) | Hybrid | Poor | Off-label medical advice tail risk |

The hybrid rows are where healthcare-bio AI departs most from every sector currently in the repository. They have three correlated properties that do not appear together in sales or productization:

1. **The verifier is an expensive human (clinician) who saturates.** NHS EDITH arbitration demand surged 142% at one site when AI replaced one of two radiologists (evidence §3.1). Epic sepsis alerting generated alerts on 18% of all hospitalizations, missed 67% of true cases, and degraded clinician response through alert fatigue (evidence §5.1). This is not "expensive verifier" as in sales (where the verifier is scarce but not saturation-prone at that timescale) and not "cheap verifier" as in productization (where the verifier scales indefinitely). It is **a priced, capacity-bounded verifier that becomes less accurate as volume rises**.
2. **Failure cost is fat-tailed in clinical-harm units, not financial units.** A missed sepsis, a missed cancer, a spurious medication, a wrong-dose recommendation — these map onto malpractice exposure, FDA adverse-event reporting, and regulatory action, not onto a deal size or a deliverability damage curve.
3. **Compliance overlay stacks more layers than any other sector already covered.** FDA SaMD pathway with PCCP, HIPAA with BAA enforcement, state AI laws (Colorado, California), EU AI Act × MDR/IVDR, False Claims Act exposure for coding, and professional malpractice for scribing all overlap.

These three properties co-occur in the clinical-decision-adjacent cluster and should be called out as a **hybrid cluster with a clinician-as-verifier constraint**, not as a new top-level domain. The two-domain frame is preserved; this is a specialized overlay inside the hybrid band already registered in [`../frameworks/skill-domain-taxonomy.md`](../frameworks/skill-domain-taxonomy.md) §9.

## 2. Special-Topic Scenarios

Each scenario below extends the repository's industry-scenario set in [`industry-scenarios.md`](industry-scenarios.md) but does not replace any of them. Numbering is prefixed `HC-` so that the original five scenarios (P1–P3, S1–S2) remain the reference set for the main research.

### HC-1: Ambient Clinical Scribing

Typical workflow: microphone captures the patient encounter → AI transcribes and drafts a structured clinical note → clinician reviews, edits, and signs → note enters EHR → downstream coding and billing proceed from the signed note.

Cost profile (see [`../frameworks/cost-taxonomy.md`](../frameworks/cost-taxonomy.md) structure):

- direct cost: per-encounter tokens for transcription and note drafting; typically low per encounter
- indirect cost, marginal: clinician sign-off minutes per encounter (the priced resource is a physician at $150–$400/hour depending on specialty)
- indirect cost, fixed: FDA enforcement discretion for CDS (currently permissive, changing); HIPAA BAA with vendor; hospital AI governance committee review
- compliance overlay: HIPAA, state AI disclosure laws, professional liability posture on hallucinated quotes in chart
- failure cost shape: fat-tailed — a fabricated symptom or mistranscribed medication can propagate into subsequent visits and billing; malpractice exposure is real

Dominant policy questions:

- What signal should route an encounter to longer human review (complex specialty, non-English primary language, high-risk patient)?
- How should hallucination detection (self-consistency, citation to transcript, uncertainty scoring) be weighted against clinician review minutes saved?
- When does a stronger model pay back through fewer edits per signed note?

Concrete 2026 anchors: JAMA showed −13.4 EHR minutes and −16.0 documentation minutes per clinician per day; burnout fell from 51.9% to 38.8% in 30 days with AI scribing; Riverside Health reported +11% wRVU and +14% HCC documentation per encounter (evidence §2.1). Abridge is approximately $208/provider/month and Suki is $299–$399+/provider/month (evidence §2.2). These anchors make a per-encounter cost-quality frontier computable.

### HC-2: Diagnostic Imaging Second Reader (Breast Screening)

Typical workflow: mammogram acquired → AI flags suspicious findings → one or two radiologists review → if disagreement, an arbitration panel adjudicates → recall or biopsy decided → biopsy result is the delayed ground truth.

Cost profile:

- direct cost: per-exam AI inference; near-negligible relative to radiologist reading time
- indirect cost, marginal: radiologist reading minutes; arbitration-panel minutes when AI and human disagree
- indirect cost, fixed: SaMD submission (510(k) or De Novo with PCCP), post-market surveillance, drift monitoring, hospital-level AI governance integration
- compliance overlay: FDA SaMD, EU AI Act high-risk (pending December 2025 Commission proposal), MDR, national screening-program rules
- failure cost shape: fat-tailed on false negatives (missed cancer → worse outcome and malpractice exposure); structural on false positives (unnecessary biopsies, patient anxiety)

Dominant policy questions:

- Is the correct operating point AI-replaces-one-reader (large capacity gain, large arbitration surge) or AI-as-safety-net (small capacity gain, small arbitration surge, high confidence in workflow continuity)?
- How should arbitration-panel minutes be priced into the total cost equation? The NHS EDITH preliminary result (142% arbitration demand surge at one site) shows this is not a small line item.
- What does the PCCP cover and what requires a new submission? Retraining on drift is the recurring trigger that determines annual compliance cost.

Anchor data (evidence §3.1, §3.2): NHS EDITH trial, approximately 700K women, £11M government support, 25% additional interval-cancer detection, 40% workload reduction as second reader, 142% arbitration surge at one site. Reimbursement: only two Category I CPT codes for new radiology AI as of January 2026 (75580 FFR-CT and 75577 CCTA plaque) — most FDA-cleared imaging AI does not yet have a payment pathway.

### HC-3: Clinical Decision Support and Early-Warning Alerts (Sepsis Archetype)

Typical workflow: EHR data streams into a scoring model → model emits a risk score → threshold triggers an alert in the clinician's workflow → clinician decides whether to act → outcome ground truth (sepsis developed, patient stable) arrives hours to days later.

This is the archetype where the repository's generic FMEA approach in [`../frameworks/ai-system-operations.md`](../frameworks/ai-system-operations.md) needs the alert-fatigue extension. The Epic Sepsis Model (evidence §5.1) generated alerts on approximately 18% of all hospitalizations and missed approximately 67% of true sepsis cases in an independent validation. The quiet failure mode is not a single alert being wrong; it is the **aggregate degradation of clinician response rates under sustained false-positive load**. Standard FMEA detection scoring treats each alert independently; that understates this mechanism systematically.

Cost profile:

- direct cost: per-patient scoring — negligible
- indirect cost, marginal: clinician-seconds per alert, multiplied by alert volume per shift; the hidden cost line is *the attention cost of the true positives that are missed because clinicians have tuned out after the tenth false positive of the day*
- indirect cost, fixed: SaMD lifecycle, hospital AI governance, drift monitoring, post-market adverse-event reporting
- compliance overlay: FDA CDS (pre-2026) vs FDA SaMD (post-2026 guidance updates)
- failure cost shape: fat-tailed; catastrophic on missed deterioration events

Policy questions:

- What saturation model correctly captures alert fatigue, so that the score threshold optimizes against *aggregate clinician response accuracy under load* rather than per-alert precision?
- How should the retraining PCCP be structured so drift triggers retraining *before* a run of false positives consumes the clinical attention budget?
- When should the model defer (no alert) rather than risk alert-fatigue contribution?

### HC-4: AI Prior Authorization (Payer Side)

Typical workflow: provider submits a prior-auth request → payer AI scores the request → denial or approval is issued → provider appeals → reviewer (human or AI) reconsiders → outcome.

This scenario sits closer to the sales-domain fat-tail than to the productization plane: the output is a counterparty-directed decision with fat-tailed regulatory exposure (class actions, CMS compliance reporting, state insurance commissioner oversight). The AI-driven 82% appeal-overturn rate in Medicare Advantage (evidence §2.4) is a direct readout that the model's operating point is mis-calibrated relative to what review boards accept.

Cost profile:

- direct cost: per-request inference — small
- indirect cost, marginal: denial → appeal → human reviewer minutes; per-case cost rises sharply for cases that reach administrative law judges
- indirect cost, fixed: AHIP-pledged reforms by January 1, 2026; class-action defense reserves; class-action discovery cost when orders hit (UnitedHealthcare nH Predict: broad discovery ordered March 2025, active March 2026)
- compliance overlay: CMS rules, state-level AI laws (Colorado, California), HIPAA, False Claims Act exposure
- failure cost shape: fat-tailed; single adverse class-action rulings can reset operating-point policy across an entire payer line of business

### HC-5: Drug Discovery Agentic Workflow (Structural + Generative)

Typical workflow: target → structure prediction (AF3-class) → generative chemistry proposes ligand candidates → ADMET prediction filters candidates → in-silico screen → in-vitro assay → iterate.

This is the clearest productization-domain analogue inside healthcare-bio AI, but with two non-standard properties:

- the "verifier" is an **assay with hours-to-weeks latency**, not a test suite. The feedback loop is longer than any productization case in the repository's existing scenarios.
- the **per-task compute profile** is dominated by specialty models (structural biology, generative chemistry) running on GPU-heavy infrastructure. This is where the repository's semi-fixed cost category becomes visible: IsoDDE-class or AF3-class model access is a semi-fixed cost tied to vendor contract tier, not a pure marginal cost.

Cost profile:

- direct cost: model access (AF3, IsoDDE, proprietary successors), agent inference, literature-search APIs
- indirect cost, marginal: medicinal chemist review per candidate batch; assay cost per candidate
- indirect cost, fixed: enterprise model licensing, internal data lake governance, GxP-aligned documentation for any molecule entering an IND
- compliance overlay: GxP, FDA/EMA joint AI principles (January 2026), CIOMS WG XIV principles for AI use where it informs safety decisions
- failure cost shape: mostly thin-tailed at the screening stage (bad candidates discarded cheaply); fat-tailed once a compound advances — the REC-994 post-long-term-data discontinuation (evidence §4.1) is the concrete reminder that early-stage AI signal does not guarantee Phase III efficacy

Representative anchors: approximately 173 AI-discovered drug programs in clinical development globally; 15–20 entering large-scale trials in 2026; Isomorphic $1.75B Eli Lilly partnership; first AF3-designed molecules expected to reach human trials by end of 2026 (evidence §4.1, §4.2).

### HC-6: AI Clinical Trial Protocol Design and Recruitment

Typical workflow: draft protocol → AI proposes design optimizations and eligibility criteria → biostatistics and clinical-operations review → protocol finalized → AI matches candidates to sites → sites enroll.

Cost profile:

- direct cost: per-protocol and per-candidate inference; small relative to trial cost
- indirect cost, marginal: clinical-operations and biostatistics reviewer hours; investigator coordinator time for eligibility confirmation
- indirect cost, fixed: EDC / RWD integration, CONSORT-AI / SPIRIT-AI / DECIDE-AI reporting infrastructure, regulatory agency AI-disclosure posture
- compliance overlay: GxP, GCP, FDA/EMA joint AI principles, site IRB AI-disclosure rules
- failure cost shape: structural on minor eligibility errors; fat-tailed if AI-introduced bias skews enrollment

Representative anchors (evidence §4.3): $5–$10M saved per trial on protocol design at one top-5 pharma; 65% enrollment rate improvement; 15–30% conservative trial-duration reduction; R&D baseline approximately $200B/year industry-wide with approximately 40% in clinical trials.

## 3. Extending the Cost Taxonomy for Healthcare

The direct-vs-indirect split in [`../frameworks/cost-taxonomy.md`](../frameworks/cost-taxonomy.md) applies cleanly. The sector-specific items below slot into existing categories rather than creating new ones.

### 3.1 Direct cost additions

- **structural-bio compute**: AF3-class protein-ligand prediction is a specialty inference line. Access is generally through a vendor agreement (Isomorphic, proprietary enterprise clones) or a self-hosted open model (OpenFold3, expected end of 2026). This is a semi-fixed direct cost (subscription tier), not pure per-token marginal cost.
- **medical-LLM vs general-LLM spread**: specialty medical LLMs (JSL-LLM at 74.9% on clinical transcription vs GPT-5 72.6%, evidence §6) narrow but do not close the domain-model gap. Pricing differences can be meaningful at hospital scale; the decision is a routing decision per the skill-domain priority table.

### 3.2 Indirect cost additions

- **clinician-minute as the priced resource**: physician cost per minute sits around $2.50–$6.50 depending on specialty; nurse cost per minute around $0.70–$1.50. This is materially higher than generic knowledge-worker minutes already modeled in the repository. Every healthcare scenario should declare the priced-minute unit explicitly in its scenario-cost-assumptions row.
- **alert-fatigue saturation**: the clinician-as-verifier resource saturates non-linearly with alert volume. A linear "minutes per alert" model understates degradation. This is a concrete candidate for tail-conditioning in [`../frameworks/cost-aggregation.md`](../frameworks/cost-aggregation.md) (fat-tail and domain-conditioned reporting), distinct from agentic resource exhaustion already covered in [`../references/industry-updates-2026-04.md`](../references/industry-updates-2026-04.md) §4.
- **arbitration-panel cost**: where the workflow disagrees with the AI, adjudication creates a third cost layer (panel hours per contested case). NHS EDITH is the reference data point; the cost line was not visible before.

### 3.3 Fixed and semi-fixed cost additions

- **FDA SaMD submission and PCCP maintenance**: 510(k) / De Novo / PMA preparation plus PCCP documentation is a one-time-plus-maintenance fixed cost. The PCCP lets the manufacturer update the model without a new submission *within* the planned modifications; changes outside the plan still trigger a new submission. This is a "semi-fixed step cost" in the sense of [`../frameworks/cost-taxonomy.md`](../frameworks/cost-taxonomy.md) §3.
- **HIPAA BAA and 2026 Security Rule overhaul**: fixed gate. The 2024 $4.75M penalty for a mid-sized hospital network over an un-BAA'd AI vendor (evidence §1.7) sets the lower-bound exposure for missing this fixed cost.
- **multi-jurisdictional compliance stack**: FDA + EU AI Act + MDR/IVDR + Colorado + California + professional liability. Each layer is an annualized fixed or step cost; a deployment that spans jurisdictions cannot elide any of them.
- **clinical validation infrastructure**: SPIRIT-AI protocol, CONSORT-AI reporting, DECIDE-AI early-stage reporting. Running even a small prospective study that meets these guidelines costs six to seven figures, and procurement from major health systems increasingly requires it.

## 4. Compliance Overlay Addition

This sector extends [`../frameworks/skill-domain-taxonomy.md`](../frameworks/skill-domain-taxonomy.md) §7 (compliance overlay as a third cost layer) with a healthcare-bio row. The shape is distinctive because the overlay combines annualized maintenance with submission-triggered step cost.

| Dimension | Healthcare-bio |
| --- | --- |
| Cost shape | Multi-jurisdictional annualized plus submission-triggered step |
| Overlay strategy | Single unified QMS covering MDR, FDA QMSR (effective February 2, 2026), ISO 13485, plus HIPAA Security Rule plus AI-specific layer (EU AI Act, state AI laws) plus GxP overlay for pharma |
| Annual overlay band | $400K–$3M/yr for a hospital-system AI portfolio across 3–5 SaMD tools; $1M–$10M+/yr for a large pharma managing a portfolio of AI-assisted pipeline assets |
| Submission-step cost | 510(k): approximately $100K–$500K per submission including consulting and clinical-data generation. De Novo: $500K–$2M. PMA: $2M–$10M+. PCCP authoring is typically $50K–$250K. |

This band is higher than any sector already covered. It supports scoring compliance cost as a binding gate in healthcare-bio deployments: many AI projects are rejected at the fixed-cost gate before any marginal-cost comparison is done.

## 5. Lifecycle Extension

[`../frameworks/ai-system-lifecycle.md`](../frameworks/ai-system-lifecycle.md) describes a generic lifecycle (PoC → pilot → production → steady state → deprecation). Healthcare-bio adds sector-specific gates that should be stacked on top:

- **Pre-market**: dataset curation with HIPAA-compliant de-identification; model development; internal silent validation; SPIRIT-AI-aligned prospective study protocol; DECIDE-AI early-stage evaluation; FDA submission with PCCP; EU AI Act conformity assessment where applicable.
- **Deployment**: EHR integration; hospital AI governance committee review; implementation (3–6 months for ambient scribing per evidence §2.2); physician training; go-live with monitoring thresholds set.
- **Steady state**: drift monitoring against PCCP-defined triggers; adverse-event reporting (FDA MedWatch, EU MDR Vigilance); PCCP-triggered retraining; periodic re-validation against updated clinical evidence.
- **Decommission**: archiving audit-grade logs under HIPAA retention; vendor BAA sunset; documentation of decommission in the quality system.

The two lifecycle properties that most differ from generic enterprise AI are: **retraining is a regulated event, not just an engineering event**, and **adverse events are externally reportable with statutory timelines**. Neither is adequately captured by the generic lifecycle doc and should be added there as a sector-specific overlay rather than inside the generic text.

## 6. FMEA Illustration: Ambient Scribing Hallucination

The repository's FMEA posture (per [`../frameworks/ai-system-operations.md`](../frameworks/ai-system-operations.md) and the user's MIT-SDM preference) uses **Action Priority (AP) logic**, not multiplicative RPN. AP uses a lookup over (S, O, D) that correctly preserves the safety ordering that multiplicative RPN can scramble (severity 10 × occurrence 2 × detection 2 is the same number as severity 2 × occurrence 10 × detection 2, but the first is a safety event and the second is a noise problem).

Illustration for one failure mode in HC-1 ambient scribing:

- **Failure mode**: AI fabricates a symptom or medication dose in the draft note.
- **Effect**: wrong clinical decision downstream; patient harm; malpractice exposure; billing based on fabricated content can trigger False Claims Act exposure.
- **Severity**: high. Clinical harm possible. Symmetric regulatory tail if the fabricated content reaches billing.
- **Occurrence**: medium. Hallucination rate for medical content is low per turn but non-zero; it is encounter-level cumulative.
- **Detection**: medium-to-low. The clinician is the detection mechanism, but sign-off review time is under pressure; documentation-heavy specialties generate more text per sign-off and reduce per-token scrutiny.
- **AP**: **High** under AIAG-VDA lookup for severity-high, occurrence-medium, detection-medium-low.
- **Required actions per AP = High**: architectural mitigation (constrained decoding for dosage and medication fields, mandatory citation-to-transcript for clinical assertions), workflow mitigation (structured sign-off UI that surfaces low-confidence spans), monitoring mitigation (post-signature audit sampling, drift monitoring on hallucination-prone field categories).

This treatment is more informative than a single RPN number because the mitigation shape (architectural + workflow + monitoring) is implied by the AP ranking, not left to the designer's synthesis.

## 7. Strategy Priority by Healthcare Scenario

The seven strategy families in [`../frameworks/strategy-taxonomy.md`](../frameworks/strategy-taxonomy.md) do not change. The per-scenario priority shifts.

| Scenario | Top 3 strategies in priority order | Rationale |
| --- | --- | --- |
| HC-1 Ambient scribing | 1. Verification (hallucination detection on clinical-fact fields) 2. Model selection (specialty medical LLM tier for dense-specialty notes) 3. Human escalation (tiered sign-off by note complexity) | Clinician-verifier is the priced resource; verification quality drives whether sign-off is fast |
| HC-2 Imaging second reader | 1. Human escalation (arbitration-panel routing policy) 2. Verification (SaMD-validated thresholds) 3. Model selection (SaMD-cleared model, not a general model) | Arbitration is where cost concentrates; thresholds determine arbitration volume |
| HC-3 CDS / sepsis alerting | 1. Difficulty-based routing (suppress alerts in low-prior contexts to protect attention budget) 2. Verification (time-of-day, patient-acuity gating) 3. Retry / self-correction (score re-check on new data, not alert-spam) | Alert fatigue is the binding cost; score precision alone is not the objective |
| HC-4 AI prior auth | 1. Human escalation (two-gate review before denial issues) 2. Verification (LLM-as-judge against clinical-guideline corpus) 3. Model selection (over-tuned models are the failure mode; keep a strong-baseline reference) | Fat-tailed regulatory cost dominates; the denial is the counterparty-facing artifact |
| HC-5 Drug discovery | 1. Model selection (specialty structural / generative models routed per stage) 2. Tool-use (assay-in-the-loop, data-platform quality) 3. Retry / self-correction (agent retry budget per stage) | Long-verifier loop; specialty models are semi-fixed cost and dominate the cost curve |
| HC-6 Trial protocol / recruitment | 1. Verification (clinical-ops review with traceability back to source data) 2. Tool-use (EDC / RWD integration quality) 3. Human escalation (biostats sign-off on AI-optimized designs) | Audit-grade traceability is the dominant cost driver, not per-call inference |

Compared with the productization-domain default priority in skill-domain §4.8 (model selection → verification → retry → difficulty routing → tool-use → human escalation → serving), the healthcare scenarios move **human escalation and verification up**, and in HC-5 promote **tool-use (assay-in-the-loop)** to a position usually occupied by retry in pure productization. This is because the healthcare-bio workflow depends on integration with non-AI systems (EHR, LIMS, EDC, CTMS) whose data quality and latency are a larger share of total cost than the agent's retry loop.

Compared with the sales-domain default (model selection → human escalation → tool-use → difficulty routing → verification → retry → serving), the healthcare scenarios (HC-4 most clearly) push **verification** higher than the sales default, because health-regulated review corpora (clinical guidelines, prior-auth criteria, formulary rules) are denser and more structured than sales collateral, so LLM-as-judge against a guideline corpus is materially more effective than LLM-as-judge against "is this proposal compelling."

## 8. Recommended Integration into the Repository

Adopting healthcare-bio as a special topic does not require restructuring the main research spine. The minimal integration:

- add this report and its evidence companion to the documentation hub (listed on a special-topic line in [`../README.md`](../README.md)) so that a reader who wants the sector-specific perspective can find it without disturbing the main reading order
- cross-reference from [`../frameworks/skill-domain-taxonomy.md`](../frameworks/skill-domain-taxonomy.md) §9 (hybrid cases) so that clinical-decision-adjacent workflows are recognized as a named hybrid cluster
- cross-reference from [`../frameworks/cost-taxonomy.md`](../frameworks/cost-taxonomy.md) §3 (fixed vs marginal) to surface the multi-jurisdictional compliance-overlay shape as a canonical example of a semi-fixed step cost
- add a "healthcare-bio" row to the compliance overlay table in [`../frameworks/skill-domain-taxonomy.md`](../frameworks/skill-domain-taxonomy.md) §7 when that table is next revised
- leave the first empirical cycle's benchmark plan unchanged; this topic is a special topic, not part of the core three-month cycle

Future option (not recommended for this cycle): if and when the repository runs a second empirical cycle, a single healthcare-bio scenario (HC-1 ambient scribing is the highest-signal candidate because of the dense 2026 evidence base and the clean cost-per-encounter model) could be added alongside the productization and sales scenarios. That would be a scope expansion decision, not a framework change.

## 9. Open Questions

These remain open after this special-topic pass and would be the natural next questions if the topic were escalated from "special" to "active."

1. **How should the alert-fatigue saturation curve be parameterized** so that CDS-style scenarios can report a cost-per-true-positive-preserved rather than a cost-per-alert? This is the strongest single modeling gap.
2. **Is the clinician-minute unit truly one parameter**, or should it be stratified by specialty and by on-call vs elective mode? The NHS arbitration-surge data suggests the latter but the evidence is sparse.
3. **How should post-market PCCP retraining cost be amortized** against per-episode cost so that direct and indirect cost stay comparable? The PCCP structure doesn't map one-to-one onto the existing fixed-vs-marginal lens.
4. **What is the right treatment of regulatory optionality** in healthcare-bio AI? The December 2025 EC proposal to remove medical devices from the EU AI Act high-risk scope is a live real-option on roughly $1–$3M/yr of compliance overlay per portfolio product. The repository's real-options framing in [`../frameworks/ai-system-economics.md`](../frameworks/ai-system-economics.md) should be applied here as a worked example.
5. **When does a self-hosted open-weight medical model (e.g., OpenFold3, open medical LLMs) overtake a proprietary medical-specialty offering** in total cost? The cross-over has been a mostly productization-domain question; in healthcare-bio it is moderated by SaMD submission cost which biases toward vendor-supplied clearances.

## 10. Scope and Non-Claims

This report is not a market analysis of healthcare AI vendors; it is a framework application. Where numbers are given, they come from [`../references/healthcare-bio-ai-evidence-2026.md`](../references/healthcare-bio-ai-evidence-2026.md), which cites primary sources. Vendor inclusion is not an endorsement and is confined to cases where the data point is load-bearing for the argument. The report does not attempt to compare AI tools on clinical-benefit grounds; that question belongs to clinical research, not cost optimization.
