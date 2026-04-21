# AI System Economics

## Purpose

This document provides a lifecycle total-cost-of-ownership (TCO) framework for AI systems, in the MIT SDM engineering-economics tradition. It extends [`cost-taxonomy.md`](cost-taxonomy.md) (which operates at the episode level) and [`cost-aggregation.md`](cost-aggregation.md) (which operates at the reporting level) to the deployment-lifecycle level. The 2026 evidence behind the framework is in [`../references/ai-system-design-evidence-2026.md`](../references/ai-system-design-evidence-2026.md).

The naive "tokens times price times volume" calculus dominant in 2023-2024 has been replaced by lifecycle frameworks that import the analytical machinery of defense and aerospace cost engineering (Fabrycky and Blanchard Life Cycle Costing; Defense Systems Management College LCC methodology). The transfer is non-trivial: AI systems lack physical wear but suffer capability obsolescence; they have no traditional O&M phase but require continuous eval debt servicing.

MIT FutureTech's `AI and Scale: A Quantitative Task-Based Theory of Automation` (Lashkari, Li, Qiu, Thompson 2026) supplies the central formal result: automation is economical only when task volume V exceeds F / (c_human − c_AI), where F is fixed automation cost and c are marginal per-task costs. Their empirical calibration shows 60-80% of current enterprise AI pilots sit below this threshold — which reframes Gartner's forecast that 40% of agentic AI projects will be cancelled by 2027 as rational option exercise rather than failure.

## 1. Fixed / Semi-Fixed / Marginal Decomposition

Following Fabrycky-Blanchard LCC taxonomy, AI system costs partition into three classes. The productization-domain and sales-domain evidence in [`../references/skill-domain-evidence-2026.md`](../references/skill-domain-evidence-2026.md) and [`../references/skill-domain-deep-dive-2026.md`](../references/skill-domain-deep-dive-2026.md) give 2026 bands.

### 1.1 Fixed (sunk at deployment, volume-independent)

- integration engineering: $200K-$2M for enterprise deployments
- prompt and eval suite construction: $50K-$500K per use case
- compliance audits: SOC 2 Type II $75-$150K; ISO 27001 $50-$100K; FedRAMP Moderate $400K-$2M amortized
- team formation: AI Platform Engineer, AI SRE, Eval Engineer hiring and enablement

### 1.2 Semi-Fixed (step function)

- new use case domain: triggers a discrete jump of $150-$400K (new eval suite, new prompt library, new failure-mode taxonomy)
- new regulator jurisdiction: $200K-$1M (EU AI Act high-risk, state-level US privacy, APAC residency)
- new tenant tier: per-tier observability and isolation infrastructure

### 1.3 Marginal (scales with task volume)

- tokens and tool API calls
- per-episode human review labor ($60-$180/hour for domain review)
- inference serving
- per-episode retry and recovery overhead

### 1.4 Orthogonality with Direct/Indirect

This decomposition is orthogonal to the direct-vs-indirect split in [`cost-taxonomy.md`](cost-taxonomy.md). Any cell of the 2x2 (direct-fixed, direct-marginal, indirect-fixed, indirect-marginal) is populated:

- direct-fixed: inference-server capacity reservation, dedicated capacity agreements
- direct-marginal: per-token usage cost
- indirect-fixed: eval suite construction, compliance audit
- indirect-marginal: per-episode human review minutes

Most cost conversations collapse this 2x2 and miss that the binding constraint is often an indirect-fixed commitment (integration, compliance) rather than a direct-marginal inefficiency (token price).

## 2. Tradespace Exploration

Single-point A/B comparisons are inadequate when the design has more than three or four free variables. The Fitzgerald-Ross Multi-Attribute Tradespace Exploration (MATE) framework treats architecture choices as design variables and sweeps them to map a Pareto frontier across multiple objectives.

### 2.1 Design Variables (2025-2026 AI)

- **architecture-layer** (from [`ai-system-architecture.md`](ai-system-architecture.md)): topology, memory stack, orchestration pattern, verification pipeline, authority gradient
- **policy-layer** (from [`strategy-taxonomy.md`](strategy-taxonomy.md)): model tier, routing policy, retry or self-consistency depth, verification depth, tool-use policy, escalation triggers
- **context-layer**: RAG chunk size, agentic tool budget, memory horizon, caching aggressiveness

### 2.2 Objective Axes

- cost per resolved task
- quality (task-specific accuracy or user satisfaction against the declared threshold)
- p95 and p99 latency
- reliability (episodic cost variance, failure rate, CVaR at p99 on the fat-tailed axis)

### 2.3 Method

Monte Carlo sampling over 10^4 to 10^5 policy configurations, scored against a held-out eval trace, has become the dominant 2025-2026 method. NASA ADEPT's application to autonomy systems and MIT ESD tradespace studies adapted to AI provide the reference methodology.

### 2.4 When Tradespace Beats A/B

- when the number of design variables exceeds three or four, making orthogonal A/B enumeration combinatorial
- when stakeholder preferences diverge, so a Pareto set rather than a single point is needed
- when operating distribution is uncertain, so sensitivity of the frontier matters more than the point estimate
- when real options are embedded in the design (see §3), because tradespace reveals the option-creating points

For routine per-call comparisons (one model vs another on one endpoint), A/B remains appropriate.

## 3. Real Options Analysis

The investment decision cadence of AI — pilot, expand, defer, abandon, switch — is naturally real-options-shaped. 2025-2026 literature (notably the MIT Sloan/SDM working paper series on AI Capability as a Real Option) has started formalizing this.

### 3.1 Option Types

- **option to expand**: pilot-to-scale is a call option. Strike = incremental platform cost; underlying = realized task value; volatility = quality and cost uncertainty. Binomial lattice treatment is more defensible than Black-Scholes because AI value distributions are path-dependent and non-log-normal.
- **option to defer**: the 2023-2026 frontier-model release cadence (approximately every 8-14 months, with 3-10x cost-per-capability improvement) makes waiting genuinely valuable. Deferral option value is maximized when current capability sits just below the deployment threshold and cost-per-capability volatility is high.
- **option to abandon**: Gartner's 40% cancellation rate on agentic AI projects is optimal option exercise when (a) per-period burn exceeds per-period information gain, (b) the realized quality-cost trajectory after N weeks has crossed below the F / (c_human − c_AI) threshold, and (c) the correlation of this pilot's lessons with the next candidate pilot is low
- **option to switch**: vendor or model or architecture switching is a compound option — pay switching cost to gain access to a new underlying. With frontier-model useful lives shortening, optionality-to-switch should be architected in, not eliminated.

### 3.2 When Fast Abandonment Is Optimal

- per-period cash burn exceeds per-period information gain
- realized quality-cost trajectory has crossed below the scale threshold implied by fixed-cost commitments
- lessons from this pilot transfer poorly to the next candidate, so continuing does not buy option value on the next investment

Under these conditions, a 40% cancellation rate on optional investments is a signature of rational option exercise, not pathological execution.

## 4. Depreciation and Upgrade Schedule

AI models do not wear out — they obsolesce. Cost-accounting treatment is equivalent to physical depreciation under a different useful-life assumption.

### 4.1 Observed 2025-2026 Useful Lives

- GPT-4 (March 2023 release, legacy status April 2026): approximately 36 months nominal, approximately 18 months effective for new deployments
- Claude 3.5 Sonnet (June 2024 release): superseded within approximately 12 months
- frontier-tier refresh cadence: 9-14 months

### 4.2 Depreciation Schedule Recommendation

- model-specific investments (prompt libraries, fine-tunes, per-model evals): 12-18 month schedule
- model-agnostic investments (abstraction layers, eval harnesses, compliance): 3-5 year schedule

### 4.3 Switching Cost

The cash outflow triggered on obsolescence:

- re-prompting: 0.3-1.5 FTE-months per major use case
- re-evaluation: 0.5-2 FTE-months
- integration rework: 0.2-1 FTE-month per downstream system

Organizations with strong model abstraction spend 30-50% of naive switching cost; those with prompt-level lock-in spend 150-200%. Abstraction is an investment that pays off on switch events, not on operation — a classic option-value argument.

## 5. Risk Reserve

PMBOK contingency reserves of 10-30% are the starting point but insufficient for AI because of three fat-tailed drivers:

- runaway agent episodes (agentic resource exhaustion)
- regulatory fines under EU AI Act (up to 7% global revenue or €35M)
- eval debt — the accrued liability from evals deferred during velocity-optimized periods

The 2025-2026 enterprise pattern is a **two-tier reserve**:

- management reserve of 15-25% for known-unknowns
- regulatory and fat-tail reserve of 5-15% held separately

The operational budget cap on agentic resource consumption (token cap, tool-call cap, wall-clock cap) is properly understood as **the reserve mechanism itself** — it bounds the tail at the episode level rather than accruing a balance-sheet reserve. This is the architectural cheaper-than-balance-sheet way to hold reserve capacity.

## 6. People Cost

Often mis-accounted because salaries are visible but adjacent costs are not. 2025-2026 US market benchmarks:

- AI Platform Engineer: $250-$400K fully loaded
- Eval Engineer: $200-$350K
- AI Product Manager: $220-$320K

Prompt Engineer as a distinct role has largely been absorbed into ML or Platform Engineer scope since 2024.

- **enablement cost**: $8-$25K per non-AI engineer over 6 months (training plus reduced velocity)
- **opportunity cost** (the most systematically omitted line item): senior engineers pulled from core product work generate an implicit cost equal to the marginal product of that forgone work — typically 1.5-2.5x loaded salary. When a pilot is abandoned, this cost is fully sunk but rarely recorded.

## 7. Lifecycle Costing Framework (Fabrycky-Blanchard Adapted)

The classical partition maps to AI as follows:

| Classical phase | AI mapping | Dominant cost driver |
| --- | --- | --- |
| R&D | Pilot and design | Eval harness construction, integration scoping |
| Acquisition | Integration and initial deployment | Platform engineering, compliance, tool integration |
| O&M | Inference cost plus eval maintenance plus prompt and model refresh | Marginal inference cost, eval refresh, drift response, human review |
| Phase-out / disposal | Migration to successor system | Switching cost, dual-run budget, data and audit preservation |

Defense Systems Management College LCC methodology's key contribution is discounted-cash-flow treatment over the full lifecycle and the observation that O&M typically dominates acquisition by 3-5x. This ratio appears to hold for production AI systems based on 2025-2026 enterprise data: inference plus eval maintenance runs approximately 4x initial integration for steady-state deployments.

## 8. Most-Omitted TCO Items

Based on 2025-2026 enterprise cost audits, the systematically under-accounted items are:

- **eval debt** — carried as unrecorded liability rather than capitalized against refresh schedule
- **switching cost** — either uncapitalized or capitalized against the wrong useful life (ignoring model obsolescence cadence)
- **opportunity cost of senior talent** — the implicit marginal product of engineers pulled from core work; never recorded on the income statement
- **fat-tail reserve** — conflated with ordinary contingency, understating the regulatory and agentic-exhaustion tail

A TCO model that surfaces these four items is sufficient to move the analysis from incomplete to actionable.

## 9. Minimal TCO Template

Every significant AI system investment should declare:

- **fixed cost floor**: integration, compliance, eval harness, team, platform — amortized over expected useful life
- **semi-fixed step map**: the boundaries (new use case, new jurisdiction, new tier) that will trigger a cost step
- **marginal cost per episode and per successful outcome**: direct and indirect, from [`cost-taxonomy.md`](cost-taxonomy.md)
- **fat-tail reserve policy**: per-episode budget cap plus balance-sheet reserve for regulatory exposure
- **switching cost estimate**: at expected model-replacement cadence, priced per major use case
- **people cost including opportunity cost**: the implicit marginal product of engineers on AI vs alternative work
- **real-options position**: expand, defer, abandon, switch — which option is currently held and what signal would exercise it

This TCO template closes the loop from architectural commitment (in [`ai-system-architecture.md`](ai-system-architecture.md)) through lifecycle stage (in [`ai-system-lifecycle.md`](ai-system-lifecycle.md)) and operational practice (in [`ai-system-operations.md`](ai-system-operations.md)) to the investment-level decision.
