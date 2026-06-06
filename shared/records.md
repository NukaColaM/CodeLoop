# CodeLoop record contract

Canonical rules for durable CodeLoop artifacts: glossary entries, decisions, questions, research, specs, tasks, and handoffs. If a skill restates a rule and conflicts with this file, this file wins.

## Record Rules

- Use ISO dates: `YYYY-MM-DD`.
- Use lowercase kebab-case slugs.
- Store durable work here:

```text
records/
├── global/
│   ├── glossary.md
│   └── decisions/
│       └── <slug>.md
└── topics/
    └── <YYYY-MM-DD>-<topic-slug>/
        ├── questions.md
        ├── spec.md
        ├── tasks/
        │   └── T<N>-<task-slug>.md
        ├── decisions/
        │   └── <slug>.md
        ├── research/
        │   └── <slug>.md
        └── handoffs/
            └── <YYYY-MM-DD>-<slug>.md
```

- Create topic folders lazily only when writing a durable topic record.
- Use `records/global/glossary.md` only for project-wide vocabulary.
- Use `records/global/decisions/` for project-wide decisions and `records/topics/<topic>/decisions/` for topic decisions.
- Keep required template headings in order; do not add top-level headings unless the template allows it.
- Valid lifecycle statuses, where required: `active`, `done`, `dropped`.
- Status fields appear only on specs and tasks.
- Put file paths in backticks or clickable markdown links; use relative links between records.
- Use `- [ ]` and `- [x]` for checklists.
- Use fenced code blocks with an info string.
- Link existing records instead of duplicating them.
- Use ASCII separators in generated records and skill outputs: `->`, `-`, `(Q1, Q2)`.
- `index.md` is nonstandard unless a fork adds a local owner and audit rule.

## Writing Rules

- If no topic exists, choose a slug from the user's goal and use the current local date.
- Create `records/global/glossary.md` only when at least one clear, evidence-backed project-wide term is ready.
- New specs and tasks start `**Status**: active`.
- A task becomes `done` only when all acceptance criteria are verified and all tests for that slice pass.
- A task becomes `dropped` only when abandoned because requirements or approach changed.
- A spec becomes `done` only when every traced task is `done` or intentionally `dropped`, no active task remains, and no unresolved acceptance gap is called out.
- Do not add lifecycle status to glossary, decision, question, research, or handoff records.
- Write side-effect decision records only after all decision criteria below pass.

## Record Owners

| Record | Format | Created by | May update |
|---|---|---|---|
| Glossary | this file | clarify, structure | clarify, structure |
| Decision | this file | clarify, structure, proto | clarify, structure, proto |
| Question | this file | clarify | clarify |
| Research | this file | clarify, diagnose, proto | clarify, diagnose, proto |
| Spec | [`../spec/ref/structuring.md`](../spec/ref/structuring.md) | spec | spec, proto for approved decision snippets, tdd for accepted contract/story/scope changes and final `done` |
| Task | [`../slice/ref/slicing.md`](../slice/ref/slicing.md) | slice | tdd for active-slice status, acceptance criteria, and notes |
| Handoff | [`../handoff/ref/summarizing.md`](../handoff/ref/summarizing.md) | handoff | handoff |

Cross-cutting formats live here. Single-skill artifacts live in that skill's `ref/` and must be indexed above.

## Glossary

Home: `records/global/glossary.md`

Use a categorized markdown table:

```markdown
## Concepts
| Term | Definition |
|---|---|
| Order | A customer's request to purchase one or more products from the catalog. |
```

Requirements:
- One row per term.
- Title Case terms unless project vocabulary differs.
- Definitions are precise, non-self-referential, and usually one sentence.

## Decisions

Homes:
- Topic: `records/topics/<YYYY-MM-DD>-<topic-slug>/decisions/<slug>.md`
- Global: `records/global/decisions/<slug>.md`

Template:

```markdown
# [Title]

**Date**: YYYY-MM-DD

## Context
[constraints and situation]

## Decision
[one clear sentence]

## Why not alternatives
- **Alternative A** - rejected because [specific reason]
- **Alternative B** - rejected because [specific reason]
```

Write a decision record only when all three are true:
1. Hard to reverse.
2. Surprising without context.
3. A real trade-off with alternatives.

## Questions

Home: `records/topics/<YYYY-MM-DD>-<topic-slug>/questions.md`

Template:

```markdown
# [Title] Questions

**Date**: YYYY-MM-DD

## Questions
| # | Question | Answer |
|---|---|---|
| Q1 | [question] | [resolved answer] |

## Stories
1. As a [actor], I want [feature], so that [benefit]. (Q1, Q3)
```

Requirements:
- Q-numbers are stable and sequential.
- Answers are resolved answers, not transcript text.
- Every story references at least one Q-number.

## Research

Home: `records/topics/<YYYY-MM-DD>-<topic-slug>/research/<slug>.md`

Template:

```markdown
# [Title] Research

**Date**: YYYY-MM-DD
**Prompted by**: Q3, diagnostic loop, prototype question, or other short context

## What was investigated
[what was investigated]

## Findings
[observed facts]

## Implications
[effect on design, questions, or decisions]
```

Write research when investigation is worth preserving: codebase exploration, library/protocol comparison, external documentation, quick experiments, confirmed diagnoses, or prototype findings. Do not write research for trivial lookups.

## Artifact QA

Before finishing a record or auditing existing records, check:

- Correct owner wrote the artifact type.
- Path, filename, date, slug, and topic folder match the expected pattern.
- Required headings are present and ordered.
- Status appears only where allowed and has a valid value.
- Question stories keep `Q<N>` references.
- Tasks have serial numbers, dependency explanations, and traceability.
- Links are relative where possible; content is not duplicated.
- Checklists use `- [ ]` or `- [x]`.
- No secrets, credentials, or personal data.

Use the adopted project's validation harness when present. Otherwise inspect manually.
