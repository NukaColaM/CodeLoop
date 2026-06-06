---
name: spec
description: Synthesize conversation context into a spec document. Use when the user wants to create a spec from the current context, or when clarify has finished and requirements are ready to be written up.
---

## Goal

Turn resolved context into an actionable spec. Do not re-interview requirements.

Strong dependency: `spec` normally reads a `clarify` question record, but may write from clear conversation context under the shared dependency policy.

## Process

1. **Gather.** Read glossary, relevant decisions, topic research, any `questions.md`, and resolved conversation context. If `questions.md` already contains user stories with Q-number annotations, reuse them.
2. **Structure.** Use [ref/structuring.md](ref/structuring.md). Identify touched modules, understand existing system context enough to spec the work, and note remaining gaps in `Further notes`. Ask one module-scope confirmation only when module choice materially changes scope, risk, or ownership.
3. **Decide.** Technical decisions may name modules, public interfaces, schemas, API contracts, or architecture. Include only decision-rich snippets from `proto`, never whole prototypes or line-by-line implementation.
4. **Write.** Create `records/topics/<date>-<topic>/spec.md` per [../shared/records.md](../shared/records.md). New specs start `**Status**: active`. `slice` owns task records.

Side effects:
- Reads: glossary, decisions, research, questions, conversation, and relevant source context.
- Writes: one spec record.
- Does not write tasks.

## Interaction format

Use [../shared/interaction.md](../shared/interaction.md).

First response:

```markdown
Using `spec` to turn resolved requirements into an actionable spec.

**Phase**: gather
**Scope**: [conversation context or records/topics/YYYY-MM-DD-[topic-slug]/questions.md]
```

## Output format

After writing:

```markdown
**Result**: Spec written.

**Evidence**:
- User stories came from [conversation | records/topics/.../questions.md].
- Technical decisions reference existing glossary and decision records where available.

**Artifacts**:
- `records/topics/YYYY-MM-DD-[topic-slug]/spec.md`

**Next**: Run `slice` to break the spec into independently deliverable tasks.
```

If blocked by a major contradiction, use the shared blocked format.

## Conflicts

- Minor contradiction: resolve explicitly in `Further notes`.
- Major contradiction: stop; do not write a partial spec unless asked after reporting it.
- Critical missing detail: ask one local question or suggest `clarify`.

## Guardrails

- No requirements interview.
- No implementation code snippets except contract-level schemas, type shapes, state machines, or API examples.
- Name things being changed, not private helper details.
- Use glossary terms.
