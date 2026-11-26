---
name: attendees-and-checkin
description: Find attendees and orders, check people in or undo a check-in, fix attendee details, move a ticket to someone else, add comps, and report door counts on Eventrise. Use for guest lists, "is this person registered", event-day check-in, or attendance numbers.
---

# Attendees and check-in

Follow `eventrise-basics` for the organization, paging and confirmations.

## Find people

- Attendees: `organization_list_attendees` with `query` (name or email) and `event_ids`. `checked_in: false` lists who hasn't arrived. Open one with `organization_get_attendee`.
- Orders: `organization_list_orders` searches by buyer, status and dates. `organization_get_order` returns the items, payments and attendees.
- Ticket PDF: `organization_get_attendee_pdf` returns a download link to share with the organizer.
- When a search returns several people with similar names, list them with email and ticket type and ask which one.

Attendee data is personal. Share only what the question needs, and don't paste whole guest lists into the chat unless the person asks for them.

## Check in

- Check in one ticket with `organization_checkin_order_item`, `checked_in_at` set to the current time. To undo, send `null`. Someone holding several tickets is checked in ticket by ticket; find their ticket ids on the attendee or the order.
- A refunded ticket, or one whose order isn't complete, is refused with `ticket_not_valid` and a reason. Tell the person why at once; don't try another path.
- Before a check-in, confirm the name and ticket type when there is any doubt about the match.

## Door counts

- Live counts by ticket type: `organization_report_event_checkin`.
- Who has and hasn't arrived: `organization_report_checkins_and_attendees`.
- For one event's arrival pace next to sales, `organization_get_sales_dashboard` shows door mode.

## Change a ticket or an order

These change what a buyer sees or receive emails, so confirm each one first:

- Fix an attendee's name, contact details or question answers: `organization_checkin_attendee` (despite its name, it updates the attendee's details and checks nobody in). Order-level answers: `organization_update_order_responses`; one ticket's answers: `organization_update_order_item_responses`.
- Give a ticket to someone else: `organization_preview_order_item_schedule_conflicts` first (it warns about overlapping sessions), then `organization_reassign_order_item`.
- Start or cancel a transfer for the holder: `organization_create_order_item_transfer`, `organization_cancel_order_item_transfer`.
- Comp tickets or record an order paid outside Eventrise: `organization_create_comped_order`. Ask whether attendees should get an email. On a seated event, every item needs a seat label: read the event's `seat_map_id`, then copy the label exactly from the `objects` keys of `organization_get_seat_map_categories`. Never guess one. Remove one with `organization_delete_comped_order`.

Refunds and order cancellations live in the `refunds` skill.
