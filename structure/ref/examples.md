# Deepening examples

Use as framing reference; candidate reports still follow `../SKILL.md`.

## Shallow Handler

```python
def cancel_order(request):
    order = Order.get(request.order_id)
    if order.status == "shipped":
        return error("cannot cancel shipped order")
    refund = stripe.Refund.create(...)
    fee = calculate_refund_fee(order.total, refund.amount)
    AuditLog.record("order_cancelled", order_id=order.id, refund=refund.id, fee=fee)
    order.status = "cancelled"
    order.save()
    return success(order)
```

Problem: the handler owns status rules, Stripe calls, fee policy, and audit logging. Testing cancellation requires refund infrastructure.

## Deepened Module

```python
class RefundService:
    def issue_refund(self, order: Order) -> Refund:
        """Issue a full refund; handles provider, fees, and audit."""
        ...

def cancel_order(request):
    order = Order.get(request.order_id)
    if order.status in ("shipped", "cancelled"):
        return error(f"cannot cancel {order.status} order")
    refund_service.issue_refund(order)
    order.status = "cancelled"
    order.save()
    return success(order)
```

Benefit: refund knowledge is local, the handler is a small state transition, and each part is independently testable.

## Scattered Validation

Problem: the same order rules appear across five handlers with slight variation. A business-rule change requires finding every copy.

Direction: move validation behind one module such as `OrderValidator.validate(order, action)`, then callers only handle returned errors.

Common pattern: deepening concentrates knowledge behind a smaller interface so callers know what to ask for, not how the behavior works.
