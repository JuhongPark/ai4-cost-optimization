# Gap Analysis

## Purpose

This note identifies the main research gaps between existing literature and the goals of this repository.

## Gap 1: Workflow-level total cost is underdefined

Many papers optimize one cost component at a time, such as API price, latency, routing, or test-time compute. Fewer papers define the full cost of solving a task from start to finish, including retries, orchestration, oversight, and failure recovery.

Why it matters:

- a cheaper first attempt may create a more expensive full workflow
- local optimization can increase global cost
- task completion should be evaluated as an end-to-end process

## Gap 2: Indirect cost is fragmented across separate literatures

Human oversight, deferral, self-correction, and recovery are studied in different research traditions. These literatures are informative, but they are not yet unified into a single framework for AI problem-solving cost.

Why it matters:

- indirect cost can dominate practical usage even when direct inference cost falls
- the same system may look cost-efficient on API bills but expensive in operational practice

## Gap 3: Quality constraints are often implicit

A large share of cost-optimization work shows accuracy retention or benchmark gains, but the minimum acceptable quality threshold is often not treated as an explicit optimization constraint.

Why it matters:

- cost reduction without a predefined quality floor is ambiguous
- practical deployments care about acceptable quality, not just relative score changes

## Gap 4: Cross-task comparability remains weak

Different papers optimize coding, QA, reasoning, or serving workloads with different metrics and assumptions. This makes it difficult to compare strategies across task classes.

Why it matters:

- the best policy for coding may not be the best policy for extraction or planning
- a general AI cost framework needs common reporting conventions

## Gap 5: Direct-cost and indirect-cost strategies are rarely analyzed together

Existing work often studies routing, speculative decoding, tool use, or self-correction separately. But practical systems combine these mechanisms in one workflow.

Why it matters:

- cost interactions may be nonlinear
- direct-cost savings may increase indirect-cost burden
- a useful framework should expose these tradeoffs explicitly

## Gap 6: Human oversight is usually treated as a fallback, not as a priced resource

Learning-to-defer and scalable-oversight work offers useful theory, but many practical AI workflow discussions still treat human review as an unpriced safety net.

Why it matters:

- human time is often the highest-value resource in deployment
- escalation policy is one of the central cost questions in real workflows

## Gap 7: Sales-domain workflows are under-represented in cost-optimization work

The AI cost-optimization literature, benchmarks, and open-source tooling are heavily concentrated in the productization domain defined in [`../frameworks/skill-domain-taxonomy.md`](../frameworks/skill-domain-taxonomy.md). SWE-Bench, HumanEval, MBPP, GAIA, τ-bench, and the published agentic-coding economics (OpenHands, Vantage, Anthropic's Claude Code trends) give the productization domain a dense measurement and comparison surface. The sales domain (selling and investment) has much thinner public infrastructure:

- there is no SWE-Bench equivalent that captures the full outbound-to-reply, proposal-to-close, or IC-memo-to-fund-return loop
- vendor-published pricing is predominantly seat-based with AI usage absorbed into the seat, so per-task cost is not directly exposed to external researchers
- failure modes (deliverability collapse, ICP drift, MNPI mishandling, regulatory exposure) are fat-tailed and realize only weeks to years after the action, so comparable episode-level logging is rare in public datasets

Why it matters:

- the repository's three original scenarios in [`../reports/industry-scenarios.md`](../reports/industry-scenarios.md) (code generation, document extraction, classification) all fall inside the productization domain, so strategy comparisons calibrated on them may not transfer to the sales domain
- the human-escalation strategy family is the dominant lever in the sales domain but has been validated mostly in productization-adjacent benchmarks; the priority reordering in [`../frameworks/skill-domain-taxonomy.md`](../frameworks/skill-domain-taxonomy.md) §4.8 needs sales-domain empirical backing before it can be treated as more than a hypothesis
- proxy benchmarks like FinanceBench, LegalBench, and τ-bench stress pieces of the sales-domain loop but do not cover its defining properties (delayed outcome signal, fat-tailed failure cost, human-as-action-gate)

A concrete contribution this repository can make is a **proposed minimal sales-domain benchmark design** that captures at least one of the three defining properties, rather than running cost-quality comparisons on inadequate proxies.

## Gap 9: AI systems are not treated as engineered systems

Most cost-optimization work treats the AI system as a black box whose cost behavior is characterized by a small number of workflow-level knobs (model choice, routing, retry, verification). This framing imports very little from traditional systems engineering, where a deployed system is characterized by its architecture, its lifecycle stage, its failure modes and effects analysis, its blast-radius and containment, its operational SLIs and SLOs, and its decision-rights design.

The MIT SDM tradition (system architecture, tradespace exploration, lifecycle costing, engineering management) offers this rigor. The repository has not yet operationalized systems architecture, commercialization, and deployment design at the framework level. Specifically:

- architecture decisions (multi-agent topology, memory architecture, orchestration pattern, verification pipeline) are rarely modeled as first-class cost drivers even though they reshape the full workflow cost trajectory
- lifecycle stage (PoC, pilot, production, steady-state, deprecation) is rarely made explicit even though the cost-quality tradeoff reorders meaningfully at each stage
- FMEA-style reliability analysis is rare in AI cost-optimization papers even though `Designing Generative Multi-Agent Systems for Resilience` (Dao & Moser, CAS 2025 Best Student Paper) shows the approach transfers and matters
- observability and SRE-for-AI practice has a large industry literature but is mostly treated as an engineering concern separate from cost; the two converge once error budgets and cost budgets are modeled jointly
- decision-architecture and team-topology design (who decides what, under which authority gradient, with which team structure) are rarely priced into the cost framework even though Conway's Law and organizational design literature predict them to be load-bearing
- lifecycle TCO modeling in the MIT SDM tradition (fixed vs marginal, tradespace exploration, real options, depreciation) is largely absent from AI cost work, even though `AI and Scale` (Lashkari, Li, Qiu, Thompson 2026) already demonstrates its relevance

Why it matters:

- architecture choices made at the prototype stage lock in 60-80% of lifetime system cost in traditional engineering; the same principle likely applies to AI systems but has not been quantified
- lifecycle and operational cost often dominate deployment-level TCO but are invisible in per-episode accounting
- the most expensive AI failures in 2026 are not model-quality failures but system-level failures: agentic resource exhaustion, provider outage propagation, regulatory exposure from insufficient audit trails, team-topology mismatch between model behavior and human decision rights

The concrete contribution the repository can make is to elevate architecture, lifecycle, reliability engineering, decision architecture, and lifecycle TCO to first-class framework elements — each covered in a dedicated framework doc alongside the existing cost-taxonomy, strategy-taxonomy, and skill-domain-taxonomy. See [`../frameworks/ai-system-architecture.md`](../frameworks/ai-system-architecture.md), [`../frameworks/ai-system-lifecycle.md`](../frameworks/ai-system-lifecycle.md), [`../frameworks/ai-system-operations.md`](../frameworks/ai-system-operations.md), and [`../frameworks/ai-system-economics.md`](../frameworks/ai-system-economics.md).

## Gap 8: Productization is not uniform on the verifier-cost axis

Even inside the productization domain, the verifier cost spans the full range observed between coding and sales. Coding, QA/testing, code-derived documentation, and structural data-pipeline work sit at the cheap-verifier end (compile, test, lint, schema contracts). Design (UX/UI), conceptual technical writing, and semantic data-quality review sit at the expensive-verifier end, where the reviewer is a human and the verifier-cost economics match the sales domain.

Why it matters:

- the verification-policy strategy is a top-priority lever for part of the productization domain but weakens sharply in design, conceptual docs, and semantic data review
- vendor pricing reflects this — design tools (Figma, v0, Galileo) price in flat tiers that absorb usage variance, similar to sales and investment tooling, precisely because the binding cost is the human reviewer's time rather than the generation cost
- scenario and strategy recommendations should be qualified by the productization sub-domain's verifier position, not only by the top-level domain

## Implications for This Repository

The repository should prioritize research outputs that directly address these gaps:

- a direct-versus-indirect cost taxonomy
- a workflow-level total-cost definition
- explicit quality thresholds by task type
- shared reporting conventions across tasks
- comparative analysis of routing, retries, tool use, and oversight under one framework

## Immediate Research Priorities

1. Formalize workflow-level total cost.
2. Define acceptance criteria by task category.
3. Define shared reporting units for direct and indirect costs.
4. Compare the most mature optimization strategies under the same conceptual framework.
5. Build benchmark-ready experimental blueprints that reflect end-to-end task solving rather than isolated inference calls.
