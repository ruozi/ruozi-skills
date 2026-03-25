# REFACTOR Phase

> Goal: Improve code structure without changing behavior. The safety net is tests — if you don't have tests, write them first.

#### Entry Condition

Code works correctly but structure needs improvement. Triggered by:
- Code smell identified during IMPLEMENT
- Hotspot file flagged during retrospective (high churn indicator)
- Tech debt item scheduled for resolution
- Preparing code for a new feature (make the change easy, then make the easy change)

#### Prerequisite: Test Coverage

**Before refactoring anything, verify that the code under change has adequate test coverage.**

- If tests exist and pass → proceed with refactoring
- If tests are insufficient → write characterization tests first (tests that capture current behavior, even if you don't fully understand it)
- **No tests = no refactoring.** Without tests, you cannot verify that behavior is preserved. Write tests first, then refactor

#### Core Workflow

1. **Identify the smell** — Be specific about what's wrong:
   - Duplicate code (DRY violation)
   - Long function (> 30 lines is a signal, not a hard rule)
   - Deep nesting (> 3 levels)
   - God class / God function (too many responsibilities)
   - Unclear naming
   - Inappropriate coupling between modules
   - Feature envy (a function that uses another module's data more than its own)

2. **Define the target** — What does "better" look like?
   - Specific, measurable improvement (e.g., "extract authentication logic into its own module with a defined interface")
   - Not vague aspirations ("make it cleaner")

3. **Small steps, always green** — Refactor in tiny increments:
   - Each step: make one change, run tests, commit if green
   - If tests fail after a step, revert and try a smaller step
   - Never be more than one undo away from a working state

4. **Common refactoring patterns:**
   - **Extract function** — pull a block of code into a named function
   - **Extract module** — pull related functions into their own file
   - **Rename** — improve names to better communicate intent
   - **Inline** — remove unnecessary indirection (the opposite of extract)
   - **Replace conditional with polymorphism** — when type-based switching dominates
   - **Simplify interface** — reduce parameters, group related parameters

5. **Verify** — After all refactoring is complete:
   - Full test suite passes
   - Behavior is identical (no observable change from the user's perspective)
   - Code is measurably better against the target defined in step 2

#### Rules

- **Behavior must not change** — refactoring changes structure, not behavior. If you're changing what the code does, that's a feature or a fix, not a refactor
- **Don't mix refactoring with features** — refactor in separate commits from feature work. Never in the same commit
- **Don't refactor without a reason** — "it could be cleaner" without a specific benefit is not justification. Refactor when the current structure actively hinders understanding, modification, or testing
- **Stop when it's good enough** — perfectionism is the enemy of progress. The code doesn't need to be beautiful; it needs to be clear and maintainable

#### Exit Condition

- All existing tests still pass (zero regressions)
- Code structure improved against the specific target
- No behavior change (verified by tests)
- Refactoring commits are separate from any feature or fix commits
- If the refactoring revealed a deeper issue, it's flagged for ARCHITECT review
