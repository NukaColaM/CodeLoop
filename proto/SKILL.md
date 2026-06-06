---
name: proto
description: Build a throwaway prototype to expose problems before a design decision is made. Use when analysis can't resolve a choice, two plausible paths have no clear winner, or the user wants to test an idea before committing.
---

## Goal

Answer one design question with the smallest throwaway build, then delete it.

Preferred input: a focused decision question from conversation, `clarify`, `spec`, or `structure`. If the user provides one clear question, proceed directly.

## Process

1. **Identify the decision.** A prototype answers one question, such as `Should sessions use Redis or Postgres?` If the request is a feature, ask one narrowing question or suggest `spec`.
2. **Choose mode.** Logic mode: runnable terminal app for algorithms, state machines, business logic, or data flow. UI mode: static, toggleable variants on one screen for comparison.
3. **Build minimum.** Use a temporary location like `.tmp/proto-[slug]/` or `tmp/proto-[slug]/`. Avoid production modules unless no isolated prototype can answer the question; if production must be touched, isolate the change for clean removal.
4. **Present finding.** Report what changed because of the prototype. For UI mode, provide route/screenshot/visual notes and pause for inspection before deletion unless automated comparison was requested.
5. **Discard.** Delete prototype files, temporary routes/imports/scripts/assets/debug output. Preserve only decision-rich snippets or findings in approved spec, decision, or research records per [../shared/records.md](../shared/records.md).

Side effects:
- Reads: source, docs, or records needed to frame the question.
- Writes: temporary prototype code; optional research/spec/decision records.
- Deletes: prototype code before final output.

## Interaction format

Use [../shared/interaction.md](../shared/interaction.md).

First response:

```markdown
Using `proto` to answer a design question with the smallest throwaway build.

**Phase**: identify decision
**Scope**: [logic mode | UI mode | undecided]
```

If unclear, ask:

```markdown
Q<N>. What single decision should this prototype answer?

Recommended answer: [specific decision question]
Why this matters: A prototype is only useful when it can prove or falsify one question.
```

## Output format

After deletion:

```markdown
**Result**: [winner found | inconclusive | question reframed]

**Evidence**:
- Question tested: [decision question]
- Prototype mode: [logic | UI]
- Finding: [what changed because of the prototype]
- Cleanup: [how prototype deletion was verified]

**Artifacts**:
- [decision/spec/research path if saved, or "none; prototype discarded"]

**Next**: Run `[skill]` because [reason].
```

For UI mode before deletion:

```markdown
**Prototype ready**: [route, screenshot path, or visual notes]
**Question**: [decision question]
**Variants**: [what to compare]

Q<N>. Have you inspected the prototype enough for me to discard it?

Recommended answer: Yes, discard it after preserving the finding.
Why this matters: UI prototypes are throwaway, but the comparison must happen before cleanup.
```

## Guardrails

- No clear question -> ask one local narrowing question or suggest `clarify`.
- Never ship prototype code.
- Do not polish or add production-grade handling.
- If the prototype reveals nothing new, build the next smallest version that can surprise you.
