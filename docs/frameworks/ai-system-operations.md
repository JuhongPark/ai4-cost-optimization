# AI System Operations

## Purpose

This document covers the operational side of AI systems in production: observability, service-level objectives, incident response, FinOps, reliability engineering, graceful degradation, fallback chain design, and blast-radius management. It is the operational counterpart to [`ai-system-architecture.md`](ai-system-architecture.md) (design-time), [`ai-system-lifecycle.md`](ai-system-lifecycle.md) (stage transitions), and [`ai-system-economics.md`](ai-system-economics.md) (investment-level). The 2026 evidence supporting this framework is in [`../references/ai-system-design-evidence-2026.md`](../references/ai-system-design-evidence-2026.md).

The framing is SRE-for-AI: Google SRE's four golden signals cover the transport layer of an LLM system but say almost nothing about whether the system is doing its job. Operational practice in 2026 has converged on extending SRE discipline with AI-specific SLIs, FMEA rigor, graceful-degradation patterns, and blast-radius containment.

## 1. SLIs and SLOs for AI

2026 consensus is a three-tier SLI stack.

### 1.1 Infrastructure SLIs (traditional)

- availability, p95 time-to-first-token, tokens-per-second throughput
- queue saturation, HTTP error rate
- provider-side error rate

These are standard SRE metrics that apply unchanged.

### 1.2 Quality SLIs (novel)

- faithfulness score against retrieval
- hallucination rate sampled via LLM-as-judge
- refusal rate
- output coherence and response relevance above a threshold

The canonical quality SLI, shared across Confident AI, Portkey, and Braintrust 2026 guides, is "share of responses exceeding a relevance-score threshold." This mirrors the SRE formula "good events over valid events" but replaces HTTP 2xx with a scored eval.

### 1.3 Agent SLIs (agentic workflows)

- task completion rate
- tool-call success rate
- unnecessary-tool-call rate
- trajectory length
- human-escalation rate
- retry rate
- cost per successful task
- **loop rate** — share of sessions that hit the max-iteration limit; the defining distinguishing signal between a healthy agent and a runaway one

Towards AI's April 2026 agent-observability synthesis treats loop rate as the central agent SLI, the one that separates healthy agents from the agentic resource exhaustion failure mode named in [`../references/industry-updates-2026-04.md`](../references/industry-updates-2026-04.md).

### 1.4 Error Budgets Extended to Quality

Error budgets extend cleanly to quality: if the hallucination-rate SLO is 2% and the rolling 28-day rate hits 2.5%, the budget is burned and auto-routing to a safer (and usually more expensive) model or to human review kicks in. This mirrors traffic-shifting during a classical outage.

The catch is the **noisy-SLI problem**: LLM-as-judge scores have 5-10% intrinsic variance. SLO burn-rate windows must be wider than for HTTP errors, and alerting thresholds need hysteresis or a dual-rate burn policy (Google SRE Workbook style) to avoid paging on sampling noise.

## 2. Observability Stack

The 2026 tooling landscape splits into three clusters.

### 2.1 LLM-Native Developer Tools

- **LangSmith** — tight LangChain/LangGraph coupling, zero-config tracing, enterprise-only self-host
- **Langfuse** — Apache-2.0, OpenTelemetry-native, session replay plus eval templates; the default open-source choice
- **Arize Phoenix** — Elastic 2.0, strength in drift clustering and RAG retrieval relevancy
- **Braintrust** — eval-first
- **Literal AI, Helicone, Weights & Biases Weave** — similar category

### 2.2 APM Incumbents

- **Datadog LLM Observability** — natively ingests OpenTelemetry GenAI semantic conventions; auto-prices spans against 800+ models at approximately $0.10 per 1,000 tokens ingested; added Google Agent Development Kit auto-instrumentation in February 2026
- **Splunk AI, Dynatrace AI Observability** — similar positioning for existing APM customers

### 2.3 Gateway and Proxy Tools

- **Portkey, LiteLLM, Helicone** — capture tracing and cost attribution at the network edge without SDK changes; useful in polyglot stacks

### 2.4 OpenTelemetry GenAI Semantic Conventions

Stable release target is late 2026; `OTEL_SEMCONV_STABILITY_OPT_IN` gates the experimental surface as of April 2026. Defines:

- `gen_ai.operation.name` (`chat`, `create_agent`, `invoke_agent`, `execute_tool`)
- agent identity attributes
- metrics spec covering token counts, cost, time-to-first-token

Datadog's February 2026 commitment to treat GenAI conventions as native schema signals that OpenTelemetry GenAI has crossed the credibility threshold. It is the answer to "how do I avoid vendor lock-in for agent traces."

### 2.5 The Observability Cost Problem

RAG pipelines generate 10-50x the telemetry volume of equivalent REST calls. Observability bills are themselves becoming a cost category. Sampling policies (head-sample by trace, tail-sample on failure and high-cost traces) have moved from nice-to-have to required at production scale.

## 3. Incident Response

AI incidents are not traditional incidents. The Anthropic August-September 2025 incident is the reference case: three overlapping infrastructure bugs — a context-window routing error peaking at 16% of Sonnet 4 requests on August 31, a TPU-server misconfiguration producing Thai/Chinese tokens for English prompts, and an XLA:TPU top-k miscompilation on Haiku 3.5 — produced a quality outage while availability SLIs looked green. Anthropic's published postmortem committed to "running quality evaluations continuously on true production systems" — an explicit acknowledgement that canonical SRE monitoring missed the regression.

### 3.1 2026 Incident Taxonomy

- provider outages (OpenAI May 2025 four-hour Kubernetes telemetry incident; June 10, 2025 ~15-hour ChatGPT outage; Anthropic March 2, 2026 claude.ai frontend outage; April 10, 2026 email-login incident)
- prompt regressions after a silent provider update
- data drift spikes
- cost spikes from runaway agents (agentic resource exhaustion)
- hallucination outbreaks
- jailbreak discoveries

### 3.2 Why Partial Outage Means Something Different

In classical SRE, partial outage means some requests fail and some succeed. In an LLM context, partial outage often means the request succeeds but the output is wrong. An availability-green, quality-red condition cannot be fixed by traditional rollback because the bad behavior is distributed across many probabilistic samples, not a deployable artifact.

**Agentic resource exhaustion** fits this mold: a looping agent returns 200 OK on every call while quietly burning through a budget. The incident signal must come from cost-per-session or trajectory-length SLOs, not HTTP status. Gartner's March 2026 forecast that "90% of organizations will experience an AI-caused outage by 2029" presumes this failure mode dominates.

## 4. FinOps for AI

CloudZero opened "agentic FinOps" in December 2025; Vantage shipped a FinOps Agent and FinOps-as-Code in 2026; Finout added ML-driven anomaly detection including seasonality. Gartner's March 2026 Data and Analytics Summit made FinOps for AI a board-level topic after reporting a "$400M collective leak" in unbudgeted agentic spend.

### 4.1 Overlap with SRE

Both disciplines run on time-series telemetry, anomaly detection, and budget-based alerting. Error budgets and cost budgets share the same statistical machinery — burn rates, multi-window alerts, budget policy as code.

### 4.2 Divergence from SRE

- **attribution granularity** — FinOps needs per-tenant, per-session, per-feature chargeback; demands tags propagated through every span from gateway to tool call
- **unit economics** — cost-per-successful-task and cost-per-active-user are business metrics, not reliability metrics; require joining traces with product telemetry
- **controllable surface** — SRE acts on deploys and traffic shifts; FinOps acts on routing, cached-prefix policy, batch scheduling, and model-tier caps

The practical implication is a shared observability layer (OpenTelemetry GenAI traces with cost attributes) with separate policy engines on top.

## 5. FMEA for AI

Classical FMEA computes Risk Priority Number (RPN = Severity × Occurrence × Detection). By 2026 the practitioner community has largely deprecated multiplicative RPN for AI, adopting AIAG-VDA's Action Priority (AP) logic — severity-first, then occurrence, then detection — because a high-severity, low-occurrence event should never be numerically equivalent to a low-severity, high-occurrence one. This matters enormously for AI where low-probability catastrophic tails dominate expected harm.

### 5.1 Severity Axis

Severity must be a matrix, not a scalar. Dimensions:

- direct harm to the end user
- second-order harm to downstream counterparties
- fat-tailed regulatory and brand exposure
- cost and capacity impact

MIT AI Incident Tracker adopted CSET's taxonomy with a 1-5 scale; NIST AI 600-1's 12 GAI risk categories (confabulation, information integrity, CBRN uplift, information security, value-chain integration, others) provide complementary severity anchors.

### 5.2 Occurrence Axis

Classical FMEA breaks here because AI failure rates are input-conditional, not Poisson-like. 2026 research (arXiv:2603.29231 "Beyond pass@1") recasts occurrence as a distributional quantity — Reliability Decay Curve and Variance Amplification Factor — showing occurrence grows super-linearly with task horizon. Empirical occurrence priors come from AgentErrorTaxonomy (arXiv:2509.25370) and the 14 multi-agent failure modes in arXiv:2503.13657.

### 5.3 Detection Axis

Detection is non-deterministic because the detector is often itself an LLM. ISO/PAS 8800 (December 2024) explicitly demands that guardrails, fallback logic, monitors, and plausibility checks be verified to higher integrity than the model itself — the AI-specific answer to classical diverse-redundancy.

### 5.4 AI-Specific Failure Mode Library

The 2026 stable enumeration, compatible with [`failure-taxonomy.md`](failure-taxonomy.md):

- hallucination and confabulation
- prompt injection
- tool misuse
- context leakage
- agentic resource exhaustion
- jailbreak
- consistency drift
- distribution drift
- instruction drift
- verifier-passing-but-wrong

NIST AI 600-1, ISO/IEC 42001 (38 controls across the AIMS lifecycle), and MLCommons AILuminate v1.0 (12 hazard categories, 43,000+ adversarial prompts; jailbreak v0.5 December 2025, v0.7 February 2026) provide industry-consensus enumerations.

## 6. Graceful Degradation Patterns

| Pattern | Cost delta | Latency delta | Quality delta | Determinism |
| --- | --- | --- | --- | --- |
| Static fallback (deterministic rule) | approximately 0 | -80% | large, abrupt | deterministic |
| Weaker-model fallback | -60 to -90% | -20 to -50% | moderate, continuous | stochastic |
| Cached response | approximately 0 | -95% | stale, abrupt | deterministic |
| Partial output plus disclosure | variable | variable | transparent | semi |
| Human handoff | +10x to +100x | hours | full quality | deterministic |
| Circuit breaker open | 0 | immediate fail | none | deterministic |

Circuit breakers for AI extend Hystrix/Resilience4j semantics: classical breakers trip on HTTP errors; AI breakers must also trip on **quality signals** (rejection rate, verifier disagreement, output-distribution drift). Portkey, LiteLLM, and Maxim document this extension.

**Step-function fallback** dominates when severity is high, uncertainty about the primary path is already calibrated, the downstream consumer cannot process partial output (payments, legal filings), or regulatory attestation requires a deterministic audit trail.

**Continuous degradation** dominates when the task is open-ended (summarization, brainstorming) and the user can tolerate and observe quality variation.

The correct rule: step function at safety-relevant boundaries, continuous within a tier. This mirrors aerospace practice where DO-178C DALs create discrete safety tiers but within-tier behavior is allowed to vary.

## 7. Fallback Chain Design

The 2026 production consensus is a four-layer chain with **different chain selection per failure class**:

- **provider outage (5xx, timeout)**: swap provider, stronger-diversity secondary. OpenAI's June 2025 34-hour outage and the 114-incident Anthropic window in Q1 2026 make cross-provider routing non-optional. Portkey, LiteLLM, and OpenRouter expose load-balanced pools.
- **rate-limit (429)**: same-provider cheaper tier first; exponential backoff with jitter (1s to 30s cap, approximately 3 retries) before escalation
- **output rejection (guardrail or verifier disagreement)**: re-ask with constraints, then weaker model with stricter template, then human
- **latency breach**: cached response or truncated partial; never silent model-swap, which leaks behavior drift

### 7.1 Three-Dimensional Retry Budget

- **token budget** — bounds worst-case cost
- **turn budget** — bounds agent loops, directly addressing agentic resource exhaustion
- **wall-clock budget** — bounds user-visible latency

Naive chains (Sonnet → GPT-4o) can **increase** cost during outages because every request pays twice. Failure-budget accounting must allocate retries, breakers, and fallbacks explicitly so each layer only absorbs the class of faults it was designed for.

## 8. Blast-Radius Management

Blast radius scales super-linearly with agent autonomy.

| Agent type | Blast radius | Containment priority |
| --- | --- | --- |
| Single agent, single session | One bad response plus its triggered side effects | Per-session budget, output verification |
| Multi-agent (Group Chat topology) | Malicious or erroneous agent propagates to peers in one step (Dao & Moser CAS 2025) | Topology change to Reflexion/Crowdsourcing/Blackboard |
| Tool-use with side effects | File write, API call, payment, email — LLM error becomes external-world event with irreversibility | Sandbox, permission gate, human approval for irreversible operations |
| Resource exhaustion | Shared cost envelope of the service — a fat-tailed loss beyond the failing episode | Per-session and per-tenant budget caps as circuit breakers |

Containment technology matured rapidly in Q1 2026:

- **Anthropic Managed Agents** (public beta April 8, 2026) architect three-way distrust between brain (Claude + harness), hands (disposable Linux containers, microVM-class), and session (append-only event log); credentials removed from the blast radius so a prompt-injection compromise produces a disposable container with no tokens
- **NVIDIA NeMo Claw, Cloudflare, Vercel, Modal, Firecrawl, E2B, Northflank, Docker Sandboxes** — equivalent microVM or gVisor isolation
- **OWASP 2026 agentic-blast-radius guidance** mandates out-of-band circuit breakers and kill switches outside the agent control plane

### 8.1 Blast-Radius Quantification

A practical quantification:

blast_radius = affected_sessions × affected_external_systems × reversibility_factor × detection_to_containment_latency

where reversibility_factor is 0 for payment or email and 1 for read-only operations. Architectures that reduce any factor reduce expected harm multiplicatively. This makes blast radius a first-class design metric, not a post-hoc concern.

## 9. Reverse Import from High-Reliability Industries

ISO/PAS 8800:2024 (road-vehicle AI safety, tailorable to IEC 62304, IEC 61508, EN 50716, DO-178C per Critical Systems Labs 2025 whitepaper) is the most important cross-domain artifact. It enforces:

- AI as **component**, not system — pre-processing plus model plus post-processing are assured as a whole
- an AI safety lifecycle covering requirements, design, V&V, deployment, field monitoring, decommissioning, aligned with ISO/IEC 42001's 38 AIMS controls
- **higher integrity for safety nets than for the model itself** — the guardrail must be more reliable than the guarded
- explicit treatment of functional insufficiencies via SOTIF (ISO 21448) extensions

The reverse-import lesson: generic AI systems gain from adopting DAL/ASIL-like tiering, independence of monitors, and field-monitoring discipline, even without certification pressure.

## 10. SRE-for-AI Maturity Model

A five-level ladder distilled from Gartner January 2026 Market Guide for AI SRE Tooling and vendor maturity frameworks:

| Level | Characteristics |
| --- | --- |
| L0 Ad-hoc | Provider dashboards only, no tracing, monthly invoice surprises |
| L1 Basic monitoring | Gateway logs, per-call cost, basic latency and error dashboards — where most pilots sit |
| L2 SLO-driven | Quality SLIs with eval-in-production, cost-per-task unit economics, defined error budgets. LLM observability at approximately 15% of GenAI deployments, projected to 50% by 2028 (Gartner) |
| L3 Continuous optimization | Automated regression gates on prompt and model changes, drift-triggered rerouting, FinOps guardrails as code |
| L4 Predictive / autonomous | AI-SRE agents (Firefly Thinkerbell and peers in the 2026 Gartner Market Guide) that diagnose and remediate |

Gartner's data shows client inquiries on AI SRE up 85% year-over-year, but production deployments remain in early-adopter territory.

## 11. Minimal Operations Plan

Every production AI system should declare:

- the three-tier SLI set with explicit SLOs and burn-rate alert policy
- the observability stack including OpenTelemetry GenAI tagging and sampling policy
- the incident runbook covering provider outage, prompt regression, drift spike, cost spike, hallucination outbreak, jailbreak discovery
- the FinOps policy including per-tenant chargeback and budget enforcement
- the FMEA severity matrix with per-dimension columns and per-failure-mode RPN-like scores
- the graceful-degradation pattern per failure class
- the fallback chain with three-dimensional retry budget (token, turn, wall-clock)
- the blast-radius quantification per deployed component and the containment architecture
- the SRE-for-AI maturity level and the next-stage investment plan
