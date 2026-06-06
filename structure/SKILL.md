---
name: structure
description: Find architectural weaknesses and propose deepening opportunities. Use when the user wants to improve architecture, reduce complexity, find refactoring candidates, or make code more testable and navigable.
---

## Goal

Find real architectural friction: shallow modules, scattered knowledge, leaky coupling, or hard-to-test interfaces. Propose deepening opportunities, not implementation designs.

Preferred inputs: glossary, decisions, and `overview` explanations for unfamiliar modules. Apply the shared dependency policy when absent. Vocabulary: [ref/language.md](ref/language.md).

## Process

1. **Clarify scope.** If the pain point is named or the user asks for a broad survey, proceed. Otherwise ask one scope question.
2. **Explore.** Read glossary/decisions if present. Inspect modules enough to find friction. Use `overview` first only when missing system context materially affects the analysis.
3. **Evaluate.** Apply the deletion test: would deleting this module remove complexity because it is pass-through, or spread complexity because it earns its keep?
4. **Present.** Report only evidence-backed candidates, strongest 3-5 for a broad survey. Cite representative files, callers, tests, duplication, or context gaps in each `Problem`.
5. **Grill.** After the user picks a candidate, ask one question at a time across interface design, migration path, risk, and scope. Do not design a final public interface before a candidate is chosen.

Side effects:
- Reads: source, tests, docs, glossary, decisions, and relevant overview context.
- Writes: no files by default; optional glossary or decision records only when shared thresholds are met.

## Interaction format

Use [../shared/interaction.md](../shared/interaction.md).

First response:

```markdown
Using `structure` to find architectural friction and deepening opportunities.

**Phase**: clarify
**Scope**: [broad survey | named area]
```

## Output format

For broad surveys, first add:

```markdown
**Surveyed**: [entry points, modules, tests, records, or docs inspected]
```

Candidate shape:

```markdown
### Candidate N: [one-line label]

**Files**: [files involved]
**Problem**: [evidence-backed friction and any context gap]
**Solution**: [refactor direction only]
**Benefit**: [improved locality and testability]
**Strength**: [Strong | Worth exploring | Speculative]
```

End with:

```markdown
**Result**: [N] structural candidates found.
**Next**: Start with Candidate [N] because [reason].
```

If none are found, say so directly in `**Result**`.

## Guardrails

- No final interfaces, method names, migration steps, or exact module shapes before the user picks a candidate.
- Use glossary terms.
- Flag contradictions with existing decisions.
- List only real friction, not theoretical cleanup.
