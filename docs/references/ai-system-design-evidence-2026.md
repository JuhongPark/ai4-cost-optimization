# AI System Design Evidence (April 2026)

## Purpose

This reference collects the 2026 academic, industry, and standards-body evidence behind the four AI-system framework documents: [`../frameworks/ai-system-architecture.md`](../frameworks/ai-system-architecture.md), [`../frameworks/ai-system-lifecycle.md`](../frameworks/ai-system-lifecycle.md), [`../frameworks/ai-system-operations.md`](../frameworks/ai-system-operations.md), and [`../frameworks/ai-system-economics.md`](../frameworks/ai-system-economics.md). The organizing framing is MIT SDM systems engineering applied to AI — architecture as cost driver, lifecycle as decision horizon, FMEA and graceful degradation as first-class reliability tools, and lifecycle TCO in the Fabrycky-Blanchard tradition.

This note is organized by framework topic, not chronologically. For chronological industry updates see [`industry-trends-2026.md`](industry-trends-2026.md) and [`industry-updates-2026-04.md`](industry-updates-2026-04.md). For skill-domain-organized evidence see [`skill-domain-evidence-2026.md`](skill-domain-evidence-2026.md) and [`skill-domain-deep-dive-2026.md`](skill-domain-deep-dive-2026.md).

## 1. Multi-Agent Architecture and Topology

**Central claim:** topology choice dominates robustness to single malicious or faulty agents. Flat group-chat topologies collapse; Reflexion, Crowdsourcing, and Blackboard topologies contain failures via a filtering or voting step. Group size improves both accuracy and resilience but at monotonically growing token cost.

- Dao & Moser, `Designing Generative Multi-Agent Systems for Resilience`, CAS 2025 (MIT SDM Best Student Paper). ScienceDirect volume 268, pp. 130-138. https://www.sciencedirect.com/science/article/pii/S1877050925025311
- MIT SDM news page. https://sdm.mit.edu/research-practice/dao-best-paper-cas-2025/
- Dao SM SDM thesis on DSpace. https://dspace.mit.edu/handle/1721.1/162506
- AdaptOrch — task-adaptive multi-agent orchestration reports 12-23% uplift over any static topology. arXiv:2602.16873. https://arxiv.org/abs/2602.16873
- Multi-Agent Collaboration Mechanisms survey. arXiv:2501.06322. https://arxiv.org/html/2501.06322v1
- Taxonomy of Hierarchical Multi-Agent Systems. arXiv:2508.12683. https://arxiv.org/pdf/2508.12683
- RAPS publish-subscribe coordination. arXiv:2602.08009. https://arxiv.org/abs/2602.08009
- AgentNet++ hierarchical decentralized coordination. arXiv:2512.00614. https://arxiv.org/html/2512.00614
- Anthropic production research multi-agent system (Opus-4 lead plus Sonnet-4 workers): ~90% uplift over single-agent at ~15x the tokens. https://www.anthropic.com/engineering/multi-agent-research-system
- Anthropic effective harnesses for long-running agents. https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents

## 2. Memory Architecture

**Central framework:** CoALA (Cognitive Architectures for Language Agents) — working memory plus long-term split into semantic, episodic, procedural.

- Sumers, Yao, Narasimhan, Griffiths — `Cognitive Architectures for Language Agents (CoALA)`. arXiv:2309.02427. TMLR 2024. https://arxiv.org/abs/2309.02427
- Zep — Temporal Knowledge Graph Architecture for Agent Memory. arXiv:2501.13956. Episode plus semantic-entity plus community subgraphs. https://arxiv.org/html/2501.13956v1
- Production memory-layer vendors: Letta (formerly MemGPT), LangGraph memory, LangMem, Zep. Memory as first-class developer-editable object (Letta) vs implicit RAG by-product.

## 3. Orchestration Pattern

**Central trade-space:** ReAct (1x baseline) vs Plan-and-Execute / ReWOO (~0.15x token, ~0.27x latency, +~9% accuracy on structured multi-step) vs Reflexion (~2x token, better on hard reasoning) vs Tree-of-Thought / LATS (~3-5x token, highest on search-heavy).

- From Prompt-Response to Goal-Directed Systems — Evolution of Agentic AI Software Architecture. arXiv:2602.10479. https://arxiv.org/html/2602.10479v1
- Temporal vs LangGraph 2026 durable-agent architecture comparison. https://cordum.io/blog/temporal-vs-langgraph
- Agentic vs Deterministic Orchestration 2026. https://liviaerxin.github.io/blog/agentic-vs-deterministic-orchestration
- Model Context Protocol — 97M monthly SDK downloads by March 2026. IBM MCP architecture patterns. https://developer.ibm.com/articles/mcp-architecture-patterns-ai-systems/

## 4. Verification and Guardrail Architecture

**Central claim:** inline critique minimizes direct cost but loses failure containment; pipeline staging roughly doubles per-episode direct cost but converts unbounded-tail failures into bounded-per-gate cost.

- NVIDIA NeMo Guardrails developer page. https://developer.nvidia.com/nemo-guardrails
- NeMo Guardrails reports ~89% input-moderation accuracy; Llama Guard ~67% on prompt-injection category assignment.
- NVIDIA docs — Llama Guard integration in NeMo Guardrails. https://docs.nvidia.com/nemo/guardrails/latest/user-guides/community/llama-guard.html
- Production LLM Guardrails comparison — NeMo, Guardrails AI, Llama Guard. https://blog.premai.io/production-llm-guardrails-nemo-guardrails-ai-llama-guard-compared/
- LlamaFirewall open-source guardrail for secure AI agents. arXiv:2505.03574. https://arxiv.org/html/2505.03574v1

## 5. Lifecycle Management and Stage-Gate

**Central framework:** PoC → Pilot → Limited Production → GA → Steady-state → Deprecation, each with distinct quality/cost/risk bars. Evaluation as continuous governing function rather than terminal checkpoint.

- Breck, Cai, Nielsen, Salib, Sculley — `The ML Test Score: A Rubric for ML Production Readiness and Technical Debt Reduction`, Google Research 2017. https://research.google/pubs/the-ml-test-score-a-rubric-for-ml-production-readiness-and-technical-debt-reduction/
- Sculley et al. — `Hidden Technical Debt in Machine Learning Systems`, NeurIPS 2015. https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems
- Wang et al. — `Evaluation-Driven Development and Operations of LLM Agents` (EDDOps). arXiv:2411.13768. https://arxiv.org/html/2411.13768v3
- PromptDebt — comprehensive study of technical debt across LLM projects; prompt-design SATD at ~6.6% of commits. arXiv:2509.20497. https://arxiv.org/html/2509.20497v1
- Natural-Language Agent Harnesses. arXiv:2603.25723. https://arxiv.org/html/2603.25723v1
- Azure MLOps Maturity Model (levels 0-4). https://learn.microsoft.com/en-us/azure/architecture/ai-ml/guide/mlops-maturity-model
- MLOps and GenAIOps for AI Workloads on Azure (Well-Architected Framework). https://learn.microsoft.com/en-us/azure/well-architected/ai/mlops-genaiops
- Databricks Well-Architected Framework. https://learn.microsoft.com/en-us/azure/databricks/lakehouse-architecture/well-architected
- Hidden Technical Debt of GenAI Systems (Databricks). https://www.databricks.com/blog/hidden-technical-debt-genai-systems

### Model Update Management

- OpenAI API Deprecations. https://developers.openai.com/api/docs/deprecations
- Retiring GPT-4o and older models in ChatGPT (February 2026). https://openai.com/index/retiring-gpt-4o-and-older-models/
- Anthropic Responsible Scaling Policy v3.0 acts as parallel capability gate on the risk axis. https://www.anthropic.com/news/responsible-scaling-policy-v3
- LangChain 1.0 GA — legacy APIs under `langchain-classic`, no breaking changes until 2.0. https://blog.langchain.com/langchain-langgraph-1dot0/
- Releasing AI Features Without Breaking Production — shadow, canary, A/B (April 2026). https://tianpan.co/blog/2026-04-09-llm-gradual-rollout-shadow-canary-ab-testing
- Safely Deploying ML Models to Production (March 2026). https://www.marktechpost.com/2026/03/21/safely-deploying-ml-models-to-production-four-controlled-strategies-a-b-canary-interleaved-shadow-testing/

### Evaluation Regime

- OpenAI Evaluation Best Practices. https://platform.openai.com/docs/guides/evaluation-best-practices
- Promptfoo (OpenAI-acquired, MIT-licensed). https://github.com/promptfoo/promptfoo
- Arize Phoenix. https://github.com/Arize-ai/phoenix
- RAGAS evaluation framework. Referenced in 2026 tool surveys. https://www.braintrust.dev/articles/deepeval-alternatives-2026
- Calibrating LLM-as-a-Judge (LangChain). https://www.langchain.com/articles/llm-as-a-judge
- AutoRubric — Unifying Rubric-based LLM Evaluation. arXiv:2603.00077. https://arxiv.org/html/2603.00077v2

### Drift Detection

- Model Drift in Production 2026 (AllDaysTech runbook). https://alldaystech.com/guides/artificial-intelligence/model-drift-detection-monitoring-response
- Detecting drift in production applications (AWS Prescriptive Guidance). https://docs.aws.amazon.com/prescriptive-guidance/latest/gen-ai-lifecycle-operational-excellence/prod-monitoring-drift.html
- Understanding Model vs Data Drift in LLMs (orq.ai 2026 Guide). https://orq.ai/blog/model-vs-data-drift
- Fiddler AI — Monitor LLMOps Performance with Drift Monitoring. https://www.fiddler.ai/blog/how-to-monitor-llmops-performance-with-drift

## 6. Observability and OpenTelemetry GenAI

**Central observation:** three-tier SLI stack (infrastructure, quality, agent). Loop rate is the defining agent SLI. OpenTelemetry GenAI has crossed the credibility threshold.

- OpenTelemetry — semantic conventions for GenAI agent and framework spans. https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/
- OpenTelemetry — semantic conventions for generative AI systems. https://opentelemetry.io/docs/specs/semconv/gen-ai/
- OpenTelemetry — semantic conventions for generative AI metrics. https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-metrics/
- Datadog LLM Observability natively supports OpenTelemetry GenAI. https://www.datadoghq.com/blog/llm-otel-semantic-convention/
- Datadog Integrates Google Agent Development Kit into LLM Observability (February 2026). https://www.infoq.com/news/2026/02/datadog-google-llm-observability/
- Datadog LLM Observability cost docs — ~$0.10 per 1,000 tokens ingested across 800+ models. https://docs.datadoghq.com/llm_observability/monitoring/cost/
- Top LLM Observability Tools in 2026 (SigNoz). https://signoz.io/comparisons/llm-observability-tools/
- Langfuse vs Arize Phoenix comparison. https://langfuse.com/faq/all/best-phoenix-arize-alternatives
- 4 best LLM gateways for observability (Braintrust). https://www.braintrust.dev/articles/best-llm-gateways-observability-2026
- The complete guide to LLM observability for 2026 (Portkey). https://portkey.ai/blog/the-complete-guide-to-llm-observability/
- LLM Observability Explained (Splunk). https://www.splunk.com/en_us/blog/learn/llm-observability.html
- Why observable AI is the missing SRE layer (VentureBeat). https://venturebeat.com/ai/why-observable-ai-is-the-missing-sre-layer-enterprises-need-for-reliable
- AI Workloads Are About to Blow Up Your Observability Bill (OneUptime). https://oneuptime.com/blog/post/2026-04-01-ai-workload-observability-cost-crisis/view
- What Is Agent Observability? Traces, Loop Rate, Tool Errors, Cost per Successful Task (Towards AI, April 2026). https://pub.towardsai.net/what-is-agent-observability-traces-loop-rate-tool-errors-and-cost-per-successful-task-dda2287f6c83
- Best AI Observability Tools for Autonomous Agents 2026 (Arize). https://arize.com/blog/best-ai-observability-tools-for-autonomous-agents-in-2026/
- Anthropic — Demystifying evals for AI agents. https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents

### SRE-for-AI Maturity

- Gartner: LLM observability to 50% of GenAI deployments by 2028. https://www.gartner.com/en/newsroom/press-releases/2026-03-30-gartner-predicts-by-2028-explainable-ai-will-drive-llm-observability-investments-to-50-percent-for-secure-genai-deployment
- Gartner Cool Vendors in AI for SRE and Observability. https://www.gartner.com/en/documents/7012298
- Top 14 AI SRE Tools in 2026 (Sherlocks). https://www.sherlocks.ai/blog/top-ai-sre-tools-in-2026
- Firefly named in 2026 Gartner Market Guide for AI SRE Tooling. https://www.firefly.ai/blog/gartner-names-fireflys-thinkerbell-ai-in-the-2026-market-guide-for-ai-sre-tooling
- 2026 Observability Predictions (APMdigest). https://www.apmdigest.com/2026-observability-predictions-1

## 7. Incident Response

**Central case:** Anthropic August-September 2025 incident — three overlapping infrastructure bugs produced a quality outage while availability SLIs looked green. Canonical SRE monitoring missed it.

- Anthropic Engineering — A postmortem of three recent issues. https://www.anthropic.com/engineering/a-postmortem-of-three-recent-issues
- InfoQ — Anthropic Reveals Three Infrastructure Bugs. https://www.infoq.com/news/2025/10/anthropic-infrastructure-bugs/
- Biggest AI outages since 2024 (Storyboard18). https://www.storyboard18.com/how-it-works/biggest-ai-outages-since-2024-chatgpt-claude-and-cloudflare-disruptions-that-shook-the-industry-91169.htm
- OpenAI Status. https://status.openai.com/
- Claude Status. https://status.anthropic.com/

## 8. FinOps for AI

- CloudZero launches agentic FinOps (December 2025). https://www.cloudzero.com/press-releases/20251201/
- FinOps in the Age of AI (Finout). https://www.finout.io/blog/finops-in-the-age-of-ai-a-cpos-guide-to-llm-workflows-rag-ai-agents-and-agentic-systems
- FinOps Tools Definitive Guide 2026 (CloudZero). https://www.cloudzero.com/blog/finops-tools/
- FinOps for Agentic AI — the $400M cloud leak (AnalyticsWeek). https://analyticsweek.com/finops-for-agentic-ai-cloud-cost-2026/

## 9. Reliability Engineering and FMEA

**Central re-derivation:** multiplicative RPN deprecated for AI; AIAG-VDA Action Priority logic (severity-first) is default. Severity must be a matrix not a scalar. Occurrence is input-conditional (distributional), not Poisson-like. Detection is non-deterministic because the detector is itself an LLM.

- Factory AI — What is FMEA? 2026 Guide. https://f7i.ai/blog/explain-fmea-the-definitive-guide-to-failure-mode-and-effects-analysis-in-2026
- AI- and Ontology-Based Enhancements to FMEA. arXiv:2511.17743. https://arxiv.org/pdf/2511.17743
- Beyond pass@1 — A Reliability Science Framework for Long-Horizon LLM Agents (introduces Reliability Decay Curve and Variance Amplification Factor). arXiv:2603.29231. https://arxiv.org/html/2603.29231v1
- Where LLM Agents Fail and How They Can Learn From Failures (AgentErrorTaxonomy). arXiv:2509.25370. https://arxiv.org/abs/2509.25370
- Why Do Multi-Agent LLM Systems Fail? (14 failure modes across three categories). arXiv:2503.13657. https://arxiv.org/abs/2503.13657
- How Do LLMs Fail In Agentic Scenarios? arXiv:2512.07497. https://arxiv.org/html/2512.07497v2
- Multi-Agent Framework for Threat Mitigation and Resilience. arXiv:2512.23132. https://arxiv.org/html/2512.23132
- NIST AI Risk Management Framework. https://www.nist.gov/itl/ai-risk-management-framework
- NIST AI 600-1 Generative AI Profile. https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf
- ISO/IEC 42001:2023 AI Management Systems (38 controls across AIMS lifecycle). https://www.iso.org/standard/42001
- ISO/PAS 8800:2024 Road vehicles — Safety and AI. https://www.iso.org/standard/83303.html
- Adapting ISO/PAS 8800 to AI/ML System Safety (Critical Systems Labs, September 2025). https://criticalsystemslabs.com/wp-content/uploads/2025/09/Adapting-ISO-PAS-8800-to-AI-and-ML-System-Safety-Assurance-within-Other-Industries-v1.0-Copyright_merged.pdf
- MLCommons AILuminate v1.0 (12 hazard categories, 43,000+ adversarial prompts). arXiv:2503.05731. https://arxiv.org/abs/2503.05731
- MLCommons Foundation for Defensible Jailbreak Benchmarking (February 2026). https://mlcommons.org/2026/02/jailbreak-0-7/
- MIT AI Incident Tracker Harm Taxonomy. https://airisk.mit.edu/ai-incident-tracker/harm-taxonomy
- Microsoft Vulnerability Severity Classification for AI/ML. https://www.microsoft.com/en-us/msrc/aibugbar

## 10. Graceful Degradation, Fallback Chain, Circuit Breakers

- Portkey — Retries, fallbacks, and circuit breakers in LLM apps. https://portkey.ai/blog/retries-fallbacks-and-circuit-breakers-in-llm-apps/
- Portkey — Failover routing strategies for LLMs in production. https://portkey.ai/blog/failover-routing-strategies-for-llms-in-production/
- Maxim — Retries, Fallbacks, and Circuit Breakers in LLM Apps (production guide). https://www.getmaxim.ai/articles/retries-fallbacks-and-circuit-breakers-in-llm-apps-a-production-guide/
- TianPan — LLM API Resilience in Production (March 2026). Naive chains can *increase* cost during outages. https://tianpan.co/blog/2026-03-11-llm-api-resilience-production

## 11. Blast-Radius Management

**Central evidence:** Anthropic Managed Agents (public beta April 8, 2026) architect three-way distrust between brain, hands, session. Credentials removed from blast radius.

- OWASP 2026 — Managing the Agentic Blast Radius in Multi-Agent Systems. https://medium.com/@parmindersk/managing-the-agentic-blast-radius-in-multi-agent-systems-owasp-2026-7f2a84337d8d
- VentureBeat — AI agent zero-trust architecture, Anthropic Managed Agents, NVIDIA NeMo Claw. https://venturebeat.com/security/ai-agent-zero-trust-architecture-audit-credential-isolation-anthropic-nvidia-nemoclaw
- SecurityWeek — The Blast Radius Problem. https://www.securityweek.com/the-blast-radius-problem-stolen-credentials-are-weaponizing-agentic-ai/
- Northflank — How to Sandbox AI Agents in 2026. https://northflank.com/blog/how-to-sandbox-ai-agents
- LoginRadius — Limiting Data Exposure and Blast Radius for AI Agents. https://www.loginradius.com/blog/engineering/limiting-data-exposure-and-blast-radius-for-ai-agents

## 12. Decision Architecture and Authority Gradient

**Central framework:** five-level authority gradient (advisor → assistant → executor → autonomous → decider), mirrors SAE J3016 levels of driving automation. Accountability migrates monotonically with level.

- Microsoft HAX (Human-AI eXperience) guidelines. Published 2019, updated 2025. Interaction-pattern primitives at the L2 boundary.
- Google PAIR — dataset and evaluation hygiene.
- IBM watsonx.governance — organizational controls.
- NIST AI Risk Management Framework 1.0 GOV function (2023); Generative AI Profile NIST-AI-600-1 (July 2024).
- Anthropic Responsible Scaling Policy v2 (2024) binds deployment authority to capability evaluations. https://www.anthropic.com/news/responsible-scaling-policy-v3
- EU AI Act Article 14 (human oversight) mandates that high-risk systems not operate above L3 without demonstrable human veto.
- EU AI Act Article 13 (transparency) constrains provenance any L4/L5 deployment must emit.

### Learning-to-Defer and Escalation

- Mozannar et al. — Consistent Estimators for Learning to Defer to an Expert. arXiv:2006.01862 (cited in [`human-oversight-optimization.md`](human-oversight-optimization.md)).
- Verma et al. — Cost-Sensitive Learning to Defer to Multiple Experts with Workload Constraints. arXiv:2403.06906.

## 13. Team Topology and Conway's Law for AI

- Skelton, Pais — `Team Topologies` (2019) — stream-aligned, platform, enabling, complicated-subsystem patterns.
- 2026 role crystallization: AI Platform Engineer, AI SRE, Eval Engineer (stream-aligned or platform), AI Product Manager, AI Ethics/Safety Lead. "Prompt Engineer" largely absorbed into Eval Engineering.
- Federated pattern (thin platform team plus stream-aligned product teams) is the modal 2026 enterprise pattern.

## 14. Lifecycle TCO and Engineering Economics

**Central formal result:** automation is economical when task volume V > F / (c_human − c_AI), where F is fixed automation cost. Lashkari, Li, Qiu, Thompson 2026 empirically show 60-80% of current enterprise AI pilots sit below this threshold.

- MIT FutureTech — `AI and Scale: A Quantitative Task-Based Theory of Automation` (Lashkari, Li, Qiu, Thompson 2026). https://futuretech.mit.edu/publication/ai-and-scale-a-quantitative-task-based-theory-of-automation
- MIT FutureTech — `The Price of Progress: Algorithmic Efficiency and the Falling Cost of AI Inference` (Thompson, Gundlach, Lynch, Mertens, November 2025). https://futuretech.mit.edu/publication/the-price-of-progress-algorithmic-efficiency-and-the-falling-cost-of-ai-inference
- Fabrycky & Blanchard — Life Cycle Costing framework.
- Defense Systems Management College LCC methodology — O&M typically dominates acquisition by 3-5x.
- Fitzgerald & Ross — Multi-Attribute Tradespace Exploration (MATE) methodology.
- NASA ADEPT tradespace exploration applied to autonomy systems.
- MIT ESD tradespace studies.
- MIT Sloan/SDM working paper series — AI Capability as a Real Option (Q3 2025 onward).

### Observed 2026 Model Useful Lives

- GPT-4 (March 2023 release) — legacy status April 2026. ~36 months nominal, ~18 months effective for new deployments.
- Claude 3.5 Sonnet (June 2024) — superseded within ~12 months.
- Frontier-tier refresh cadence: 9-14 months.

### 2026 People Cost Benchmarks

- AI Platform Engineer: $250-$400K fully loaded.
- Eval Engineer: $200-$350K.
- AI Product Manager: $220-$320K.
- Non-AI engineer enablement: $8-$25K per head over 6 months.

## 15. MIT SDM Anchors

The repository's existing MIT SDM note at [`mit-sdm-related-work.md`](mit-sdm-related-work.md) already identifies SDM's contribution as "systems architecture, commercialization, and deployment design." This evidence reference operationalizes that contribution across the four framework documents.

- Barua SM SDM thesis — `A strategic perspective on the commercialization of artificial intelligence`. https://sdm.mit.edu/research-practice/thesis-a-strategic-perspective-on-the-commercialization-of-artificial-intelligence/
- Dao SM SDM — `Designing Generative Multi-Agent Systems for Resilience`, CAS 2025 Best Student Paper (coauthor Dr. Bryan Moser).
- MIT Sloan IDE — `Generative AI and the Nature of Work` (Nagle and collaborators; August 2025, January 2026).
- MIT Industrial Performance Center — Work of the Future working group (Armstrong, Shah, Kellogg).
- Kellogg and Valentine on algorithmic management and AI+organizational sociology.
