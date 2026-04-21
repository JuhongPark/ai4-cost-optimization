# Research Backlog

## Purpose

This document captures the next investigation queue after the first empirical cycle is frozen.

## Highest Priority

- strengthen coding evaluation with executable tests
- replace brittle extraction scoring with field-aware grading
- add sensitivity analysis to weighted comparison scripts
- parameterize human review assumptions in machine-readable config

## Medium Priority

- add scenario-aware result tables
- add queue-load reporting for classification workflows
- compare confidence-gated vs verifier-gated escalation more directly
- expand extraction benchmarks to include noisier real-world documents

## Later Priority

- add agent workflow benchmarks
- separate infrastructure-serving studies from workflow-policy studies
- model downstream failure cost more explicitly
- compare human review with weaker-model oversight paths

## Skill-Domain Follow-Ups

These items extend the work captured in [`../frameworks/skill-domain-taxonomy.md`](../frameworks/skill-domain-taxonomy.md), [`../references/skill-domain-evidence-2026.md`](../references/skill-domain-evidence-2026.md), and the deeper subdomain evidence in [`../references/skill-domain-deep-dive-2026.md`](../references/skill-domain-deep-dive-2026.md).

### Sales-Domain Pilot Design

- propose a minimum sales-domain benchmark that captures at least one of the three defining properties (delayed outcome signal, fat-tailed failure cost, human-as-action-gate); this is Gap 7 in [`../references/gap-analysis.md`](../references/gap-analysis.md)
- evaluate whether FinanceBench plus a controlled outbound-quality protocol can serve as a proxy first cycle for the sales domain
- specify the per-tier human-review depth schema (cold sequence, named-account proposal, IC memo) and validate that the [`../frameworks/logging-schema.md`](../frameworks/logging-schema.md) sales extension fields cover real-world artifact tiers

### Hybrid Workflow Cost Characterization

- quantify the verifiable-vs-judgment cost split for marketing operations, customer support tiers L1/L2/L3, and DevRel content with the same logging schema
- test whether outcome-based pricing (HubSpot Breeze approximately $0.50 per resolved conversation, Sierra negotiated outcomes) maps cleanly onto per-episode total cost when indirect costs are included
- characterize the L2-or-L3 escalation as the binding cost constraint in customer support, replacing the older "L1 deflection rate" framing

### Productization Verifier-Cost Sub-Split

- treat productization as non-uniform on the verifier axis (Gap 8 in [`../references/gap-analysis.md`](../references/gap-analysis.md)): coding/QA/structural-data/code-derived-docs at the cheap-verifier end vs design/conceptual-docs/semantic-data at the expensive-verifier end
- design at least one experiment that compares verification-policy leverage between a cheap-verifier subdomain and an expensive-verifier subdomain inside productization

### Cross-Domain Comparison Methodology

- specify when cross-domain comparison is legitimate (per-domain cost vector, normalized success against domain threshold, separate tail-risk indicator) versus when it is misleading (single weighted scalar across domains)
- write a short methods note that downstream readers can cite when interpreting frontier plots

### Regulatory and Compliance Overlay

- maintain an overlay of regulatory cost per domain (GDPR, CAN-SPAM, CASL, MNPI, fiduciary, IP/copyright, EU AI Act high-risk classification, EU CSRD/EmpCo, Korea PIPA, Japan APPI, China PIPL) and price the compliance burden into the human-review minutes for affected scenarios
- track agentic-resource-exhaustion as a finance accounting category, not a research curiosity, given the 2026 enterprise FinOps trajectory already noted in [`../references/industry-updates-2026-04.md`](../references/industry-updates-2026-04.md)

### Asynchronous Outcome Joins

- design and validate the join between episode-level logs and the asynchronous outcome arrival (reply, meeting booked, deal close, fund return) using the new `async_outcome_reference` field
- compare policies on both per-episode cost and per-realized-outcome cost where the latter is available

### Korea/APAC Pricing and Regulatory Track

- extend industry data collection to the Korean enterprise stack (Linq Alpha, Persona AI, Channel Talk, Naver HyperCLOVA X B2B, Samsung SDS reseller economics) and the Japanese sovereign-LLM and Chinese AI-compute-pricing trajectories
- factor the data-residency multiplier (China-tenant infra typically 1.5–2.5x the Korean/Japan equivalent) into multi-region cost models

## Rule For Pulling Work

Prefer backlog items that improve:

1. benchmark validity
2. policy comparability
3. indirect-cost realism
4. reporting clarity
5. sales-domain measurement infrastructure (no current public benchmarks cover the full sales-domain loop)
