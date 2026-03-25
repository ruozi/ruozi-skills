# Feedback Mechanism

> The rz-finance methodology needs continuous iteration. Market conditions evolve, new insights emerge, and personal circumstances change.

## Contributor Mode (Methodology Feedback)

At the end of each phase, self-evaluate: Was the workflow smooth? Did the axioms apply? Were there situations the checklist didn't cover?

**Self-evaluation score: 0-10**
- 10 = process fully applicable, zero friction
- < 10 = room for improvement

**When score < 10 AND the issue is with rz-finance methodology itself**, automatically write a Field Report:

```
.rz-finance/contributor-logs/{date}.md
```

### Field Report Format

```markdown
## {date} — {phase name}

- **Doing what:** {user/agent goal}
- **What happened:** {actual issue encountered}
- **Score:** {0-10} — {scoring rationale}
- **Reproduction steps:** {how to reproduce the issue}
- **What would make it a 10:** {specific improvement suggestion}
- **rz-finance version:** {current version}
- **Skill:** rz-finance
```

**Calibration examples:**
- Worth recording: Long-term investing checklist doesn't address private market investments (angel investing, venture)
- Worth recording: Moat analysis framework lacks guidance for platform businesses with multi-sided markets
- NOT worth recording: User's stock pick didn't work out (that's a user decision, not a methodology issue)

### Investment Journal

Beyond methodology feedback, maintain an investment journal for every significant decision:

```
.rz-finance/journal/{date}-{ticker-or-topic}.md
```

**Journal entry format:**
```markdown
## {date} — {action: BUY/SELL/HOLD/PASS} — {ticker or topic}

- **Thesis:** {why you're making this decision}
- **Checklist result:** {which steps passed/failed}
- **Key assumptions:** {what must be true for this to work}
- **Bear case:** {the strongest argument against}
- **Position size:** {% of portfolio}
- **Review date:** {when to re-evaluate}
```

This journal is permanent. Never delete entries. Review old entries during MONITOR phase to learn from past decisions — both good and bad.

### Feedback Flywheel

```
Use rz-finance workflow
    ↓
Every decision logged in investment journal
    ↓
Phase end: self-evaluate methodology
    ↓
< 10 + methodology issue → write Field Report
    ↓
Periodic review: compare thesis vs. outcome for past decisions
    ↓
Update methodology based on learnings
```
