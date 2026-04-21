# Cost Aggregation

## Purpose

This document defines how raw episode logs should be aggregated into research metrics.

## Reporting Layers

Research outputs in this repository should report results at three layers:

### 1. Raw Component Layer

Report disaggregated metrics:

- model spend
- tool spend
- token usage
- latency
- retries
- human minutes
- verification count
- recovery steps

### 2. Cost Vector Layer

Report a cost vector per policy:

- average direct monetary cost per episode
- average total latency per episode
- average human minutes per episode
- average retries per episode
- average verification steps per episode
- threshold-satisfying success rate

### 3. Weighted Total-Cost Layer

When scenario-specific comparison is needed, compute:

`WeightedTotalCost = a * direct_cost_usd + b * latency_seconds + c * human_minutes + d * retries + e * tool_cost_usd + f * recovery_steps`

The coefficients must be declared alongside every table or figure that uses this score.

## Aggregation Rules

- failed episodes still count toward average cost
- cost should be reported both per episode and per successful episode
- human escalation should remain visible as both a rate and a cost term
- retries should be counted beyond the first attempt only
- tool cost should be reported separately before inclusion in total direct cost

## Minimum Output Table

Each benchmark comparison should include:

| Policy | Quality threshold met | Success rate | Direct cost / episode | Direct cost / success | Latency / episode | Human minutes / episode | Retries / episode | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |

## Frontier Reporting

The default analytical view should be a frontier rather than a single ranking. A policy is useful when it offers one of the following:

- lower cost at the same quality level
- higher quality at the same cost level
- lower indirect cost at the same direct cost and quality level

## Interpretation Rule

No policy should be called better by default unless it is clear which cost component improved and which constraints remained fixed.

## Fat-Tail and Domain-Conditioned Reporting

The mean-centered reporting layers above are adequate for productization-domain workloads where failure cost is bounded and approximately thin-tailed. The sales domain defined in [`skill-domain-taxonomy.md`](skill-domain-taxonomy.md) violates this assumption: deliverability collapse, regulatory exposure, MNPI mishandling, and brand reputation damage have failure-cost distributions where the upper tail dominates the mean. Reporting only the mean systematically understates the true expected total cost.

For sales-domain episodes (and for productization episodes prone to agentic resource exhaustion), the following additions are recommended:

- report `p50`, `p95`, and `p99` for direct cost per episode and for human review minutes per episode in addition to the mean
- report `CVaR` (conditional value at risk) at `p95` or `p99` for any cost line known to be fat-tailed in the relevant domain
- report a separate `tail_event_rate` for workflow-level catastrophic failures (e.g., domain deliverability collapse, MNPI exposure) whose blast radius is broader than the failing episode itself
- when comparing policies across domains, do not collapse the two domains onto the same mean-cost-per-episode plot; mean-cost summaries are not comparable when their tail mass differs

The two productization extension fields most relevant here are `agent_turn_count` and `accumulated_context_tokens`. The two sales extension fields most relevant here are `deliverability_score` and `async_outcome_reference`. Aggregators should expose these by default for any episode that carries them.

## Cross-Domain Comparability

Cross-domain frontier plots are misleading because the verification mechanism, feedback-loop length, and human-cost asymmetry differ. When a comparison is needed across domains, it should be done at the level of:

- a domain-specific cost vector reported per domain
- a normalized success rate against the domain's own quality threshold
- a separate tail-risk indicator per domain

A single weighted total cost should not be used to rank policies across domains.
