---
name: refunds
description: Review and act on Eventrise refund requests, refund a ticket without a request, and cancel orders. Use when someone asks about refunds, a buyer wants their money back, or an order has to be cancelled.
---

# Refunds and cancellations

Follow `eventrise-basics` for the organization, money units and confirmations. Every action here moves real money through Stripe and emails the buyer, and none of it can be undone. Never refund or cancel without the person's explicit yes to the exact amount and ticket.

## Work the queue

1. `organization_get_refund_desk` shows pending requests one at a time with a previewed amount (in apps that show views). Elsewhere, list them with `organization_list_refund_requests` (pending by default).
2. For each request, call `organization_preview_refund` with the ticket's `order_item_id`. It returns the most you can refund, fee by fee, and any add-ons on other orders that depend on this ticket.
3. Show the buyer, ticket, event, the amount you propose and whether they keep the ticket. Ask the person to approve, change the amount, or reject.
4. Approve with `organization_approve_refund` (`refund_amount_cents`, `refund_reason`, an optional message to the buyer). Reject with `organization_reject_refund` and a reason.

## Refund without a request

`organization_refund_order_item` refunds one ticket on the organizer's own initiative. Preview first, same as above. Set `can_keep_ticket` only when the person says the buyer keeps their entry.

## Cancel a whole order

`organization_cancel_order` voids every ticket on the order that hasn't been refunded, frees the seats and inventory, and sends one email. It refunds each ticket in full unless you pass `issue_refund: false`.

1. Call it with `dry_run: true` first. That changes nothing and lists add-ons on other orders that depend on these tickets.
2. Show the order, the tickets, the total refund and the dependent add-ons. Ask whether to include those add-ons (`include_order_item_ids`).
3. Cancel only after a clear yes.

## Locked settlements

If an event's settlement is locked, a refund answers `settlement_adjustment_confirmation_required`. Explain that the refund will change a settlement the organizer already closed, and that Eventrise records it as an adjustment. Pass `confirm_settlement_adjustment: true` only after the person agrees.

## Reasons

`refund_reason` must be one of the values the tool lists. Use `OTHER` with `refund_reason_other` only when none fits. Write any message to the buyer in plain, friendly words, and show it to the person before you send it.

To cancel an entire event and refund everyone, see `event-setup` (`organization_cancel_event`). Refund totals over time: `organization_report_refunds`.
