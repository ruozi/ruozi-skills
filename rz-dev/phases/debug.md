# DEBUG Phase

> Goal: Find and fix the root cause of a bug using evidence, not intuition. Every fix includes a regression test.

#### Entry Condition

Something is broken or behaving unexpectedly. Can be triggered from:
- IMPLEMENT phase (bug discovered during development)
- Production incident
- Test failure
- User report

#### Core Workflow

1. **Reproduce** — Make the bug happen reliably.
   - Define the exact steps to trigger the bug
   - Identify the expected behavior vs. actual behavior
   - If the bug is intermittent, gather enough observations to identify a pattern
   - **Cannot reproduce → cannot fix.** Gather more data before proceeding

2. **Hypothesize** — Form a specific, falsifiable hypothesis.
   - "I believe the bug occurs because [specific mechanism] in [specific location]"
   - A good hypothesis predicts: "If I do X, Y will happen because of Z"
   - A bad hypothesis: "something is wrong somewhere"

3. **Gather evidence** — Prove or disprove the hypothesis.
   - **Logs** — what do the logs say at the time of the failure?
   - **Traces** — what code path was executed?
   - **Breakpoints** — what are the variable values at the point of failure?
   - **Bisect** — `git bisect` to find the exact commit that introduced the bug
   - **Simplify** — can you reproduce in a minimal test case?

4. **Diagnose** — Root cause identified.
   - Explain the chain of causation: input → processing → failure point → symptom
   - Distinguish root cause from symptoms. Fix the cause, not the symptom
   - If your hypothesis was wrong, form a new one and return to step 3

5. **Fix** — Write the minimal fix.
   - Fix the root cause, not the symptom
   - Minimal change — don't refactor surrounding code, don't add features, don't "improve" unrelated things
   - The fix should be reviewable in isolation

6. **Verify** — Prove the fix works.
   - Run the reproduction steps — the bug must no longer occur
   - Run the full test suite — no regressions introduced
   - If the fix changes behavior, verify the new behavior is correct

7. **Prevent** — Add a regression test.
   - Write a test that reproduces the exact bug (would have failed before the fix)
   - Test must pass with the fix applied
   - Include attribution comment:
     ```
     // Regression: {description of what broke}
     // Fixed: {date}, root cause: {brief explanation}
     ```

#### Three-Strike Rule

Same bug, three failed fix attempts → **stop**. Do not attempt a fourth fix of the same kind.

Instead:
- Re-examine your assumptions about the root cause
- Consider whether the bug is a symptom of a deeper architectural issue
- Retreat to ASSESS and re-evaluate the system's design
- If still stuck, escalate (ask for help, pair with someone, take a break)

#### Severity Classification

| Severity | Definition | Response |
|----------|-----------|----------|
| CRITICAL | Crash, data loss, security vulnerability | Drop everything, fix immediately |
| HIGH | Feature broken, workflow blocked | Fix before any new work |
| MEDIUM | Feature works but degraded experience | Schedule fix, don't ignore |
| LOW | Cosmetic, minor annoyance | Log it, fix when convenient |

#### Exit Condition

- Root cause identified and documented
- Minimal fix applied and verified
- Regression test committed that would have caught this bug
- Full test suite passes (no regressions)
- If the bug revealed a systemic issue, it's flagged for ARCHITECT review
