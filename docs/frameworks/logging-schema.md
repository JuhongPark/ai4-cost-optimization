# Logging Schema

## Purpose

This document defines the minimum logging schema for benchmark episodes in this repository.

## Principles

- logging should happen at the episode level
- repeated attempts within one task must remain visible
- direct cost and indirect cost must be separable
- failure should be explicit, not inferred from missing success

## Episode Record

Each problem-solving episode should include the following fields.

| Field | Type | Description |
| --- | --- | --- |
| `episode_id` | string | Unique identifier for the full problem-solving episode. |
| `task_family` | string | High-level family such as `coding`, `classification`, `extraction`, or `agent_workflow`. |
| `task_id` | string | Unique identifier for the task instance. |
| `policy_id` | string | Identifier for the execution policy. |
| `policy_class` | enum | `full_automation`, `selective_hitl`, or `human_first`. |
| `model_id` | string | Primary model used in the episode. |
| `prompt_version` | string | Prompt or policy version identifier. |
| `started_at` | timestamp | Episode start time. |
| `ended_at` | timestamp | Episode end time. |
| `duration_seconds` | float | Total elapsed episode duration. |
| `final_status` | enum | `success`, `failure`, `human_escalation`, or `budget_exhausted`. |
| `failure_category` | enum or null | Failure reason if not successful. |
| `quality_score` | float or null | Task-specific quality score where applicable. |
| `quality_threshold_met` | boolean | Whether the predefined threshold was satisfied. |

## Attempt-Level Fields

An episode may contain one or more attempts. Each attempt should capture:

| Field | Type | Description |
| --- | --- | --- |
| `attempt_index` | integer | Attempt number within the episode. |
| `attempt_model_id` | string | Model used in this attempt. |
| `input_tokens` | integer | Input tokens consumed in the attempt. |
| `output_tokens` | integer | Output tokens generated in the attempt. |
| `attempt_latency_seconds` | float | Latency for this attempt. |
| `attempt_cost_usd` | float | Direct monetary cost for this attempt. |
| `verification_count` | integer | Number of verification steps used in this attempt. |
| `tool_call_count` | integer | Number of external tool calls in this attempt. |
| `tool_cost_usd` | float | External tool/API cost in this attempt. |
| `attempt_outcome` | enum | `accepted`, `rejected`, `failed`, or `escalated`. |

## Indirect-Cost Fields

Indirect-cost accounting should include:

| Field | Type | Description |
| --- | --- | --- |
| `retry_count` | integer | Number of retries beyond the first attempt. |
| `human_review_count` | integer | Number of human review events. |
| `human_review_minutes` | float | Estimated human review time. |
| `human_intervention_count` | integer | Number of explicit interventions or handoffs. |
| `escalation_trigger` | string or null | Trigger for escalation, such as confidence threshold, verifier failure, or policy default. |
| `recovery_step_count` | integer | Number of recovery or fallback steps. |
| `routing_decision_count` | integer | Number of routing decisions. |
| `fallback_path_used` | boolean | Whether any fallback path was activated. |

## Derived Fields

The following should be computed from raw logs:

- `total_direct_cost_usd`
- `total_tool_cost_usd`
- `total_token_count`
- `total_latency_seconds`
- `total_human_minutes`
- `total_retry_count`
- `total_verification_count`
- `total_recovery_steps`

## Failure Categories

The default failure taxonomy is:

- `wrong_answer`
- `quality_below_threshold`
- `timeout`
- `budget_exhausted`
- `tool_failure`
- `verification_failure`
- `routing_failure`
- `unrecovered_workflow_failure`
- `human_escalation`

Domain-specific failure categories (productization-domain modes such as `agentic_resource_exhaustion` and `instruction_drift`, sales-domain modes such as `deliverability_collapse`, `icp_drift`, `regulatory_exposure`, `citation_but_wrong`, and `mnpi_handling_breach`) are defined in [`failure-taxonomy.md`](failure-taxonomy.md) §Domain-Specific Failure Modes and may be used as primary categories when an episode's domain warrants them.

## Domain-Specific Extension Fields

The fields above are required for every episode and are domain-neutral. The two skill domains defined in [`skill-domain-taxonomy.md`](skill-domain-taxonomy.md) carry additional state that should be logged when the benchmark or scenario sits in that domain. Extension fields are optional in the schema and present only when the episode's domain warrants them.

### Productization Extension Fields

| Field | Type | Description |
| --- | --- | --- |
| `skill_domain` | enum | `productization` for episodes in this group. |
| `build_status` | enum or null | `passed`, `failed`, or `not_run` for the final build state. |
| `test_pass_count` | integer or null | Number of tests passing at episode end. |
| `test_fail_count` | integer or null | Number of tests failing at episode end. |
| `type_check_status` | enum or null | `passed`, `failed`, or `not_run`. |
| `agent_turn_count` | integer or null | Number of plan-and-act turns the agent took. |
| `accumulated_context_tokens` | integer or null | Peak input-context size carried into a single request. |
| `verifier_loop_count` | integer or null | Number of verifier-driven self-correction loops. |
| `pr_review_status` | enum or null | `pending`, `approved`, `changes_requested`, or `merged`. |

These fields support analysis of agentic resource exhaustion, instruction drift across long trajectories, and the empirical observation that token cost per turn scales non-linearly with accumulated context (see [`../references/skill-domain-evidence-2026.md`](../references/skill-domain-evidence-2026.md)).

### Sales Extension Fields

| Field | Type | Description |
| --- | --- | --- |
| `skill_domain` | enum | `sales` for episodes in this group. |
| `artifact_tier` | enum | Tier label such as `cold_sequence`, `named_account_proposal`, `investment_memo_section`, `ic_memo`, `due_diligence_package`. |
| `human_edit_distance` | float or null | Normalized edit distance between AI draft and final human-shipped artifact, when measurable. |
| `human_review_depth` | enum or null | `surface_skim`, `line_edit`, `substantive_rewrite`, or `discarded`. |
| `time_to_counterparty_seconds` | float or null | Time between artifact generation and external send; useful for distinguishing batch outbound from real-time assist. |
| `deliverability_score` | float or null | Sender-domain deliverability or list-health metric at episode time, when applicable. |
| `citation_density` | float or null | Number of source-anchored claims per artifact section, for investment-domain artifacts. |
| `citation_check_minutes` | float or null | Human time spent verifying citations during review. |
| `deal_stage` | enum or null | `prospect`, `qualified`, `proposal`, `negotiation`, `closed_won`, `closed_lost`, or investment-side equivalents (`screening`, `dd`, `ic`, `closed`, `passed`). |
| `async_outcome_reference` | string or null | Identifier for the delayed outcome record (reply event, meeting booked, deal close, fund return) so that asynchronous outcome arrival can be joined back to the episode. |
| `async_outcome_arrival_seconds` | float or null | Time between artifact send and outcome-event arrival, when known. |

These fields support the sales-domain reality that the success signal is delayed by weeks to months, that artifact tiers carry very different review depth, and that fat-tailed regulatory or deliverability failures are workflow-wide rather than per-episode.

## Recommended Storage Format

The simplest recommended format is one JSON object per episode with nested attempt records. A tabular export can then be derived for analysis. When extension fields are present, they should sit at the same level as the core episode fields so that downstream aggregators can join them into per-domain reports without schema migrations.
