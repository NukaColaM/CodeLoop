# Testing

TDD reports follow `../../shared/interaction.md`.

## Good Tests

- Read like a behavior spec.
- Exercise the public interface or system boundary the user cares about.
- Survive internal refactors.
- Are deterministic and fast.
- Assert observable outcomes, not private state.

Avoid tests that mock internal collaborators, call private methods, query internals instead of APIs, or know file/helper structure.

## Mocking

Mock only boundaries you do not control: external APIs, databases, file systems, message queues, system clock. If you control the code, prefer testing the real path.

## Untested Code

First create or find a seam:
- Public API or function from outside.
- Dependency injection for external collaborators.
- Small extraction behind an interface when a hard-coded boundary blocks testing.

Before refactoring untested behavior, write a characterization test that captures current behavior, even when the behavior is wrong.

## Test Shape

One scenario per test:
1. arrange/given
2. act/when
3. assert/then

Focus on happy paths, critical errors, complex logic, and spec-important behavior. Skip trivial getters, framework boilerplate, and startup-failing config.
