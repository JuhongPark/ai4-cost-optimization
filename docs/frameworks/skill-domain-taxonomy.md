# Skill Domain Taxonomy

## Purpose

This document divides AI use cases into two **skill domains** based on what the AI output participates in:

- **sales domain**: AI use cases whose output participates in revenue-generating commercial transactions with external counterparties (selling and investment).
- **productization domain**: AI use cases whose output is product or system artifacts consumed by internal engineering processes (product implementation only).

The repository's other frameworks — [`cost-taxonomy.md`](cost-taxonomy.md), [`strategy-taxonomy.md`](strategy-taxonomy.md), and [`policy-design-space.md`](policy-design-space.md) — are domain-neutral. This document is a complementary lens: the same direct-vs-indirect cost split and the same seven strategy families apply to both domains, but their **priorities reorder** depending on which domain the workflow lives in.

This split is motivated by a concrete observation about this repository: the three industry scenarios in [`../reports/industry-scenarios.md`](../reports/industry-scenarios.md) (code generation, document extraction, classification routing) all sit in the productization domain or in operational back-office work that resembles it. The sales domain — outbound, deal research, investment analysis — has different verification mechanisms, different feedback-loop timescales, and different human-cost asymmetries, and was not previously made explicit in the repository.

## 1. Sales Domain

### 1.1 Boundary

Sales-domain AI workflows produce artifacts that influence a **counterparty decision** — a prospect, customer, limited partner, or investment target. The "ground truth" of correctness only resolves when that counterparty acts: a deal closes, a contract is signed, a check is wired, a portfolio company succeeds or fails.

### 1.2 Subdomains

**Selling**

- outbound prospecting and lead enrichment
- conversation intelligence (call recording, summarization, coaching signal extraction)
- proposal, RFP response, and quote generation
- contract analysis and redlining
- account research and account-plan drafting
- sales coaching and rep enablement

**Investment / Equity Research / Due Diligence**

- deal sourcing and pipeline triage
- market sizing and competitive landscape
- financial modeling and scenario analysis
- investment memo drafting
- term sheet and definitive document analysis
- due diligence interview transcription and synthesis
- portfolio reporting and quarterly LP letters

### 1.3 Cost Profile

Mapped onto [`cost-taxonomy.md`](cost-taxonomy.md):

- **direct cost**: usually low to moderate per artifact, because the output is a single document, email, memo, or call summary. Token volume per task is bounded by the document length, not by long agentic loops.
- **indirect cost**: dominated by **human review** and by **downstream business outcome**. The salesperson, partner, or principal must read and adjust the AI output before it leaves the firm. There is rarely an automated verifier: no compile step exists for an outbound email or an investment memo.

The dominant indirect-cost components in the sales domain are:

- human oversight cost — the salesperson's, analyst's, or partner's time
- failure recovery cost — when an artifact reaches the counterparty with a wrong fact, the recovery is a damaged relationship or a lost deal, which is fat-tailed
- orchestration cost is comparatively low because workflows are usually shallow (research → draft → human review → send), not deeply agentic

## 2. Productization Domain

### 2.1 Boundary

Productization-domain AI workflows produce artifacts that flow into **internal engineering processes**: code, tests, documentation, infrastructure-as-code, runbooks. The "ground truth" of correctness resolves on a much shorter timescale because automated verifiers exist.

### 2.2 Subdomains

**Coding assistance (IDE-integrated)**

- inline autocomplete and chat-in-IDE
- refactor and rename
- debugging help and error explanation

**Agentic coding**

- task-level autonomous execution against a repository
- multi-step plan-and-act with tool use, tests, and recovery
- background long-horizon work

**Code review and test generation**

- automated PR review
- unit, mutation, and property-based test generation
- security and dependency review

**DevOps and SRE**

- infrastructure-as-code generation and review
- runbook drafting and incident triage assist
- log and trace analysis

### 2.3 Cost Profile

Mapped onto [`cost-taxonomy.md`](cost-taxonomy.md):

- **direct cost**: highly variable. Inline autocomplete is cheap per call but high in volume; agentic coding tasks can run dozens or hundreds of model calls per task with significant token budgets, especially when retries and tool use accumulate.
- **indirect cost**: dominated by **retry / self-correction** and by **verification**. Failed tests, build breaks, and type errors give the system a cheap and immediate signal that triggers a retry or refinement loop.

The dominant indirect-cost components in the productization domain are:

- retry and self-correction cost — agentic coding loops can drive token consumption far above the first attempt
- failure recovery and orchestration cost — multi-step plans, tool use, and rollback paths
- human oversight cost is real but bounded — PR review is a standard, scheduled gate, and many failures are caught by tests before a human is involved

## 3. Why the Split Matters

The two domains differ along four dimensions that change which optimization levers matter most.

| Dimension | Sales domain | Productization domain |
| --- | --- | --- |
| Verification mechanism | Subjective business judgment; downstream outcome metrics | Cheap, objective tests (compile, type-check, unit, integration, CI) |
| Feedback-loop length | Weeks to months (deal lifecycle, fund return) | Seconds to minutes (REPL, test run, CI) |
| Human cost asymmetry | Sales rep, partner, or principal time is expensive AND the human is the action gate at the closing step | Developer time is expensive but partially substitutable; merge gate is human but is preceded by automated gates |
| Failure cost shape | Fat-tailed: a single bad output can blow a $100K-$10M deal or a wrong investment thesis | Mostly thin-tailed: regressions are caught and reverted; wasted compute is bounded |

The verification dimension is the most consequential. The productization domain has access to a class of indirect-cost reduction levers — automated test feedback, type checking, lints, CI — that simply do not exist in the sales domain at the same fidelity. This single difference cascades into the strategy priority differences in §4.

## 4. Strategy Priority by Domain

This section walks through the seven strategy families in [`strategy-taxonomy.md`](strategy-taxonomy.md) and notes how their priority shifts by domain. The strategy taxonomy itself does not change; only the relative leverage and risk profile per strategy depends on the domain.

### 4.1 Model Selection

- **Productization**: mid-to-high tier on agentic tasks pays back because the verifier catches errors fast and downstream blast is bounded. Cheap models are viable on short, well-tested completions where retry is acceptable.
- **Sales**: high-tier models on counterparty-facing artifacts (proposals, memos, outbound at named accounts) where hallucination has no automated catcher and outcome is fat-tailed. Cheap models acceptable on internal-only research artifacts that a human will read in full anyway.

### 4.2 Difficulty-Based Routing

- **Productization**: works well — task difficulty is partially observable from the request (one-line fix vs multi-file refactor) and from execution signals (tests failing in surprising ways).
- **Sales**: harder — "difficulty" is often unknown until a human reviews the output. Routing by **deal size**, **counterparty risk tier**, or **regulatory exposure** is often a better practical lever than routing by task difficulty alone.

### 4.3 Retry Policy

- **Productization**: high leverage. Failed tests give a clean retry signal; iterative refinement is natural; coding agents retry against the verifier until tests pass.
- **Sales**: low leverage at the output stage. Retrying outbound emails or investment-memo paragraphs without a verifier rarely measurably improves them; the meaningful retry signal comes from the human reviewer, which collapses retry policy back into human escalation policy.

### 4.4 Verification Policy

- **Productization**: **the dominant lever**. Cheap automated verification (unit tests, integration tests, type checks, lints, CI) reshapes the cost-quality frontier. Strategies that add verification almost always pay back at moderate-or-higher task complexity.
- **Sales**: **expensive and weak**. No automated tests exist for "is this proposal compelling" or "is this investment thesis sound." LLM-as-judge can catch obvious factual issues (numbers don't tie, named entity wrong, regulatory phrase missing) but cannot verify business judgment. Compliance and legal review are the closest analogues but operate as human gates, not as automated verifiers.

### 4.5 Tool-Use Policy

- **Productization**: tools are technical (compilers, debuggers, file system, language servers, MCP servers, CI). Tool-use cost is mostly orchestration overhead.
- **Sales**: tools are data sources (CRM, market data, LinkedIn, regulatory filings, internal data rooms, web search). The **quality and freshness of tool data** matters more than orchestration sophistication.

### 4.6 Human Escalation Policy

- **Productization**: moderate leverage. PR review is the standard gate; selective escalation works because most failures are caught earlier by automated gates.
- **Sales**: **the dominant lever**. The human is the closer. The right framing is rarely "automate with selective escalation" but rather "human-first with AI assist": what should the AI prepare so the salesperson's, analyst's, or partner's expensive time is spent at highest leverage? This inverts the default policy class implied by [`policy-design-space.md`](policy-design-space.md): sales domain default is closer to **Human-First** than to **Selective HITL**.

### 4.7 Serving Optimization

- **Productization**: matters in IDE-integrated assistants where latency is felt continuously (autocomplete, chat-in-IDE). For agentic coding, it matters less than direct token cost and verifier loop count.
- **Sales**: matters less in most workflows; latency is tolerable for batch outbound and overnight research. Matters in conversational contexts (live sales chat, real-time assist during a call).

### 4.8 Suggested Reordering

The repository's current strategy priority order in [`strategy-taxonomy.md`](strategy-taxonomy.md) is universal. Under this domain lens, a suggested per-domain reordering is:

**Productization:**

1. model selection
2. **verification policy**
3. retry policy
4. difficulty-based routing
5. tool-use policy
6. human escalation policy
7. serving optimization

**Sales:**

1. model selection
2. **human escalation policy** (closer to Human-First default)
3. tool-use policy (data-source quality)
4. difficulty-based routing (by deal size or counterparty risk)
5. verification policy (LLM-as-judge for surface checks; human review for substance)
6. retry policy
7. serving optimization

The headline shift: verification policy is the second-strongest lever in productization but the second-weakest in sales, while human escalation is the inverse.

## 5. Productization Sub-Split on the Verifier-Cost Axis

The productization domain is not uniform. The 2026 subdomain evidence in [`../references/skill-domain-deep-dive-2026.md`](../references/skill-domain-deep-dive-2026.md) §2 shows that verifier cost inside productization spans the same range as the coding-vs-sales gap.

| Productization subdomain | Verifier cost | Closest analogue |
| --- | --- | --- |
| Coding (IDE and agentic) | LOW | Coding |
| QA / testing | LOW | Coding |
| Docs (code-derived) | LOW | Coding |
| ML / data (structural) | LOW | Coding |
| Security / IAM | MEDIUM | Coding-with-human-gate |
| SRE / incident | MEDIUM | Operations |
| ML / data (semantic) | HIGH | Sales |
| Design (UX/UI) | HIGH | Sales |
| Docs (conceptual) | HIGH | Sales |

The cheap-verifier end is where the productization-default strategy priority order in §4.8 applies most cleanly. The expensive-verifier end — design, conceptual docs, semantic data work — sits closer to the sales-domain priority order on the verification axis because the binding cost is the human reviewer's judgment rather than the cost of running an automated check. Pricing models confirm the split: design and conceptual-docs vendors (Figma, v0, Mintlify Enterprise) price in flat tiers that absorb usage variance, similar to sales and investment tooling, while QA and structural-security tools price per-event or per-seat with explicit overage. This is registered as Gap 8 in [`../references/gap-analysis.md`](../references/gap-analysis.md) and should inform strategy-comparison design inside the productization domain.

## 6. Time-to-Feedback as a First-Class Dimension

The four dimensions in §3 include feedback-loop length, but the full spectrum warrants being made explicit because it determines how aggressive retry and refinement policies can be.

| Workflow class | Time-to-feedback | Retry/refinement feasibility |
| --- | --- | --- |
| Productization (cheap-verifier subdomains) | Seconds to minutes (REPL, CI, test suite) | Aggressive; verifier gives clean stop signal |
| Productization (expensive-verifier subdomains) | Minutes to hours (designer review, data-steward review) | Moderate; verifier is a human |
| Hybrid (customer support L1, DevRel) | Seconds to minutes at the episode level; days for true outcome (customer satisfaction, ticket reopen rate) | Aggressive at the episode, moderate for outcome-conditioned retries |
| Hybrid (marketing operations) | Hours to days (open rates, click rates) | Moderate; A/B harnesses approximate faster feedback |
| Sales (selling) | Weeks (reply, meeting booked, pipeline movement) | Limited at the output stage; feedback dominated by human review before send |
| Sales (investment IC memo) | Weeks to months (IC decision, deal close) | Limited; dominated by analyst and partner review |
| Sales (investment outcome) | Months to years (deal performance, fund return) | Effectively zero at the LLM stage; applies only at portfolio-level post-mortem |

This ties back to the logging-schema extension in [`logging-schema.md`](logging-schema.md) §Sales Extension Fields, which adds `async_outcome_reference` and `async_outcome_arrival_seconds` precisely because the sales-domain feedback signal arrives on a different timescale than the episode it refers to.

## 7. Compliance Overlay as a Third Cost Layer

Direct cost and indirect cost cover the inside of the workflow. A third layer — compliance overlay — sits across both and is shaped by the regulatory regime applicable to the artifact, not the artifact itself. The evidence is in [`../references/skill-domain-deep-dive-2026.md`](../references/skill-domain-deep-dive-2026.md) §5. The summary:

| Domain | Cost shape | Overlay strategy | Annual overlay band |
| --- | --- | --- | --- |
| Sales | Per-event fat-tail (penalties scale linearly with message/call count) | Convert unbounded tail into bounded fixed cost via consent platform + suppression + DPIA + legal review | $150K-$500K/yr |
| Investment | Per-incident catastrophic (single MNPI leak or AI-washing claim is multi-million) | Reduce tail probability via PBAC + telemetry retention + substantiation files + human sign-off | $200K-$1M/yr |
| Productization | Structural / amortized (audits, conformity assessment, license scanning, FedRAMP) | Pay once for market access, then maintain; volume-independent | $300K-$1.5M one-time + $150K-$400K/yr maintenance |

The cost-aggregation rules in [`cost-aggregation.md`](cost-aggregation.md) §Fat-Tail and Domain-Conditioned Reporting cover the per-episode side of compliance-shaped cost. The compliance overlay itself should be tracked as an annualized cost line that scales with the regulatory regime, not with episode count.

## 8. Where the Existing Repository Already Aligns

This domain split does not contradict the existing repository; it specializes it.

- [`cost-taxonomy.md`](cost-taxonomy.md): the direct-vs-indirect split applies cleanly to both domains. This document only adds the observation that *which* indirect-cost components dominate differs by domain.
- [`policy-design-space.md`](policy-design-space.md): the six design axes apply to both domains. The sales domain's natural policy class is closer to **Human-First**; the productization domain's is closer to **Selective HITL**.
- [`../reports/research-questions-v2.md`](../reports/research-questions-v2.md) Q3 ("How task-specific is the optimal policy?") is the natural home for this lens. The Sales-vs-Productization split is one concrete instance of the task-specificity hypothesis.
- [`../reports/practitioner-guidance.md`](../reports/practitioner-guidance.md) rule 5 ("Start with routing and verification before complex orchestration") is well-supported in the productization domain and weaker in the sales domain, where verification leverage is limited.

## 9. Boundary and Hybrid Cases

Some workflows do not sit cleanly in one domain. The 2026 evidence in [`../references/skill-domain-deep-dive-2026.md`](../references/skill-domain-deep-dive-2026.md) §3 suggests that hybrid workflows are better treated as a third population than as boundary cases, because they have their own converging pricing pattern (outcome-based per-resolution metering) and their own verifiable-plus-judgment cost split.

- **Marketing operations**: verifiable share approximately 40-50% (subject-line A/B, deliverability, click rate); judgment share approximately 50-60% (brand voice, narrative angle, segmentation). Human handoff approximately 30-50% of generated assets. Pricing is converging on outcome-based (HubSpot Breeze $0.50/resolved conversation from April 2026).
- **Customer support (L1/L2/L3)**: verifiable share approximately 70-80% of L1 volume, approximately 25% of L2, under 10% of L3. Human handoff: 30-50% on L1, approximately 85% on L2, approximately 100% on L3. Per-resolution pricing ranges from Intercom Fin $0.99 to Zendesk AI $2.00 to Sierra negotiated outcomes. The binding cost constraint in 2026 has migrated from L1 deflection to L2 and L3, where AI's role is fact-assembly for human debuggers.
- **Developer relations content**: verifiable share approximately 75-85% (API signatures, parameter behavior, version diffs); judgment share approximately 15-25% (architectural recommendations, "is this a bug" calls). Human handoff is the lowest of the three hybrid classes at approximately 5-15%, but those handoffs concentrate the most expensive engineering minutes.
- **Product analytics and BI**: report generation can resemble extraction (productization-adjacent operations); investment-grade quarterly business reviews resemble investment memos (sales).
- **Internal compliance and legal review**: closer to sales in failure cost shape (fat-tailed, downstream consequence) but resembles document extraction in operational structure.

For true boundary cases, the right move is still to characterize the workflow on the four dimensions in §3 (verification mechanism, feedback-loop length, human cost asymmetry, failure cost shape) plus the two dimensions added in §5-§6 (verifier-cost position, time-to-feedback). Apply the per-domain priority that matches the dominant dimensions rather than forcing a binary classification.

## 10. How to Use This Lens

When reading or extending the repository:

- when picking a benchmark, identify which domain it sits in and check whether the existing benchmark set already covers that domain
- when designing a policy comparison, prefer comparisons that hold the domain constant rather than mixing domains in one cost-quality frontier plot
- when reporting practitioner guidance, qualify rules that are domain-conditional (especially the verification rule)
- when reading industry data, segment by domain — sales-AI spend trends and productization-AI spend trends are not interchangeable
