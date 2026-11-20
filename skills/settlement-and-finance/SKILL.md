---
name: settlement-and-finance
description: Track an Eventrise event's budget, costs, vendors and invoices, review its profit and loss, and close out the settlement after the show. Use for event P&L, budgets, expenses, vendor or sponsor invoices, organizer fees, or settling up an event.
---

# Settlement and finance

Follow `eventrise-basics` for the organization, money units and confirmations. Read before you write: show the current figures first, then propose changes.

## See where an event stands

- `organization_get_settlement_sheet`: profit and loss, attendance recap, top sales sources and the settlement lock, as a view where supported.
- `organization_get_finance_summary`: the same figures as data, including the lock state, the snapshot taken at lock time and any later adjustments.
- `organization_get_finance_budget`: the budget lines next to actuals.

## Record costs and income

- Entries: `organization_list_finance_entries`, `organization_create_finance_entry`, `organization_update_finance_entry`, `organization_delete_finance_entry`. Entries an invoice manages answer `managed_by_invoice`: change the invoice instead.
- Budget: `organization_update_finance_budget`.
- Vendors: `organization_list_finance_vendors`, `organization_create_finance_vendor` and the related tools; `organization_list_finance_vendor_entries` shows what a vendor was paid.
- Confirm amounts, dates and categories before each write, and say which event they belong to.

## Invoices

Invoices bill a sponsor, vendor or partner and can be paid online.

- Draft with `organization_create_invoice`, check it with `organization_preview_invoice`, then send with `organization_send_invoice` only after the person has seen the preview and said yes. Sending emails the recipient.
- `organization_remind_invoice` sends a reminder email. Confirm first.
- `organization_record_invoice_payment` records money received outside Eventrise; `organization_undo_invoice_payment` reverses that record.
- `organization_void_invoice` cancels an invoice for good. Confirm first.

## Organizer fees

Organizer fees (a facility fee, a service charge) are added to ticket prices and kept by the organizer. They have tax and consumer-law rules, and creating or changing one requires the organizer to attest to them. Use the fee tools (`organization_list_fees`, `organization_list_event_fees`, `organization_preview_fee` and the rest) to read and explain them. Preview any change with `organization_preview_fee`, show the warnings it returns, and only save after the person reads them and agrees.

## Close out the settlement

After sales end (or the event is cancelled):

1. Review the settlement sheet with the person: ticket revenue, fees, costs, comps, refunds and the bottom line.
2. Fix anything missing first. Locking freezes comps, manual orders, event fees, finance entries, budget lines and the event dates.
3. On a clear yes, call `organization_lock_event_settlement`. It snapshots the profit and loss as the settled figure. While sales are still open it answers `settlement_not_lockable`.
4. `organization_unlock_event_settlement` reopens it for edits; the next lock takes a fresh snapshot. Confirm before unlocking.

Refunds stay possible after the lock; see the `refunds` skill.
