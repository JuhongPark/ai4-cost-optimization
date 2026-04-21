# Scenario Cost Assumptions

## Purpose

This document translates the repository's general cost framework into scenario-specific assumptions that can support applied comparisons.

## Why Assumptions Need To Be Explicit

Weighted cost comparisons are only meaningful if the repository states what each unit of delay, human time, or downstream failure is assumed to cost. The goal is not perfect realism. The goal is transparent, revisable assumptions.

## Shared Assumption Types

Every scenario should declare assumptions for:

- direct model spend
- latency sensitivity
- human review minutes
- escalation capacity
- downstream failure cost
- acceptable quality threshold

## Scenario A: Code Generation and Repair

### Operational assumption

- each failed code output can create nontrivial debugging overhead
- executable verification is available
- human review is relatively expensive but high value

### Suggested initial assumptions

- quality gate: test pass required
- one human review event: 8 to 15 minutes
- unresolved failed episode: high downstream cost
- latency penalty: medium
- verification cost: low relative to debugging cost

### Interpretation

This scenario should usually favor policies that spend more upfront on verification if they sharply reduce debugging and failed handoff burden.

## Scenario B: Document Extraction and Back-Office Processing

### Operational assumption

- large task volume
- partial errors are common
- cleanup queues exist
- some fields may have compliance or audit sensitivity

### Suggested initial assumptions

- quality gate: target precision and recall or field-level F1
- one human review event: 2 to 6 minutes
- unresolved failed episode: medium to high downstream cost
- latency penalty: low to medium
- validation cost: low to medium

### Interpretation

This scenario often makes selective review attractive because blanket human QA is expensive at scale, but silent extraction errors can also accumulate hidden correction cost.

## Scenario C: Classification and Routing Operations

### Operational assumption

- episodes are short
- model spend is low relative to volume
- queue load from escalation can quickly become the bottleneck

### Suggested initial assumptions

- quality gate: target accuracy or F1 above operating threshold
- one human review event: 1 to 4 minutes
- unresolved failed episode: medium downstream cost with some high-priority outliers
- latency penalty: medium to high for urgent routing contexts
- verification cost: usually low unless human confirmation is required

### Interpretation

This scenario is often most sensitive to escalation rate and queue saturation rather than per-call API spend.

## Scenario D: Outbound Selling and Customer Outreach

This scenario sits in the **sales** domain as defined in [`skill-domain-taxonomy.md`](skill-domain-taxonomy.md). It maps to scenario S1 in [`../reports/industry-scenarios.md`](../reports/industry-scenarios.md). Concrete 2026 industry data points are in [`../references/skill-domain-evidence-2026.md`](../references/skill-domain-evidence-2026.md).

### Operational assumption

- no automated verifier exists; the salesperson is the verifier and the action gate
- outcome signal (reply, meeting booked, pipeline movement) arrives weeks after the action
- failure modes are fat-tailed: deliverability damage, regulatory exposure, brand reputation
- artifacts split into tiers (named-account proposals vs cold sequences) with very different review depth and per-artifact cost

### Suggested initial assumptions

- quality gate: human send-approval at the artifact tier appropriate for the outreach
- one human review event: 2 to 10 minutes for cold sequence; 20 to 60 minutes for named-account proposal
- unresolved failed episode: medium per-artifact, fat-tailed at the workflow level (deliverability collapse, regulatory exposure)
- latency penalty: low for batch outbound, high for real-time conversational assist
- verification cost: high if attempted at AI level (LLM-as-judge catches surface issues only); the dominant verification cost is human time

### Interpretation

This scenario should usually favor policies that minimize the number of artifacts that reach a counterparty without high-quality human review, and that protect shared infrastructure (sending domain reputation, regulatory posture) as a separate cost category from per-artifact spend.

## Scenario E: Investment Research and Due Diligence

This scenario sits in the **sales** domain as defined in [`skill-domain-taxonomy.md`](skill-domain-taxonomy.md). It maps to scenario S2 in [`../reports/industry-scenarios.md`](../reports/industry-scenarios.md).

### Operational assumption

- ground truth resolves over years (deal performance, fund return)
- the priced human is an analyst or partner-equivalent, with deal sizes in the $10M to $1B+ range
- citation density is the closest analogue to an automated verifier, but every citation costs analyst review minutes
- per-task agent runs can consume 0.5 to 2M tokens including retries; per-deal diligence cost the workflow offsets is in the tens to hundreds of thousands of dollars

### Suggested initial assumptions

- quality gate: every cited claim must be traceable to source; partner-level review at IC memo stage
- one human review event: 5 to 20 minutes per memo section, with citation spot-checks
- unresolved failed episode: high (cited-but-wrong content reaching IC); fat-tailed at the workflow level (regulatory MNPI handling, fiduciary breach)
- latency penalty: low for memo drafting, medium for live deal-team workflows
- verification cost: medium per task (citation review by analyst); cost-effective relative to the per-deal diligence baseline

### Interpretation

This scenario should usually favor multi-model routing (reasoning-tier reserved for evaluation and synthesis, cheaper models for extraction) and per-stage budget caps that prevent agentic-resource-exhaustion on a single deep-research task.

## Suggested Weighting Profiles

The repository should not use one universal weighted-cost function. It should compare a small number of scenario-aligned profiles.

### Profile 1: Automation-Heavy Volume Setting

Best match:

- classification
- high-volume extraction

Emphasis:

- API spend
- latency
- escalation rate

De-emphasis:

- per-episode review depth

### Profile 2: Reliability-Critical Knowledge Work

Best match:

- code generation
- compliance-sensitive extraction

Emphasis:

- failure recovery cost
- human review value
- verification effectiveness

De-emphasis:

- small differences in first-pass latency

### Profile 3: Mixed Operations Setting

Best match:

- teams balancing throughput and correctness

Emphasis:

- direct spend
- human minutes
- retries
- moderate failure penalty

### Profile 4: Sales-Domain Setting

Best match:

- outbound selling
- investment research and due diligence

Emphasis:

- human review minutes (the dominant cost line)
- fat-tailed failure cost (deliverability collapse, MNPI mishandling)
- shared-infrastructure cost (sending domain reputation, compliance posture)
- per-artifact-tier differentiation (cold sequence vs named-account proposal vs IC memo)

De-emphasis:

- per-call API spend at low artifact tiers (it is dominated by seat and integration cost)
- aggressive automated retry without human gating

## Sensitivity Analysis Rule

Every scenario-weighted result should be accompanied by at least one sensitivity check:

- faster vs slower human review
- lower vs higher downstream failure penalty
- narrower vs wider quality threshold

If rankings change under small assumption shifts, the project should report that instability explicitly.

## Recommended Research Use

This document should be used alongside cost-vector reporting. It should inform weighted comparisons, not replace transparent raw metrics.
