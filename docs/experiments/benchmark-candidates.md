# Benchmark Candidates

## Purpose

This document proposes initial benchmark candidates for the first research cycle.

## Selection Criteria

Each candidate benchmark should satisfy most of the following:

- reproducible task instances
- measurable success criteria
- practical relevance
- support for cost-sensitive policy variation
- manageable setup cost for early experiments

## 1. Coding

### Primary candidates

- **HumanEval**
  - fit: clean correctness signal through tests
  - good for: model selection, retry policy, verification policy
- **MBPP**
  - fit: broader coding task variety with runnable tests
  - good for: baseline comparisons and retry analysis

### Why this family should start first

- correctness is relatively objective
- pass/fail thresholds are easy to communicate
- retries and verification naturally matter

## 2. Classification

### Primary candidates

- **MMLU subsets**
  - fit: broad subject coverage and controlled evaluation
  - good for: strong-vs-cheap model routing and selective escalation
- **Domain-specific label classification tasks**
  - fit: practical task framing with measurable accuracy or F1
  - good for: deferral and review policy analysis

### Why this family should come early

- easy to compare direct cost against quality
- low workflow complexity makes policy effects easier to isolate

## 3. Information Extraction

### Primary candidates

- **Structured extraction from documents or web pages**
  - fit: precision/recall style evaluation
  - good for: tool use, verification, cleanup policy
- **Relation or field extraction benchmarks**
  - fit: measurable field-level accuracy
  - good for: cheap-vs-strong model comparisons and review thresholds

### Why this family matters

- closer to real business workflows
- useful for evaluating cleanup and review overhead

## 4. Multi-step Agent Workflows

### Primary candidates

- **GAIA**
  - fit: multi-step, tool-using assistant tasks
  - good for: routing, tool use, retries, failure recovery
- **MiniWoB++ or workflow-style sandbox tasks**
  - fit: explicit sequence of decisions and environment interaction
  - good for: orchestration cost and fallback analysis

### Why this family should come later

- richer orchestration and recovery behaviors
- harder to evaluate cleanly
- best used after the logging and failure taxonomy are stable

## 5. Sales-Domain Benchmarks

The four families above all sit in the productization domain as defined in [`../frameworks/skill-domain-taxonomy.md`](../frameworks/skill-domain-taxonomy.md), or in operations work that resembles it. The sales domain (selling and investment) is under-represented in public benchmarks, which is itself a research finding worth flagging. The closest public benchmarks for the sales domain are:

### Selling and Customer Interaction

- **τ-bench (tau-bench)**
  - fit: tool-using agent in simulated customer-service settings; measures whether the agent completes a customer request and updates system state correctly
  - good for: verification-like check structures, human-handoff thresholds in customer-facing workflows
  - caveat: customer-support slice; does not cover outbound selling

### Investment and Financial Reasoning

- **FinanceBench**
  - fit: open-book question answering over financial filings with 10,231 hand-labeled Q&A pairs on public-company filings
  - good for: retrieval-grounded investment workflows, citation-density policy analysis
- **FinQA and ConvFinQA**
  - fit: numerical reasoning over financial documents
  - good for: multi-step reasoning policies in investment research
- **BizBench and FPB (Financial PhraseBank)**
  - fit: financial sentiment and business reasoning
  - good for: baseline classification in investment workflows

### Legal and Compliance (overlap with both domains)

- **LegalBench**
  - fit: 162 legal reasoning tasks from US law
  - good for: compliance-sensitive sales and investment workflows where regulatory exposure is a fat-tailed failure mode

### Why This Family Should Be Flagged, Not Prioritized

- no public benchmark currently measures the full sales-domain loop (outbound → reply → meeting → deal), because that loop takes weeks and is confounded by deliverability, market seasonality, and counterparty behavior
- no public benchmark currently measures investment-memo or IC-level decision quality over multi-year fund returns
- the closest research-cycle equivalent is to treat FinanceBench and τ-bench as **proxy benchmarks** that stress citation policy and tool-use policy respectively, while acknowledging that they do not cover the full sales-domain failure surface (deliverability collapse, regulatory exposure, ICP drift)

This is Gap 7 in [`../references/gap-analysis.md`](../references/gap-analysis.md): sales-domain workflows are under-represented in cost-optimization benchmarks, not just in cost-optimization literature. A research deliverable from the first empirical cycle could be a **proposed minimal sales-domain benchmark design** rather than running a sales-domain cost-quality frontier on an inadequate proxy.

## Recommended First-Cycle Benchmark Set

For the first cycle, the most practical benchmark set is:

1. HumanEval
2. MBPP
3. one classification benchmark or MMLU subset
4. one structured extraction task set
5. one multi-step agent benchmark such as GAIA

Sales-domain benchmarks in §5 are not included in the first cycle because of the proxy-benchmark concern above. They should enter a later cycle only after a minimum sales-domain benchmark design is proposed.

## Policy Priorities by Benchmark Family

### Coding

- strong-model single pass
- cheap-model single pass
- retry-enabled policy
- verification-enabled policy

### Classification

- strong-model single pass
- cheap-model single pass
- difficulty-based routing
- defer-to-review policy

### Extraction

- strong-model single pass
- cheap-model single pass
- tool-assisted extraction
- verification and cleanup policy

### Agent Workflows

- strong-model single pass
- routing policy
- tool policy
- retry and fallback policy
- human escalation policy

## Recommendation

The first operational research cycle should begin with coding and classification, then expand to extraction and agent workflows once the measurement stack is stable.
