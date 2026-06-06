# CodeLoop interaction contract

Shared rules for skill introductions, questions, approvals, dependency fallback, and final reports.

## Rules

- Name the active skill in the first user-visible response: `Using [skill] because [reason].`
- State `**Phase**: [name]` when the skill has phases.
- Keep progress updates to one or two concrete sentences.
- Ask one user-facing question at a time unless a skill explicitly requires an approval checklist.
- Do not mix analysis, a user question, and final output in one response.
- Ask only when the answer materially changes the next action. Otherwise proceed with a stated assumption and surface it in `**Evidence**` or `**Next**`.

## Dependencies

- **Preferred input**: helpful context. If missing, continue from conversation context and note gaps.
- **Strong dependency**: normal best path. If missing, warn that confidence may be lower, then proceed from context, ask one local question, or create a minimal local substitute.
- **Internal hard rule**: active-skill method rule, such as `diagnose` does not fix code.

Avoid making cross-skill relationships hard gates. Prefer `normally reads`, `best used after`, `if present`, and `consider running`.

## Skill Prompt Shape

```text
[skill]: [desired outcome].
Context: [one or two relevant sentences].
Artifact: [record path, code path, bug report, or "conversation so far"].
Output: [question, report, record, task files, tests, or handoff].
Constraints: [optional scope boundary].
```

## Question Shape

```markdown
Q<N>. [One concrete question]

Recommended answer: [the recommended choice or answer]
Why this matters: [the consequence of this decision]
```

Rules:
- Number questions sequentially within the skill session.
- Ask only one question per response.
- If options are useful, list two or three before `Recommended answer:`.
- Reuse Q-numbers in records and summaries.

## Approval Shape

```markdown
**Proposed action**: [specific change]
**Reason**: [why this is next]
**Will change**: [paths or artifact types]
**Will not change**: [scope boundary]

Q<N>. Should I proceed?

Recommended answer: Yes, proceed with [specific action].
Why this matters: Approval fixes the scope before artifacts are written.
```

Approval is required for ambiguous, risky, irreversible, or user-visible scope choices. It is not required for routine tracing, implied record creation, fixture-backed audits, cleanup, or testing a clear plan.

## Output Shape

Use stable labels in this order when they fit:

```markdown
**Result**: [what happened]

**Evidence**:
- [fact, path, command result, or observation]

**Artifacts**:
- `path/to/artifact.md`

**Next**: [single recommended skill or action]
```

Blocked output:

```markdown
**Blocked on**: [specific blocker]
**Tried**: [short checks already performed]
**Need**: [single input, artifact, permission, or environment change]
```

If no issue or work exists, say so in `**Result**`.
