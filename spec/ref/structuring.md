# Structuring a spec

Specs live at `records/topics/<YYYY-MM-DD>-<topic-slug>/spec.md` and follow `../../shared/records.md`.

## Format

```markdown
# [Title]

**Status**: active

## Problem
[user-visible gap]

## Solution
[user-understandable fix or feature]

## User stories
1. As a [actor], I want [feature], so that [benefit]. (Q1)

## Technical decisions
- [modules, public interfaces, schemas, API contracts, or architectural choices]

## Test strategy
- [key behaviors and public interfaces to test]

## Out of scope
[explicit exclusions]

## Further notes
[open questions, follow-on work, related specs, context gaps]
```

Requirements:
- Keep headings exactly as shown and in order.
- `**Status**` is `active`, `done`, or `dropped`.
- User stories are numbered and keep Q-number annotations when available.
- If a `questions.md` exists, copy its stories verbatim.
- Technical decisions name modules/contracts, not line-by-line implementation.
- Include only decision-rich parts of `proto` artifacts such as state machines, type shapes, or schemas.

## Section Guidance

- **Problem**: state the gap, not the solution.
- **Solution**: use user-facing language.
- **Technical decisions**: include modules to build/modify, interface changes, schema changes, API contracts, and architecture.
- **Test strategy**: focus on behavior through public interfaces and note useful prior tests.
