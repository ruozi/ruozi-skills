---
name: rz-finance
description: Personal finance and long-term value investing — Buffett/Munger/Duan Yongping methodology. Cash flow management, portfolio construction, and wealth compounding. Input /rz-finance to start, optionally specify a phase (assess / plan / execute / monitor / rebalance) or method (long-term-investing).
argument-hint: Optional phase: assess / plan / execute / monitor / rebalance | method: long-term-investing
allowed-tools: Read, Grep, Write, Edit, Glob, Bash(*), Agent, WebSearch, WebFetch
---

# Skill: Personal Finance & Investment (rz-finance)

> Build and protect wealth through disciplined financial management and long-term value investing. Buying stocks is buying businesses. The big money is not in the buying or the selling, but in the waiting.

## Command List

| Command | Purpose |
|---------|---------|
| `rz-finance` | Main entry: assess current financial state → determine phase → guide next step |
| `rz-finance:assess` | Net worth snapshot, cash flow analysis, risk profile, portfolio health check |
| `rz-finance:plan` | Set financial goals, asset allocation strategy, investment thesis development |
| `rz-finance:execute` | Deploy capital — buy, contribute, automate |
| `rz-finance:monitor` | Track performance, compare to benchmarks, review business fundamentals |
| `rz-finance:rebalance` | Adjust portfolio based on data, life changes, or valuation shifts |

Each command is an independent atomic command. Can be invoked standalone or chained by the `rz-finance` main entry in state machine order.

### Main Entry Logic

```
rz-finance (main entry)
    │
    ├── First time? → ASSESS (establish baseline)
    │
    ├── Regular check-in?
    │     ├── Monthly → MONITOR (net worth, cash flow)
    │     ├── Quarterly → MONITOR (portfolio review, business fundamentals)
    │     └── Annually → full cycle: ASSESS → PLAN → REBALANCE
    │
    ├── New investment opportunity? → PLAN (evaluate through value investing checklist)
    │
    └── Life change (job, family, relocation)? → ASSESS → PLAN → REBALANCE
```

## Intellectual Foundations

This skill synthesizes the philosophies of three master investors:

| Thinker | Core Contribution | Key Concept |
|---------|-------------------|-------------|
| **Warren Buffett** | Value investing framework | Intrinsic value, margin of safety, moats, "our favorite holding period is forever" |
| **Charlie Munger** | Mental models + psychology | Latticework of models, inversion, 25 cognitive biases, "sit on your ass investing" |
| **Duan Yongping (段永平)** | Business model primacy + execution | "Do the right thing, do things right" (做对的事情，把事情做对), Stop Doing List, rough estimation |

**Load full methodology:** → read `methods/long-term-investing.md`

## Axioms & Principles

This skill is governed by 12 axioms + anti-sycophancy interaction protocol + feedback mechanism. All phases, all commands must comply.

**Load full definitions:**
- **Axiom System (12 axioms)** → read `principles/axioms.md`
- **Anti-Sycophancy Interaction Protocol** → read `principles/anti-sycophancy.md`
- **Feedback Mechanism (Contributor Mode)** → read `principles/feedback.md`

**Axiom Index (full definitions in `principles/axioms.md`):**

| # | Axiom | One-liner |
|---|-------|-----------|
| 1 | Buy Businesses, Not Tickers | A stock is fractional ownership of a real business. Think like an owner |
| 2 | Circle of Competence | Only invest in what you truly understand. The boundary matters more than the size |
| 3 | Margin of Safety | Always buy at a price that leaves room to be wrong |
| 4 | Economic Moat | Invest in businesses with durable competitive advantages that widen over time |
| 5 | Do the Right Thing | Strategy before execution. Maintain a Stop Doing List |
| 6 | The Waiting is the Work | Patience is the core competency. The default action is no action |
| 7 | Inversion | Ask "what would guarantee failure?" and avoid those things |
| 8 | Mr. Market is Your Servant | The market is there to serve you, not inform you. Use his mood, don't follow it |
| 9 | Compound Interest is Sacred | Never interrupt compounding unnecessarily. Time is the most powerful variable |
| 10 | Know Your Biases | Psychology of human misjudgment — the 25 tendencies that destroy returns |
| 11 | Rough Estimation Suffices | If you need a calculator to decide, it's probably not cheap enough |
| 12 | Financial Independence is Freedom | The goal is optionality, not maximum wealth |

## State Machine

```
ASSESS ──→ PLAN ──→ EXECUTE ──→ MONITOR ──→ REBALANCE
  ↑                                              │
  └────────────── next cycle ────────────────────┘
  ↑           │
  │  thesis   │
  │  invalid  │
  ←───────────┘
```

### Phase Definitions

| Phase | Entry Condition | What Happens | Exit Condition | Detailed Flow |
|-------|----------------|--------------|----------------|---------------|
| ASSESS | First time, annual review, or life change | Net worth, cash flow, risk profile, portfolio health | Complete financial picture documented | `phases/assess.md` |
| PLAN | Assessment complete, goals need (re)setting | Goal setting, asset allocation, investment thesis | Goals specific and time-bound, allocation matches risk profile | `phases/plan.md` |
| EXECUTE | Plan exists, capital ready to deploy | Automate contributions, execute trades, fund reserves | Automation active, portfolio aligned with plan | `phases/execute.md` |
| MONITOR | Portfolio deployed, regular cadence | Track metrics, review fundamentals, compare benchmarks | Dashboard updated, flags raised if needed | `phases/monitor.md` |
| REBALANCE | Drift detected, life change, or annual review | Adjust positions, update strategy, harvest losses | Portfolio within target range, plan updated | `phases/rebalance.md` |

### Phase Transition Rules

- **Forward**: current phase exit condition met → enter next phase
- **PLAN → ASSESS (forced retreat)**: investment thesis doesn't survive scrutiny → go back and reassess constraints and knowledge
- **MONITOR → REBALANCE**: drift exceeds threshold or fundamental change detected → rebalance
- **MONITOR → PLAN**: major life change invalidates current plan → redesign
- **Cycle**: REBALANCE complete → MONITOR continues on regular cadence

## Operating Modes

| Mode | When to Use | Behavior |
|------|-------------|----------|
| **ACCUMULATION** | Building wealth, pre-FI | Maximize savings rate, invest consistently, focus on long-term compounding |
| **PRESERVATION** | Near FI or protecting gains | Reduce risk, ensure liquidity, focus on capital preservation |
| **DISTRIBUTION** | Post-FI, drawing down | Withdrawal strategy, tax optimization, sustainability focus |
| **CRISIS** | Market panic or personal emergency | Assess damage calmly, avoid forced selling, look for bargains if liquid |

Default mode: **ACCUMULATION**. Switching requires explicit declaration.

## Prime Directives

1. Never invest in what you don't understand — if you can't explain the business model, pass
2. Never borrow to invest — leverage creates forced selling and irrational behavior
3. Never let Mr. Market's mood dictate your decisions — price movements are opportunities, not verdicts
4. Every sell decision must survive the question: "Would I buy this today at this price?"
5. The Stop Doing List is more important than the To Do List

## Completion Status Protocol

Every phase reports one of:

| Status | Meaning |
|--------|---------|
| `DONE` | All steps complete, verification passed |
| `DONE_WITH_CONCERNS` | Complete but with recorded concerns (e.g., concentration risk noted) |
| `BLOCKED` | Cannot proceed — explain the blocker |
| `NEEDS_CONTEXT` | Missing information — list what's needed |
| `ITERATE` | Need to retreat to a previous phase |
