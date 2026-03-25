# rz-product-dev

Product development lifecycle — from requirement to release.

## Scope

Full product development state machine covering ideation, requirements, solution design, review, development, testing, and release. This skill governs the **what** and **why** of building products, while `rz-dev` governs the **how**.

## Reference

This skill extends **FL Playbook: product-dev**. The canonical workflow, axioms, and phase definitions live in:

```
../fl-playbook/product-dev/
```

## Workflow

```
INIT → REQUIRE → SOLUTION → REVIEW → DEV → TEST → RELEASE
```

| Phase | Purpose | FL Playbook Reference |
|---|---|---|
| Init | Cold-start from existing code | `phases/init.md` |
| Require | Requirements elicitation and specification | `phases/require.md` |
| Solution | User-facing and engineering design | `phases/solution.md` |
| Review | Three-viewpoint review gate | `phases/review.md` |
| Dev | TDD-driven implementation | `phases/dev.md` |
| Test | QA and test coverage | `phases/test.md` |
| Release | Deployment and changelog | `phases/release.md` |

## Axioms (Summary)

The full 11 axioms are defined in `fl-playbook/product-dev/principles/axioms.md`. Key highlights:

1. **Documentation** — `docs/` is the single source of truth
2. **MVP Discipline** — ship the smallest thing that validates the hypothesis
3. **Verification-First** — prove it works before calling it done
4. **Search-Before-Build** — check if it already exists
5. **Goal-Backward Planning** — start from the desired outcome

## Completion Status Protocol

Every phase reports one of: `DONE`, `DONE_WITH_CONCERNS`, `BLOCKED`, `NEEDS_CONTEXT`, `ITERATE`

## RZ Layer

Personal extensions on top of FL Playbook:

- **Side project mode** — relaxed review gate for solo work; still requires REQUIRE and TEST
- **Learning projects** — skip RELEASE; focus on REQUIRE → DEV → REFLECT (via rz-dev)
- **Portfolio tracking** — each shipped project feeds into rz-personal growth metrics
