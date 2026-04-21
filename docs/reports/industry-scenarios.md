# Industry Scenarios

## Purpose

This document grounds the repository's framework in a small set of realistic deployment scenarios. Scenarios are organized by **skill domain** as defined in [`../frameworks/skill-domain-taxonomy.md`](../frameworks/skill-domain-taxonomy.md): productization scenarios produce internal engineering artifacts and benefit from cheap automated verifiers; sales scenarios produce artifacts directed at external counterparties and rely on human review for verification. Concrete 2026 industry data points behind each scenario are collected in [`../references/skill-domain-evidence-2026.md`](../references/skill-domain-evidence-2026.md).

## Productization-Domain Scenarios

### Scenario P1: Code Generation and Repair

Typical workflow:

- developer asks for implementation or patch help
- AI proposes code
- tests or review determine acceptance
- failures create debugging and rework cost

Why this scenario fits:

- quality can be measured with tests
- verification is natural
- human oversight is common but expensive

Most relevant policy questions:

- Is a strong model cheaper than repeated cheap-model retries?
- How much value does executable verification provide?
- When should unresolved failures be escalated to a developer?

Dominant cost risks:

- debugging overhead
- latency in developer workflow
- hidden defects that pass shallow review
- agentic resource exhaustion in long trajectories (cost of a failed retry at turn 40 is approximately 3x the first-turn cost in the same session because accumulated context travels with every request)

### Scenario P2: Document Extraction and Back-Office Processing

Typical workflow:

- AI extracts fields from forms, invoices, or internal documents
- validation and cleanup happen downstream
- uncertain cases are corrected by operations staff

Why this scenario fits:

- structured outputs support precision and recall targets
- human cleanup burden is easy to model
- tools and validators are plausible

Most relevant policy questions:

- When does validator-assisted extraction beat stronger direct generation?
- Is selective review cheaper than blanket human QA?
- How costly are partial errors compared with outright failures?

Dominant cost risks:

- silent field errors
- rework queues
- compliance-sensitive mistakes

### Scenario P3: Classification and Routing Operations

Typical workflow:

- AI classifies or routes tickets, emails, claims, or requests
- hard or high-risk cases are escalated
- bad routing creates downstream handling cost

Why this scenario fits:

- episodes are short and repeatable
- confidence-based deferral is realistic
- queue economics matter

Most relevant policy questions:

- What confidence threshold minimizes total cost?
- When is a stronger default model worth it?
- How much human load does selective escalation create?

Dominant cost risks:

- misrouting
- backlog from over-escalation
- delayed handling on high-priority cases

## Sales-Domain Scenarios

### Scenario S1: Outbound Selling and Customer Outreach

Typical workflow:

- AI enriches accounts and contacts and drafts personalized outbound (email, social, sequence cadence)
- AI listens to discovery calls and produces summaries, scorecards, deal-risk signals
- salesperson reviews and sends; manager uses conversation intelligence at the deal-review stage
- counterparty reply or pipeline movement is the delayed signal

Why this scenario fits:

- there is no automated test for "is this outbound compelling"
- reply-rate and pipeline signal arrives weeks after the action
- failure modes (deliverability damage, ICP drift, regulatory exposure) are fat-tailed
- the salesperson is the action gate and is the most expensive priced resource in the workflow

Most relevant policy questions:

- What is the right human-review depth per artifact tier (named-account proposal vs cold sequence)?
- When does a stronger model on customer-facing artifacts pay back via reduced human edit time and fewer reputational misses?
- How should the workflow protect domain deliverability and compliance as a shared infrastructure cost rather than a per-email cost?
- How should conversation-intelligence "active user" economics be tracked, given that license counts often exceed active users by approximately 2x?

Dominant cost risks:

- domain reputation collapse and ISP downgrade affecting all future email
- multi-million-dollar regulatory exposure (GDPR, CAN-SPAM, CASL)
- effective per-active-user cost drift for conversation intelligence (e.g., approximately $550/mo effective vs $250 list)
- customer churn from over-automated workflows (approximately 70% of teams running fully autonomous AI SDR churn within 90 days)

### Scenario S2: Investment Research and Due Diligence

Typical workflow:

- AI agent ingests data rooms, filings, transcripts, and market data
- AI drafts memos, comparable analyses, market sizing, and decision-support views
- analyst, principal, or partner reviews each cited claim and makes the deal call
- counterparty negotiation, IC approval, and post-close performance are the delayed signals

Why this scenario fits:

- ground truth is "did the deal perform" measured over years
- the priced human is an analyst at $58–$132/hr or a partner-equivalent making the deal call, on $10M–$1B+ deal sizes
- failure cost is symmetric on the upside (a missed insight equals lost deal value) and asymmetric on the downside (regulatory MNPI handling, fiduciary breach)
- citation-anchored output is the closest the domain has to an automated verifier, but it costs analyst minutes per citation

Most relevant policy questions:

- Where in the workflow should multi-model routing apply (e.g., reasoning-tier models reserved for evaluation and synthesis, cheaper models for routine extraction)?
- How should citation density be tuned against analyst review time?
- How should agent-task budget caps be set per deal stage (initial screening vs final IC memo)?
- When does premium seat cost (e.g., approximately $10K/seat/yr) clear the bar relative to $25K–$500K+ per-deal diligence cost it offsets?

Dominant cost risks:

- cited-but-wrong content reaching IC
- regulatory exposure from MNPI mishandling
- cost overrun on deep-research tasks (per-task token spend can run 0.5–2M tokens with retries)
- analyst burnout from high-volume citation review even with citation-first design

## Cross-Scenario Insight

These five scenarios create distinct stress tests for the framework, organized by domain:

Productization domain:

- code generation stresses verification and recovery
- extraction stresses structured quality and cleanup
- classification stresses routing and deferral

Sales domain:

- outbound selling stresses human-first review and fat-tailed failure containment
- investment research stresses citation-grounded synthesis and per-stage budget control

The two productization-leaning scenarios that resemble back-office operations (P2, P3) and the two sales-domain scenarios (S1, S2) together cover the four cells implied by the [`../frameworks/skill-domain-taxonomy.md`](../frameworks/skill-domain-taxonomy.md) §3 dimensions: cheap-verifier vs expensive-verifier crossed with thin-tailed vs fat-tailed failure cost.

That makes the five scenarios a stronger foundation for a first research cycle than the original three, because the original set was concentrated in the cheap-verifier / thin-tailed quadrant.

## Recommended Research Use

When presenting results, each benchmark family should be tied back to one of these scenarios so that the cost assumptions feel operational rather than abstract. Cross-domain comparisons (for example, comparing a code-generation policy directly against an outbound-selling policy on the same cost-quality plot) should be avoided; the verification mechanisms and human-cost asymmetries are different enough that one frontier plot would mislead.
