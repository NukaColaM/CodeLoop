---
name: diagnose
description: Find the root cause of a bug or performance regression through structured diagnosis. Use when the user reports a bug, says something is broken or slow, asks "why is this happening", or wants to debug an issue.
---

## Goal

Find the root cause before changing behavior. Do not fix code in this skill.

Preferred downstream input for `tdd`: a report, research record, or skipped/xfail test that preserves the reproduction loop.

## Process

### 1. Loop

Build a fast, deterministic pass/fail signal before isolating causes. Use a runtime check when possible, or a deterministic static proof when runtime reproduction is not applicable. See [ref/looping.md](ref/looping.md) for loop patterns.

If the bug is intermittent, run the trigger repeatedly, narrow timing, and raise reproduction reliability. If no trustworthy loop or proof is possible, stop with `**Blocked on**`, `**Tried**`, and `**Need**`.

### 2. Isolate

1. Reproduce the bug across multiple runs and confirm it matches the report. If the signal differs, pause and report the discrepancy.
2. State 3-5 ranked falsifiable hypotheses before testing. Continue without approval unless a check is expensive, destructive, risky, or needs unavailable access.
3. Test one hypothesis at a time. Change one variable at a time. Tag temporary debug output with a unique marker like `[DEBUG-a4f2]`.
4. Report the confirmed root cause, code location, correct hypothesis, and loop details. Remove all temporary instrumentation and throwaway harnesses unless intentionally preserved.

If no hypothesis is confirmed, report what was falsified and what remains unknown. If the cause is architectural, say so and suggest `structure`.

Preserve durable findings in a topic research record when useful; follow [../shared/records.md](../shared/records.md).

Side effects:
- Reads: reports, source, tests, logs, traces, records.
- Writes: temporary harnesses/instrumentation, skipped/xfail tests, or research records when useful.
- Deletes: temporary harnesses and instrumentation before final output unless intentionally preserved.

## Interaction format

Use [../shared/interaction.md](../shared/interaction.md).

First response:

```markdown
Using `diagnose` to find the root cause before changing code.

**Phase**: loop
**Scope**: [reported bug or path]
```

Before isolation, show hypotheses:

```markdown
**Hypotheses**:
1. [Most likely cause] - falsified if [specific check fails]
2. [Second cause] - falsified if [specific check fails]
3. [Third cause] - falsified if [specific check fails]
```

If approval is required, ask one shared-format question before testing.

## Output format

For a confirmed diagnosis:

```markdown
**Result**: Root cause found.

**Evidence**:
- Loop: [command, test, trace, or harness] reproduces [bug signal].
- Confirmed hypothesis: [hypothesis number and summary].
- Code: [path and relevant symbol].

**Artifacts**:
- [preserved skipped/xfail test, topic research record, or "none"]

**Next**: Run `tdd` with the preserved loop artifact, or `structure` if the cause is architectural.
```

If blocked, use the shared blocked format.

## Guardrails

- Do not fix the bug.
- Never test multiple hypotheses at once.
- If the user asks for a fix, finish the diagnosis report first, then suggest `tdd`.
