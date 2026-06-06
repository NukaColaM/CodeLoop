# Building a diagnostic loop

A loop is any repeatable signal for "bug present" or "bug absent." Preserve the command or trigger clearly enough for later `tdd`.

## Categories

- **Test**: failing unit, integration, E2E, or Playwright test through a public seam. Do not leave the main suite red; keep valuable repros skipped/xfail or delete throwaway probes.
- **Trace**: replay a captured HTTP request, event log, core dump, production payload, or similar artifact.
- **Harness**: minimal isolated runner for the broken path, such as one script, one service, mocked boundaries, or a small Compose setup.
- **Bisect**: script "checkout/build/run loop" for `git bisect run` or side-by-side regression comparison.
- **Static proof**: compiler/type/linter/source-invariant proof when runtime reproduction is not applicable.

## Loop Description

```markdown
**Loop**: [test, trace, harness, bisect, or static proof]
**Command**: `[exact command or trigger]`
**Bug signal**: [what fails when the bug is present]
**Expected signal**: [what passes when the bug is absent]
**Reliability**: [N/N reproductions, or observed failure rate]
```

## Flaky Bugs

- Repeat the trigger 100-1000x and measure the failure rate.
- Add stress: concurrency, load, timing variance.
- Narrow scope until a smaller part fails at a higher rate.
- Instrument boundaries to catch the failure earlier.

A 50% reproduction rate is debuggable. A 1% rate needs a sharper loop.
