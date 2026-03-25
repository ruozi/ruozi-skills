# LEARN Phase

> Goal: Deliberately invest in skill growth. Knowledge compounds — today's learning pays dividends across every future project.

#### Entry Condition

Dedicated skill development time. This phase operates independently of the task cycle (ASSESS → ARCHITECT → IMPLEMENT) and can run at any time.

Triggers:
- Scheduled learning time (weekly/monthly)
- Knowledge gap discovered during a task ("I don't know enough about X to design this properly")
- New technology or pattern needs evaluation
- Post-retrospective: identified skill area needing investment

#### Core Workflow

1. **Identify the learning target** — Be specific:
   - BAD: "Learn about databases"
   - GOOD: "Understand PostgreSQL query planning well enough to diagnose slow queries using EXPLAIN ANALYZE"
   - The target should connect to a real need (current project gap, upcoming project requirement, recurring pain point)

2. **Search existing knowledge** — Before learning from scratch:
   - Official documentation (always the first stop)
   - Source code (the ultimate truth — docs can be wrong, code can't lie)
   - Peer-reviewed content (conference talks, technical papers, reputable blogs)
   - Community knowledge (Stack Overflow, GitHub discussions — but verify, don't trust blindly)

3. **Build to learn** — Reading without doing is not learning:
   - Build a minimal prototype that exercises the concept
   - Break it deliberately — understanding failure modes is where real learning happens
   - Measure it — if performance is the concern, benchmark it
   - Teach it — explain what you learned (to a colleague, in writing, or to a rubber duck)

4. **Catalog** — Record what you learned for future reference:
   - Key concepts and mental models
   - Pitfalls and gotchas discovered
   - Code snippets and patterns worth reusing
   - Links to the best resources found
   - Personal knowledge base entry (not just bookmarks — write your own summary)

5. **Connect** — Link new knowledge to existing skills:
   - How does this change how you'd approach problem X?
   - What does this invalidate from your previous understanding?
   - What adjacent topics should you explore next?

#### Learning Dimensions

| Dimension | Description | Examples |
|-----------|-------------|---------|
| **Depth** | Master your primary stack to the point where you can debug framework internals | Read framework source code, understand runtime behavior, debug without documentation |
| **Breadth** | Learn enough about adjacent domains to collaborate effectively | Ops basics for a frontend dev, SQL fundamentals for a mobile dev, security essentials for everyone |
| **Craft** | Improve the meta-skills of engineering | Debugging methodology, code review skills, technical writing, estimation, system design |
| **Tools** | Know your editor, terminal, debugger, VCS deeply | Keyboard shortcuts, custom scripts, debugger features, git internals |

#### Interaction Rules

- **Demand specificity** — "I want to learn React" is too vague. "I want to understand React's reconciliation algorithm well enough to diagnose re-render performance issues" is a learning target
- **Challenge tutorial addiction** — Completing tutorials is not learning. Building something with the concepts is. "Have you built anything with this yet?" should be the follow-up to every tutorial
- **Connect to practice** — Every learning target should connect to a real project or upcoming need. Learning for its own sake is fine as a hobby, but for professional growth, it needs application

#### Exit Condition

- At least one new concept or tool explored with depth (not just surface-level reading)
- Prototype or hands-on practice completed (not just reading/watching)
- Notes captured in personal knowledge base for future reference
- Clear connection identified to current or upcoming work
- Next learning priority identified (feed the cycle)
