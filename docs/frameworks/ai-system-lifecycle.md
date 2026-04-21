# AI System Lifecycle

## Purpose

This document treats the deployed AI system as a lifecycle object with stages, transitions, gate criteria, and retirement, in the MIT SDM tradition of engineered-systems lifecycle management. The repository's prior frameworks focus on workflow-level and episode-level policy design; this document frames the *deployment-level* question of how an AI system moves from prototype through production into retirement, and how the dominant cost and risk axes reorder at each stage.

Traditional stage-gating (Cooper 1990; INCOSE SE Handbook) assumes a build-once-then-operate artifact with a fixed Technology Readiness Level progression. LLM and agent systems violate that assumption in three load-bearing ways:

- the capability-critical component, the pre-trained model, is sourced externally and re-released on quarterly cycles with limited backward compatibility
- the unit of change is a natural-language prompt plus a tool schema, not compiled code, which amplifies the CACE principle (Changing Anything Changes Everything; Sculley et al. 2015)
- correctness is distributional, not binary, so acceptance tests become statistical rubrics rather than assertions

A defensible 2026 lifecycle model keeps the six-stage skeleton but re-instruments every gate around **evaluation evidence, tail-aware cost, and upstream provider risk** rather than feature completeness.

## 1. Stage Model

| Stage | Defining property | Dominant risk | Dominant cost axis |
| --- | --- | --- | --- |
| PoC | Hypothesis tested on small golden set | Misunderstanding of the task | Fixed cost of integration and eval harness construction |
| Pilot | Deployed to a bounded user group | Unknown failure modes at scale | Fixed cost of compliance and platform integration; semi-fixed step costs as new edge cases surface |
| Limited Production | Opened to larger user group with rollback capacity | Silent quality regression | Marginal per-episode cost becomes visible; tail cost may not yet be |
| GA (General Availability) | Full production traffic; SLOs declared | Provider-side update breaking prompt | Marginal cost plus reserve for tail events |
| Steady-state Operation | Continuous operation under SLOs | Drift, eval debt accumulation, prompt debt | Operational stack (observability, FinOps, incident) plus refresh investment |
| Deprecation | Replaced by successor or retired | Migration cost, data and audit preservation | Switching cost; dual-run budget |

Each row maps to a distinct cost-quality trade-off and therefore to a distinct **optimal policy profile**. A policy that is correct at GA may be wasteful at PoC (over-investment in eval harness before the task is clear) or inadequate at steady-state (under-investment in drift detection).

## 2. Stage-Gate Criteria

A stage-gate is a quality bar, a cost bar, and a risk bar. The quality bar is statistical, not assertional. The cost bar must include the tail, not only the mean. The risk bar must include upstream risks (provider deprecations, regulatory shift) that the team does not control.

### PoC → Pilot

- **quality bar**: golden set of at least 30 items; offline eval at or above human baseline on the agreed rubric; ML Test Score at least 1 on each of data, model, infrastructure, monitoring axes (Breck et al. 2017)
- **cost bar**: known per-call cost; no catastrophic tail observed in the first 100 runs
- **risk bar**: system-level safety case v0; no PII leakage path; red-team pass against known prompt-injection vectors

### Pilot → Limited Production

- **quality bar**: golden set versioned; LLM-as-judge calibrated against at least 100 human labels; shadow eval against current baseline on replayed traffic
- **cost bar**: p95 episode cost bounded; retry budget fixed; fat-tail quantile monitored (p99 or CVaR)
- **risk bar**: incident runbook; rate limiting; full prompt-injection red team; EU AI Act high-risk classification assessed where applicable

### Limited Production → GA

- **quality bar**: canary at at least 10% with no slice regression beyond agreed delta; CI gate blocks merge on eval regression
- **cost bar**: unit economics signed off (cost per call, cost per resolved case); cache break-even hit
- **risk bar**: deployment-policy review passed; human-in-the-loop path defined per authority gradient in [`ai-system-architecture.md`](ai-system-architecture.md) §5

### GA → Steady-state

- **quality bar**: continuous eval from production telemetry; drift dashboards green across slices; weekly review board
- **cost bar**: cost observability (FinOps and AgentOps) live with budget alerts; tail-conditioned cost modeled
- **risk bar**: model-deprecation migration plan active; versioned safety case

### Steady-state → Deprecation

- **quality bar**: replacement passes parity eval on full traffic replay; N-day deprecation notice honored
- **cost bar**: migration cost amortization plan; dual-run budget capped
- **risk bar**: contractual and compliance sunset checklist

## 3. Evaluation Regime Evolution

The 2026 consensus, visible across the Evaluation-Driven Development and Operations of LLM Agents paper (EDDOps, Wang et al. arXiv:2411.13768), Promptfoo, Ragas, DeepEval, Arize Phoenix, and OpenAI's evaluation best practices, is a three-layer regime that tracks the lifecycle:

1. **offline evaluation on curated golden sets** — versioned inputs, contexts, expected outputs, slice tags — run in CI on every prompt change as a merge-blocking gate
2. **online evaluation** — shadow mode (replay last week of production traffic through the candidate; LLM-as-judge compares pairs) and A/B or canary in live traffic
3. **continuous evaluation** — production telemetry seeds new eval items whenever a novel failure mode appears, closing the loop from operations to offline suite

LLM-as-judge itself evolves along a ladder: **pairwise → rubric → calibrated.** Research in 2026 (RULERS, AutoRubric, Self-Preference Bias in Rubric-Based Evaluation) shows pairwise reduces calibration variance; analytic rubrics outperform holistic rubrics; few-shot calibration against 100-200 human labels materially changes judge verdicts. LangSmith Align Evals and similar features make human-alignment a tracked metric.

Golden-set refresh is itself a managed asset with debt. 2026 guidance is quarterly refresh plus trigger-based refresh when any slice shows drift or a provider releases a new model snapshot. This is where **eval debt** accumulates: outdated goldens, slice coverage gaps, missing negative tests.

## 4. Model Update Management

Model updates are structurally unlike code deploys: behavior changes without a commit. Three deployment patterns map to three distinct failure modes.

| Pattern | Addresses | Cost | Operational complexity |
| --- | --- | --- | --- |
| Shadow deployment | Silent quality regression (the hardest mode — users notice before metrics do) | Roughly 2x inference spend during shadow window; must be time-bounded | Low; requires pair-wise LLM-as-judge |
| Canary release | Bounded blast-radius for unknown-unknowns | Small | High; rollback trigger definition is the real cost |
| Blue/green for AI | Provider-side deprecation and fast rollback | Memory for two pinned versions | Moderate |

Real 2026 deprecation examples illustrate why blue/green is not optional: OpenAI retired GPT-4o, GPT-4.1, GPT-4.1 mini, and o4-mini in ChatGPT on 2026-02-13; Azure OpenAI guarantees at least 60 days' GA retirement notice with a 12-month GA window; Claude 3.5 Sonnet (June 2024) was superseded within approximately 12 months.

**Version pinning vs always-latest** is the underlying policy decision. Pinning is the only defensible default for regulated or contractually bound systems but forces an explicit migration project every time a provider deprecates a snapshot. The 2026 baseline: pin, but budget quarterly migration windows. LangChain 1.0 (October 2025) moved the agent-framework layer to the same discipline — legacy APIs under `langchain-classic` with no breaking changes until 2.0.

Anthropic's Responsible Scaling Policy v3.0 acts as a parallel gate on the risk axis: models above defined capability thresholds must clear ASL evaluations before release. Consumers inherit a deployment calendar they do not control — a governance input to the lifecycle plan.

## 5. Drift Detection and Bimodal Cost Structure

Four drift types with different detection cost and response cost:

- **input drift** — user query embedding distribution shifts; cheap to detect (Wasserstein on embeddings; Kolmogorov-Smirnov is discouraged for high-dimensional embeddings); response is usually prompt or routing adjustment
- **output drift** — response distribution shifts even when inputs and model are unchanged, typically after a silent provider update or tool-output format change; detectable only if outputs are logged and embedded
- **concept drift** — the task definition itself shifts (what counts as a good triage response); detectable only through downstream business metrics and user-feedback slicing; the most expensive drift to detect and the most expensive to ignore
- **performance drift** — quality decay on golden set or continuous production eval; detectable cheaply if continuous eval is wired

Drift creates a **bimodal cost structure**: detection cost (sensors, eval compute, human review time) vs ignore cost (degraded outcomes, escalation cost, reputation, incident response) vs response cost (reprompt, retrain, re-architect).

The 2026 decision rule is a staircase:

1. if the fix is within a guardrail threshold and reversible, apply it at runtime (AgentOps bounded adjustment)
2. if the fix requires prompt or tool-schema change, treat it as a code change and run it through the CI eval gate
3. if the fix requires swapping models or retrieval backends, re-enter the Pilot gate on the affected slice
4. retrain or fine-tune is the last resort, not the default — reprompt and re-architect usually dominate economically in LLM systems

## 6. AI-Specific Technical Debt

Sculley et al. 2015 identified CACE, glue code, pipeline jungles, dead experiment paths, and data debt as traditional ML technical debt. LLM and agent systems add three more categories:

- **prompt debt** — accreted "just one more line" instructions in system prompts; managed by prompt versioning, CI eval gating, and quarterly prompt audits. PromptDebt (arXiv:2509.20497) reports prompt-design-related self-admitted technical debt at approximately 6.6% of commits in LLM projects, with instruction-based prompts most vulnerable.
- **context debt** — system prompt plus tool list plus few-shots bloating past the cache-friendly prefix, silently inflating per-episode cost. Relevant because Anthropic's March 14, 2026 removal of the long-context surcharge made prefix design the remaining cost lever for 1M-token workloads.
- **eval debt** — coverage gaps, stale goldens, un-calibrated judges; the liability accrued when evals are deferred during velocity-optimized periods

**Pipeline or harness debt** — orchestration complexity that makes failure modes hard to isolate — is the hybrid category and spans the agentic framework layer.

Debt service should be an explicit line item in the steady-state budget, not a post-hoc cleanup. The quarterly refresh cadence in §3 is the default debt service interval.

## 7. How the Optimal Policy Evolves Across Stages

| Stage | Strategy priority shift |
| --- | --- |
| PoC | Model selection dominates; verification and routing are premature; retry is acceptable as quick iteration |
| Pilot | Add verification (executable first); difficulty-based routing becomes measurable; escalation triggers get defined |
| Limited Production | Retry policy is bounded by budget; verification-routing tradespace explored; observability stack enters |
| GA | Full strategy taxonomy in play; policy comparison uses the frontier in [`cost-aggregation.md`](cost-aggregation.md) |
| Steady-state | Drift response policy dominates; eval debt service becomes recurring; model-update cadence as first-class decision |
| Deprecation | Switching cost analysis; migration policy planning; abandon option evaluation |

This reordering is why a single strategy-taxonomy priority list in [`strategy-taxonomy.md`](strategy-taxonomy.md) cannot be the final word: the list is stage-conditional. A system that declares its stage makes its strategy priorities legible.

## 8. Minimal Lifecycle Plan

Every deployed AI system should declare and maintain:

- current lifecycle stage and the evidence used to enter it
- the gate criteria for the next transition
- the drift-response staircase and the triggers that move up the staircase
- the model-update cadence and the pattern (shadow, canary, blue/green) for each update type
- the eval refresh schedule and the debt-service budget
- the deprecation plan or at minimum the deprecation trigger conditions (provider retirement, cost ceiling, quality ceiling, regulatory shift)

This lifecycle plan is the bridge between architectural commitments in [`ai-system-architecture.md`](ai-system-architecture.md), operational practice in [`ai-system-operations.md`](ai-system-operations.md), and the economic model in [`ai-system-economics.md`](ai-system-economics.md).
