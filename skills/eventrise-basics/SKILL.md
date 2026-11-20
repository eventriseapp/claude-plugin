---
name: eventrise-basics
description: Ground rules for working with the Eventrise connector. Use whenever a request touches Eventrise events, tickets, orders, attendees, reports or money, before calling any Eventrise tool.
---

# Working with Eventrise

Eventrise is a ticketing and event management platform. The Eventrise connector gives you the organizer's own account: everything you do runs with their sign-in and their role, and Eventrise refuses what their role does not allow.

## Find the organization first

1. Call `organization_list_organizations`. It returns every organization the person can reach and their role in each.
2. If there is more than one, ask which one they mean, unless the request already names it.
3. Pass that `organization_id` to every other tool.
4. Event tools also need an `event_id`. Find it with `organization_list_events` (search by name) instead of guessing.

## Read the numbers right

- Money is in integer cents: `1234` means $12.34. Show amounts as money in the event's currency, never as raw cents.
- Percentages and tax rates are basis points: `825` means 8.25%. Fields ending in `_ppm` are parts per million.
- Dates are ISO 8601. Show them in the event's time zone when the event has one.
- Lists page with `limit` and `offset`, 100 rows at most per page. When a question needs every row, keep paging and say how many rows you read.

## Handle answers and errors

- Every tool answers `{"success": true, "data": ...}` or `{"success": false, "error": "<code>", "message": ...}`.
- Read `message`, `details` and `blocking_items` and explain them in plain words. Don't retry a write that failed with `validation_failed`, `forbidden` or `settlement_locked`: fix the cause or tell the person.
- `forbidden` means the person's role can't do this. Say which role can (an owner or admin, usually) instead of trying another way around it.
- An `insufficient_scope` error means the connection lacks a permission. Ask the person to reconnect Eventrise and grant the permission the error names.
- Read-only tools are safe to retry.

## Ask before you change anything that matters

Before any write that moves money, emails buyers, or is hard to undo, show the person exactly what will happen and wait for a clear yes. That includes publishing, unpublishing, closing or cancelling an event, refunds, cancelling orders, comps that email attendees, deleting anything, and locking a settlement. Never batch several of these into one confirmation.

## Prefer the interactive views

Four read-only tools open an interactive view in Claude apps that support them, and return a text summary everywhere else:

- `organization_get_event_studio`: one event's details, tickets, page preview and publish checklist
- `organization_get_sales_dashboard`: sales pace, sources, promo codes and abandoned carts for one event, or the upcoming events without an `event_id`
- `organization_get_refund_desk`: pending refund requests, one at a time
- `organization_get_settlement_sheet`: profit and loss, attendance recap and the settlement lock

Changes made inside a view run when the organizer clicks, through the same tools and permissions.

## What you can't do here

Connecting Stripe, changing a team member's role, and billing for the Eventrise plan happen in the Eventrise dashboard at https://eventrise.com/dashboard. Send the person there for those.
