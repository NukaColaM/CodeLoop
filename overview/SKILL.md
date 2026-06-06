---
name: overview
description: Explain code in the context of the whole system. Use when the user needs a system-level explanation — how code fits, what depends on it, why it exists — not a local description of what a function does.
---

## Goal

Explain where code sits in the system: callers, callees, rationale, assumptions, and context gaps.

Preferred inputs: global glossary and relevant decisions. Apply the shared dependency policy when absent.

## Process

1. **Gather.** Read glossary and relevant global/topic decisions if present.
2. **Trace.** Before explaining, inspect upstream callers, downstream dependencies, rationale from history/records, and assumptions. See [ref/explaining.md](ref/explaining.md).
3. **Explain.** Use project vocabulary. If rationale, ownership, callers, or terms are unclear, list them as context gaps instead of guessing.
4. **Follow up.** Suggest `structure` for shallow modules or untestable/scattered behavior; otherwise suggest the next skill only when it follows from the explanation.

Side effects:
- Reads: source, tests, docs, glossary, decisions, git history as needed.
- Writes: no durable records by default.
- May suggest glossary or decision work, but does not switch into it unless asked.

## Interaction format

Use [../shared/interaction.md](../shared/interaction.md).

First response:

```markdown
Using `overview` to explain code in system context.

**Phase**: trace
**Scope**: [symbol, module, path, or feature]
```

Ask one narrowing question only when scope is too broad and the user did not ask for a whole-project survey.

## Output format

For a focused explanation:

```markdown
## [Name] - system context

**Where it sits**: [callers] -> [this code] -> [callees]

**Why it exists**: [one sentence, or "Unknown from available records/history"]

**What depends on it**: [callers and what they need]

**Assumptions**:
- [assumption]

**Context gaps**:
- [missing caller, rationale, decision, owner, or term]

**Key detail**: [the most important thing to understand]

**Next**: [optional next skill and reason]
```

For a whole-project survey:

```markdown
## [Project or area] - system context

**Entry points**: [main commands, routes, packages, or runtime surfaces]

**Main modules**:
- [module] - [role and most important dependency]

**Where it sits**: [external users/systems] -> [project] -> [external services/storage]

**Why it exists**: [one sentence, or "Unknown from available records/history"]

**Assumptions**:
- [project-level assumption]

**Context gaps**:
- [missing glossary, decision, owner, or rationale]

**Key detail**: [highest-leverage thing to understand]

**Next**: [optional next skill and reason]
```

## Guardrails

- Explain fit, not just local behavior.
- Use project vocabulary.
- Do not invent rationale.
- Surface assumptions explicitly.
- If too large to trace, narrow to one entry point or module.
