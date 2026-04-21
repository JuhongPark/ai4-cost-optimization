# Skill-Domain Deep Dive (April 2026)

## Purpose

This note extends [`skill-domain-evidence-2026.md`](skill-domain-evidence-2026.md) with deeper subdomain coverage, hybrid-workflow cost profiles, Korea/APAC industry context, and a compliance/regulatory cost overlay. The first evidence note covered the dominant cases (AI SDR, conversation intelligence, agentic coding, code review). This note fills the gaps that were named but not quantified there. It supports [`../frameworks/skill-domain-taxonomy.md`](../frameworks/skill-domain-taxonomy.md), the failure-taxonomy, the logging-schema, and the gap-analysis updates that depend on per-subdomain detail.

Numbers are current as of April 2026 unless noted otherwise.

## 1. Sales Subdomain Depth

### 1.1 Selling Subdomains

**RFP automation (Responsive, Loopio, RocketDocs, Tribble, Arphie).**

- Pricing is seat-based with platform fees, AI bundled rather than metered. Loopio entry approximately $20K/yr for 10 seats (approximately $2,000-$2,500/seat/yr); enterprise Responsive deployments approximately $40K-$120K+/yr.
- Per-RFP economics: AI auto-completes 70-90% of questions on the first pass; humans review the remaining 10-30%. Loopio's 2026 Trends Report claims response time drops from approximately 25 hours to under 5 hours per RFP, and 153 RFPs/year (industry average) yields approximately 3,000 hours saved. At a fully loaded proposal-manager rate of approximately $75/hr that is approximately $1,500/RFP in labor avoided versus a Loopio seat amortized cost of approximately $130/RFP — roughly a 10x labor-to-license ratio.
- Win-rate moved from approximately 43% (2024) to approximately 45% (2025), the largest YoY jump in five years, attributed largely to AI-assisted quality. A single misaligned answer that loses one $500K deal wipes out 25 years of seat fee at the median tier — the implicit ROI math.
- Failure modes: misalignment between library content and the specific RFP question; stale content library entries (security questionnaires from 2024 about deprecated SOC 2 controls); over-reliance leading to compliance gaps in regulated bids.

**Account planning and ABM (6sense, Demandbase, Outreach Account Planning, Salesloft Rhythm).**

- Pricing is hybrid seat + credit. 6sense $60K-$100K/yr mid-market and $100K-$250K+/yr enterprise with mandatory multi-year contracts. Demandbase starts approximately $40K-$80K/yr with approximately $29K onboarding plus $1,200-$3,000/seat for additions beyond approximately 10 bundled seats. Outreach/Salesloft sequences cost an additional $100-$150/user/mo on top.
- 6sense exposes credits explicitly: 1 credit per contact reveal, 1 credit per export. A 20-rep team researching 10 accounts/week consumes approximately 800+ credits/month; a 500-credit contract triggers overage or rationing.
- Adoption: approximately 81% of sales teams use AI in some capacity in 2026, but only approximately 26% specifically for content/proposal generation and approximately 24% for CRM auto-fill.
- Failure modes: stale TALs (approximately 40% of marketers cite dirty CRM data as the top ABM execution blocker); batched intent signals presented as real-time; hallucinated firmographics built on duplicate or outdated CRM records.

**Customer success and expansion (Gainsight, Catalyst/Totango, ChurnZero, Vitally).**

- Gainsight ranges $2,400-$4,200/user/yr depending on edition; a 25-user Essentials deployment approximately $60K/yr plus $30K-$120K implementation. Insight Agent (Staircase AI integration) is a separately priced add-on. ChurnZero approximately $1,500/mo for mid-market with 4-8 week deployments.
- Gainsight's April 2026 MCP launch lets customers wire AI agents into retention workflows in minutes instead of weeks — a meaningful reduction in setup labor, which is the dominant cost line for CS AI.
- Failure modes: false-positive churn alerts. A documented 2026 calibration band: false-positive rate above 30% indicates oversensitive thresholds and erodes CSM trust; below 10% suggests missed risk. Recommended rollout is 30-90 days in observability mode with weekly CSM-led false-positive flagging before alerts go live. Wrong expansion plays — pushing upsell to an unhappy account — actively accelerate churn rather than just wasting outreach.

**Partner channel (Crossbeam-Reveal, PartnerStack, Channeltivity).**

- Crossbeam Connector $4,800/yr platform + $1,800/seat/yr with a 5,000-record export cap. PartnerStack approximately $19K-$24K/yr per Vendr/OMR median, plus a 3-15% override on partner commissions. The merged Crossbeam-Reveal network covers 25,000+ companies, the largest ecosystem dataset feeding GTM AI tools.
- 3-Year TCO for a 10-seat Connector deployment is approximately $63,000 — small relative to a single co-sourced enterprise deal.
- Failure modes: partner conflict (two vendors both claim the same account); leaked CRM data through misconfigured sharing rules (the merger explicitly sells "secure sharing" as the differentiator); attribution disputes on co-sold deals.

### 1.2 Investment Subdomains

**VC deal sourcing (Affinity, Specter, Harmonic, Tribe AI).**

- Per-seat-per-year, mid four to low five figures. Affinity Essential/Scale/Advanced $2,000 / $2,300 / $2,700 per user/yr; Vendr-observed contracts $12K-$35K (5-15 seats, Essential) and $40K-$120K (15-40 seats, Advanced). Harmonic.ai (a16z, Accel, Floodgate as customers; tracking 30M+ companies, 190M people profiles) and Specter (50M companies, 500M people) are quote-only; enterprise plans land in low six figures/yr.
- Per-task economics: a high-funnel, cheap-per-item workload. Per-record enrichment plus scoring is dominated by retrieval and embedding cost (cents to low dollars per company), not generation. Affinity 2026 survey: 82% of dealmaker firms now use AI on the sourcing leg, with 85% on at least one task (up from 76% in 2025).
- Funnel: mid-market firm baseline approximately 500-2,000 deals reviewed/yr → approximately 50 serious looks → approximately 5 closes (approximately 99.5% rejection). VC-backed CFOs report a median $50K/yr 2026 AI spend, doubled from $20K in 2025.

**Public equity research (Bloomberg Terminal + BloombergGPT, FactSet Mercury, AlphaSense, SymphonyAI).**

- Bloomberg Terminal $31,980/yr single seat, $28,320/yr multi-seat (BloombergGPT bundled, no per-query meter). FactSet base approximately $12,000/yr/seat with FactSet Mercury included. AlphaSense median contract $18K/yr ($10K-$20K/seat), enterprise $50K-$100K+ to $1M+ (approximately $500M ARR Oct 2025; 7,000 enterprise customers, 90% of S&P 100, approximately 70% of S&P 500 by April 2026).
- AlphaSense Generative Search next-gen (Jan 2026) compresses Deep Research from "weeks" to "minutes," with vendors citing approximately 40% reduction in research costs. A Deep Research run is typically 0.5-2M input tokens (citation-grounded), placing raw inference at $5-$30/report on Sonnet/o-tier — roughly 0.5-2% of one analyst-day at $58-$132/hr.
- Failure modes: stale transcript/filing windows; cross-document attribution errors; PM acting on a synthesized number that sources to a context-stripped quote. A single bad buy/sell call on a $50M+ position dwarfs annual seat fees by 3-4 orders of magnitude.

**Hedge fund quant research (Two Sigma, Jane Street, Citadel; academic cluster).**

- Two Sigma's April 2026 "AI-First" internal mandate is the most explicit published case: every employee expected to integrate frontier LLMs, with named workflows in code generation and debugging, data cleaning, incident response, knowledge management. Jane Street and Citadel have not published equivalent statements; inference cost as a line item is invisible relative to compensation.
- Academic cluster (live 2025-2026): `AlphaAgent`, `QuantaAlpha`, `CogAlpha`, `Automate Strategy Finding`, and the `QuantCode-Bench` benchmark (400 Backtrader tasks, frontier models hit only 70-76% Judge Pass single-turn). Best models stay below 80% on first attempt; multi-turn agentic loops close the gap but at 5-10x token cost.
- Domain placement: code generation and backtesting clearly sit in productization (cheap automated verifiers exist: compile, unit test, backtest P&L on held-out windows). Signal/alpha research sits closer to sales (ground truth is delayed, no cheap give-up signal exists, alpha decay punishes overfitting silently). Within one firm the LLM stack straddles both regimes — the productization branch is where ROI is announced; the sales-shaped branch is where claims should be discounted.

**ESG research (Datamaran, Clarity AI, RepRisk).**

- Pricing: contact-only. Estimated bands: Clarity AI low five to low six figures/yr depending on data scope. RepRisk SaaS scales with company/project coverage (300K companies, 130K projects, 2.5M docs/30 languages indexed). Datamaran's Feb 2026 Regulatory Monitoring product targets sustainability/legal/compliance teams.
- CSRD compliance reports cost €500K+ for large enterprises and €50K-€150K for SMEs all-in (software €40K-€80K/yr large, plus €50K-€200K audit, €30K-€100K consulting). Generative-AI automation vendors cite approximately 70% time and cost reduction on the reporting leg.
- Greenwashing exposure is the fat tail. EU CSRD national fines reach 5% of global turnover; California SB 253 caps at $500K/yr. Recent enforcement: Invesco $17.5M SEC settlement; DWS €25M (Frankfurt prosecutor, April 2025).

### 1.3 VC Sourcing vs PE Due Diligence Cross-Cut

The two investment subdomains sit on opposite cells of the funnel-vs-per-item-cost grid:

| Dimension | VC sourcing | PE due diligence |
| --- | --- | --- |
| Funnel size | 500-2,000+ companies/yr/firm | 5-50 deep dives/yr/firm |
| Per-item LLM cost | cents to approximately $1 | approximately $25K-$500K all-in |
| Per-item human review | partner-minutes (high count) | analyst-days per deal |
| Failure cost shape | unbounded miss + lost IRR | regulatory + fiduciary fat tail |

Pricing models track this: Affinity-class seat at $2K-$2.7K/user/yr (cost is funnel throughput); Hebbia at approximately $10K/seat/yr (cost is per-deal verification depth).

## 2. Productization Subdomain Depth

The previous evidence note covered IDE coding assistants, agentic coding, agent benchmarks, and code review/test generation. The remaining productization subdomains divide cleanly on the verifier-cost axis.

### 2.1 Design (UX/UI) — HIGH Verifier Cost

- Pricing: hybrid seat plus included AI credits. Figma $16-$90/editor/mo with 500-3,000 AI credits/mo bundled. v0 by Vercel $20 (Premium) / $30 (Team) / $100 (Business) per user/mo with matching credit pools; over 6M users by March 2026. Galileo AI rolled into Google Stitch, free in beta with limits. Uizard $12-$39/seat/mo.
- Per-artifact cost: a v0 generation typically consumes approximately $0.10-$1.00 of credits per non-trivial UI iteration; a complete production-grade screen often takes 5-20 iterations, so approximately $1-$15/screen of marginal AI cost.
- Verification: designer eyeball + design-system token-conformance check + visual regression test downstream. There is no cheap automated verifier for "is this UI good." v0's pivot in 2026 is explicitly to import the customer's repo so that generated code compiles and lints against existing components — borrowing the coding verifier — but the aesthetic gate remains a human.
- Failure modes: Figma Make was temporarily suspended in 2025 after generating screens nearly identical to Apple's iOS Weather app — IP-mimicry is a fat-tail downstream cost. Hallucinated component names that don't exist in the design system are routine waste.

### 2.2 QA / Testing — LOW Verifier Cost

- Pricing: quote-based, volume-tiered. Mabl approximately $30K-$80K/yr; Testim starts approximately $450/user/mo; Applitools Eyes free tier 100 visual checkpoints/mo, paid approximately $399-$969+/mo.
- Per-artifact cost: per-snapshot Applitools approximately $0.005-$0.05 depending on tier; a full E2E suite run is sub-dollar for most teams. Test-case generation amortizes to roughly $5-$30 of tooling cost per stable test created (vs approximately 30-60 minutes of QA-engineer time without AI).
- Verification: cheapest verifier of the productization subdomains. A generated test either passes or fails against the application. Visual diff outputs a pixel score. Self-healing reconciles selectors automatically.
- Failure modes: auto-heal masking a real regression; visual diff false positives flooding the queue when CSS animations or fonts shift.

### 2.3 Security / IAM — MEDIUM Verifier Cost

- Pricing: per-developer, annual, sales-led. Snyk Team $25/dev/mo; median annual approximately $45K (range $15K-$182K). Cycode median annual approximately $70K; Apiiro approximately $55K. Semgrep open source free, Pro/Team paid.
- Per-artifact cost: SAST cost per scan is sub-dollar in marginal compute; realized cost per triaged finding is the operational metric. A 25-developer team spends 3-5 hours/week triaging Snyk alerts even with DeepCode AI's "near-zero false positive" claim.
- Verification: mid-cost. Static analysis itself is the verifier (rule fires or doesn't), but rule + AI suggestion correctness needs human approval. Snyk reports DeepCode auto-fix suggestions correct in 65% of cases; Cycode's exploitability agent claims 94% false-positive reduction; Semgrep Assistant 96% alignment with human triage.
- Failure modes: false negatives (missed CVEs in production) carry the worst tail. False-positive fatigue causes alert-blindness. AI-generated fixes that compile but introduce subtle insecurity are an emerging 2026 concern.

### 2.4 SRE / Incident Response — MEDIUM Verifier Cost

- Pricing: mostly per-event consumption with seat-plus-AIOps overlay. PagerDuty AIOps $699/mo flat on top of $21-$41/user/mo Incident Response. Datadog Bits AI SRE $500-$600 per 20 conclusive investigations/mo (approximately $25-$30 per investigation).
- Verification: mid-to-high cost. The verifier is the post-incident retrospective — high-quality but slow and human-driven. Within an incident, the verifier is whether the proposed remediation actually resolves the page; clean signal but only after action.
- 2026 data: Resolve.ai cites 72% MTTR reduction at Coinbase and 30% fewer engineers/incident at Zscaler. Datadog Bits AI claims 70-90% faster resolution; Traversal at DigitalOcean documented 36,000 engineering hours saved annually.
- Failure modes: wrong root-cause hypothesis sends an on-call down a rabbit hole — measurable in extended MTTR. Auto-remediation that itself causes an outage is the regulated tail (most vendors deliberately stop at recommendation).

### 2.5 ML / Data Engineering — SPLIT (Structural LOW, Semantic HIGH)

- Pricing: token-metered AI functions on top of warehouse credits. Snowflake Cortex AISQL token-based; $10-$100/mo for typical use cases but documented $5K single-query incidents on premium models. Cortex GA cost monitoring shipped March 2026. Databricks AI Functions integrated into platform credits. dbt Copilot tier-based.
- Per-artifact cost: a production pipeline built with dbt Copilot adds approximately $5-$50 of AI marginal cost per non-trivial model. AISQL on a 10M-row classification job ranges from cents to thousands.
- Verification: highly data-dependent. dbt tests, schema contracts, and Great Expectations give a coding-style cheap verifier for structural quality. Semantic quality (does this column actually mean what we think it does?) has no automated verifier and falls back to data-steward review.
- Failure modes: silent data-quality drift propagating to downstream dashboards. The $5K runaway-query case shows the fat-tail risk of per-token AI inside SQL.

### 2.6 Technical Writing / Docs — SPLIT (Code-Derived LOW, Conceptual HIGH)

- Pricing: seat-based, flat tiers. Mintlify Pro $250/mo (5 seats), Enterprise approximately $600+/mo. ReadMe Pro $250-$300/mo plus $150/mo Ask AI add-on. Swimm approximately $17.78/seat (paid).
- Verification: two-tier. Code-grounded docs (Mintlify auto-generated from OpenAPI; Swimm Auto-sync against source) give a near-coding-strength verifier — docs and code must agree, and a CI job can enforce this. Free-text conceptual prose has no verifier.
- Failure modes: Mintlify itself frames the dominant failure as staleness, not fabrication — outdated docs become wrong inputs to downstream agents.

### 2.7 Verifier-Cost Ranking Inside Productization

| Subdomain | Verifier cost | Closest analogue |
| --- | --- | --- |
| QA / testing | LOW | Coding |
| Docs (code-derived) | LOW | Coding |
| ML / data (structural) | LOW | Coding |
| Security / IAM | MEDIUM | Coding-with-human-gate |
| SRE / incident | MEDIUM | Operations |
| ML / data (semantic) | HIGH | Sales |
| Design (UX/UI) | HIGH | Sales |
| Docs (conceptual) | HIGH | Sales |

The productization domain is not uniform on the verifier-cost axis. The cheap-verifier end is where the productization-default strategy priority order applies most cleanly. The expensive-verifier end sits closer to sales-domain priorities on the verification axis. This is registered as Gap 8 in [`gap-analysis.md`](gap-analysis.md).

Pricing models inside productization confirm this split: QA and security vendors price predictably (per-seat, per-event); design and conceptual-docs vendors price like sales tools (flat tiers absorbing usage variance) precisely because the human reviewer is the binding cost.

## 3. Hybrid Workflows

Three workflow classes sit between the two skill domains. Their cost profile is mixed (verifiable parts plus judgment parts), and the 2026 vendor pricing trend is converging on outcome-based or per-resolution metering.

### 3.1 Marketing Operations

- HubSpot Breeze moved Customer Agent to outcome-based pricing on April 14, 2026: $0.50 per resolved conversation (down from $1.00 under the previous flat model). Marketing Hub Professional $800/mo seat floor, Customer Platform Pro $1,300/mo, plus a HubSpot Credit pool that meters Breeze AI and a $3-$7K onboarding fee. Adobe Marketo Engage seat- and contact-tier based (typically $1,000+/mo). Jasper Pro $59/seat/mo, Business by quote (typically $1-$2K/mo for approximately 10 seats).
- Episode-cost mental model: a typical mid-funnel campaign (one email, one landing page, three social variants, one paid-ad set) lands around $4-$8 in pure model spend if executed end-to-end on Jasper-class tools. Real attribution is dominated by seat license amortized over assets (often $30-$80 per finished asset) plus the outcome charge for the agentic reply legs.
- Verifiable share approximately 40-50% (subject-line A/B winner, deliverability, click rate); judgment share approximately 50-60% (brand voice, narrative angle, segmentation calls). Human handoff approximately 30-50% of all generated assets that ever ship.

### 3.2 Customer Support (L1/L2/L3 Tiered)

- Per-resolution rates anchor on Intercom Fin at $0.99/resolution with a 50% automation guarantee (refunds below threshold) and a published approximately 67% resolution rate across 40M conversations. Zendesk AI Enterprise $115/agent/mo plus $2.00/automated resolution at standard rate or $1.50 with committed volume. Ada starts approximately $30K/yr (median approximately $70K), Sierra opens at approximately $150K/yr with $50-$200K setup, Decagon median approximately $400K/yr. Sierra is exclusively outcome-based.
- Tier economics: human-only L1 averages $4-$6/inquiry, AI-deflected L1 $0.50-$0.99, AI-assisted L2 (bot collects context, human debugs) $8-$15, pure human L3 $25-$60/ticket on technical B2B products.
- 2026 reframing: L1 deflection is now table-stakes; the binding cost constraint has migrated to L2/L3, where AI's role is fact-assembly for human debuggers, not deflection. Verifiable share approximately 70-80% of L1 volume but only approximately 25% of L2 and under 10% of L3. Human handoff: 30-50% on L1 (Fin claims 33%, Freddy claims 47%), approximately 85% on L2, approximately 100% on L3.

### 3.3 DevRel Content and Community

- Algolia DocSearch free for OSS docs (with branding), otherwise Algolia standard meter: $0.40/1K records beyond the 100K floor and $0.50-$0.75/1K extra search requests. Inkeep Starter $200/mo, Scale $500/mo, enterprise by quote. Kapa.ai serves 200+ companies (OpenAI, monday.com, Logitech), 30M+ questions answered, custom enterprise typical $1.5-$3K/mo.
- Per-question episode cost: approximately $0.004-$0.016 in raw model spend (assuming 2-4K input tokens of doc context, 300-600 output tokens, multi-model router) and $0.05-$0.15 fully loaded once subscription, ingestion, and human-in-the-loop accuracy maintenance are amortized. Inkeep's published cost analysis: 50K monthly LLM calls run $200-$800 with router that sends routine queries to small models.
- Verifiable share high (approximately 75-85% of doc questions are about API signatures, parameter behavior, version diffs); judgment share approximately 15-25% (architectural recommendations, "is this a bug" calls). Human handoff lowest of the three hybrid classes: best-in-class deployments report approximately 5-15% escalation, but those handoffs concentrate the most expensive engineering minutes.

### 3.4 Outcome-Based Pricing Convergence

The dominant 2026 pricing trend across these hybrid workflows is outcome-based metering: HubSpot Breeze $0.50/resolved conversation, Sierra negotiated outcomes per contract, Intercom Fin $0.99/resolution. This is structurally different from both the productization-side per-token/per-credit metering and the sales-side flat seat. It works because the hybrid workflows have a measurable resolution event (ticket closed, conversation resolved) that the LLM-side per-token cost does not.

Whether outcome-based pricing maps cleanly onto per-episode total cost when indirect costs (human handoff time, regulatory exposure on bad-handoff cases) are included is an open question worth empirical study; the entry is in [`../reports/research-backlog.md`](../reports/research-backlog.md) under the hybrid-workflow section.

## 4. Korea/APAC Industry Context

The previous evidence note was US-vendor-centric. Korean and broader APAC patterns differ enough that they should not be inferred from US data.

### 4.1 Korea Sales and Investment

- Linq Alpha (Boston-HQ but with significant Korean go-to-market via the founders' Seoul roots) closed a $20M Series A in February 2026 led by TQ Ventures; reported metrics include 132% QoQ customer growth and 134K monthly active users on its messaging-embedded research agents.
- Persona AI completed a pre-IPO round backed by defense and institutional capital, repositioned around "sovereign physical AI."
- Channel Talk (채널톡), the dominant Korean SMB chat/support stack, restructured pricing 2025-11-28 to a Managed-User tier with no per-agent or per-chat overage. RAG+Tasks AI module internally claims up to 80% inquiry resolution. Early plans start under KRW 50K/mo — the de facto cheapest Korean entry point.
- Korean B2B selling remains relationship-heavy, so SDR-style cold outbound automation has lower attach than US peers. The leading wedge in 2026 is internal sales-ops AX: Daesang Group reported 82% time reduction on sales strategy analysis and 5,400 hours/year saved after deploying internal AI on accumulated B2B sales data.
- On the buy-side, Mirae Asset built an internal-network LLM AI Market Assistant with strict on-prem security as the gate. Korea Investment Securities relaunched its MTS in March 2026 with three new AI-driven menus, partnering with external AI vendors rather than building in-house. Both stop short of letting AI execute trades.

### 4.2 Korea Productization

- Naver shut down the consumer CLOVA X chat service on 2026-04-09 after approximately 2.5 years; HyperCLOVA X continues as a B2B/cloud offering through CLOVA Studio with code-completion features, but no public per-seat enterprise SKU competitive with Cursor.
- Samsung SDS announced a KRW 500B (approximately $341M) 2026 capex for AI infrastructure, became the official Korean reseller of OpenAI's ChatGPT Enterprise, and raised a KRW 1.22T (approximately $829M) convertible from KKR specifically for the AI build-out — buy-then-build is the dominant Korean enterprise productization play.
- NCSoft VARCO and Samsung Gauss remain workgroup-internal with no published external pricing. Among Korean developers, Cursor + Claude Code is the most-discussed pairing in 2026 trade press; no validated nationwide adoption survey exists, but the Lenovo CIO 2026 study reports Korea posted the steepest YoY enterprise AI adoption climb of all surveyed countries (jumping seven places to #18).

### 4.3 Japan and China Comparison

- Japan's signature April 2026 move: SoftBank-led consortium (NEC, Sony, Honda, Preferred Networks engineering) to build a sovereign Japanese foundation model with JPY 1T over five years from FY2026. Pricing not yet public. Fujitsu positioning a Japanese-LLM-on-Nutanix private appliance. NEC and NTT Data anchor enterprise AI to long consulting cycles.
- China's market consolidated to ten serious providers (Alibaba/Qwen, Tencent, Baidu, ByteDance/Doubao, DeepSeek, Moonshot, MiniMax, StepFun, Zhipu, Xiaomi). Alibaba leads Chinese LLM token share at 32% (H2 2025), AI revenue posted ten consecutive quarters of triple-digit YoY growth.
- April 2026 brought the first Chinese AI compute up-cycle in years: Alibaba, Tencent, Baidu, and Zhipu raised AI compute prices 5-34% effective April-May 2026. DeepSeek V4 (March 2026) holds the price floor at $0.30/M input and $0.50/M output. ByteDance Doubao 2.0 (Feb 2026) reaches 155M weekly active users, positioned approximately 90% cheaper than GPT-5.2 for enterprise summarization.

### 4.4 APAC Regulatory Differences (Sales-Domain Cost Impact)

- Korea: Framework Act on AI Development and Trustworthiness (enacted Jan 2025) takes effect January 2026. PIPC clarified PIPA Art. 15(1)(vi) "legitimate interests" can ground processing of public data for AI training. Penalties under PIPA up to 3% of global annual revenue. 2026 enforcement focuses on repeat offenders and high-risk personal data (biometrics, video). Public-sector AI now requires PIA (Personal Information Impact Assessment).
- Japan: April 2026 APPI amendment removes mandatory opt-in consent for AI training when risk is "low" or use qualifies as research/statistics, making Japan the most AI-training-friendly major jurisdiction. Administrative surcharges for serious violations are being introduced.
- China: PIPL tightened January 1, 2026 with sweeping CAC enforcement against foreign fintech and e-commerce. Max penalty now 5% of global revenue or CNY 5M, whichever higher. Cross-border data transfer hurdles have grown — pushing multinational sales-AI vendors to keep Chinese tenants on locally hosted instances, materially raising infra cost per Chinese customer (typically 1.5-2.5x the Korean/Japan equivalent).

## 5. Compliance and Regulatory Cost Overlay

This section maps regulatory exposure into the cost framework. The shape of compliance cost differs sharply by domain.

### 5.1 Sales-Domain Regulations

- **GDPR (EU)**: penalty ceiling €20M or 4% of global turnover (€10M / 2% for minor violations). Cumulative GDPR fines crossed €7.1B by Q1 2026; email-marketing-related violations approximately 15-20% of total enforcement actions. Notable 2025 cases: Garante fined Replika operator Luka Inc. €5M for chatbot data processing without lawful basis; Acea Energia €3M for unconsented telemarketing; CNIL fined Google €200M for ad-disguised emails in Gmail. Cost overlay: DPIA approximately $8-$30K each, consent management platform $15-$60K/yr, EU representative $1.5-$5K/mo. Each AI outbound campaign requires per-segment lawful-basis attestation, adding 4-12 hours of legal review per cohort.
- **CAN-SPAM (US)**: per-email civil penalty rose to $53,088 (FTC Jan 2025 inflation adjustment), no aggregate cap. The FTC itself uses ML for detection, compressing detection latency.
- **CASL (Canada)**: maximum AMP C$10M per violation for corporations (C$1M individuals). 2025 CRTC enforcement: 153 Notices to Produce, 123 Warning Letters; actual AMPs C$5K-C$250K. Express opt-in (not implied) is the default — strictest of the three Anglosphere regimes.
- **CCPA/CPRA (California)**: effective Jan 1, 2026, CPPA's ADMT regulations narrow scope to systems that "substantially replace human decisionmaking." DROP (Delete Request and Opt-out Platform) goes live August 1, 2026 with 45-day SLA for data brokers. Statutory penalty $2,500/violation, $7,500 if intentional.
- **TCPA (US, AI voice)**: FCC's Feb 2024 Declaratory Ruling held AI-generated voices are "artificial" under TCPA, automatically triggering prior-express-written-consent regardless of how human-like. Penalty $500-$1,500 per call, no cap. A 10K-call campaign without consent is $5-$15M exposure.

### 5.2 Investment-Domain Regulations

- **MNPI**: SEC enforcement shifting from individual insider trading toward systemic supervisory failures. December 2025: Virtu Americas $2.5M settlement over generic-credential database access to post-trade MNPI for 15 months without per-user audit. AI agents reading from data rooms multiply this risk: an agent retrieving documents under a service-account identity defeats per-user audit trails. Cost overlay: PBAC (policy-based access control), per-prompt logging with persistent IDs, MNPI tagging.
- **Fiduciary duty / FINRA Reg BI**: 2026 Regulatory Oversight Report (Dec 9, 2025) explicitly says firms must use AI to inform, not replace, advisor judgment, and requires documented consideration of alternatives plus human sign-off on any AI-generated/summarized recommendation.
- **SEC Marketing Rule 206(4)-1 / AI-washing**: first AI-washing actions Delphia ($225K) and Global Predictions ($175K) settled March 2024. First Marketing Rule action under Chair Atkins September 4, 2025. December 2025 Risk Alert flagged testimonials/endorsements and third-party ratings for next enforcement wave.
- **EU MiFID II / MAR**: ESMA's February 26, 2026 supervisory briefing extended pre-trade controls and stress testing to AI-driven algorithmic trading. Dutch AFM and Italian Consob jointly warned MAR cannot adequately address AI-collusion risk.
- **ESG (SFDR/CSRD/EmpCo)**: SFDR 2.0 proposed November 20, 2025; CSRD limited assurance mandatory now, reasonable assurance from 2028. EmpCo (anti-greenwashing) in force September 27, 2026, up to 4% turnover for cross-border violations. Recent: Invesco $17.5M SEC; DWS €25M Frankfurt prosecutor.

### 5.3 Productization-Domain Regulations

- **AI-code IP/copyright**: *Doe v. GitHub* in Ninth Circuit appeal as of Feb 2026. Judge Tigar dismissed DMCA 1202(b) and direct-copying claims June 2024; only open-source license violation and breach of contract survive. November 2025 Munich Regional Court held that AI memorization can constitute copyright reproduction if outputs are "substantially identical" — first such European precedent. EU AI Act Article 53(1)(d) training-data summary obligation took effect August 2, 2025; enforcement powers activate August 2, 2026. Non-compliance: up to 3% of worldwide turnover or €15M.
- **License contamination**: studies report AI regurgitation rates up to approximately 80% for some assistants. GPL/AGPL output in proprietary code can force open-sourcing of the entire derivative work. Mitigation: SCA + license-block scanners $20-$100K/yr enterprise, plus per-PR license-classifier review (approximately $0.50-$5/PR in tooling cost).
- **Vulnerability disclosure**: AI-discovered vulnerabilities (12 OpenSSL CVEs found by an AI in fall/winter 2025) raise CVD (coordinated vulnerability disclosure) load. CVE volume forecast at approximately 50,000 in 2026 (up 27.9% YoY).
- **EU AI Act high-risk classification**: February 2, 2026 Commission published practical-implementation guidelines for Article 6. August 2, 2026 most remaining provisions enforceable. August 2, 2027 Article 6(1) safety-component rules apply. Coding agents writing code for medical devices, automotive, aviation, or critical infrastructure can be pulled into Annex I (high-risk), triggering conformity assessment, technical documentation, CE marking. Penalty ceiling €35M or 7% of worldwide turnover.
- **SOC 2 / ISO 27001 / FedRAMP**: SOC 2 Type II $15-$75K (audit) plus $30-$50K (readiness), totaling $45-$125K over 18-24 months. FedRAMP authorization 12-24 months and "six-figure" licensing for enterprise platforms. FedRAMP 20x (announced August 2025) is fast-tracking AI services; IBM watsonx and 10 other IBM tools authorized April 1, 2026.

### 5.4 Compliance Cost-Shape Comparison

The shape of regulatory cost differs sharply by domain.

| Domain | Cost shape | Overlay strategy | Annual overlay range |
| --- | --- | --- | --- |
| Sales | Per-event fat-tail (penalties scale linearly with message/call count, AI compresses time-to-mass-emission) | Convert unbounded tail into bounded fixed cost via consent platform + suppression infra + DPIA + legal review | $150K-$500K/yr |
| Investment | Per-incident catastrophic (single MNPI leak or AI-washing claim is a multi-million settlement plus reputational tail) | Reduce tail probability via PBAC + telemetry retention + substantiation files + human sign-off (binding constraint is sign-off latency, not per-event cost) | $200K-$1M/yr |
| Productization | Structural / amortized (audits, conformity assessment, license scanning, FedRAMP) | Pay once for market access, then maintain. Volume-independent. The trade-off is timing — vendors who postpone face binary market exclusion (no enterprise/no EU) | $300K-$1.5M one-time + $150K-$400K/yr maintenance, plus FedRAMP $500K-$2M+ if applicable |

Marginal cost per AI message after the sales-domain overlay is near-zero; the overlay pays back via single-incident avoidance. Marginal AI deal-research cost after the investment-domain overlay is unchanged but throughput is throttled by sign-off. Productization overlay is largely usage-independent — it gates market access, not per-action cost.

## 6. Cross-Cut Patterns

### 6.1 Pricing Model Patterns by Domain Layer

Three layers, three pricing patterns.

| Layer | Dominant pricing model | Why |
| --- | --- | --- |
| Productization (cheap-verifier subdomains) | Per-seat plus metered usage (per-token or per-credit) with explicit overage | Workload variance is high and tied to a measurable artifact (request, agent run); usage exposure helps vendors price tail consumers correctly |
| Productization (expensive-verifier subdomains) and Sales | Premium flat seat with implicit usage absorption | Workload variance is lower at the artifact level; binding cost is human reviewer time, not generation cost; vendors price for the integration and reliability premium |
| Hybrid (marketing, support, DevRel) | Outcome-based per-resolution metering, emerging in 2026 | A measurable resolution event (ticket closed, conversation resolved) provides a clean billable unit that aligns vendor incentives with workflow value |

The pricing structure is downstream of where the dominant indirect cost lives, which is downstream of the verifier-cost position.

### 6.2 The Verifier-Cost Spectrum is Wider than the Domain Split

The skill-domain taxonomy puts sales and productization on opposite ends of the verifier-cost axis. The deeper data shows the productization domain itself spans the full verifier-cost range (Gap 8). The cleaner story is:

- **verifier-cost is the load-bearing axis**, not the domain label
- domain labels remain useful because they correlate with the cluster of dimensions (verification mechanism, feedback-loop length, human-cost asymmetry, failure-cost shape) but they do not fully predict verifier-cost
- inside productization, design / conceptual docs / semantic data work sit on the same verifier-cost end as sales — and their pricing models confirm it
- inside sales, investment-with-citation-anchored output is closer to a verifier than pure outbound; that is why Hebbia/AlphaSense-class pricing tolerates premium seat economics (the verifier exists, even if it costs analyst minutes)

### 6.3 Compliance Overlay Is a Third Cost Layer

Direct cost (per-token, per-call) and indirect cost (retry, verification, human review) cover the inside of the workflow. Compliance overlay is a third layer that sits across both and is shaped by the regulatory regime applicable to the artifact, not the artifact itself:

- the same outbound email costs the same in tokens regardless of CASL exposure, but a CASL-exposed sender bears C$10M per-violation tail
- the same investment memo costs the same in tokens regardless of who sees it, but an MNPI-exposed memo path triggers per-prompt logging requirements and a sign-off latency that throttles throughput
- the same generated code costs the same in tokens regardless of whether the consumer is an EU AI Act high-risk system, but the conformity assessment + CE marking cost gates the entire commercial relationship

The cost-aggregation rules in [`../frameworks/cost-aggregation.md`](../frameworks/cost-aggregation.md) §Fat-Tail and Domain-Conditioned Reporting cover the per-episode side; the compliance overlay should be tracked as an annualized cost line that scales with the regulatory regime, not with episode count.

## 7. Implications for Repository Updates

The next-step backlog implied by this deep dive is captured in [`../reports/research-backlog.md`](../reports/research-backlog.md) under "Skill-Domain Follow-Ups." The most concrete cross-cutting items are:

- the productization sub-split on the verifier-cost axis (Gap 8) should be a first-class consideration when designing strategy comparisons inside the productization domain
- hybrid workflows are a third population, not a boundary case, and benefit from outcome-based per-resolution accounting
- compliance overlay should enter the cost framework as a third layer, with shape per domain
- Korea/APAC industry context should not be inferred from US data; data residency, regulatory regime, and Korean enterprise buy-then-build patterns materially alter the cost profile

## Sources

Sales subdomains:

- [Loopio 2026 pricing — Sparrow Genie](https://www.sparrowgenie.com/blog/loopio-pricing)
- [Responsive 2026 pricing — Sparrow Genie](https://www.sparrowgenie.com/blog/responsive-pricing)
- [Loopio 2026 trends and benchmarks](https://loopio.com/trends-report/)
- [2026 best AI tools for RFP responses — Loopio](https://loopio.com/blog/best-ai-software-rfp-responses/)
- [6sense pricing 2026 — Warmly](https://www.warmly.ai/p/blog/6sense-pricing)
- [Demandbase vs 6sense — AiSDR](https://aisdr.com/blog/demandbase-vs-6sense/)
- [Gainsight features 2026 — Oliv](https://www.oliv.ai/blog/gainsight-features)
- [Gainsight MCP April 2026 launch — National Today](https://nationaltoday.com/us/ma/boston/news/2026/04/02/gainsight-opens-platform-with-mcp-bringing-customer-retention-into-ai-era/)
- [Crossbeam pricing](https://www.crossbeam.com/pricing)
- [Crossbeam-Reveal merger announcement](https://www.crossbeam.com/crossbeam-and-reveal-merger-announcement)
- [PartnerStack pricing — Vendr](https://www.vendr.com/marketplace/partnerstack)

Investment subdomains:

- [Affinity pricing 2026 — Vendr](https://www.vendr.com/marketplace/affinity)
- [Harmonic.ai PitchBook profile 2026](https://pitchbook.com/profiles/company/453414-79)
- [VC tech stack 2026 — Standard Metrics](https://standardmetrics.io/library/the-top-ai-powered-vc-tech-stack-tools-in-2026/)
- [VC-backed CFO AI spend — CFO Brew](https://www.cfobrew.com/stories/2026/04/14/vc-backed-cfos-expect-ai-spending-to-double-this-year)
- [AlphaSense pricing — Vendr](https://www.vendr.com/marketplace/alphasense)
- [AlphaSense Generative Search next-gen Jan 2026](https://www.alpha-sense.com/resources/product-articles/generative-search-next-generation/)
- [AlphaSense revenue $500M ARR — Sacra](https://sacra.com/c/alphasense/)
- [Bloomberg Terminal pricing 2026 — CostBench](https://costbench.com/software/financial-data-terminals/bloomberg-terminal/)
- [FactSet Mercury launch](https://investor.factset.com/news-releases/news-release-details/factset-launches-factset-mercury-supercharge-junior-banker/)
- [Two Sigma AI-First mandate — HedgeCo](https://www.hedgeco.net/news/04/2026/two-sigmas-ai-first-internal-mandate-the-race-for-operational-alpha-in-the-age-of-frontier-models.html)
- [QuantCode-Bench — arXiv:2604.15151](https://arxiv.org/abs/2604.15151)
- [Datamaran Regulatory Monitoring launch Feb 2026 — ESG News](https://esgnews.com/datamaran-launches-ai-regulatory-monitoring-platform-as-global-esg-rules-intensify/)
- [CSRD compliance costs and AI 70% reduction — Omdena](https://www.omdena.com/blog/generative-ai-csrd-esrs-reporting-automation-guide)

Productization subdomains:

- [Figma plans and pricing](https://www.figma.com/pricing/)
- [v0 by Vercel pricing](https://v0.app/pricing)
- [Updated v0 pricing — Vercel](https://vercel.com/blog/updated-v0-pricing)
- [Vercel v0 and the 90% problem — VentureBeat](https://venturebeat.com/infrastructure/vercel-rebuilt-v0-to-tackle-the-90-problem-connecting-ai-generated-code-to)
- [Mabl pricing](https://www.mabl.com/pricing)
- [Applitools Eyes pricing](https://applitools.com/platform-pricing/)
- [AI testing tools comparison 2026 — Testcollab](https://testcollab.com/blog/ai-testing-tools)
- [Snyk DeepCode AI](https://snyk.io/platform/deepcode-ai/)
- [AppSec pricing guide 2026 — AppSec Santa](https://appsecsanta.com/aspm-tools/appsec-pricing-guide)
- [PagerDuty AIOps pricing](https://www.pagerduty.com/pricing/aiops/)
- [Datadog Bits AI SRE](https://www.datadoghq.com/product/ai/bits-ai-sre/)
- [Resolve.ai Series A](https://resolve.ai/blog/series-a-funding)
- [Snowflake Cortex AISQL overview — Select](https://select.dev/posts/snowflake-cortex-ai-sql-overview-and-cost-monitoring)
- [Snowflake Cortex pricing 2026 — Data Engineer Hub](https://dataengineerhub.blog/articles/snowflake-cortex-cost-comparison)
- [dbt Copilot — dbt Labs](https://www.getdbt.com/product/dbt-copilot)
- [Mintlify pricing](https://www.mintlify.com/pricing)
- [Mintlify on AI hallucinations and staleness](https://www.mintlify.com/resources/ai-hallucinations)

Hybrid workflows:

- [HubSpot outcome-based Breeze pricing — MarTech](https://martech.org/hubspot-moves-to-outcome-based-pricing-for-some-breeze-ai-agents/)
- [HubSpot AI agent pricing 2026 — eesel](https://www.eesel.ai/blog/hubspot-ai-agent-pricing-2026)
- [Marketo Engage pricing](https://business.adobe.com/products/marketo/pricing.html)
- [Jasper plans](https://www.jasper.ai/pricing)
- [Intercom Fin pricing](https://fin.ai/pricing)
- [Fin AI resolution outcomes — Intercom](https://www.intercom.com/help/en/articles/8205718-fin-ai-agent-outcomes)
- [Zendesk AI dynamic pricing 2026 — eesel](https://www.eesel.ai/blog/zendesk-ai-dynamic-pricing-plan)
- [Sierra outcome-based pricing](https://sierra.ai/blog/outcome-based-pricing-for-ai-agents)
- [Decagon AI pricing — eesel](https://www.eesel.ai/blog/decagon-ai-pricing)
- [AI agent pricing comparison 2026 — Fin.ai](https://fin.ai/learn/ai-customer-service-agent-pricing-comparison)
- [Tier-1 deflection guide — eesel](https://www.eesel.ai/blog/ai-for-tier-1-support-deflection)
- [Kapa.ai pricing page](https://www.kapa.ai/pricing)
- [Inkeep pricing](https://docs.inkeep.com/cloud/faqs/pricing)
- [Inkeep LLM cost analysis](https://inkeep.com/blog/50-000-llm-calls-cost-less-than-you-think-a-2026-pricing-rea)
- [Algolia DocSearch program](https://docsearch.algolia.com/docs/docsearch-program/)

Korea/APAC:

- [Linq Series A — TechCrunch](https://techcrunch.com/2026/02/02/linq-raises-20m-to-enable-ai-assistants-to-live-within-messaging-apps/)
- [Persona AI pre-IPO — KoreaTechDesk](https://koreatechdesk.com/persona-ai-pre-ipo-korea-sovereign-physical-ai)
- [Channel Talk pricing change notice](https://docs.channel.io/updates/ko/articles/%EC%A4%91%EC%9A%94-%EA%B3%B5%EC%A7%80-%EC%B1%84%EB%84%90%ED%86%A1-%EA%B0%80%EA%B2%A9%EC%A0%9C-%EA%B0%9C%ED%8E%B8-%EC%95%88%EB%82%B4251128--8bd5ddd0)
- [한국투자증권 MTS AI 시황 — InsightKorea](https://www.insightkorea.co.kr/news/articleView.html?idxno=243708)
- [미래에셋 AI 어시스턴트 — News1](https://www.news1.kr/finance/general-stock/5545955)
- [대상그룹 B2B AX — 전자신문](https://www.etnews.com/20260112000114)
- [CLOVA X 종료 — 나무위키](https://namu.wiki/w/CLOVA%20X)
- [Samsung SDS OpenAI 리셀 — Korea Herald](https://www.koreaherald.com/article/10661664)
- [Samsung SDS KKR convertible — KED Global](https://www.kedglobal.com/corporate-strategy/newsView/ked202604150007)
- [Lenovo CIO Korea AI 7-rank jump — CIO](https://www.cio.com/article/4144097/)
- [Cursor vs Claude Code 2026 (KR) — Wavespeed](https://wavespeed.ai/blog/ko/posts/cursor-vs-claude-code-comparison-2026/)
- [Japan SoftBank consortium — Japan Times](https://www.japantimes.co.jp/business/2026/04/12/companies/softbank-ai-new-firm/)
- [Fujitsu private LLM — Computer Weekly](https://www.computerweekly.com/news/366622848/Fujitsu-targets-private-AI-with-Japanese-LLM-on-Nutanix)
- [China AI compute price hike — TrendForce](https://www.trendforce.com/news/2026/04/10/news-ai-compute-prices-rise-across-china-tencent-joins-alibaba-baidu-in-hikes-zhipu-raises-prices-again/)
- [Caixin China cloud price hike](https://www.caixinglobal.com/2026-03-19/alibaba-tencent-hike-cloud-prices-as-ai-boom-drives-up-hardware-costs-102424744.html)
- [DeepSeek V4 pricing — NXCode](https://www.nxcode.io/resources/news/deepseek-api-pricing-complete-guide-2026)
- [Doubao 2.0 — ABHS](https://www.abhs.in/blog/china-ai-model-war-doubao-qwen-deepseek-kimi-2026)
- [PIPA Korea 2026 enforcement — Hogan Lovells](https://www.hoganlovells.com/en/publications/south-korea-considers-updates-to-data-and-cyber-laws)
- [PIPC AI guidelines — Baker McKenzie](https://connectontech.bakermckenzie.com/south-korea-sets-ai-standard-pipcs-guidelines-for-generative-ai-present-obligations-opportunity/)
- [Japan APPI 2026 amendment — Reed Smith](https://www.reedsmith.com/our-insights/blogs/viewpoints/102l2yi/japan-in-focus-data-protection-and-ai-in-japan/)
- [China PIPL 2026 enforcement — Sesame Disk](https://sesamedisk.com/china-pipl-compliance-2026/)
- [APAC AI regulations — Xenoss](https://xenoss.io/blog/asia-pacific-apac-ai-regulations)

Compliance overlay:

- [GDPR fines for AI systems — DPO Europe](https://data-privacy-office.eu/fines-for-gdpr-violations-in-ai-systems-and-how-to-avoid-them/)
- [Kiteworks GDPR fines 2026](https://www.kiteworks.com/gdpr-compliance/gdpr-fines-data-privacy-enforcement-2026/)
- [CAN-SPAM penalties 2026 — Prospeo](https://prospeo.io/s/can-spam-penalties)
- [CASL email compliance penalties — Prospeo](https://prospeo.io/s/casl-email-compliance)
- [CRTC CASL enforcement](https://web.crtc.gc.ca/eng/internet/pub/20250331.htm)
- [FCC AI voice TCPA ruling](https://www.fcc.gov/document/fcc-confirms-tcpa-applies-ai-technologies-generate-human-voices)
- [Wilson Sonsini FCC AI voices TCPA](https://www.wsgr.com/en/insights/fcc-rules-ai-generated-voices-are-artificial-under-the-tcpa.html)
- [CCPA/CPRA amendments effective Jan 1, 2026 — Freeman Mathis](https://www.fmglaw.com/cyber-privacy-security/ccpa-cpra-amended-regulations-approved-and-effective-january-1-2026/)
- [SEC MNPI enforcement Q4 2025 — Morrison Foerster](https://www.mofo.com/resources/insights/260126-top-5-sec-enforcement-developments-for-q4-2025)
- [SEC AI-washing first enforcement — Mayer Brown](https://www.mayerbrown.com/en/insights/publications/2024/04/securities-and-exchange-commission-brings-first-enforcement-actions-over-aiwashing)
- [FINRA 2026 Regulatory Oversight Report PDF](https://www.finra.org/sites/default/files/2025-12/2026-annual-regulatory-oversight-report.pdf)
- [Snell & Wilmer FINRA 2026 Autonomous AI](https://www.swlaw.com/publication/finras-2026-oversight-report-signals-a-supervisory-reckoning-for-autonomous-ai/)
- [ESMA Feb 2026 algorithmic trading briefing — Linklaters](https://financialregulation.linklaters.com/post/102mknu/mifid-ii-esma-issues-supervisory-briefing-on-algorithmic-trading)
- [SFDR 2.0 proposal — Linklaters](https://sustainablefutures.linklaters.com/post/102mnmn/esg-quick-guide-eu-sustainable-finance-disclosure-regulation-sfdr)
- [Doe v GitHub — BakerHostetler tracker](https://www.bakerlaw.com/the-copilot-litigation/)
- [GitHub Copilot litigation case updates](https://githubcopilotlitigation.com/case-updates.html)
- [EU AI Act Article 53 GPAI obligations — Steptoe](https://www.steptoe.com/en/news-publications/steptechtoe-blog/eu-ai-act-obligations-for-gpai-models-now-applicable.html)
- [EU AI Act fines explained — RegDossier](https://regdossier.eu/eu-ai-act-fines-explained/)
- [GPL propagation in AI models — Open Source Guy](https://shujisado.org/2025/11/27/gpl-propagates-to-ai-models-trained-on-gpl-code/)
- [AI-Discovered CVEs 2026 — Bloo](https://bloo.io/resources/articles/ai-discovered-cves-prepare)
- [EU AI Act Article 6 high-risk classification](https://artificialintelligenceact.eu/article/6/)
- [SOC 2 cost 2026 — Cavanex](https://cavanex.com/blog/soc-2-compliance-cost-2026)
- [GSA FedRAMP 20x AI initiative](https://www.gsa.gov/about-us/newsroom/news-releases/gsa-fedramp-prioritize-20x-authorizations-for-ai-08252025)
- [IBM watsonx FedRAMP authorization April 2026](https://newsroom.ibm.com/2026-04-01-IBM-Expands-FedRAMP-Portfolio-with-Authorization-of-11-Software-Solutions,-Including-watsonx)
