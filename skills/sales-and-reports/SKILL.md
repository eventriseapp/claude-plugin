---
name: sales-and-reports
description: Answer questions about Eventrise ticket sales, revenue, traffic sources and attendance, and set up recurring emailed reports. Use for "how are sales", sales summaries, revenue by ticket type or day, sales tax, payouts, or scheduling a report.
---

# Sales and reports

Follow `eventrise-basics` for the organization, money units and paging.

## Pick the right source

| Question | Tool |
| --- | --- |
| How is one event doing? | `organization_get_event_insights_overview` (or `organization_get_sales_dashboard` with `event_id` for the interactive view) |
| How is the whole organization doing? | `organization_get_insights_overview` (or `organization_get_sales_dashboard` without `event_id`) |
| Which tickets sell? | `organization_get_sales_by_ticket_type` or `organization_report_sales_summary` |
| Where do buyers come from? | `organization_get_sales_by_source`, and `organization_list_tracking_links` for named links |
| Sales by day | `organization_report_sales_by_day` |
| Revenue and fees | `organization_report_revenue_summary`, `organization_report_payouts_and_fees`, `organization_report_payout_summary` |
| Sales tax owed | `organization_report_sales_tax` |
| Promo code results | `organization_report_promo_code_usage` |
| Abandoned carts | `organization_report_abandoned_carts` |
| Refunds and transfers | `organization_report_refunds`, `organization_report_transfers` |
| Comps and manual orders | `organization_report_comps`, `organization_report_manual_orders` |
| Order-level detail | `organization_report_orders_details` |

## Write the answer

- Lead with the figure that answers the question, then two or three supporting numbers. Compare with the previous period when the tool returns one.
- Show money in the event's currency, converted from cents.
- Say which period the numbers cover.
- Net sales already take out discounts and refunds. Don't add or subtract them again.
- Tickets sold counts admission tickets. Add-ons are separate.
- For a table or chart, keep it short: top rows, then a total.

## Recurring reports

`organization_create_scheduled_report` emails a CSV on a schedule. Confirm the report, the frequency and the recipients before you create it. List existing ones with `organization_list_scheduled_reports`; `organization_delete_scheduled_report` stops one at once, so confirm first.
