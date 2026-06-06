# Writing a handoff

Handoffs live at `records/topics/<YYYY-MM-DD>-<topic-slug>/handoffs/<YYYY-MM-DD>-<slug>.md` and follow `../../shared/records.md`.

## Format

```markdown
# Handoff - [Topic]

**Date**: YYYY-MM-DD
**Suggested skills**: [skill-1], [skill-2], ...

## Context
[what was being worked on and why]

## Progress
- [x] Thing done

## Current state
- Branch: `[branch name]`
- Dirty files: `[none, or short list]`
- Running commands: `[none, or command/session]`
- Verification: `[commands run, failing checks, or not run]`

## Remaining
- [ ] Next step

## Decisions
[key decisions and rationale; link decision records]

## Vocabulary
[existing glossary links or glossary candidates]

## Artifacts
- `../spec.md`
- `../tasks/T1-xxx.md`
- `../decisions/xxx.md`
- `../../../global/decisions/xxx.md`
```

Requirements:
- Keep headings exactly as shown and in order.
- Use checkboxes only in `Progress` and `Remaining`.
- Include `**Suggested skills**` and `Current state`, even when values are `none`.
- Link artifacts by path or URL; do not paste full specs, decisions, or tasks.
- Use `Vocabulary` for existing glossary links or candidates; `handoff` does not edit the glossary.

## Quality Bar

A good handoff is specific enough for a zero-context agent: what was done, what remains, operational state, and exact starting artifact/command. If the session was exploratory with no concrete progress, still write what was tried and why there is nothing actionable.
