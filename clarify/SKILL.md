---
name: clarify
description: Interview the user relentlessly about a plan or design until requirements are solid. Use when the user wants to stress-test a plan, clarify what they want before building, or align on requirements.
---

## Goal

Resolve fuzzy requirements one question at a time. For code topics, preserve resolved questions as stories and write only glossary, decision, or research records that meet the shared thresholds.

Preferred input for `spec`: a `questions.md` record. If absent, `spec` follows the shared dependency policy.

## Process

1. **Scope.** If the request is clear and low-risk, use it. Otherwise ask what the user wants to build or decide. Classify the session as code or non-code.
2. **Interview.** Ask exactly one numbered `Q<N>` per response using the shared question format. Include a recommended answer and why it matters, then wait. Cover actor/goal, success signal, non-goals, failure modes, data/security/privacy, rollout/reversibility, terminology, dependencies, edge cases, and scope boundaries.
3. **Record code topics.** When the interview is complete, write `records/topics/<date>-<topic>/questions.md` per [../shared/records.md](../shared/records.md). Store resolved answers, not transcript text. Map resolved question clusters to numbered user stories in the form `As a [actor], I want [feature], so that [benefit]. (Q1, Q4)`. Keep topic-only caveats in the question record instead of creating extra record types.
4. **Optional records.** If investigation informed the answers, write research. Add project-wide terms to `records/global/glossary.md`. Offer a decision record only when all shared decision criteria are met.
5. **Finish.** Stop when the user says they are ready, or when actors, boundaries, important paths, terms, and load-bearing decisions are sufficiently covered. Call out any remaining gap instead of forcing more questions.

Side effects:
- Reads: glossary, topic records, and source/docs only when useful for a code-topic question.
- Writes: code-topic question records; optional glossary, research, or decision records.
- Does not write durable records for non-code topics.

## Interaction format

Use [../shared/interaction.md](../shared/interaction.md).

First response:

```markdown
Using `clarify` to resolve requirements before artifacts are written.

**Phase**: interview
**Scope**: [code topic | non-code topic]
```

Each response asks only the current `Q<N>`.

## Output format

Use shared output labels.

For code topics:
- `**Result**`: requirements are ready for `[next skill]`.
- `**Evidence**`: list resolved question range and covered areas.
- `**Artifacts**`: `questions.md` plus any glossary, research, or decision records written.
- `**Next**`: normally `spec`.

For non-code topics, report clarified requirements, `Artifacts: none`, and the single next action.

## Stop conditions

Stop and say what is missing if the user cannot answer a core question after two attempts, the problem keeps shifting, or the scope becomes too large for one clarify session.

## Guardrails

- Never ask multiple questions at once.
- Do not move forward until the current question is resolved.
- For non-code topics, do not explore code, write glossary records, or offer decisions.
- Challenge fuzzy language and contradictions against the glossary immediately.
