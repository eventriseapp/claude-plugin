---
name: promotions
description: Create and manage Eventrise promo codes, group discounts, tracking links and featured events, and see how they perform. Use for discounts, presale codes, campaign links with UTM tags, or choosing which events the organizer page features.
---

# Promotions

Follow `eventrise-basics` for the organization, money units and confirmations.

## Promo codes

- List with `organization_list_promo_codes` (`status` is `live` by default; `archived` or `all` to see more). Open one with `organization_get_promo_code`.
- Create with `organization_create_promo_code`. Confirm before creating:
  - the code text and the event
  - the discount: `kind` percentage with `value` in basis points (1000 = 10%), or a fixed amount with `value` in cents
  - whether it applies to each ticket or the whole order
  - limits: total uses, tickets it may discount in total and per order, dates
  - which tickets it covers, if not all
- Group discounts apply on their own once a cart reaches a minimum quantity (`auto_apply` with `min_quantity`).
- A code can also unlock hidden tickets or a presale.
- `organization_update_promo_code` leaves out what you don't send, so it can't clear a limit. Say so if the person asks to remove one.
- Turn a code off but keep its history with `organization_archive_promo_code` (`organization_unarchive_promo_code` brings it back). `organization_delete_promo_code` archives instead of deleting when orders used the code.
- Results: `organization_report_promo_code_usage`.

## Tracking links

- `organization_create_tracking_link` needs a name; add UTM tags and an optional promo code from the same event. The answer carries a short link and the full link to share.
- `organization_list_tracking_links` sorts by clicks, orders or revenue, for one event or all.
- After the first click or the first order, a link's UTM tags lock. Its name never locks.
- `organization_delete_tracking_link` archives a link that has orders, so its revenue keeps its source.

## Featured events

The organizer's public page can feature chosen events. Use `organization_list_featured_events`, `organization_create_featured_event`, `organization_reorder_featured_events`, `organization_delete_featured_event` and `organization_update_featured_events_mode`. These change a public page, so confirm the final order before saving.

- Start with `organization_list_featured_events` and read `featured_events_mode`.
- In `automatic` mode the page shows the next upcoming events, listed in `automatic_events`. The picks in `data` are saved for later and don't show. Reordering or deleting a pick changes nothing on the page.
- To reorder or remove what the page shows, first switch to manual with `organization_update_featured_events_mode` (`mode: "manual"`). Tell the person before you do: the page then shows the saved picks, or a copy of the automatic events when there are none. List again to get the new ids, then reorder or delete.
- Adding an event with `organization_create_featured_event` switches an automatic page to manual on its own. Say so before you add it: the page then shows the saved picks plus the new one.
