# CodeLoop routing and audit

This file answers two questions: which skill to use, and whether existing records follow the library format. When an agent doesn't know which skill to pick, or needs to validate record structure, consult this file.

## First-time setup

When adopting CodeLoop in a repo, create the record structure:

```text
records/
├── global/
│   └── decisions/
└── topics/
```

Create `records/global/glossary.md` only when at least one term has a clear, evidence-backed definition. Never create an empty glossary. Do not create topic folders until there is a known topic and at least one durable record to place there — skills create topic folders lazily when they write records.

Do not edit application code during setup.

## Skill routing

This table is the installed routing contract for CodeLoop skills. Individual `SKILL.md` frontmatter remains discovery metadata, and the README is only a user-facing overview. Pick one primary skill. Use other skills only as supporting context when the primary skill explicitly points to them or when the user asks for a compound workflow. Use the situation, not user phrasing alone:

| Situation | Skill |
|---|---|
| Unclear requirements or fuzzy terms | `clarify` |
| Existing code needs explanation | `overview` |
| Architectural pain or refactor search | `structure` |
| Unresolved design choice between approaches | `proto` |
| Requirements are ready for an artifact | `spec` |
| Spec or inline requirements need implementation tasks | `slice` |
| Task or acceptance criteria are ready for implementation | `tdd` |
| Bug cause is unknown | `diagnose` |
| Session needs preservation | `handoff` |
| Adopting CodeLoop or checking record structure | use this audit section |

Ask at most one routing question if the skill cannot be chosen from available evidence.

## Record audit

Check existing records against the canonical audit checklist in [`records.md`](records.md) (Artifact QA checklist) - path and filename pattern, heading order, valid `**Status**`, ISO dates and kebab-case slugs, relative links instead of duplicated content, checkbox syntax, and topic grouping.

Use the adopted project's validation harness when one exists. Otherwise inspect manually against the canonical checklist in [`records.md`](records.md).

Only fix formatting and record-structure issues. Do not rewrite requirements, decisions, or technical meaning without confirmation.
