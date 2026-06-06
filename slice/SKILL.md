---
name: slice
description: Break a spec into vertical-slice tasks, each independently deliverable. Use when a spec is ready and the user wants to decompose it into actionable work items.
---

## Goal

Turn a spec or clear inline requirements into independently deliverable vertical tasks. Each task must prove value without waiting for a future task.

Strong dependency: `slice` normally reads a topic spec record. Without one, proceed from clear inline requirements under the shared dependency policy and note lower traceability.

## Process

1. **Read.** Read the spec if present, plus glossary and relevant decisions. If neither spec nor clear inline requirements exist, ask one local requirements question.
2. **Slice.** Create the thinnest meaningful vertical increments: user/operator-visible, independently testable, and traceable to stories, acceptance areas, or inline requirements. See [ref/slicing.md](ref/slicing.md).
3. **Order.** Number tasks `T1`, `T2`, ... so foundational and risky work appears early. Foundation work must still be inside a verifiable vertical task. Explain each dependency by why it exists, not just which task it references.
4. **Write.** Create task records per [ref/slicing.md](ref/slicing.md) and [../shared/records.md](../shared/records.md). Each task starts `**Status**: active` and includes a `Traceability:` line in `## Notes`.

Side effects:
- Reads: spec or inline requirements, glossary, decisions, relevant source context.
- Writes: task records only.
- Does not edit implementation code.

## Interaction format

Use [../shared/interaction.md](../shared/interaction.md).

First response:

```markdown
Using `slice` to turn the spec into independently deliverable tasks.

**Phase**: read
**Scope**: `records/topics/YYYY-MM-DD-[topic-slug]/spec.md` or inline requirements
```

## Output format

```markdown
**Result**: Spec sliced into [N] active tasks.

**Evidence**:
- Each task delivers user-visible progress.
- Dependencies are serial-numbered and explained.
- Each task notes which story or requirement it covers.

**Artifacts**:
- `records/topics/YYYY-MM-DD-[topic-slug]/tasks/T1-[task-slug].md`
- `records/topics/YYYY-MM-DD-[topic-slug]/tasks/T2-[task-slug].md`

**Next**: Run `tdd` on `records/topics/YYYY-MM-DD-[topic-slug]/tasks/T1-[first-task].md`.
```

## Guardrails

- Vertical slices only; never batch by layer.
- Unclear requirements -> ask one local question or suggest `clarify`.
- A task that cannot deliver user-visible progress alone is a subtask.
