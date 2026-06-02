<p align="center">
  <img src="./logo.png" width="120" height="120" alt="Intentions" />
</p>

<h1 align="center">Intentions MCP Server</h1>

Personalized timing intelligence for AI agents. Ask *"Should I do X on this date?"* and
get a 0–100 alignment score, a clear verdict, and the reasoning behind it — grounded in the
user's personal energy profile and the Five Elements framework.

Built for agentic workflows: trip planning, product launches, content calendars,
interview/meeting scheduling, negotiation prep, and relationship/family timing.

- **Homepage:** https://www.intentions.me
- **MCP endpoint:** `https://mcp.intentions.me/mcp` (Streamable HTTP)

---

## What it does

You give it a decision and a time window; it returns a structured reading your agent can
reason over and explain in plain language:

- **Score** (0–100) and a **verdict** (e.g. *favorable*, *proceed with caution*, *wait*)
- **Friction** (0–100) — an independent measure of execution resistance
- **Element breakdown** and per-layer (year / month / day / hour) signals
- **Adverse alerts** with actionable, behavioral guidance — never event predictions

Chain the tools to narrow from "which year" → "which month" → "which day" → "which hour".

---

## Tools

| Tool | What it answers | Tier |
|------|-----------------|------|
| `intentions_ask_year` | A full calendar year as a whole | Free |
| `intentions_ask_month` | A specific month, or the best month in a window (≤12 months) | Free |
| `intentions_ask_day` | A specific date, comparison, or best day in a range (≤31 days) | Free |
| `intentions_ask_hour` | Best hour within a day; morning vs afternoon | **Pro** |
| `intentions_energy_chart` | ASCII chart overview — `weekly` / `yearly` (free), `hourly` (**Pro**) | Mixed |
| `intentions_set_birth_info` | Register or update the user's birth date / time / gender | Free |
| `intentions_get_profile` | Read the currently stored birth info | Free |

All timing inputs must fall within `currentYear − 1 … currentYear + 1`.

---

## Installation

The server is **remote** (Streamable HTTP) — nothing to install or self-host.

1. Create an account at https://www.intentions.me
2. Generate an API key from your account page (format: `itm_…`)
3. Add the server to your MCP client using the config below

### Claude Desktop / MCP client config

```json
{
  "mcpServers": {
    "intentions": {
      "type": "http",
      "url": "https://mcp.intentions.me/mcp",
      "headers": {
        "Authorization": "Bearer itm_your_api_key_here"
      }
    }
  }
}
```

### claude.ai custom connector

Add a custom connector with:

- **URL:** `https://mcp.intentions.me/mcp`
- **Authentication:** Bearer token — paste your `itm_…` key

---

## Authentication

Every request authenticates with a Bearer API key in the `Authorization` header:

```
Authorization: Bearer itm_0123456789abcdef0123456789abcdef
```

Keys are issued per account at https://www.intentions.me/account. Treat the key like a
password — it carries your quota and your stored energy profile.

---

## Pricing

| | Free | Pro |
|---|------|-----|
| Day / month / year readings | 5 per day (resets midnight UTC) | Unlimited |
| Hour-by-hour precision (`ask_hour`, hourly charts) | — | ✓ |
| Weekly / yearly charts | ✓ | ✓ |

The free tier is enough to evaluate the server end-to-end. See
https://www.intentions.me/pricing for current Pro pricing.

---

## Links

- **Homepage:** https://www.intentions.me
- **Pricing:** https://www.intentions.me/pricing

---

*This repository contains documentation only. The Intentions MCP Server is a hosted,
proprietary service; the implementation source is not open source.*
