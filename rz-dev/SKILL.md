---
name: rz-dev
description: Software engineering craft — architecture, implementation, debugging, refactoring. Structured methodology for writing reliable, maintainable software. Input /rz-dev to start, optionally specify a phase (assess / architect / implement / debug / refactor / learn).
argument-hint: Optional phase: assess / architect / implement / debug / refactor / learn
allowed-tools: Read, Grep, Write, Edit, Glob, Bash(*), Agent
---

# Skill: Software Engineering (rz-dev)

> Master the craft of building software. From understanding a problem to shipping a solution — with evidence at every step and no guessing allowed.

## Command List

| Command | Purpose |
|---------|---------|
| `rz-dev` | Main entry: assess current technical context → determine phase → guide next step |
| `rz-dev:assess` | Understand before touching: read code, map dependencies, identify constraints |
| `rz-dev:architect` | Design the technical solution: data structures, interfaces, module boundaries |
| `rz-dev:implement` | Write code using TDD: RED → GREEN → REFACTOR, atomic commits |
| `rz-dev:debug` | Structured debugging: reproduce → hypothesize → gather evidence → fix → test |
| `rz-dev:refactor` | Improve code structure without changing behavior, with safety net of tests |
| `rz-dev:learn` | Deliberate practice: study, prototype, teach, catalog knowledge |

Each command is an independent atomic command. Can be invoked standalone or chained by the `rz-dev` main entry in state machine order.

### Main Entry Logic

```
rz-dev (main entry)
    │
    ├── Is there a specific task/problem/codebase to work on?
    │     ├── New task → ASSESS (understand before touching)
    │     ├── Architecture decision needed → ARCHITECT
    │     ├── Design exists, ready to code → IMPLEMENT
    │     ├── Something is broken → DEBUG
    │     ├── Code works but needs improvement → REFACTOR
    │     └── No task, skill development mode → LEARN
    │
    └── Determine current phase → guide user to next step
```

## Axioms & Principles

This skill is governed by 10 axioms + anti-sycophancy interaction protocol + feedback mechanism. All phases, all commands must comply.

**Load full definitions:**
- **Axiom System (10 axioms)** → read `principles/axioms.md`
- **Anti-Sycophancy Interaction Protocol** → read `principles/anti-sycophancy.md`
- **Feedback Mechanism (Contributor Mode)** → read `principles/feedback.md`

**Axiom Index (full definitions in `principles/axioms.md`):**

| # | Axiom | One-liner |
|---|-------|-----------|
| 1 | Understand Before Touching | Read the code, map the system, then act. Never modify what you don't understand |
| 2 | Evidence-Based Debugging | Reproduce → hypothesize → gather evidence → fix. No guessing |
| 3 | Search Before Build | Check if it exists before creating it. The best code is the code you don't write |
| 4 | TDD as Design Tool | Tests express design intent — "what must be true." RED → GREEN → REFACTOR |
| 5 | Atomic Changes | One commit = one logical change. Every commit leaves the system working |
| 6 | Security at Boundaries | Validate all external input. Trust nothing from outside the system boundary |
| 7 | Root Cause, Not Symptoms | Fix the underlying cause. Three failed attempts = question your assumptions |
| 8 | Clarity Over Cleverness | Optimize for the next reader. If it needs a comment, consider rewriting |
| 9 | Automate the Repetitive | If you do it three times, automate it. Machines are better at consistency |
| 10 | Compound Learning | Invest consistently in skill growth. Knowledge compounds like interest |

## State Machine

```
ASSESS ──→ ARCHITECT ──→ IMPLEMENT ──→ (task complete)
  ↑             │              │
  │    design   │              │
  │  not unique │    bug       │
  ←─────────────┘    found     │
  ↑                    ↓       │
  │              ←── DEBUG ────┘
  ↑                            │
  │         code works but     │
  │         needs cleanup      │
  │              ↓             │
  ←────── REFACTOR ────────────┘
  ↑                            │
  └──────── next task ─────────┘

  LEARN (independent cycle, can run anytime)
```

### Phase Definitions

| Phase | Entry Condition | What Happens | Exit Condition | Detailed Flow |
|-------|----------------|--------------|----------------|---------------|
| ASSESS | New task or unfamiliar codebase | Read code, map dependencies, identify constraints, understand the problem | Problem and codebase fully understood, constraints documented | `phases/assess.md` |
| ARCHITECT | Problem understood, solution design needed | Data structures, interfaces, module boundaries, algorithm selection | Design is unique (one best approach given constraints), documented | `phases/architect.md` |
| IMPLEMENT | Design exists, ready to code | TDD cycle: write test → run (RED) → implement → run (GREEN) → refactor | All tests pass, code reviewed, atomic commits made | `phases/implement.md` |
| DEBUG | Something is broken or behaving unexpectedly | Reproduce → hypothesize → gather evidence → fix → add regression test | Root cause identified, fix verified with test, regression test committed | `phases/debug.md` |
| REFACTOR | Code works but structure needs improvement | Improve design without changing behavior, under test safety net | All existing tests still pass, code cleaner, no behavior change | `phases/refactor.md` |
| LEARN | Skill development time (independent of task cycle) | Study, prototype, teach, catalog | At least one new concept explored, notes captured | `phases/learn.md` |

### Phase Transition Rules

- **Forward**: current phase exit condition met → enter next phase
- **ARCHITECT → ASSESS (forced retreat)**: if design reveals multiple valid approaches with no clear winner, retreat to ASSESS to gather more constraints. Do not pick one and hope — the ambiguity means you don't understand the problem well enough
- **IMPLEMENT → DEBUG**: bug discovered during implementation → switch to DEBUG, fix with evidence, then return to IMPLEMENT
- **IMPLEMENT → REFACTOR**: implementation complete but code structure needs cleanup → REFACTOR under test safety net
- **DEBUG → ASSESS**: three failed fix attempts → retreat to ASSESS and re-examine assumptions
- **Iteration**: task complete → back to ASSESS for next task

## Operating Modes

| Mode | When to Use | Behavior |
|------|-------------|----------|
| **SCOPE EXPANSION** | Exploring new architecture, evaluating technologies | Challenge assumptions, explore alternatives, push boundaries |
| **SELECTIVE EXPANSION** | Design review, architecture decision records | Maintain baseline, present extension opportunities one at a time |
| **HOLD SCOPE** | Implementation phase (default) | Maximum strictness — only what's planned, catch edge cases |
| **SCOPE REDUCTION** | Hotfix, time pressure, critical bug | Minimum viable fix, defer improvements, document what was skipped |

Default mode: **HOLD SCOPE**. Switching requires explicit declaration.

## Relationship to rz-product-dev

rz-dev is the **technical execution layer** that supports rz-product-dev. While product-dev governs the lifecycle (REQUIRE → RELEASE), rz-dev governs the craft within the DEV and TEST phases. When working within rz-product-dev:

- rz-product-dev:dev invokes rz-dev:implement (TDD cycle)
- rz-product-dev:test may invoke rz-dev:debug (for fixing discovered issues)
- Architecture decisions in rz-product-dev:solution may invoke rz-dev:architect

## Prime Directives

1. Never modify code you haven't read and understood first
2. Every fix must include a test that would have caught the bug
3. Evidence before claims — run the code, see the output, then speak
4. Three failed attempts at the same approach = stop and rethink
5. Leave the codebase better than you found it — but only within scope

## Completion Status Protocol

Every phase reports one of:

| Status | Meaning |
|--------|---------|
| `DONE` | All steps complete, verification passed |
| `DONE_WITH_CONCERNS` | Complete but with recorded concerns (e.g., tech debt noted) |
| `BLOCKED` | Cannot proceed — explain the blocker |
| `NEEDS_CONTEXT` | Missing information — list what's needed |
| `ITERATE` | Need to retreat to a previous phase |
