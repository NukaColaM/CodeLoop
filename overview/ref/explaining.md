# Explaining code in system context

A system-context explanation says where code sits, what depends on it, why it exists, and what assumptions it makes.

## Trace First

1. **Upstream**: callers. Same module, cross-system, HTTP, queue, CLI? If many, group by category and focus on representative/critical callers.
2. **Downstream**: callees. External services, databases, filesystem, other modules, queues.
3. **Reason**: original problem solved. Check git blame and `records/global/decisions/` or `records/topics/*/decisions/`. If unrecoverable, say so.
4. **Assumptions**: implicit contracts such as validated input, request context, pooled DB connection, env vars, permissions, or idempotency.

## Output Structure

```markdown
## [Name] - system context

**Where it sits**: [callers] -> [this code] -> [callees]

**Why it exists**: [one sentence, or "Unknown from available records/history"]

**What depends on it**: [callers and what they need]

**Assumptions**:
- [assumption]

**Context gaps**:
- [missing caller, rationale, decision, owner, or term]

**Key detail**: [most important thing to understand]
```

## Good Explanation

Good output replaces "this function calls Stripe" with the system role: refund paths converge here; cancellation, admin refunds, and reconciliation depend on atomic refund behavior; callers must validate refundable state before calling; fee calculation is the only payment-method-specific detail.

That is the level of context a reader would otherwise have to recover from callers, dependencies, and history.
