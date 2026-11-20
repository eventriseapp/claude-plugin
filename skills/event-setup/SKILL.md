---
name: event-setup
description: Create and publish an Eventrise event end to end, from a draft through venue, tickets, images and questions to a passing publish checklist. Use when someone wants to set up, build, copy or launch an event on Eventrise.
---

# Set up an event

Follow `eventrise-basics` for the organization, money units and confirmations.

## 1. Gather the essentials

Ask only for what you don't have:

- Event name, start and end date and time, and time zone
- In person, online or both, and the venue name and address for in-person events
- Ticket types: name, price, quantity (blank means unlimited) and any sales window
- Who pays the fees, if the person cares (the organization default applies otherwise)

If they want to repeat a past event, find it with `organization_list_events` and offer `organization_duplicate_event`, which copies tickets, venues, sessions and questions. Then change only what differs.

## 2. Build the draft

1. `organization_create_event` with the name and dates, and no `status`. It starts as a draft, so nothing is public yet.
2. Venue: reuse a saved place from `organization_list_saved_locations` when it matches, otherwise `organization_create_venue`.
3. Tickets: `organization_create_ticket` for each type. Use `organization_calculate_ticket_price` to show what a buyer pays and what the organizer receives for each price.
4. Images: `organization_create_event_image` takes a data URI (JPG, PNG or WEBP, 10 MB at most, five per event). The first image is the cover.
5. Optional: custom checkout questions (`organization_create_custom_question`), sessions and speakers for multi-track events, and promo codes (see the `promotions` skill).

Summarize the draft after each step in one or two lines, not a full dump.

## 3. Check it is ready

Call `organization_get_event_checklist` (or `organization_get_event_studio` for the visual version). Walk through every failing item and fix what you can. Common blockers:

- `payments_connected`: a paid event needs Stripe connected. Only the organizer can do this, in the Eventrise dashboard under Settings, Payments.
- `account_confirmed`: every owner of the organization has to confirm their email address.
- `future_end_date`: the event has already ended. Move the dates.

## 4. Publish only on a clear yes

Publishing makes the event page public and opens ticket sales. Show the event name, dates, venue and each ticket with its buyer price, then ask. On yes, call `organization_update_event` with `status: "PUBLISHED"`, then read the event back with `organization_get_event`.

- If the status is `PUBLISHED`, tell the person the event is live.
- If it is still a draft, Eventrise is holding the first publish for a quick review by the Eventrise team (this happens to some free events from new organizations). Tell the person it will go live once approved, and don't try to publish it again.

## After publishing

- Stop sales but keep the page up: `organization_close_event` (reopen with `organization_reopen_event`).
- Take the page down: `organization_unpublish_event`, which works only before the first completed order.
- Cancel for good: `organization_cancel_event` refunds every buyer and cannot be undone. Confirm twice in plain words before you call it.
