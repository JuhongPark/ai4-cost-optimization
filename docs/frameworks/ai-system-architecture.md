# AI System Architecture

## Purpose

This document treats the AI system's internal architecture — multi-agent topology, memory organization, orchestration pattern, verification pipeline, and decision architecture — as a first-class cost driver. The repository's prior frameworks ([`cost-taxonomy.md`](cost-taxonomy.md), [`strategy-taxonomy.md`](strategy-taxonomy.md), [`skill-domain-taxonomy.md`](skill-domain-taxonomy.md)) treat the system as a workflow with a small number of policy knobs. That framing is correct but incomplete: in traditional systems engineering, 60-80% of lifetime system cost is locked in by architectural decisions made before the first working prototype. This document operationalizes that observation for AI systems and registers it against Gap 9 in [`../references/gap-analysis.md`](../references/gap-analysis.md).

Concrete 2026 evidence supporting this framework is in [`../references/ai-system-design-evidence-2026.md`](../references/ai-system-design-evidence-2026.md). The MIT SDM framing is explicitly drawn from `Designing Generative Multi-Agent Systems for Resilience` (Dao & Moser, CAS 2025 Best Student Paper).

## 1. Multi-Agent Topology

Four canonical topologies appear in 2025-2026 production literature. They differ on coordination cost, adversarial resilience, and failure propagation.

| Topology | Coordination cost | Redundancy | Failure propagation | Best suited for |
| --- | --- | --- | --- | --- |
| Supervisor / orchestrator-worker | O(N) at the lead; concentrated | Low | Lead failure cascades; worker failure is local | Parallelizable research, decomposable tasks with a strong lead model |
| Swarm / peer-to-peer | O(N²) redundant computation | High | Localized; no single point of failure | Peer-strength workers, overlapping work units, latency-sensitive paths where a lead would be the bottleneck |
| Hierarchical (nested delegation) | O(N log N) across layers | Moderate | Compounded supervisor failure at every level | Privacy-segmented work, bounded-authority escalation |
| Blackboard (shared memory) | Read-write contention on shared state | Low | Consistency failures in shared state | Shared-context multi-expert work |

The central empirical result from Dao & Moser CAS 2025 for a systems-engineering audience: **topology choice dominates robustness to a single malicious or faulty agent.** Flat group-chat topologies collapse because bad content propagates to every peer in one step. Reflexion, Crowdsourcing, and Blackboard topologies contain failures because bad content must survive a filtering or voting step before affecting the collective output. Group size improves both accuracy and resilience, but at monotonically growing token cost. Step-back abstraction prompting independently reduces hallucinations.

The architectural consequence is that **resilience is primarily a topology property, not a model property.** A system designed for a filtering-topology pays an upfront architectural cost but avoids recurring reliability cost; a system designed for flat broadcast pays less upfront but accumulates reliability cost indefinitely. This is a classic fixed-vs-marginal trade (see [`cost-taxonomy.md`](cost-taxonomy.md) §3 Orthogonal Dimension).

AdaptOrch-style runtime topology switching (reported 12-23% uplift over any static choice in 2026 academic work) reframes topology as a tunable design variable rather than a hard commitment. For tradespace exploration this means topology should be a first-class axis, not a pre-commitment.

## 2. Memory Architecture

The organizing vocabulary is **CoALA** (Sumers, Yao, Narasimhan, Griffiths, TMLR 2024): working memory plus long-term memory split into semantic, episodic, and procedural, with an explicit decision loop over internal and external actions. CoALA is not a product — it is the reference frame the 2025-2026 memory-layer vendors (Zep, Letta, MemGPT, LangGraph memory, LangMem) align to.

Production memory stacks converge on a layered pattern:

- **short-term**: context window plus scratchpad (ReAct-style notes, tool-call history)
- **long-term semantic**: vector DB (pgvector, Pinecone, Weaviate, Redis) for fuzzy recall
- **long-term episodic**: time-indexed interaction logs; Zep's temporal knowledge graph structures episodes as episode plus semantic-entity plus community subgraphs, which lets an agent answer "when did X happen" rather than only "what is X"
- **procedural**: Letta and LangMem let the agent rewrite its own system instructions from feedback — essentially persisted policy improvement
- **explicit state**: Letta (formerly MemGPT) makes memory a first-class, developer-editable object rather than an implicit RAG by-product

The cost-quality-consistency triangle:

- vector-only is cheapest per write but degrades on entity-heavy queries
- graph memory is expensive per write but answers multi-hop queries without prompt-level reasoning
- episodic buffers are the only defense against the "agent forgot what it just decided" inconsistency class

2026 industry norm is a **hybrid stack** — vector for recall, episodic for coherence, graph only for the queries that justify the schema cost. The architectural decision is which class of inconsistency or latency the deployment is willing to accept, not which vendor to pick.

## 3. Orchestration Pattern

The reasoning-loop trade-space:

| Pattern | Token cost vs ReAct | Latency cost vs ReAct | Best suited for |
| --- | --- | --- | --- |
| ReAct (thought/action/observation loop) | 1x | 1x | Adaptive exploration where the plan is uncertain |
| Plan-and-Execute / ReWOO | approximately 0.15x | approximately 0.27x | Structured multi-step tasks with stable plans |
| Reflexion (self-critique loop) | approximately 2x | approximately 2x | Hard reasoning with verifiable failure signal |
| Tree-of-Thought / LATS | approximately 3-5x | approximately 3-5x | Search-heavy tasks with branching hypotheses |

(Ratios from 2025-2026 published comparisons; specific numbers in the evidence reference.)

The orchestration substrate has bifurcated in 2026:

- **durable execution** (Temporal, Dagster, Prefect) for state that must survive worker restarts
- **agentic state machines** (LangGraph) for reasoning

The default production pattern is **durable + agentic as a two-layer composition**. Pure agentic autonomy without a durable outer layer correlates with agentic resource exhaustion — the operational phenomenon named in [`../references/industry-updates-2026-04.md`](../references/industry-updates-2026-04.md).

**MCP (Model Context Protocol)** hit 97M monthly SDK downloads by March 2026. Architecturally it collapses N×M tool integrations into N+M (each client, each server). The forthcoming agent-to-agent extension will blur the server/agent boundary and make topology a protocol-level concern, not only an application concern.

## 4. Verification Architecture

Three structural choices:

- **inline self-critique** — same model critiques its own output. Cheapest, weakest containment; a jailbroken model self-approves.
- **two-step (separate verifier)** — e.g., Llama Guard as external classifier. Independent failure modes. NeMo Guardrails reports approximately 89% input-moderation accuracy; Llama Guard approximately 67% on prompt-injection category assignment.
- **pipeline (staged gates)** — input rails → model → output rails → executable checks. NeMo Guardrails' Colang, Guardrails AI schema validation, LlamaFirewall sit here.

Verification types compose orthogonally:

- **structural** (JSON schema, grammar-constrained decoding) — cheap and high-confidence for format correctness
- **semantic** (LLM-as-judge) — flexible but opinion-like and requires calibration against human labels
- **executable** (unit tests, SQL dry-run, sandboxed code run) — the only ground-truth class for code and data tasks

Architectural consequence: inline critique minimizes direct cost but loses failure containment; pipeline staging roughly doubles per-episode direct cost but converts a class of unbounded-tail failures into bounded-per-gate cost. This is the canonical direct-cost-vs-indirect-cost trade the repository is already built around, now expressed at the architecture layer.

## 5. Decision Architecture

An AI system is a decision-making system. Its architecture should explicitly specify who decides what, under which authority, with which accountability. 2025-2026 practice converges on a five-level authority gradient:

| Level | Pattern | AI action | Human role | Accountability shift |
| --- | --- | --- | --- | --- |
| L1 Advisor | Suggest only | Surface suggestions | Judge and act | Human owns judgment and error |
| L2 Assistant | Draft for approval | Draft artifacts | Approve or revise before acting | Human owns final decision |
| L3 Executor | Act in policy envelope | Act within declared bounds | Monitor in real time | Shared; envelope design is human, action is AI |
| L4 Autonomous | Act with audit | Act freely within bounds | Audit after the fact | Organization owns policy envelope |
| L5 Decider | Act, inform human | Act and notify | Informed, not consulted | Organization owns policy; operator owns exception handling |

This mirrors SAE J3016's levels of driving automation conceptually. The cost connection is direct: per-event AI cost rises with level (more autonomous action means more tool calls, more self-verification, more logging); human time per event falls. The repository's total-cost illustration in [`../references/industry-trends-2026.md`](../references/industry-trends-2026.md) §4 (a low-cost model with 20% human escalation costs more per task than a mid-tier model with 5% escalation) is the same curve read through the authority-gradient lens.

### 5.1 Escalation Triggers as First-Class Policy

Escalation is the operational surface of the authority gradient. The 2026 catalog:

- **confidence-triggered** — model self-reported or calibrated confidence crosses a threshold
- **exception-triggered** — category, user segment, or monetary value membership
- **time-triggered** — SLA or tool-timeout
- **cost-triggered** — per-episode or per-session budget envelope (essential given agentic resource exhaustion)
- **consistency-triggered** — disagreement across ensemble or self-consistency samples

The 2025-2026 learning-to-defer literature is converging on composite triggers trained jointly with routing policy, so escalation rate becomes a tunable cost-quality knob rather than a tuned-once threshold. This matters because escalation policy is the dominant indirect-cost lever once the model is selected.

### 5.2 Auditability as a Design Requirement

Auditability is not observability. Observability serves operations; auditability serves regulators and legal. A 2026 audit-ready log captures:

- decision provenance: model identifier and version, prompt or policy version, context-window contents (or verifiable hash), tool-call graph, evaluator identity
- decision timestamp and versioning: monotonic, reproducible against the T-version of model, prompt, and retrieval index
- human review trail: who reviewed, when, what they saw, what they did

Three regulatory regimes drive these requirements: EU AI Act Article 13 (transparency and traceability for high-risk systems), GDPR Article 22 (right not to be subject to solely automated decisions with legal or similarly significant effects), and SEC Regulation BI plus Reg SCI's documentation obligations. OpenTelemetry's GenAI semantic conventions (stable release targeted late 2026) and W3C Verifiable Credentials extensions supply the transport layer.

The practical implication for the repository's [`logging-schema.md`](logging-schema.md) is that the existing fields are the right primitives but need three audit-specific additions: `decision_authority_level`, `policy_envelope_id`, and `provenance_hash`.

### 5.3 RACI for AI Lifecycle Decisions

Decision rights concentrate at six gates: model selection, prompt or policy change, eval update, deployment, rollback, deprecation. A defensible 2026 RACI:

- **Recommends**: stream-aligned product team
- **Approves**: product lead, with ethics/safety veto for high-risk categories
- **Consults**: platform team, legal and compliance
- **Informed**: downstream operators and customer-facing staff

The separation-of-duties principle matters: approval authority for a prompt change that affects a high-risk determination cannot sit with the same engineer who wrote the prompt. SIFMA and ABA Task Force reports make the same point in regulated-industry language.

## 6. Team Topology and Conway's Law for AI

Pais and Skelton's `Team Topologies` (2019) — stream-aligned, platform, enabling, complicated-subsystem — applies to 2026 AI organizations with clear implications for lifecycle cost.

- **stream-aligned AI team** — product-embedded, owns evals tied to that product's task family, moves at product cadence
- **platform AI team** — owns shared inference infrastructure, prompt and eval tooling, model-access governance; its users are the stream-aligned teams
- **enabling team** — short-lived internal consultancy for domain-specific adoption (two-month engagement to help a risk function productionize one workflow)
- **complicated-subsystem team** — owns retrieval indices, multi-agent orchestration, safety classifiers

The 2026 role set that has crystallized: AI Platform Engineer, AI SRE, Eval Engineer (stream-aligned or platform depending on task specificity), AI Product Manager, AI Ethics/Safety Lead. "Prompt Engineer" remains contested; 2026 practice has largely absorbed it into Eval Engineering because evals, not prompts, are the durable artifact.

Conway's Law implication: a centralized platform-only topology produces monolithic AI systems with slow product fit but strong governance; a fully stream-aligned topology produces fast iteration but duplicated infrastructure and regulatory fragmentation. The **federated pattern** — thin platform team owning shared primitives (logging schema, model access, safety defaults) plus stream-aligned product teams — is the modal 2026 enterprise pattern and is explicitly a decision-rights design, not a reporting-line choice.

## 7. How Architecture Choices Shape the Cost Trajectory

The central claim that ties this document to the rest of the repository:

- **topology** shapes the resilience floor and the coordination-vs-redundancy balance
- **memory architecture** shapes the consistency ceiling and per-episode context cost
- **orchestration pattern** shapes the exploration-vs-execution balance and the agentic-resource-exhaustion tail
- **verification architecture** shapes the direct-vs-indirect-cost frontier at the episode level
- **decision architecture** shapes the per-level cost-quality curve and the audit-readiness floor
- **team topology** shapes the lifecycle cost via Conway's Law and the governance-vs-speed balance

These are the six architectural axes that should be explored as a tradespace before a per-episode policy comparison begins. The lifecycle model in [`ai-system-lifecycle.md`](ai-system-lifecycle.md) uses this tradespace at each stage gate; the TCO model in [`ai-system-economics.md`](ai-system-economics.md) prices the architectural commitments against the full lifecycle.

## 8. Minimal Architecture Decision Record

Every significant AI system should declare the following before production, and revisit at each lifecycle gate:

- topology choice and rationale (which resilience and coordination profile is being bought)
- memory stack and retention policy per layer
- orchestration pattern and durable-outer-layer policy
- verification pipeline including input rails, output rails, executable checks, and their budget
- authority-gradient level per task family and the escalation triggers that route between levels
- audit logging additions (authority level, policy envelope, provenance hash) and the regulatory regimes they serve
- team topology and RACI for the six lifecycle gates

This ADR is the bridge between the architectural tradespace and the operational practice in [`ai-system-operations.md`](ai-system-operations.md).
