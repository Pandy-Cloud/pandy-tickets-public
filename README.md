# Pandy Tickets - Agent Skill & Plugin

Official agent skill, plugin and MCP server for [Pandy Tickets](https://tickets.pandy.cloud), Guatemala's self-serve ticketing platform for events.

**[Website](https://tickets.pandy.cloud)** · **[Create your free account](https://tickets.pandy.cloud/register)** · **[Pricing](https://tickets.pandy.cloud/pricing)** · **[How it works](https://tickets.pandy.cloud/como-funciona)** · **[Pandy Tickets + AI](https://tickets.pandy.cloud/ia)** · **[Developers](https://tickets.pandy.cloud/developers)**

MCP endpoint: `https://tickets.pandy.cloud/mcp` (Streamable HTTP, public, no API key)

## What is Pandy Tickets?

Pandy Tickets is a Guatemalan platform where organizers publish events, sell tickets (by card or bank transfer), take free registrations, and check people in at the door with QR codes. Prices are in Guatemalan quetzales (GTQ).

### Key Features

- 🎫 **Public event pages** with shareable links
- 💳 **Flexible payment options**: Credit card or bank transfer
- 📱 **QR code check-in** from mobile devices
- 📊 **Sales reports** and attendee management
- 🎭 **Numbered seating** with 3D venue previews
- 🎟️ **Early Bird pricing**, presales, coupons, and waiting lists
- 📧 **Email campaigns** to followers
- 🔄 **Offline check-in** with Pandy Escáner mobile apps (Android & iPhone)

### Pricing

- **Free**: 150 attendees per month
- **Q3 per person** after 150 attendees
- **6% commission** (min Q3) for card payments
- **No commission** for bank transfers
- **Evento Completo**: Unlimited attendees with custom pricing

Bank transfer payments include **assisted receipt review**: Pandy Tickets flags issues (amount, destination account, duplicates, date) but the organizer always manually approves each receipt with one click.

[Learn more about pricing →](https://tickets.pandy.cloud/pricing)

## Installation

### Any MCP client (Claude, ChatGPT, Cursor, LobeHub, …)

Add a remote MCP server with this URL. No key or sign-in needed:

```
https://tickets.pandy.cloud/mcp
```

Or in an `mcpServers` config:

```json
{
  "mcpServers": {
    "pandy-tickets": {
      "type": "streamable-http",
      "url": "https://tickets.pandy.cloud/mcp"
    }
  }
}
```

Organizers who want to read their own events, sales and attendees can connect the OAuth organizer server at `https://tickets.pandy.cloud/mcp/organizer` instead.

### For Hermes Agent

```bash
hermes plugins install pandy-tickets
```

### For Other Coding Agents (via skills.sh)

```bash
npx skills add Pandy-Cloud/pandy-tickets-public
```

Choose the skills and coding agents to install to.

## What This Package Provides

This package includes:

1. **MCP Server Connection** (`mcp.json`): Connect to Pandy Tickets' official MCP server at `https://tickets.pandy.cloud/mcp`
2. **Plugin Manifest** (`plugin.json`): Standard Agent Plugins v1 package metadata
3. **LobeHub Manifest** (`lhm.plugin.json`): Listing for the [LobeHub](https://lobehub.com) MCP marketplace
4. **Agent Skill** (`skills/pandy-tickets/SKILL.md`): Comprehensive instructions for using Pandy Tickets features

### Available MCP Tools

- `search-events`: Find upcoming events in Guatemala
- `get-event`: Get full event details, pricing, and availability
- `get-checkout-link`: Get the purchase URL for an event
- `draft-event`: Create a draft event for an organizer to claim

**No authentication required** for public event searches. Organizers can use API keys for managing their own events and sales.

## Usage

Once installed, your agent can:

- Search for upcoming events in Guatemala
- Get event details, ticket prices, and availability
- Generate checkout links for ticket purchases
- Create event drafts that organizers can claim
- Access sales reports and attendee data (with organizer API keys)

### Example Queries

- "Find upcoming concerts in Guatemala"
- "What events are happening in Guatemala City this weekend?"
- "Create a draft event for my conference"
- "Get the checkout link for [event name]"

## Documentation

- **Platform**: [tickets.pandy.cloud](https://tickets.pandy.cloud)
- **How It Works**: [tickets.pandy.cloud/como-funciona](https://tickets.pandy.cloud/como-funciona)
- **Developer Docs**: [tickets.pandy.cloud/developers](https://tickets.pandy.cloud/developers)
- **MCP Registry**: [registry.modelcontextprotocol.io](https://registry.modelcontextprotocol.io/v0/servers?search=pandy)

## API Access

### Public API (No Authentication)

- Search events: `GET https://tickets.pandy.cloud/api/v1/events`
- Event details: `GET https://tickets.pandy.cloud/api/v1/events/{slug}`

[OpenAPI specification →](https://tickets.pandy.cloud/developers)

### Organizer API (Requires API Key)

Organizers can create API keys in **Mi cuenta › Llaves de API**:

- **Read-only keys**: Access events, sales, orders, and attendees
- **Write keys** (with «Permitir cambios»): Create events, manage tickets, approve receipts, import attendees, and more

Use `Authorization: Bearer pt_live_...` header for authenticated requests.

[Full API documentation →](https://tickets.pandy.cloud/developers)

## Important Notes

- **Agents never process payments**: Always direct users to the official checkout URL
- **Prices are in quetzales (GTQ)**: Don't convert to other currencies
- **Receipt review is assisted, not automatic**: Pandy Tickets flags issues, but organizers manually approve receipts
- **Offline check-in**: Works only in Pandy Escáner mobile apps (Android/iPhone), not in browsers
- **API keys are sensitive**: Store securely, never commit to repositories

## Support

- **Email**: tickets@pandy.cloud
- **Instagram**: [@pandytickets.gt](https://instagram.com/pandytickets.gt)
- **Facebook**: [Pandy Tickets](https://facebook.com/pandytickets.gt)
- **LinkedIn**: [Pandy Tickets](https://linkedin.com/company/pandy-tickets)

## License

MIT License - see [LICENSE](LICENSE) file for details.

---

## Español

### ¿Qué es Pandy Tickets?

Pandy Tickets es la plataforma guatemalteca de autoservicio para publicar eventos, vender boletos por tarjeta o transferencia bancaria, recibir registros gratuitos y controlar el acceso con códigos QR.

### Características principales

- Páginas públicas para cada evento
- Pago por tarjeta (6%, mínimo Q3 por entrada) o transferencia con revisión asistida
- Entradas con código QR que llegan por correo
- Escáner en la puerta desde el teléfono (apps con modo offline)
- Asientos numerados con vista 3D del escenario
- Early Bird, preventa, cupones, 2x1/3x2 y mejora a VIP
- Reportes de venta y herramientas de marketing

### Precios

- 150 personas gratis al mes
- Después, Q3 por persona
- Con tarjeta: 6% de comisión (mínimo Q3)
- Sin comisión por transferencia

[Crea tu cuenta gratis →](https://tickets.pandy.cloud/register) · [Precios →](https://tickets.pandy.cloud/pricing) · [Cómo funciona →](https://tickets.pandy.cloud/como-funciona)

---

**Made by Pandy Cloud** 🇬🇹
