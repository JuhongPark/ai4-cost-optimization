# Research Questions V2

## Purpose

This document narrows the repository's broad thesis into a smaller set of investigation-ready research questions.

## Primary Research Question

Under explicit quality thresholds, which AI execution policy achieves the lowest total cost for a given task family?

This question keeps the repository focused on decision-making rather than generic capability comparison. It also matches the episode-level logging and benchmark structure already present in the project.

## Secondary Research Questions

### 1. When does selective human oversight beat full automation?

This question tests the repository's core claim that human involvement should be treated as a priced resource rather than a binary design preference.

Key sub-questions:

- At what failure rate does selective escalation become cheaper than repeated AI retries?
- How sensitive is the answer to human review time and queue constraints?
- Which escalation trigger works best: confidence, verifier failure, retry exhaustion, or policy default?

### 2. Which indirect-cost components dominate in practice?

This question distinguishes between workflows where API spend is the main issue and workflows where retries, verification, or human review become the real bottleneck.

Key sub-questions:

- When do retries erase the savings of a cheaper model?
- When does verification prevent enough downstream failure to pay for itself?
- Which task families create the largest human-minute burden?

### 3. How task-specific is the optimal policy?

This question asks whether a single policy family can generalize across tasks or whether each task family needs its own cost strategy.

Key sub-questions:

- Does coding favor verifier-heavy policies more than classification?
- Does extraction benefit more from tools and structured validation than from stronger base models?
- Do low-latency classification tasks justify routing more cleanly than high-variance workflows?

### 4. What is the right optimization objective?

This question evaluates whether weighted total cost should be the default objective or only one view among several reporting modes.

Key sub-questions:

- When is a cost vector better than a scalar score?
- When should the project use threshold-constrained optimization instead of weighted aggregation?
- How much do policy rankings change under different weight assumptions?

### 5. How do architecture choices shape the cost trajectory?

This question elevates system architecture from an implementation detail to a first-class cost driver. Its home is [`../frameworks/ai-system-architecture.md`](../frameworks/ai-system-architecture.md) and its motivation is Gap 9 in [`../references/gap-analysis.md`](../references/gap-analysis.md).

Key sub-questions:

- Which multi-agent topology (supervisor, swarm, hierarchical, blackboard) minimizes total cost for a given task family, and how does that answer change with adversarial robustness as a constraint (Dao & Moser, CAS 2025)?
- Do memory-architecture choices (CoALA-style semantic vs episodic vs procedural) change indirect cost more than direct cost, and on which timescale does that show up?
- When does inline self-critique give the same quality as a separate verifier at a fraction of the direct cost, and when is staged verification the only architecture that contains a fat-tailed failure class?
- How much of lifetime system cost is locked in by architectural commitments made at the prototype stage, and is the traditional "60-80% locked at design" figure from systems engineering transferable to AI systems?

### 6. How does the optimal policy evolve across the lifecycle?

This question treats the AI system as having a lifecycle (PoC, pilot, production, steady-state, deprecation) with cost-quality trade-offs that reorder at each stage. Its home is [`../frameworks/ai-system-lifecycle.md`](../frameworks/ai-system-lifecycle.md).

Key sub-questions:

- Which strategies dominate at the PoC stage (where fixed cost is sunk but eval harness is thin) versus at the steady-state stage (where marginal cost dominates and eval regression prevention is critical)?
- How should model-update cadence be chosen, and which release pattern (shadow vs canary vs blue/green) is cheapest per unit of reliability delivered under which conditions?
- How should prompt debt, eval debt, and context debt be amortized into TCO, and what is the cost of *not* refactoring?
- What is the right time to deprecate a deployed AI system, analyzed as a real option (abandon / defer / switch)?

### 7. What is the reliability frontier, and how much does it cost to move along it?

This question applies systems-engineering reliability rigor (FMEA, graceful degradation, blast-radius analysis) to AI systems. Its home is [`../frameworks/ai-system-operations.md`](../frameworks/ai-system-operations.md).

Key sub-questions:

- For an agentic system, what is the FMEA severity × occurrence × detection profile, and which failure modes dominate the RPN budget at 2026 frontier-model quality?
- How do graceful-degradation patterns (weaker-model fallback, cached response, human handoff) compare on the cost-quality frontier when measured against the same quality floor?
- What is the minimum logging and observability investment required to make agentic resource exhaustion a bounded-cost failure rather than a fat-tailed one?
- When is reliability cheaper to buy through architecture (topology choice, pipeline staging) versus through operations (monitoring, SLOs, incident response)?

### 8. How should decision rights and team topology be priced?

This question elevates organizational design to a first-class cost driver, following MIT SDM's systems-engineering-meets-management tradition. Its home is [`../frameworks/ai-system-architecture.md`](../frameworks/ai-system-architecture.md) §Decision Architecture.

Key sub-questions:

- How does the authority gradient (AI as advisor / assistant / executor / autonomous / decider) map onto the cost-quality frontier, and where is the human's time best spent under each level?
- Does centralized AI platform team architecture or stream-aligned AI team architecture produce lower lifecycle cost, and under what conditions does the answer flip?
- Which audit-readiness logging fields are load-bearing for EU AI Act / SEC Reg BI / GDPR Article 22 compliance, and what is the per-episode overhead?
- What is the cost of Conway's Law misalignment — when the AI system's technical architecture does not match the team structure that operates it?

## Working Hypotheses

The current investigation should treat the following as hypotheses to test rather than conclusions:

- Selective HITL will often outperform both full automation and human-first handling on medium-difficulty, medium-risk tasks.
- The best policy will vary by task family; there will not be a single universal winner.
- Indirect cost will often change the ranking produced by direct cost alone.
- Verification and routing will be higher-leverage early policy levers than complex multi-step orchestration.

## Questions to Deprioritize for Now

These are valid but should not lead the first research cycle:

- pure serving-efficiency optimization
- model pretraining efficiency
- frontier-model capability scaling
- organization-wide platform cost allocation

They matter, but they are downstream of the workflow-level decision framework this repository is trying to establish.

## Recommended Decision Rule

The first empirical cycle should answer four concrete questions for each benchmark:

1. What quality threshold must the policy satisfy?
2. Which policy classes satisfy it?
3. What direct and indirect costs do they incur?
4. Which policy is cheapest under the declared objective?
