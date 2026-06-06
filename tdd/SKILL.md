---
name: tdd
description: Test-driven development with a red-green-refactor loop. Use when a task or acceptance criteria are ready for implementation, when the user wants to build features or fix bugs test-first, mentions TDD or "red-green-refactor", or asks for test-driven development.
---

## Goal

Build one vertical slice test-first: failing behavior test, minimal code, refactor, repeat. Tests verify public behavior, not implementation details.

Strong dependency: `tdd` normally works from a topic task record. Without one, derive local acceptance criteria from the request, state them before coding, and suggest `slice` when durable traceability would help.

## Process

1. **Plan.** Read the task/spec, glossary, decisions, and any diagnosis loop. State the public interface and behaviors to test in priority order. Ask one local question only when acceptance criteria or interface are too ambiguous to test. Proceed without approval when the request fixes behavior and risk is low.
2. **Tracer bullet.** Write one behavior test, watch it fail, then write minimal code to pass. This proves the path works.
3. **Loop.** For each remaining behavior: `RED` next test -> `GREEN` minimal code. One behavior at a time; do not prebuild future behavior.
4. **Refactor.** Only while green. Remove duplication, deepen modules where locally appropriate, and rerun tests after each change. If broader structural issues appear, stop and suggest `structure`.
5. **Status.** If using a task record, mark it `done` only after all acceptance criteria and tests pass; mark `dropped` only when abandoned. Mark the spec `done` only when every traced task is `done` or intentionally `dropped`, no active task remains, and no unresolved acceptance gap exists.

Side effects:
- Reads: task or inline criteria, spec, glossary, decisions, diagnosis loops, source, tests.
- Writes: tests, implementation code, and active task status/notes.
- May update a spec only for accepted public-contract/story/scope changes or final `done` status.
- Does not create task records.

## Interaction format

Use [../shared/interaction.md](../shared/interaction.md).

First response:

```markdown
Using `tdd` to implement one vertical slice test-first.

**Phase**: plan
**Scope**: `records/topics/YYYY-MM-DD-[topic-slug]/tasks/T<N>-[task-slug].md` or inline acceptance criteria
```

When approval is needed:

```markdown
**Public interface**: [what callers/users will use]

**Behaviors to test**:
1. [highest-priority observable behavior]
2. [next behavior]
3. [next behavior]

**Will change**: [paths or modules expected]
**Will not change**: [explicit scope boundary]

Q<N>. Should I start the red-green-refactor loop with this interface and behavior list?

Recommended answer: Yes, start with behavior 1.
Why this matters: TDD needs a confirmed public interface before tests can describe behavior.
```

During work, label progress `RED`, `GREEN`, and `REFACTOR`.

## Output format

```markdown
**Result**: Task complete and verified.

**Evidence**:
- RED/GREEN cycles completed for [behaviors].
- Verification command: `[command]`
- Task status updated if a task record was used.
- Spec status updated only if this was the final traced task and all completion criteria were met.

**Artifacts**:
- `records/topics/YYYY-MM-DD-[topic-slug]/tasks/T<N>-[task-slug].md` (if used)
- [changed code/test paths]

**Next**: [next task path, "none - spec complete", or "resolve remaining spec gap"]
```

## Divergence

- Wrong interface: stop, propose the revised public interface, confirm when needed, update the task, then continue.
- Incomplete or wrong acceptance criteria: update the task; update the spec only for accepted public-contract, story, or scope changes.
- Oversized task: suggest re-slicing instead of expanding scope.

## Guardrails

- Unknown bug cause -> first build a diagnostic loop or suggest `diagnose`.
- Vertical slices only: `test 1 -> code 1 -> test 2 -> code 2`. Do not write all tests first or all code first.
- No speculative features.

See [ref/testing.md](ref/testing.md) for test quality and mocking guidance.
