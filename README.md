# Eventrise for Claude

Run your events on [Eventrise](https://eventrise.com) from Claude. Ask Claude to set up an event and its tickets, check how sales are going, find an attendee and check them in, handle a refund, or close out an event's budget and settlement. Claude works through your own Eventrise account, with your permissions.

This plugin connects Claude to the Eventrise connector and adds skills, commands and an agent that teach Claude how organizers work: what to check before publishing, how to read the numbers, and when to stop and ask you first.

## What's inside

**Connector:** the Eventrise MCP server at `https://mcp.eventrise.com/mcp`, the same server as the Eventrise connector in the Claude directory. It covers events, tickets, venues, sessions, speakers, attendees, check-in, orders, refunds, promo codes, tracking links, reports, budgets, invoices and settlements.

**Skills** (Claude uses these on its own when they fit):

| Skill | What it covers |
| --- | --- |
| `eventrise-basics` | Picking the organization, reading money and dates, errors, and confirming before changes |
| `event-setup` | Building an event as a draft, passing the publish checklist, publishing |
| `sales-and-reports` | Sales, revenue, sources, tax and payout reports, scheduled report emails |
| `attendees-and-checkin` | Finding people and orders, check-in, door counts, ticket changes and comps |
| `promotions` | Promo codes, group discounts, tracking links, featured events |
| `refunds` | The refund queue, refunding a ticket, cancelling an order |
| `settlement-and-finance` | Budgets, costs, vendors, invoices, organizer fees, locking the settlement |

**Commands** (in Claude Code and Cowork): `/eventrise:new-event`, `/eventrise:sales`, `/eventrise:checkin`, `/eventrise:refund`.

**Agent** (in Claude Code and Cowork): `event-ops`, for multi-step jobs such as a full event build, an event-day briefing or a post-event recap.

## Get started

1. Install Eventrise from the Claude plugin directory.
2. Connect Eventrise when Claude asks, and sign in with your Eventrise account. You choose which permissions to grant. You don't need an API key.
3. Ask something like "How are ticket sales for the spring gala?" or "Set up a new event for June 12."

You need an Eventrise account with a role in at least one organization. What Claude can see and change depends on your role there: a volunteer can check people in, an analyst can read reports, an owner or admin can do everything.

To try the plugin from a clone in Claude Code, run `claude --plugin-dir ./claude-plugin`, then `/mcp` to sign in to Eventrise.

## Safety

The skills tell Claude to show you exactly what it is about to do, and to wait for your yes, before anything that publishes an event, emails buyers, moves money, deletes something or locks a settlement. Eventrise also enforces your role's permissions on every request, whatever Claude asks for.

## Data and privacy

- The plugin itself is text: instructions for Claude and a connector address. It runs no code on your computer and stores nothing.
- Every request goes to one place, Eventrise's MCP server at `https://mcp.eventrise.com/mcp`, over HTTPS, signed in with your own Eventrise account. The plugin sends nothing to any other service.
- What Claude reads from Eventrise (events, orders, attendee names and emails, sales figures) comes back into your conversation with Claude. What you ask Claude to create or change is saved in your Eventrise account, like any change you make in the dashboard.
- Eventrise handles that data under the [Eventrise Privacy Policy](https://eventrise.com/privacy-policy) and [Terms](https://eventrise.com/terms-and-conditions). Your conversations with Claude are covered by Anthropic's terms.
- You can disconnect at any time from Claude's connector settings, or revoke the connection from your Eventrise account.

## Help

- Documentation: https://eventrise.com/docs/mcp
- Support: support@eventrise.com or https://eventrise.com/contact-us

## License

MIT. See [LICENSE](LICENSE).
