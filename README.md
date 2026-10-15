<p align="center"><img src="assets/logo.png" width="160" alt="Trisport"></p>

# Trisport MCP Server

Connect **ChatGPT, Claude, Perplexity, Cursor, VS Code** or any MCP client to **[Trisport.ro](https://www.trisport.ro)** — a sports store in Romania for running, cycling, swimming, triathlon and outdoor.

This repository holds the documentation only. The server is hosted by Trisport; there is nothing to install.

| | |
|---|---|
| **Server URL** (catalog without sign-in; account tools ask to sign in) | `https://www.trisport.ro/mcp` |
| **Account-first URL** (sign-in on connect — Claude, Perplexity) | `https://www.trisport.ro/mcp/cont` |
| Transport | Streamable HTTP |
| Auth | OAuth 2.1 (PKCE, dynamic client registration, client ID metadata documents) — only for account tools |
| Registry | `ro.trisport/store` in the official MCP Registry |
| Docs & privacy | https://www.trisport.ro/mcp/docs/ |
| Customer guide (Romanian) | https://www.trisport.ro/asistent-ai/ |

## Tools

| Tool | What it does |
|---|---|
| `search_products` | Search the live catalog: only products that can be bought now, price in RON (VAT incl.), discount, delivery estimate, sizes, link. Filters: max price, size. |
| `get_product` | One product: description, every size with its own stock and delivery estimate, other colors. |
| `get_recommendations` | Products other customers buy together, matching accessories. |
| `create_cart_link` | A link that opens the trisport.ro cart with the chosen products. Nothing is ordered or paid by the assistant. |
| `store_info` | Contact, store address, delivery / returns / terms pages. |
| `get_my_orders` 🔐 | The customer's recent orders: status, total, courier tracking link. |
| `get_order` 🔐 | One order with live parcel tracking from the courier and the link to start a return. |
| `get_loyalty_points` 🔐 | Available and pending loyalty points and their value. |
| `get_wishlist` 🔐 / `add_to_wishlist` 🔐 | Read the wishlist / add a product to it. |

🔐 = requires the customer to connect their Trisport account (sign-in on trisport.ro, then an explicit *Allow*). The assistant never sees the password and cannot place orders, pay or change account details.

## Connect

**Claude** — Settings → Connectors → Add custom connector → URL `https://www.trisport.ro/mcp/cont` → Authentication *Sign in now*, OAuth client *Use Claude's published identity* → Add → Connect.

**ChatGPT** — Plugins → **+** → *Add custom MCP server* → Name `Trisport`, Connection URL `https://www.trisport.ro/mcp` (OAuth is discovered automatically). Submitted to the ChatGPT plugin directory.

**Claude Code**
```bash
claude mcp add --transport http trisport https://www.trisport.ro/mcp/cont
```

**VS Code** (`.vscode/mcp.json`)
```json
{"servers": {"trisport": {"type": "http", "url": "https://www.trisport.ro/mcp"}}}
```

**Cursor** (`~/.cursor/mcp.json`)
```json
{"mcpServers": {"trisport": {"url": "https://www.trisport.ro/mcp"}}}
```

**Gemini CLI** (`~/.gemini/settings.json`)
```json
{"mcpServers": {"trisport": {"httpUrl": "https://www.trisport.ro/mcp"}}}
```

## Example prompts

- "Find women's trail running shoes at Trisport under 700 lei in size 38."
- "What sizes of the Garmin Forerunner 165 are in stock at Trisport, and how fast is delivery?"
- "Put a pair of CEP compression running socks from Trisport in my cart."
- "Show my Trisport orders and where my parcel is."

## Support

Trisport Online SRL · [contact@trisport.ro](mailto:contact@trisport.ro) · [trisport.ro/contact](https://www.trisport.ro/contact/)
