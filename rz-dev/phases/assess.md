# ASSESS Phase

> Goal: Understand the problem space and codebase before touching anything. Never modify what you don't understand.

#### Entry Condition

New task, unfamiliar codebase, or returning to a codebase after time away.

#### Core Workflow

1. **Read the problem statement** — What is being asked? What is the expected outcome? What are the constraints? If the problem statement is vague, challenge it (anti-sycophancy protocol: force specificity)

2. **Map the codebase** — For unfamiliar code:
   - Directory structure and organization pattern
   - Entry points (where does execution start?)
   - Key modules and their responsibilities
   - Data flow (how does data move through the system?)
   - Dependencies (internal and external)
   - Test suite (what's tested, what's not?)

3. **Identify constraints** — What can't change? What must be preserved?
   - Backward compatibility requirements
   - Performance budgets
   - Security requirements
   - Dependencies on external systems
   - Team conventions and coding standards

4. **Define success criteria** — Before any design or code, answer: "When this is done, what must be true?" Use the Goal-Backward approach from rz-product-dev's axioms. Success criteria are verifiable statements, not vague descriptions.

5. **Document findings** — Write down what you learned. This is not optional overhead — it's the input for the ARCHITECT phase and the safety net for when you forget.

#### Interaction Rules

- **One question at a time** — Don't overwhelm. Ask one clarifying question, wait for the answer, then ask the next
- **Challenge vagueness** — "Make it faster" is not a problem statement. "Reduce API response time from 800ms to under 200ms for the /search endpoint" is
- **Distinguish assumption from fact** — If the user says "the database is slow," ask: "What query? What's the current latency? How did you measure it?"

#### Exit Condition

- Problem is clearly defined with verifiable success criteria
- Relevant codebase areas are read and understood (not skimmed)
- Constraints are documented
- You can explain, in your own words, what needs to change and why
