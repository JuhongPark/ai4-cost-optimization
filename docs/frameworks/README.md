# Frameworks

This directory stores evaluation frameworks, metric definitions, and cost models used in the research.

Suggested reading order: cost taxonomy → evaluation framework → evaluation objectives → policy design space → strategy taxonomy → skill domain taxonomy → AI system architecture → AI system lifecycle → AI system operations → AI system economics → logging schema → cost aggregation → failure taxonomy → scenario cost assumptions.

## Foundations

- [`cost-taxonomy.md`](cost-taxonomy.md): direct-cost vs indirect-cost framework plus the orthogonal fixed-vs-marginal dimension for AI problem solving.
- [`evaluation-framework.md`](evaluation-framework.md): quality-constrained total-cost evaluation framework.
- [`evaluation-objectives.md`](evaluation-objectives.md): candidate optimization objectives and when to use them.

## Policy and Strategy Space

- [`policy-design-space.md`](policy-design-space.md): explicit design axes for model, routing, verification, retry, tools, and oversight.
- [`strategy-taxonomy.md`](strategy-taxonomy.md): categories of optimization strategies compared across experiments.
- [`skill-domain-taxonomy.md`](skill-domain-taxonomy.md): sales (selling and investment) vs productization (product implementation) skill-domain split that reorders strategy priorities by domain.

## System Design and Management (MIT SDM Lens)

- [`ai-system-architecture.md`](ai-system-architecture.md): multi-agent topology, memory architecture, orchestration, verification pipeline, decision architecture, and team topology as first-class cost drivers.
- [`ai-system-lifecycle.md`](ai-system-lifecycle.md): stage-gate model (PoC → pilot → production → steady-state → deprecation) with per-stage strategy priority shifts, evaluation regime evolution, model update management, drift response, and technical-debt management.
- [`ai-system-operations.md`](ai-system-operations.md): SLIs and SLOs for AI, observability stack, incident response, FinOps for AI, FMEA, graceful degradation, fallback chain, blast-radius management, SRE-for-AI maturity.
- [`ai-system-economics.md`](ai-system-economics.md): lifecycle TCO with fixed-vs-marginal decomposition, tradespace exploration, real options analysis, model depreciation, risk reserve, people cost including opportunity cost.

## Operational Schemas

- [`logging-schema.md`](logging-schema.md): episode-level logging schema for benchmark runs with per-domain extension fields.
- [`cost-aggregation.md`](cost-aggregation.md): aggregation and reporting rules including fat-tail and domain-conditioned reporting.
- [`failure-taxonomy.md`](failure-taxonomy.md): shared failure classes plus productization-domain and sales-domain specific failure modes.

## Applied Assumptions

- [`scenario-cost-assumptions.md`](scenario-cost-assumptions.md): scenario-specific assumptions for weighted cost comparisons, including sales-domain scenarios.
