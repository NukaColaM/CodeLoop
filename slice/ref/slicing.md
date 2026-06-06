# Slicing

Tasks live at `records/topics/<YYYY-MM-DD>-<topic-slug>/tasks/T<N>-<task-slug>.md` and follow `../../shared/records.md`.

## Format

```markdown
# [Title]

**Status**: active
**Serial**: T1
**Spec**: ../spec.md (or "none - sliced from inline requirements")
**Depends on**: T0 (none - this task stands alone)

## Goal
[user-facing outcome in one sentence]

## Acceptance
- [ ] Specific, observable condition
- [ ] Another condition

## Notes
Traceability: [spec stories, acceptance areas, or inline requirements].

[design decisions, constraints, prior art, pitfalls]
```

Requirements:
- Headings stay exactly as shown and in order.
- `**Serial**` is unique and sequential within the spec.
- `**Depends on**` names the dependency and why it matters.
- Acceptance criteria are observable and independently checkable.
- `## Notes` starts with traceability.

## Vertical Slice Test

After this task, can a user or operator do or verify something they could not before?

- Yes: task candidate.
- No: subtask or horizontal layer.

Good auth slices: signup sends confirmation email; confirmed login shows dashboard; password reset sends link and accepts new password.

Bad slices: users table, model, controller, email service, UI. These defer feedback until every layer exists.

## Sizing and Order

- Too big: cannot finish in one session or touches many modules.
- Too small: one private function/file with no user-visible result.
- Order as `T1`, `T2`, ... with foundational and risky behavior early.
- Embed foundations in the first task that proves behavior; do not create standalone schema/model/setup tasks unless directly user/operator-verifiable.
