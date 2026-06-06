---
name: handoff
description: Compact the current conversation into a handoff document so another agent can continue the work. Use when the user wants to save progress, hand off to another session, or preserve context before switching tasks.
---

## Goal

Write a self-contained handoff so a fresh agent can continue without this conversation.

Preferred inputs: topic records, task/spec statuses, decisions, glossary entries. If absent, follow the shared dependency policy and state that no durable artifacts were available.

## Process

1. **Summarize.** Capture current intent, why it matters, completed work, remaining work, key decisions, terminology, and glossary candidates. Before finalizing, honor the newest user instruction if it supersedes earlier intent.
2. **Freshness check.** Compare known topic records, specs, task statuses, recent decisions, and handoffs against session context. Call out discrepancies.
3. **Operational state.** Record branch, dirty files, running commands/servers, verification commands/results, blocked checks, and the exact next artifact or command.
4. **Next skills.** List which skill(s) the next agent should use and why.
5. **Reference artifacts.** Link to specs, tasks, decisions, glossary entries, commits, or PRs. Summarize rather than duplicating record bodies.
6. **Redact and write.** Remove secrets, credentials, tokens, and PII. Write the handoff using [ref/summarizing.md](ref/summarizing.md) and [../shared/records.md](../shared/records.md).

Side effects:
- Reads: topic records, glossary, decisions, git status/history, verification output, conversation context.
- Writes: one handoff record.
- Does not edit implementation code or glossary.

## Interaction format

Use [../shared/interaction.md](../shared/interaction.md).

First response:

```markdown
Using `handoff` to preserve current session context for the next agent.

**Phase**: summarize
**Scope**: [current session, named feature, or named path]
```

Ask only if handoff scope is ambiguous.

## Output format

```markdown
**Result**: Handoff written.

**Evidence**:
- Captured progress, remaining work, decisions, and artifacts.
- Captured branch, dirty files, running commands, and verification state.

**Artifacts**:
- `records/topics/YYYY-MM-DD-[topic-slug]/handoffs/YYYY-MM-DD-[slug].md`

**Next**: Run `[skill]` because [reason from the handoff].
```

If no concrete progress occurred, still write a brief handoff noting what was tried and why there is nothing actionable.

## Guardrails

- Reference existing artifacts instead of duplicating them.
- Do not create or update glossary entries.
- Explain enough for a zero-context agent.
- Keep it concise.
