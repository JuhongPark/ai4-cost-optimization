# Skill-Domain Evidence (April 2026)

## Purpose

This note collects 2026 industry data points organized by the **sales** vs **productization** skill domains defined in [`../frameworks/skill-domain-taxonomy.md`](../frameworks/skill-domain-taxonomy.md). It complements the chronological [`industry-trends-2026.md`](industry-trends-2026.md) and [`industry-updates-2026-04.md`](industry-updates-2026-04.md) by re-cutting the same kind of evidence along the skill-domain axis, so that scenario design and strategy prioritization can be grounded in concrete numbers per domain.

The data here is current as of April 2026 and is intended to be cited rather than restated in scenario or framework documents.

## 1. Sales Domain

### 1.1 Selling

**Pricing models converge on seat-based, not usage-based.**

- 11x.ai "AI worker" contracts run a median of approximately $40K/yr per Vendr marketplace data, with quoted ranges of $1,230–$5,000+/mo and 12-month commitments. Artisan starts at approximately $1,500/mo and does not publish prices.
- Apollo runs a hybrid: $49–$149/seat/mo plus credits, where one email reveal is one credit and overages run $0.20/credit.
- Gong runs $120–$250/user/mo with a $5K–$50K platform fee plus $15K–$65K implementation. A typical Gong+Clari stack is approximately $450–$500/user/mo, or roughly $540K–$600K/yr for 100 users. Buyers report a 63% variance in per-seat quotes.

**Inference cost is a small fraction of the seat price.** The 11x "Alice" worker advertises approximately 3,000 contacts/mo per seat. Using approximately 1.5K input plus 300 output tokens per personalized email on a Sonnet-class model, raw inference cost lands in the $2–$15 range per 1,000 emails — roughly an order of magnitude below the per-seat price. The customer is paying for orchestration, integrations, and reliability, not tokens.

**Human review is the operationally enforced default, not an optional gate.**

- In fully autonomous AI-SDR mode, approximately 70% of teams that buy AI SDRs churn within 90 days.
- Operational guidance in 2026 has converged on approximately 15–20 hours per week of human oversight per AI SDR seat. The seat does not replace a salesperson; it shifts the salesperson from author to reviewer.
- Regie.ai's positioning ("AI writing assistant on top of Outreach/Salesloft, rep still sends") is the structural endpoint the rest of the segment is moving toward.

**Failure cost is fat-tailed.**

- Templated AI volume → ISP flagging → permanent deliverability damage to the sending domain, which then degrades human-written email as well.
- One documented case escalated to multi-million-dollar regulatory exposure (GDPR, CAN-SPAM, CASL).
- B2B cold-email reply rates have collapsed from approximately 6.8% (2023) to approximately 4–5% (2025), partly attributed to AI-driven volume saturation. This is a tragedy-of-the-commons cost imposed across the segment.

**Active-user economics matter.** Companies typically buy approximately 110 Gong licenses with only approximately 50 active users, raising effective cost per active user to approximately $550/mo against a $250 list price.

### 1.2 Investment / Equity Research / Due Diligence

**Pricing is premium seat-based and unit economics work even at high seat prices.**

- Hebbia Professional: approximately $10,000/seat/yr; Lite tier $3,000–$3,500/seat/yr. Hebbia claims approximately 33% of top global asset managers by AUM as customers.
- Rogo raised approximately $50M Series B (over $75M total) targeting the same segment.
- Per-deal due diligence runs approximately $25K–$500K+ depending on size (0.2%–4% of deal value). Annual diligence spend including dead deals is approximately $4M–$15M for a typical mid-market PE firm. AI license cost — even at a $1M+ enterprise contract — is roughly 10–25% of the cost it offsets.

**Multi-model architecture with explicit cost routing is published practice.** Rogo's published architecture reserves o1/o3 for evaluation, synthetic data generation, and high-stakes reasoning, and routes routine queries to cheaper models. This is the closest published industry analogue to the routing/cascading work in the repository's [`../frameworks/strategy-taxonomy.md`](../frameworks/strategy-taxonomy.md).

**Verification is shifted, not eliminated.** Hebbia's design choice is "citation-first by default; every number, clause, and claim links back to the precise source." This converts hallucination cost into review cost — the analyst clicks the citation to confirm — rather than zero cost. This is the closest the sales domain comes to an automated verifier, and it costs analyst minutes per citation.

**Reported ROI is large enough that vendor pricing tolerates it.**

- Investment bankers: approximately 30–40 hours saved per deal on marketing materials.
- PE: approximately 20–30 hours saved per deal on screening, diligence, expert-network research.
- Industry-wide: PE firms report approximately 40–60% total diligence cost reduction, approximately 71% time reduction, and capacity to evaluate approximately 50% more deals without headcount growth. One cited firm reports an 80% diligence-cost cut.

**Search APIs sit underneath the agent products.**

- Tavily: $0.008/credit, approximately $30/mo entry, approximately $800 for 100K pages.
- Perplexity Sonar: $5 per 1,000 searches plus $0.30/1M input tokens; Sonar Pro $5 per 1,000 searches plus $3/1M input/output tokens.
- Comparison anchor: Gemini Search Grounding at $35 per 1,000 queries, 4–7x more expensive than Sonar/Tavily at scale.
- Search-API line is typically approximately 2–10% of total task cost in research-agent workflows; the LLM line dominates.

## 2. Productization Domain

### 2.1 IDE-Integrated Coding Assistants

**Pricing pattern.** Universal: per-seat subscription for unlimited tab autocomplete, plus a metered "premium request" or credit pool for chat and agent features.

- GitHub Copilot: Pro $10/mo, Pro+ $39/mo, Business $19/user/mo, Enterprise $39/user/mo. Premium-request overage $0.04/request.
- Cursor: Pro $20/mo, Ultra $200/mo, Teams $40/user/mo. Switched to usage-based credits in mid-2025 with documented community pushback over unpredictable bills.
- Windsurf: Pro $15/mo (500 credits), Ultimate $60/mo (unlimited). Repriced March 19, 2026 from credits to daily/weekly quotas. Tab autocomplete remains unlimited even after credits exhaust.

**Acceptance rates and observed productivity.** Autocomplete acceptance rate sits at approximately 27–30%, climbing to approximately 34% by month 6 of tenure with the tool. Approximately 88% of accepted suggestions survive into committed code. Aggregate productivity studies report task speed-ups of approximately 55% and PR-merge time dropping from approximately 9.6 to 2.4 days, with an 84% increase in successful builds.

**Verification position is the live IDE/CI loop.** Compile, lint, and test are the verifier; rejection cost is essentially zero (the developer presses Esc).

### 2.2 Agentic Coding

**Per-session token economics scale non-linearly.** Vantage's measurement of a representative 50-turn agentic session: approximately 1M input tokens and approximately 40K output tokens, with input dominating approximately 85% of cost. Token use scales non-linearly with turn count because context accumulates: approximately 5K input tokens/turn during exploration (turns 1–10), approximately 20K/turn during implementation (turns 11–30), and approximately 35K/turn during testing/iteration (turns 31–50).

**Cost per session.** A 50-turn session: $6.00 on Claude Opus 4.6 vs $0.60 on Composer 2 Standard — a 10x model-choice gap on the same workload. Anthropic enterprise data: approximately $13/developer/active-day for Claude Code (Sonnet 4.6), with 90% of users below $30/day, total approximately $100–250/developer/month. Agent Teams (multi-instance) consume approximately 7x a single-agent session.

**Pricing across agentic products.**

- Claude Code: Pro $20/mo, Max $100–200/mo, or pay-per-token via API (Opus $5/$25, Sonnet $3/$15 per MTok; 1M-token context now flat-rate after Anthropic's March 14, 2026 surcharge removal already noted in [`industry-updates-2026-04.md`](industry-updates-2026-04.md)).
- Codex CLI/Cloud: bundled in ChatGPT Plus/Pro/Business; $200 Pro tier is 20x Plus quota. API mode: codex-mini at $1.50/$6.00, GPT-5 at $1.25/$10.00 per MTok.
- Devin (Cognition): Core $20/mo plus ACUs at $2.25 each (1 ACU ~ 15 min of work); reported all-in cost approximately $8–12 per completed task.
- Replit Agent: effort-based pricing introduced in 2025; simple change &lt;$0.25/checkpoint, but heavy users have reported approximately 6x cost increases on equivalent builds versus the old model.

**Failure / retry profile.** Agentic loops generate approximately 3–10x more LLM calls than chatbots; single customer queries can trigger 10–50 LLM calls under the hood; industry-consensus retry rate from LLM failure alone is approximately 5–10%. The cost of a failed retry at turn 40 is approximately 3x the first-turn cost in the same session because the accumulated context travels with every request — the empirical basis for the agentic-resource-exhaustion fat-tail risk already flagged in [`industry-updates-2026-04.md`](industry-updates-2026-04.md).

### 2.3 Agent Benchmarks (Per-Task Cost)

The reliably citable per-instance numbers:

- SWE-bench Verified, OpenHands harness (November 2025): Claude 3.5 Sonnet approximately $0.30/issue at 27% resolve; DeepSeek-V2.5 approximately $0.003/issue. The OpenHands authors call out prompt caching as the cost driver.
- SWE-Bench Pro: cost cap is approximately $2/trajectory with a 50-turn limit, designed precisely so that tests give a cheap stop signal before unbounded retry.
- Aider Polyglot top-tier models: approximately $0.05–$0.65/instance depending on reasoning effort. Concrete: GPT-5 (high) $0.13/run at 88.0% pass; GPT-5 (low) $0.05/run at 81.3%; o3-Pro (high) $0.65/run at 84.9%. The marginal $0.08 between GPT-5 (low) and (high) buys approximately 7 percentage points and is the working operating point for many teams; o3-Pro at $0.65/run buys negative ROI relative to GPT-5 (high).
- DeepSeek V3.2-Exp on Aider Polyglot: approximately $1.30/run at 74.2%, reported as approximately 22x cheaper than GPT-5 at comparable quality.
- SWE-Bench Verified (April 2026 leaderboard): Claude Opus 4.7 leads at 87.6%, GPT-5.3-Codex 85.0%, Gemini 3.1 Pro 80.6%.

**SWE-Bench Pro failure breakdown for Claude Opus 4.1** (only the categories overlap, so they sum above 100%): 74.0% submission rate; non-submission failures break down as 48.5% wrong syntax, 32.7% incorrect instruction following, 69.9% stuck-in-loop. Dominant productization failure mode is cascading instruction drift inside long trajectories, not isolated hallucinated APIs.

### 2.4 Code Review and Test Generation

- CodeRabbit: $24/user/mo, unlimited reviews, no per-PR overage.
- Greptile: $30/seat/mo includes 50 reviews; each additional review $1. A 3-PRs/day developer is approximately $45/seat/mo. Independent benchmarks report Greptile catches 82% of seeded bugs vs CodeRabbit's 44%, but with materially more false positives.
- Bito: $15/user/mo.
- Qodo (formerly CodiumAI): Free 30 PR reviews plus 250 IDE/CLI credits; Teams $30/user/mo with 2,500 credits (Claude Opus calls 5 credits, Grok 4 calls 4 credits).

**Aggregated economics:** approximately $15–25 per AI-reviewed PR; a 10-PR/day team is approximately $4.5–7.5K/mo. Per 1,000 LOC, automated review cost is approximately $150–300, a 75–85% reduction vs manual review, but PR review elapsed time is reported up 91% in some studies because developers must triage AI comments — a "noise abandonment" anti-pattern that some teams hit when every PR returns dozens of comments.

## 3. Cross-Domain Patterns Worth Noting

The two-domain comparison surfaces three patterns that the repository's existing notes do not yet make explicit:

**Pattern 1: vendor pricing model is itself a domain signal.** Productization vendors converged on seat plus metered usage with explicit per-token or per-credit overage, because workload variance is high and tied to a measurable artifact (request, agent run). Sales and investment vendors converged on premium flat seat with implicit usage absorption, because workload variance is lower and the bigger cost driver is enterprise integration, compliance, and the human-handoff workflow. The pricing structure is downstream of where the dominant indirect cost lives.

**Pattern 2: the two domains both observe a "human shift, not human replacement" outcome, but for different reasons.** In productization, automated verifiers catch most failures and humans gate at PR review (selective HITL is the empirical equilibrium). In sales and investment, automated verifiers do not exist at the relevant fidelity, so humans gate before the artifact ever leaves the firm (human-first with AI assist is the empirical equilibrium). The 70% AI-SDR churn rate and the 15–20 hr/week-per-seat oversight pattern are the sales-side data point; the standard PR review gate is the productization-side data point.

**Pattern 3: failure cost shape determines acceptable retry policy.** Productization tolerates aggressive retry because the verifier is cheap and the failure ceiling is bounded — explicit per-trajectory caps (SWE-Bench Pro's $2) work because the verifier defines a clean give-up signal. Sales tolerates retry only at the human-review stage, because there is no cheap give-up signal and the failure tail is multi-million-dollar regulatory or reputational exposure. The agentic-resource-exhaustion fat tail noted in [`industry-updates-2026-04.md`](industry-updates-2026-04.md) is felt very differently in the two domains.

## 4. Implications for Repository Documents

- [`../reports/industry-scenarios.md`](../reports/industry-scenarios.md) should add at least one selling and one investment scenario, since all three existing scenarios sit in the productization domain or operations work that resembles it.
- [`../frameworks/scenario-cost-assumptions.md`](../frameworks/scenario-cost-assumptions.md) should declare per-domain assumption families (verification cost, human-minute cost, downstream failure shape) that match the patterns above.
- [`../frameworks/strategy-taxonomy.md`](../frameworks/strategy-taxonomy.md) priority order should be qualified as domain-conditional, with the per-domain reordering in [`../frameworks/skill-domain-taxonomy.md`](../frameworks/skill-domain-taxonomy.md) §4.8 cited as the operational refinement.

## Sources

Sales / RevOps:

- [11x.ai pricing — Vendr marketplace](https://www.vendr.com/marketplace/11x)
- [11x.ai 2026 pricing breakdown — Landbase](https://www.landbase.com/blog/11x-ai-pricing)
- [The AI SDR Bubble Is Popping — GTM AI Podcast](https://www.gtmaipodcast.com/p/the-ai-sdr-bubble-is-popping-heres)
- [The AI SDR Playbook: What Actually Works in 2026 — Product Growth](https://www.productgrowth.blog/p/the-ai-sdr-playbook-what-actually-works)
- [AI SDR risks and mitigation — Everworker](https://everworker.ai/blog/ai_sdr_pipeline_risks_and_mitigation)
- [Email deliverability 2026 — Landbase](https://www.landbase.com/blog/low-email-deliverability-heres-how-ai-protects-your-domain-health)
- [Outbound SDR statistics 2025 — Sales So](https://salesso.com/blog/outbound-sdr-statistics/)
- [Apollo.io pricing 2026 — Salesmotion](https://salesmotion.io/blog/apollo-pricing)
- [Clay pricing 2026 — Warmly](https://www.warmly.ai/p/blog/clay-pricing)
- [Gong pricing calculator — Oliv.ai](https://www.oliv.ai/blog/gong-io-pricing)
- [Gong vs Clari — Oliv.ai](https://www.oliv.ai/blog/gong-vs-clari)
- [Gong pricing — Vendr](https://www.vendr.com/marketplace/gong)
- [Ironclad: AI agents in legal operations](https://ironcladapp.com/resources/articles/the-reality-of-ai-agents-in-legal-operations-today)
- [Feedback-loop speed — Alchemyst AI](https://getalchemystai.com/blog/feedback-loop-speed)
- [Top 10 reasons AI agent implementations fail — SaaStr](https://www.saastr.com/the-top-10-reasons-your-ai-agent-implementation-is-failing/)

Investment / Equity Research / Due Diligence:

- [Hebbia pricing](https://www.hebbia.com/pricing)
- [Hebbia AI pricing 2025 — eesel AI](https://www.eesel.ai/blog/hebbia-ai-pricing)
- [Hebbia automates 90% of finance and legal — OpenAI](https://openai.com/index/hebbia/)
- [Rogo scales financial research with OpenAI o1 — OpenAI](https://openai.com/index/rogo/)
- [Rogo multi-model architecture — ZenML LLMOps Database](https://www.zenml.io/llmops-database/scaling-financial-research-and-analysis-with-multi-model-llm-architecture)
- [PitchBook LLM partnerships with Anthropic, Perplexity, Rogo, Hebbia](https://www.businesswire.com/news/home/20250722027538/en/PitchBook-Announces-LLM-Partnerships-with-Anthropic-Perplexity-Rogo-and-Hebbia-to-Expand-Access-to-Private-Capital-Market-Data)
- [Tavily vs Exa vs Perplexity vs You.com 2026 — Humai](https://www.humai.blog/perplexity-vs-tavily-vs-exa-vs-you-com-the-complete-ai-search-engine-comparison-2026/)
- [AI Search API pricing April 2026 — buildmvpfast](https://www.buildmvpfast.com/api-costs/ai-search)
- [O3-Deep-Research pricing — pricepertoken](https://pricepertoken.com/pricing-page/model/openai-o3-deep-research)
- [AI-driven due diligence in PE 2025 — Dynamiq](https://www.getdynamiq.ai/post/ai-driven-due-diligence-through-to-exit-how-private-equity-firms-are-using-genai-in-2025)
- [PE firm cuts diligence costs 80% — Stack AI](https://www.stackai.com/customers/how-a-pe-firm-automated-company-due-diligence-process-with-ai)
- [TFSF Ventures: PE diligence compression 50–70% — National Law Review](https://natlawreview.com/press-releases/tfsf-ventures-details-how-ai-agents-compress-private-equity-due-diligence-50)
- [Due diligence costs 2026 — Peony](https://www.peony.ink/blog/due-diligence-cost-breakdown)

Productization (IDE assistants, agentic coding, benchmarks, review):

- [GitHub Copilot plans](https://github.com/features/copilot/plans)
- [GitHub Copilot premium requests](https://docs.github.com/en/billing/concepts/product-billing/github-copilot-premium-requests)
- [Windsurf vs Cursor pricing — uibakery](https://uibakery.io/blog/windsurf-vs-cursor-pricing)
- [Devin pricing](https://devin.ai/pricing/)
- [Devin billing](https://docs.devin.ai/admin/billing)
- [Devin 2.0 cost cut — VentureBeat](https://venturebeat.com/programming-development/devin-2-0-is-here-cognition-slashes-price-of-ai-software-engineer-to-20-per-month-from-500)
- [Replit effort-based pricing](https://blog.replit.com/effort-based-pricing)
- [OpenAI Codex pricing](https://developers.openai.com/codex/pricing)
- [Claude API pricing](https://platform.claude.com/docs/en/about-claude/pricing)
- [Claude Code costs](https://code.claude.com/docs/en/costs)
- [Qodo pricing](https://www.qodo.ai/pricing/)
- [Greptile pricing](https://www.greptile.com/pricing)
- [SWE-Bench Pro — arXiv:2509.16941](https://arxiv.org/abs/2509.16941)
- [SWE-Lancer — arXiv:2502.12115](https://arxiv.org/pdf/2502.12115)
- [MLE-bench — arXiv:2410.07095](https://arxiv.org/abs/2410.07095)
- [BIRD-Interact ICLR 2026 — arXiv:2510.05318](https://arxiv.org/abs/2510.05318)
- [SWE-bench leaderboard](https://www.swebench.com/)
- [Aider leaderboards](https://aider.chat/docs/leaderboards/)
- [Epoch AI: Aider Polyglot benchmark](https://epoch.ai/benchmarks/aider-polyglot)
- [Epoch AI: SWE-bench Verified benchmark](https://epoch.ai/benchmarks/swe-bench-verified)
- [How LLM agents fail in agentic scenarios — arXiv:2512.07497](https://arxiv.org/pdf/2512.07497)
- [Where LLM agents fail and how they learn from failures — arXiv:2509.25370](https://arxiv.org/pdf/2509.25370)
- [Agentic coding cost evaluation — OpenHands](https://openhands.dev/blog/evaluation-of-llms-as-coding-agents-on-swe-bench-at-30x-speed)
- [Agentic coding costs — Vantage](https://www.vantage.sh/blog/agentic-coding-costs)
- [Measuring GitHub Copilot's impact on productivity — CACM](https://cacm.acm.org/research/measuring-github-copilots-impact-on-productivity/)
- [SWE-bench Sonnet — Anthropic](https://www.anthropic.com/research/swe-bench-sonnet)
- [Claude Sonnet 4.5 — Anthropic](https://www.anthropic.com/news/claude-sonnet-4-5)
- [2026 Agentic Coding Trends Report — Anthropic](https://resources.anthropic.com/2026-agentic-coding-trends-report)
- [AI code review benchmark 2026 — byteiota](https://byteiota.com/ai-code-review-benchmark-2026-first-real-results/)
