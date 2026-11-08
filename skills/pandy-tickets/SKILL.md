---
name: pandy-tickets
description: Find events in Guatemala, create events, set ticket types and prices, sell via card or bank transfer with assisted receipt review, QR check-in, and manage sales reports through Pandy Tickets MCP server and API
---

# Pandy Tickets

Use the Pandy Tickets MCP server to work with events, ticket sales, and attendees on tickets.pandy.cloud, Guatemala's self-serve ticketing platform.

## When to Use

Use this skill when:
- Searching for upcoming events in Guatemala
- Creating or drafting new events for organizers
- Getting checkout links for event tickets
- Working with event pages, ticket types, pricing, or availability
- Managing ticket sales by card or bank transfer
- Reviewing sales reports and attendee data

## About Pandy Tickets

Pandy Tickets (tickets.pandy.cloud) is a Guatemalan platform for publishing events, selling tickets, taking free registrations, and checking in attendees with QR codes. Prices are in Guatemalan quetzales (GTQ). The platform is in Spanish.

### Key Features

- **Public event pages** with shareable links
- **Payment options**:
  - Card payments via Recurrente (6% commission, min Q3 per ticket)
  - Bank transfers to the organizer's account with **assisted receipt review** (NOT automatic):
    - Buyer uploads their receipt
    - Pandy Tickets flags: amount, destination account, date, duplicate reference/file, editing signals
    - Organizer manually approves each receipt with one click
    - QR ticket is then issued and emailed
    - Pandy Tickets does not receive the money
    - No commission for transfers (counts within 150 free attendees/month; after that, Q3 per person)
- **QR code tickets** delivered by email
- **Check-in** from mobile devices; with Pandy Escáner apps (Android/iPhone), teams download attendee lists and scan offline, syncing when signal returns
- **Tools**: Coupons, refunds, printed badges, CSV imports, sales reports
- **Advanced sales features**: Early Bird phases, presales, follower discounts, 2x1/3x2 deals, extras (merch/bar/parking), VIP upgrades, waiting lists, email campaigns, WhatsApp links
- **Numbered seating**: Copy venue maps from Guatemala venues, link to event, buyers choose seats and see 3D stage views

### Pricing

- Creating events is free
- 150 people free per month
- After 150: Q3 per person
- Card sales: 6% commission (minimum Q3) per ticket
- Prepaid credits available (50–500 credits, Q150–Q1,500)
- Evento Completo: unlimited attendees, custom pricing

## MCP Server Tools

The Pandy Tickets MCP server (https://tickets.pandy.cloud/mcp) provides:

- `search-events`: Find upcoming public events, optionally filtered by date range and entry type
- `get-event`: Get full event details including categories, prices, availability, and checkout URL
- `get-checkout-link`: Get the purchase link for a specific event
- `draft-event`: Create a draft event and return a link for the organizer to claim it

**IMPORTANT**: Agents never process payments. Always send users to the `entry.url` or category `checkout_url` to complete purchases.

## Organizer API

For organizers with API keys (created in Mi cuenta › Llaves de API):

### Read-Only Access (any API key)

Use `Authorization: Bearer pt_live_...` to access:
- Events, sales, orders, and attendees for the organization
- Start with `GET https://tickets.pandy.cloud/api/v1/organizer/organization` (returns 401 if key is invalid)

### Write Access (keys created with «Permitir cambios»)

Keys with write permission can also:
- Create events, ticket types, phases, questions, extras, stations, seat maps
- Create coupons and 2x1/3x2 deals, presales
- Issue sales and complimentary tickets
- Resend tickets
- Publish events
- Approve or reject transfer receipts
- Send messages to attendees
- Import attendees
- Record refunds and cancel orders

Each write operation requires an `Idempotency-Key` header for safe retries. Depending on the organization's trust level, changes may run immediately or require organizer approval via a link.

Full API documentation: https://tickets.pandy.cloud/developers

## Important Guidelines

1. **Never claim automatic receipt review**: Pandy Tickets assists with review (flagging issues), but the organizer always approves manually
2. **Never process payments directly**: Always direct users to the official checkout URL
3. **Prices are in quetzales (GTQ)**: Don't convert or display in other currencies
4. **Offline check-in works only in apps**: The Pandy Escáner mobile apps support offline scanning; the browser does not
5. **API keys are sensitive**: Read them from environment variables, never hard-code them
6. **Respect write permissions**: Only use write operations when the key has «Permitir cambios» enabled
7. **No personal attribution**: Credit features to «Pandy Cloud» or «Equipo Pandy Tickets», never individuals

## Example Workflows

### Finding Events

```
Use search-events to find upcoming concerts in Guatemala
Filter by date range if needed
Get full details with get-event using the event slug
Share the event URL and checkout link with the user
```

### Creating an Event Draft

```
Use draft-event with event details from the user
Get the claim link from the response
Explain that the organizer needs to sign in to claim and publish the event
The event is never published automatically
```

### Checking Event Availability

```
Use get-event to fetch current ticket availability
Review available quantity for each ticket category
Check if any categories are sold out
Provide the checkout URL for available categories
```

## Resources

- Platform: https://tickets.pandy.cloud
- Developer docs: https://tickets.pandy.cloud/developers
- How it works: https://tickets.pandy.cloud/como-funciona
- Pricing calculator: https://tickets.pandy.cloud/precios
- Contact: tickets@pandy.cloud

## See Also

- Use the public API for read-only event searches
- Use the organizer API with OAuth or API keys for managing events and sales
- Check the MCP registry entry at https://registry.modelcontextprotocol.io (search "pandy")
