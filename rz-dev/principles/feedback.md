# Feedback Mechanism

> The rz-dev methodology itself needs continuous iteration. Feedback is the fuel for iteration.

## Contributor Mode (Methodology Feedback)

At the end of each phase, the agent self-evaluates: Was the workflow smooth? Were there situations outside the rules? Were axioms or processes not applicable?

**Self-evaluation score: 0-10**
- 10 = process fully applicable, zero friction
- < 10 = room for improvement

**When score < 10 AND the issue is with rz-dev methodology itself (not the user's project)**, automatically write a Field Report:

```
.rz-dev/contributor-logs/{date}.md
```

### Initialization Requirement (enforced on first use)

The first time the skill runs in a project, ensure `.rz-dev/` directory is git-tracked:

1. **Create directory structure**:
   ```bash
   mkdir -p .rz-dev/contributor-logs
   touch .rz-dev/contributor-logs/.gitkeep
   ```

2. **Check `.gitignore`**: If `.gitignore` has rules that would block `.rz-dev/` (like `.*` or `.rz-*`), add explicit unblock:
   ```
   # rz-dev feedback logs must be tracked
   !.rz-dev/
   ```

3. **Commit confirmation**: Commit `.rz-dev/` directory and `.gitignore` changes together, ensuring feedback logs are version-controlled from day one

**This directory must be committed to the repository, not blocked.** Feedback logs are the fuel for methodology iteration — blocking them cuts the feedback loop.

### Field Report Format

```markdown
## {date} — {phase name}

- **Doing what:** {user/agent goal}
- **What happened:** {actual issue encountered}
- **Score:** {0-10} — {scoring rationale}
- **Reproduction steps:** {how to reproduce the issue}
- **What would make it a 10:** {specific improvement suggestion}
- **rz-dev version:** {current version}
- **Skill:** rz-dev
```

**Calibration examples:**
- Worth recording: ARCHITECT phase has no guidance for choosing between competing data structures when performance constraints are ambiguous
- Worth recording: DEBUG phase protocol doesn't account for non-reproducible race conditions
- NOT worth recording: user's code had poor variable naming (that's the user's project issue, not a methodology issue)

### Feedback Flywheel

```
Use rz-dev workflow
    ↓
Agent self-evaluates at each phase end
    ↓
< 10 + methodology issue → write Field Report
    ↓
ruozi-skills maintainer reads Field Reports → decides whether to fix
    ↓
Fix rz-dev → git push
    ↓
Project git pull → next iteration uses improved workflow
```

## Retrospective (on-demand)

Analyze git history and prior Field Reports to identify trends and problem signals.

**Storage:** `.rz-dev/retros/{date}.json`

**Analysis dimensions:**
- **Code quality trend** — test coverage changes, bug density, fix ratio (fix commits / total commits — > 50% may indicate review gaps)
- **Hotspot files** — frequently modified files (churn indicator — consider refactoring)
- **Debug frequency** — how often does the workflow enter DEBUG? Are the same areas recurring?
- **Phase compliance** — did each phase produce its required outputs? Were any phases skipped?
- **Field Report summary** — how many methodology issues were found? How many resolved?

**Trend comparison:** Load prior retro snapshots, show trends for each metric (↑ improving / ↓ worsening / → stable)
