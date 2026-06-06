# CodeLoop

CodeLoop is a set of nine plain-markdown agent skills for software engineering. It works with any model or harness that supports the [Agent Skills standard](https://agentskills.io), and is designed to be forked, edited, and carried between projects.

The skills are small workflows, not a rigid delivery pipeline. They help an agent ask better questions, understand code in context, preserve durable records, and move from diagnosis or requirements into implementation without losing the thread.

This README is a human-facing guide. Runtime behavior lives in:

- [shared/routing.md](shared/routing.md) - skill selection and record audit
- [shared/interaction.md](shared/interaction.md) - questions, approvals, dependency fallback, final reports
- [shared/records.md](shared/records.md) - artifact paths, owners, templates, statuses, and QA
- each `SKILL.md` and its local `ref/` files

## Why CodeLoop Exists

Long agent sessions often fail for the same reasons:

- requirements stay fuzzy until implementation exposes contradictions
- useful discoveries disappear into chat history
- bugs get fixed before the cause is known
- refactors start from taste instead of evidence
- tasks are sliced by layer instead of by user-visible progress
- handoffs omit operational state, so the next session repeats discovery

CodeLoop addresses those problems with narrow skills and durable records. The goal is not ceremony. The goal is to keep just enough structure that a future agent can continue from facts instead of reconstructing intent.

## Skills

| Skill | Use it when | Output |
|---|---|---|
| `clarify` | Requirements, terms, or scope are fuzzy | Numbered questions, resolved stories, optional glossary/decision/research records |
| `overview` | Existing code needs system context | Explanation of callers, callees, rationale, assumptions, and gaps |
| `structure` | Architecture feels shallow, coupled, scattered, or hard to test | Evidence-backed refactor candidates |
| `proto` | A design choice needs a small experiment | Finding, optional research/decision record; prototype deleted |
| `spec` | Requirements are resolved enough to document | `records/topics/<date>-<topic>/spec.md` |
| `slice` | A spec or clear requirements need implementation tasks | `records/topics/<date>-<topic>/tasks/T<N>-<task>.md` |
| `tdd` | One task or acceptance criteria are ready to build | Passing tests, code, optional task/spec status updates |
| `diagnose` | A bug or regression has unknown cause | Root-cause report, optional preserved loop/research |
| `handoff` | Work needs to survive a session switch | `records/topics/<date>-<topic>/handoffs/<date>-<slug>.md` |

## Choosing a Skill

Use the situation, not just the user's wording:

- If the request is ambiguous, start with `clarify`.
- If the user asks "how does this work?", use `overview`.
- If the code is painful to change or test, use `structure`.
- If two approaches both look plausible, use `proto`.
- If requirements are ready but not written, use `spec`.
- If a spec needs implementation steps, use `slice`.
- If one slice is ready to build, use `tdd`.
- If something is broken and the cause is unknown, use `diagnose`.
- If work needs to continue elsewhere, use `handoff`.

The installed routing contract is [shared/routing.md](shared/routing.md). Ask at most one routing question when the right skill cannot be chosen from available evidence.

## Common Flows

```text
Unclear requirements
  -> clarify -> spec -> slice -> tdd

Understand existing code
  -> overview -> optional structure

Refactor search
  -> structure -> optional proto -> spec -> slice -> tdd

Bug with unknown cause
  -> diagnose -> tdd

Design choice
  -> proto -> spec or decision record

Session switch
  -> handoff
```

Skills are allowed to proceed without upstream artifacts when the conversation has enough context. For example, `spec` normally reads `questions.md`, but can write from a clear conversation. `tdd` normally reads a task record, but can work from explicit inline acceptance criteria. This fallback behavior is defined in [shared/interaction.md](shared/interaction.md).

## Prompting

A good prompt names the skill, desired outcome, relevant artifact, and output:

```text
[skill]: [desired outcome].
Context: [one or two relevant sentences].
Artifact: [record path, code path, bug report, or "conversation so far"].
Output: [question, report, record, tasks, tests, or handoff].
Constraints: [optional boundary].
```

Examples:

```text
clarify: Stress-test checkout recovery before a spec.
Context: Users need a way back into checkout after payment failure.
Artifact: conversation so far.
Output: questions record and user stories.
Constraints: Do not choose a payment provider yet.
```

```text
overview: Explain the refund module in system context.
Context: I need to change cancellation behavior safely.
Artifact: app/refunds.py.
Output: caller/callee/rationale explanation and context gaps.
```

```text
tdd: Implement the reset-link recovery task.
Context: The spec and task already exist.
Artifact: records/topics/2026-06-02-checkout-recovery/tasks/T1-reset-link.md.
Output: passing tests, code changes, and updated task status.
```

## Records

Records give future sessions durable context without preserving a long chat thread.

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
        ├── research/
        └── handoffs/
```

Global records hold project-wide vocabulary and decisions. Topic records hold context for one feature, bug, refactor, investigation, or design question.

Specs and tasks have `**Status**: active | done | dropped`. Glossary, decision, question, research, and handoff records do not use lifecycle status. Exact paths, owners, and templates are canonical in [shared/records.md](shared/records.md).

## Record Flow

Records are how skills pass context without depending on a single long conversation:

- `clarify` writes `questions.md`, optional glossary entries, optional decisions, and optional research.
- `spec` reads resolved context and writes `spec.md`.
- `slice` reads a spec or clear inline requirements and writes task files.
- `tdd` reads a task or inline acceptance criteria, writes tests/code, and may update status.
- `diagnose` preserves loops or root-cause findings when useful.
- `proto` preserves findings or decision-rich snippets, not prototype code.
- `overview` and `structure` read glossary and decisions when present.
- `handoff` links existing artifacts and records current operational state.

## Adoption

To use CodeLoop in a project:

1. Copy the skill folders and `shared/` contracts into the target skill library.
2. Create only the base record folders:

```text
records/
├── global/
│   └── decisions/
└── topics/
```

3. Do not create an empty glossary. Create `records/global/glossary.md` only when a real project-wide term has been resolved.
4. Do not create empty topic folders. Skills create topics lazily when writing durable records.
5. Keep harness-specific metadata outside this repository so the skills stay portable.

## Validation

This repository intentionally has no persistent validation scripts or fixtures. For changes, use temporary local checks or your harness.

Useful checks:

- `SKILL.md` frontmatter exists and has `name` and `description`.
- Local markdown links resolve.
- Referenced `ref/` files exist.
- Record examples follow [shared/records.md](shared/records.md).
- At least one realistic routing prompt still selects each skill.
- Record audits use the canonical checklist in [shared/records.md](shared/records.md).

## Design Notes

CodeLoop keeps hard stops inside a skill's method, not between skills. `diagnose` does not fix code because the skill's purpose is root cause. `tdd` requires testable behavior because implementation without acceptance criteria is guesswork. But `spec` does not require `clarify` as a hard gate, and `tdd` does not require a task file when the user provides clear acceptance criteria.

That distinction keeps the workflow disciplined without turning it into bureaucracy.

## Acknowledgments

Adapted from [Matt Pocock's skills library](https://github.com/mattpocock/skills).
