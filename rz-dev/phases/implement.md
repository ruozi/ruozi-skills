# IMPLEMENT Phase

> Goal: Write code using TDD — tests express design intent, production code makes them pass. Atomic commits, working state at every step.

#### Entry Condition

Design exists (ARCHITECT complete), ready to write code.

#### Core Workflow

1. **Load the design** — Read the architecture document, interface contracts, and test strategy from ARCHITECT phase. The design is the blueprint; implementation follows it.

2. **Write tests first** — Transform the design's interface contracts and success criteria into executable tests. Tests answer "what must be true" — they are the formal expression of design intent.

3. **TDD Cycle** — For each unit of functionality:
   - **RED** — Write a test that describes the desired behavior. Run it. It must fail. If it passes, either the test is wrong or the feature already exists
   - **GREEN** — Write the minimum production code to make the test pass. No more, no less. Do not write code that isn't demanded by a failing test
   - **REFACTOR** — Clean up both test and production code while keeping all tests green. Improve names, extract functions, simplify logic — but change no behavior

4. **Atomic commits** — Each logical change gets its own commit:
   - One test + its implementation = one commit
   - One refactor = one commit
   - One bug fix = one commit
   - Commit message format: `{type}({scope}): {what and why}`
   - Types: `feat`, `fix`, `refactor`, `test`, `docs`, `chore`

5. **Integration** — After individual units work:
   - Run the full test suite — ensure no regressions
   - Test module boundaries — do modules communicate correctly?
   - Test error paths — do failures propagate and recover correctly?

#### TDD Principles

> Tests are not overhead. Tests are the design made executable. "No failing test, no production code" is the iron rule.

- **Tests first, always** — wrote production code first? Delete it, write the test, watch it fail, then rewrite the production code
- **Meaningful tests only** — every test must verify specific business behavior. `assert(true)` is not a test
- **Test error paths** — happy paths are easy. Error handling, boundary conditions, and failure modes need tests too
- **Tests are documentation** — a new developer should be able to read the test suite and understand what the system does

#### Interaction Rules

- **Review code as you go** — Don't wait until the end. Review each logical unit after implementing it
- **Bugs found during implementation** → switch to DEBUG phase, fix with evidence, then return
- **Design was wrong** → Don't hack around it. Flag it, retreat to ARCHITECT (or ASSESS if the problem is deeper)
- **Scope creep** — In HOLD SCOPE mode (default), implement only what the design specifies. "While I'm here I might as well..." is scope creep

#### Exit Condition

- All tests pass (both new and existing)
- Code follows project conventions (style, linting, formatting)
- No known security vulnerabilities introduced (Security axiom check)
- Each logical change has an atomic commit with meaningful message
- Code is ready for review (either self-review or peer review)
