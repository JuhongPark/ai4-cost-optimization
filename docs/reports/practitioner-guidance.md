# Practitioner Guidance

## Purpose

This document translates the current research program into practical guidance for teams using AI systems.

## Core Guidance

### 1. Do not optimize API spend alone

A cheaper model path is not automatically cheaper in practice if it increases retries, verification effort, or human review.

### 2. Define acceptable quality before cost optimization

Without a quality floor, cost reduction claims are not decision-ready.

### 3. Measure full episodes, not single calls

If a task usually requires retries, tools, or fallback review, the real unit of cost is the whole episode.

### 4. Separate direct cost from indirect cost

Teams should report both:

- direct monetary spend
- operational overhead such as human time, retries, and recovery

### 5. Start with routing and verification before complex orchestration

The most practical early gains usually come from:

- replacing unnecessary strong-model usage
- routing based on task difficulty
- adding targeted verification where failure is expensive

### 6. Treat human escalation as a priced resource

Human review should be measured explicitly in minutes, rates, or queue load rather than treated as free safety margin.

### 7. Do not assume full automation is the optimal endpoint

In many workflows, the best policy is not zero human involvement but selective escalation. If a cheaper model path causes repeated retries or downstream correction work, targeted human review may lower total cost.

## System Design Principles

The principles above operate at the per-episode workflow level. The principles below apply at the system-design and lifecycle level, in the MIT SDM tradition. Their home frameworks are [`../frameworks/ai-system-architecture.md`](../frameworks/ai-system-architecture.md), [`../frameworks/ai-system-lifecycle.md`](../frameworks/ai-system-lifecycle.md), [`../frameworks/ai-system-operations.md`](../frameworks/ai-system-operations.md), and [`../frameworks/ai-system-economics.md`](../frameworks/ai-system-economics.md).

### 8. Treat architecture as a cost-locking decision

Multi-agent topology, memory architecture, orchestration pattern, and verification pipeline choices made at the prototype stage bound the lifecycle cost trajectory. The CAS 2025 Best Student Paper (Dao & Moser, MIT SDM) shows that resilience to a single malicious or faulty agent is primarily a topology property — cheaper to get from the architecture than to bolt on later. Architecture review, not just capability review, belongs on the PoC → pilot gate.

### 9. Make lifecycle stage explicit

A PoC, a pilot, a production system, and a steady-state operation are not the same system with growing traffic. Each stage has different cost-quality trade-offs and different dominant risks. Stage-gate criteria (quality bar, cost bar, risk bar) should be declared before work begins so that the system advances or retires on evidence rather than momentum.

### 10. Separate fixed from marginal cost

Direct cost and indirect cost split along one axis; fixed cost and marginal cost split along another. Integration, eval-suite construction, and compliance audit are fixed costs. Tokens, tool calls, and per-episode human review are marginal costs. Many AI cost conversations collapse the two and miss that the project's binding constraint is a fixed-cost commitment, not a per-token inefficiency.

### 11. Run an FMEA before production deployment

Failure Modes and Effects Analysis is the systems-engineering tradition's minimum hygiene step before deployment. For agentic systems in 2026, the dominant failure modes are not hallucination but instruction drift, agentic resource exhaustion, tool misuse, and context leakage. List them, rate severity and occurrence and detection, and design the graceful-degradation path for each. Budget cap, turn cap, and circuit-breaker are the AI analogues of fuses, breakers, and dead-man switches in traditional engineering.

### 12. Design the authority gradient deliberately

AI-as-advisor, AI-as-assistant, AI-as-executor, AI-as-autonomous, AI-as-decider are different systems with different accountability and different operational cost profiles. The choice should be explicit in the system specification, not an emergent property of whoever deploys the feature. Audit-trail requirements (provenance, version, review trail) follow from the authority level, not the other way around.

### 13. Price the operational stack alongside the inference stack

Observability (LangSmith, LangFuse, Arize, Datadog LLM), SLO definition, incident response for AI-specific failures, and FinOps for AI are not optional add-ons. At production scale they are a meaningful fraction of lifecycle cost and are load-bearing for reliability. SRE-for-AI maturity should be evaluated on the same rubric as inference quality.

### 14. Model the system's economics as a lifecycle, not a unit cost

Unit cost per token or per episode is one slice of TCO. Lifecycle cost includes fixed integration, semi-fixed step costs (new jurisdiction, new tenant tier, new use case), people cost, switching cost between models/vendors/architectures, reserve for fat-tailed failures, and the real-option value of waiting vs acting. Pilots should usually be priced as call options, and weak pilots should be abandoned on option logic rather than sunk-cost momentum.

## Operational Checklist

- define the task-level quality threshold
- log per-episode cost and outcome
- report retries separately from first-pass success
- report human review load separately from API cost
- compare policies on a frontier, not only on a single score
- declare the lifecycle stage and the gate criteria before building
- run an FMEA and design graceful degradation before production
- specify the authority gradient (advisor / assistant / executor / autonomous / decider) in the system specification
- make fixed versus marginal cost visible in every cost figure
- budget the operational stack (observability, SLO, incident response, FinOps) as a line item, not a contingency
