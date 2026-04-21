# Failure Taxonomy

## Purpose

This document defines a shared failure taxonomy for episode-level analysis.

## Failure Classes

### Quality Failures

- `wrong_answer`: the final answer is incorrect
- `quality_below_threshold`: output exists but does not satisfy the minimum quality rule

### Budget Failures

- `timeout`: the episode exceeds the allowed time budget
- `budget_exhausted`: the episode exhausts the allowed cost or attempt budget

### Tool and Verification Failures

- `tool_failure`: an external tool or API call fails
- `verification_failure`: the verifier rejects the answer or the verification path breaks

### Policy Failures

- `routing_failure`: the routing decision sends the task to an inadequate path
- `fallback_failure`: a fallback path is triggered but still fails to recover the episode
- `unrecovered_workflow_failure`: a multi-step execution fails without successful recovery

### Human-Related Outcomes

- `human_escalation`: the task is escalated to a human before acceptable completion
- `human_rejection`: human review rejects the answer after generation

## Domain-Specific Failure Modes

The categories above are domain-neutral. The two skill domains defined in [`skill-domain-taxonomy.md`](skill-domain-taxonomy.md) introduce additional failure modes that map onto the categories above but carry domain-specific cost shapes. Concrete 2026 evidence behind these modes is in [`../references/skill-domain-evidence-2026.md`](../references/skill-domain-evidence-2026.md).

### Productization-Domain Failures

- `agentic_resource_exhaustion`: long-horizon agent loop accumulates context-laden retries until the trajectory budget is exhausted. Maps to `budget_exhausted`. Cost shape: a failed retry at turn 40 costs approximately 3x the first-turn cost in the same session because accumulated context travels with every request.
- `instruction_drift`: agent loses adherence to the original instruction over a long trajectory. Maps to `wrong_answer` or `unrecovered_workflow_failure`. Observed as the dominant non-submission failure mode in SWE-Bench Pro evaluations of frontier models.
- `hallucinated_api_or_dependency`: agent invokes a non-existent function, package, or interface. Maps to `tool_failure` or `verification_failure` depending on whether tests catch it.
- `regression_past_pr_review`: change merges through PR review but breaks behavior the test suite did not cover. Maps to `wrong_answer`. Cost is bounded by revert + re-ship.
- `verifier_passing_but_wrong`: tests pass and the change ships, but the test itself was inadequate (a "broken test masquerading as success"). Maps to `verification_failure` with a delayed-detection variant.

### Sales-Domain Failures

- `deliverability_collapse`: AI-driven outbound volume triggers ISP downgrade or domain blocking, degrading deliverability for all future email including human-written. Maps to `unrecovered_workflow_failure` at the workflow level. Cost is fat-tailed — affects all subsequent episodes, not just the failing one.
- `icp_drift`: artifact (outbound, account plan, memo) is sent to a counterparty whose profile does not match the intended ICP. Maps to `wrong_answer`. Cost is asymmetric — the rep wastes time on a low-fit counterparty AND damages list quality.
- `regulatory_exposure`: artifact reaches a counterparty in a way that violates GDPR, CAN-SPAM, CASL, MNPI, fiduciary, or comparable regulation. Maps to `human_rejection` if caught at review, or `unrecovered_workflow_failure` if shipped. Cost is fat-tailed and multi-million-dollar per documented case.
- `citation_but_wrong`: investment-domain artifact contains a cited claim, but the citation does not actually support the claim. Maps to `wrong_answer` with a delayed-detection variant — analyst review may not catch this on every citation.
- `reputation_damage`: customer-facing artifact reaches a counterparty with a hallucinated detail or persona miss. Maps to `wrong_answer`. Cost is fat-tailed at the brand level when patterned across multiple counterparties.
- `mnpi_handling_breach`: investment-domain agent inadvertently surfaces material non-public information to an unauthorized recipient or context. Maps to `regulatory_exposure`. Cost is fat-tailed and includes regulator enforcement risk.

## Usage Rule

Every unsuccessful episode should be assigned one primary failure category, even if multiple things went wrong. Secondary notes can be kept separately if needed.

When a benchmark or scenario is associated with one of the skill domains, the domain-specific failures above should be available as primary categories. When reporting, group costs by failure category but flag fat-tailed sales-domain failures separately so that mean-cost summaries do not understate them. The cost-aggregation rules in [`cost-aggregation.md`](cost-aggregation.md) §Fat-Tail and Domain-Conditioned Reporting cover this in more detail.
