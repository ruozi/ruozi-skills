# Axiom System

> The following axioms govern all phases and all commands of the rz-dev skill.

## Philosophy

Software engineering is not typing. It is the disciplined application of evidence, design, and craft to build systems that work reliably and can be understood by others. The marginal cost of doing it right is nearly zero in the age of AI-assisted development. Don't cut the last 20%.

## 1. Understand Before Touching (Assessment Axiom)

Before modifying any code, you must understand it. This means reading the relevant files, tracing the data flow, and mapping the dependencies. "I'll figure it out as I go" is not a strategy — it's how you introduce regressions.

Three levels of understanding:
1. **Surface** — you can describe what the code does (reading)
2. **Structural** — you can explain why it's organized this way (architecture)
3. **Behavioral** — you can predict what will happen if you change it (mental model)

Level 1 is the minimum before any modification. Level 3 is required for non-trivial changes.

**Prohibited:**
- Modifying code you haven't read — "it's probably fine" is how regressions happen
- Relying on file names or function names to assume behavior — read the implementation
- Starting to code before understanding the surrounding system — one module's change can cascade
- Skipping dependency mapping — "I only changed one file" but three others import it

## 2. Evidence-Based Debugging (Debugging Axiom)

Never guess. Every debugging session follows a strict protocol:

1. **Reproduce** — make the bug happen reliably. If you can't reproduce it, you can't fix it
2. **Hypothesize** — form a specific, falsifiable hypothesis about the root cause
3. **Gather evidence** — logs, traces, breakpoints, print statements — prove or disprove your hypothesis
4. **Fix** — write the minimal fix that addresses the root cause
5. **Verify** — confirm the fix works AND didn't break anything else
6. **Prevent** — add a regression test that would have caught this bug

**Prohibited:**
- "Let me try this and see if it works" without a hypothesis — that's random mutation, not debugging
- Fixing what you think the problem is without reproducing it first — you might be fixing the wrong thing
- Declaring "fixed" without running the verification — until the test passes, it's not fixed
- Same fix attempted three times with minor variations — if it didn't work twice, your hypothesis is wrong. Step back
- Removing error handling or suppressing exceptions to make a test pass — that's hiding the bug, not fixing it

## 3. Search Before Build (Prior Art Axiom)

The first instinct should be "has someone solved this?" not "let me design from scratch." The cost of searching is nearly zero; the cost of reinventing is a worse wheel.

Three-layer knowledge framework:
1. **Tried and True** — standard patterns, mature libraries. You may already know, but occasionally questioning the obvious is where insights come from
2. **New and Popular** — current best practices, community trends. But be cautious — the crowd can be wrong. Search results are input, not answers
3. **First Principles** — original insights derived from the problem itself. Most valuable. The best solutions avoid reinventing (Layer 1) while delivering innovation (Layer 3)

**Prohibited:**
- Encountering an unfamiliar domain and jumping straight to implementation — search first, understand the landscape
- Finding one solution and adopting it immediately — search results are input, not answers. Evaluate against your specific constraints
- Skipping search because "I know how to do this" — your knowledge may be outdated. The cost of checking is zero
- Adding a dependency without verifying it solves your actual problem — read the docs, check the issues, verify compatibility

## 4. TDD as Design Tool (Test-Driven Axiom)

Tests are not a chore after the fact. Tests express design intent — "what must be true." Writing tests first forces you to think about interfaces, edge cases, and error handling before you write a single line of production code.

The TDD cycle:
1. **RED** — write a test that describes the desired behavior. Run it. It must fail
2. **GREEN** — write the minimum production code to make the test pass
3. **REFACTOR** — clean up both test and production code while keeping all tests green

**Prohibited:**
- Writing production code without a failing test — if you wrote code first, delete it and start with the test
- Writing tests that don't test meaningful behavior — `expect(true).toBe(true)` is not a test
- Skipping the RED step — if your test passes before you write production code, either the test is wrong or the feature already exists
- Writing tests only for the happy path — error paths, edge cases, and boundary conditions need tests too
- Treating tests as optional or "nice to have" — untested code is unverified code, and unverified code is a liability

## 5. Atomic Changes (Commit Discipline Axiom)

Every commit is one logical change. Every commit leaves the system in a working state. This is not pedantry — it's what makes `git bisect` work, code review possible, and rollbacks safe.

Rules:
1. **One commit = one change** — a bug fix is one commit. A feature is one commit (or a logical sequence). A refactor is one commit. Never mix them
2. **Working state** — after every commit, the system builds and tests pass. No "WIP" commits on shared branches
3. **Meaningful messages** — the commit message explains why, not what. The diff shows what

**Prohibited:**
- "Fix stuff" as a commit message — if you can't describe it, you don't understand it
- Commits that mix feature code, bug fixes, and formatting changes — split them
- Commits that break the build — every commit must be independently viable
- Giant commits with 500+ lines changed across 20 files — break them into logical steps

## 6. Security at Boundaries (Security Axiom)

The system boundary is where trust ends. Everything crossing that boundary — user input, API responses, file contents, environment variables, LLM output — must be validated before use.

Trust zones:
1. **External input** (user forms, API calls, file uploads) — never trusted, always validated
2. **Third-party services** (APIs, databases, LLM responses) — validated for schema and content
3. **Internal code** — trusted within the module boundary, validated at module interfaces for critical paths

**Prohibited:**
- String-concatenating user input into SQL queries — use parameterized queries, always
- Rendering user input as HTML without escaping — XSS is not a theoretical risk
- Trusting API responses without schema validation — external services can return anything
- Hardcoding secrets in source code — use environment variables or secret management
- Using `eval()` or equivalent with external input — this is code injection
- Assuming internal-only APIs won't be accessed externally — if it's reachable, it will be reached

## 7. Root Cause, Not Symptoms (Root Cause Axiom)

Patching symptoms is not efficiency — it's failure. It creates tech debt and hides systemic issues.

Protocol:
1. **Locate before fixing** — find the root cause before proposing a solution
2. **Three-strike rule** — same problem, three failed fix attempts → stop, question your assumptions or the architecture. Do not attempt a fourth fix of the same kind

**Prohibited:**
- Seeing a symptom and immediately patching it — "fix it now, understand later" is how tech debt accumulates
- Attempting the same category of fix repeatedly — three failures means the direction is wrong, not the execution
- "It's fixed but I don't know why" — an unexplained fix is not a fix, it's a time bomb that happens to work
- Suppressing error messages instead of fixing the underlying cause — the error is telling you something

## 8. Clarity Over Cleverness (Readability Axiom)

Code is read far more than it is written. Every line should be optimized for the next reader — who might be you in six months, and you will have forgotten everything.

Principles:
1. **Names are documentation** — variable names, function names, class names should make the code self-explanatory
2. **Structure communicates intent** — code organization, module boundaries, and file structure should tell a story
3. **Comments explain why, not what** — if the code needs a comment to explain what it does, rewrite the code. Comments explain business reasons, non-obvious constraints, and historical context

**Prohibited:**
- Clever one-liners that require mental parsing — unpack them into readable steps
- Abbreviations and single-letter variables outside of tight loops — `usr_acct_mgr` is not a name, it's a cipher
- Deeply nested conditionals (> 3 levels) — extract functions or use early returns
- Magic numbers without named constants — `if (retries > 3)` should be `if (retries > MAX_RETRY_ATTEMPTS)`
- "It's obvious" as justification for unclear code — obvious to whom? When? After how much context?

## 9. Automate the Repetitive (Automation Axiom)

If you do it three times, automate it. Humans are terrible at consistency; machines are great at it. CI/CD, linting, formatting, testing, deployment — every manual step is a step that can be forgotten or done wrong.

Priorities:
1. **Tests** — automated test suite that runs on every commit
2. **Formatting** — auto-formatter on save, no debates about style
3. **Linting** — catch common mistakes before code review
4. **Deployment** — one command (or zero commands) to deploy
5. **Environment setup** — new developer should be productive within an hour

**Prohibited:**
- "We test manually before each release" — manual testing doesn't scale and is never comprehensive
- "Just remember to run the linter before committing" — if it's not automated, it won't happen consistently
- Deployment procedures that require more than one step — if it's complex, script it
- Environment setup that requires a multi-page wiki — if it's that complicated, automate it

## 10. Compound Learning (Growth Axiom)

Software engineering is a field where knowledge compounds. Today's investment in learning pays dividends across every future project. Deliberate, consistent learning beats sporadic cramming.

Framework:
1. **Depth** — master your primary stack to the level where you can debug framework internals
2. **Breadth** — learn enough about adjacent domains (ops, security, data, design) to collaborate effectively
3. **Teaching** — explain what you learn. Teaching forces clarity and reveals gaps in your understanding
4. **Cataloging** — maintain a personal knowledge base. What you learned but didn't record, you'll learn again

**Prohibited:**
- "I don't have time to learn" — this is a debt that compounds against you
- Learning only when something breaks — reactive learning is expensive learning
- Tutorial-only learning without building — understanding requires doing, not just reading
- Hoarding knowledge — sharing knowledge multiplies it, hoarding depreciates it
