# ARCHITECT Phase

> Goal: Design the technical solution — data structures, interfaces, module boundaries, algorithm selection. The design must be the unique best approach given the constraints.

#### Entry Condition

Problem is understood (ASSESS complete), solution design needed.

#### Design Decision Priority

When trade-offs are necessary, follow this priority (high to low):

1. **Correctness** — it must work correctly. No trade-off justifies incorrect behavior
2. **Clarity** — the solution must be understandable by the next developer
3. **Maintainability** — the solution must be easy to modify, test, and debug
4. **Performance** — only optimize after correctness, clarity, and maintainability are secured. Premature optimization is the root of all evil

When priorities conflict, higher beats lower. Never sacrifice correctness for performance. Never sacrifice clarity for cleverness.

#### Core Workflow

1. **Search before designing** — Apply the Prior Art axiom. Check:
   - Does a standard pattern solve this? (Tried and True)
   - What's the current best practice? (New and Popular)
   - Is there a novel insight from the problem constraints? (First Principles)

2. **Define interfaces first** — Before any implementation detail:
   - What are the inputs and outputs?
   - What are the module boundaries?
   - What data structures cross those boundaries?
   - What error conditions must be handled?

3. **Design data structures** — Data structures drive algorithms. Get the data model right and the code often writes itself. Get it wrong and no amount of clever algorithms will save you.

4. **Consider failure modes** — For every component:
   - What happens when it fails?
   - Is the failure detectable?
   - Is recovery possible?
   - What does the user see?

5. **Evaluate alternatives** — If multiple approaches seem viable:
   - List the specific criteria that differentiate them
   - If you can't determine a winner, the constraints are insufficient → **retreat to ASSESS**
   - If one is clearly better, document why and proceed

6. **Document the design** — The design is not in your head. Write it down:
   - Architecture overview (modules, boundaries, data flow)
   - Key design decisions with rationale ("we chose X because Y; we rejected Z because W")
   - Interface contracts (input types, output types, error types)
   - Test strategy (what to test, at what level)

#### YAGNI Principle

Design only for current requirements. Actively remove all "might need later" provisions:
- No unused interfaces
- No unnecessary abstraction layers
- No configuration for hypothetical future needs
- If it's not in the requirements, it's not in the design

#### Uniqueness Check

Borrowed from FL Playbook's Solution Uniqueness Definition: if the constraints are fully specified, the best approach is unique. If you find yourself choosing between options, the problem isn't well-enough understood.

- **Design is unique** → proceed to IMPLEMENT
- **Multiple viable designs, can't determine winner** → retreat to ASSESS, gather more constraints

#### Exit Condition

- Design is unique — one clear best approach given all known constraints
- Interfaces and data structures are defined
- Failure modes are considered
- Design is documented (not just in your head)
- Test strategy is outlined
