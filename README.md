# Meta Ads MCP — Facebook & Instagram ads for Claude, ChatGPT, Cursor and n8n

> **This is not a standalone MCP server.** It is the complete field, action and troubleshooting reference for the **Meta Ads connector inside the Porter Metrics MCP** — one hosted server, 30+ connectors. Install it once at [`mcp.portermetrics.com/mcp`](https://mcp.portermetrics.com/mcp); there is no package to clone from this repo.

> **Meta Ads (Facebook + Instagram) MCP server — read campaign performance and manage campaigns from any AI assistant. 500 metrics, 167 dimensions, full campaign CRUD. Hosted remote MCP, OAuth login, no API keys, no developer token, no self-hosting.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![MCP Protocol](https://img.shields.io/badge/MCP-Protocol-blue)](https://modelcontextprotocol.io)
[![Meta Ads](https://img.shields.io/badge/Meta%20Ads-Marketing%20API%20v25-0081FB?logo=meta&logoColor=white)](#available-fields)
[![Powered by Porter](https://img.shields.io/badge/Powered%20by-Porter%20Metrics-6C5CE7)](https://portermetrics.com)
[![Verified](https://img.shields.io/badge/catalog%20verified-2026--09--07-brightgreen)](docs/FIELDS.md)

---

## What is this?

An MCP server that connects **Meta Ads — Facebook and Instagram** to Claude, ChatGPT, Cursor, Windsurf, n8n and any other MCP client. Ask questions in plain language and get real numbers from your ad account; create and edit campaigns without opening Ads Manager.

It is **hosted and remote**. There is nothing to install, no Meta developer token to request, no app review, and no server to run.

## Why this exists

Meta's Marketing API is powerful and unfriendly. Getting a single number out of it normally means an app, a system user, a token, and a week of reading docs. This removes all of that: you log in with OAuth once, and your assistant can read the account.

It is also **not Meta-only**. The same Porter MCP covers Google Ads, GA4, TikTok, LinkedIn, Shopify, HubSpot and 25+ connectors — so "compare Meta and Google spend this month" is one question, not two exports and a spreadsheet.

## Works with

| Client | Status | Guide |
|---|---|---|
| Claude Desktop | ✅ | [docs/SETUP_CLAUDE.md](docs/SETUP_CLAUDE.md) |
| Claude Code | ✅ | [docs/SETUP_CLAUDE_CODE.md](docs/SETUP_CLAUDE_CODE.md) |
| ChatGPT | ✅ | [docs/SETUP_CHATGPT.md](docs/SETUP_CHATGPT.md) |
| Cursor | ✅ | [docs/SETUP_CURSOR.md](docs/SETUP_CURSOR.md) |
| Windsurf | ✅ | [docs/SETUP_WINDSURF.md](docs/SETUP_WINDSURF.md) |
| n8n | ✅ | [docs/SETUP_N8N.md](docs/SETUP_N8N.md) |

## Quick start

```json
{
  "mcpServers": {
    "porter": { "url": "https://mcp.portermetrics.com/mcp" }
  }
}
```

Then ask: **"List my Meta ad accounts."**

Full per-client instructions are in [`docs/`](docs/), paste-ready files in [`configs/`](configs/).

## What you can ask it

```
How much did I spend on Meta ads last month, by campaign?
Which placement had the cheapest cost per link click?
Break my Meta spend down by age and gender.
Which of my ads stopped delivering, and why?
Compare Meta and Google Ads spend for the last 30 days.
Create a paused Traffic campaign targeting Colombia, 25–54.
Upload this image and build an ad from it.
```

More, with real outputs: [docs/EXAMPLES.md](docs/EXAMPLES.md)

## Available fields

**500 metrics and 167 dimensions** for Meta Ads alone — the full catalog is in [docs/FIELDS.md](docs/FIELDS.md), including:

- Spend, impressions, reach, frequency
- Four distinct click types — all clicks, unique, link clicks, outbound
- ~60 cost variants: CPC, CPM, CPP, cost per link click, cost per result
- All 10 standard pixel events **plus a revenue twin for each**
- ~80 deduplicated `unique_*` variants
- Video funnel: 3-second plays, ThruPlays, 25/50/75/95/100%, and 17 second-by-second retention fields
- Offline conversions, messaging conversions, quality rankings

## Competitor research — no account needed

The same server reads **any brand's live Meta ads** from the public Ad Library by name, with no access to their account:

```
Show me every ad Nike is running on Meta right now, deduplicated.
Audit my three biggest competitors' Meta creative and tell me what they all do that I don't.
```

Actions: `meta_ads_research.run_audit`, `meta_ads_research.publish_report`. There is a Google equivalent (`google_ads_research.*`) that reads the Ads Transparency Center.

## Tools

Campaign, ad set, ad and creative CRUD; audiences and lookalikes; asset upload; insights with breakdowns.
Full list with parameters: [docs/TOOLS.md](docs/TOOLS.md)

## Limitations

We publish what it **cannot** do, verified against the live connector: [docs/LIMITATIONS.md](docs/LIMITATIONS.md)

## Troubleshooting

Real errors and their fixes, including Meta's less obvious subcodes: [docs/TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md)

## How this compares

An independent, receipt-backed comparison against **Meta's own official Ads MCP** — 58 tests, including where this server loses: [docs/COMPARISON.md](docs/COMPARISON.md)

## Other Porter MCP servers

Google Ads · Google Analytics 4 · Google Search Console · TikTok Ads · LinkedIn Ads · Shopify · HubSpot · Klaviyo · Amazon Seller · and more — see [porter-mcp](https://github.com/portermetricsample/porter-mcp).

## FAQ

**Is there an MCP for Meta ads?** Yes — this one, and Meta ships an official one. [The comparison](docs/COMPARISON.md) covers both.

**Does Meta have an official MCP?** Yes, released April 2026. It is Meta-only and gated to accounts Meta has enabled. This server covers Meta plus 25 other connectors and is not subject to that rollout.

**Is there an MCP for Facebook?** Facebook and Instagram ads are the same Meta Ads account, so yes — this is it.

**Do I need a Meta developer token?** No. OAuth login only.

**Does it work with ChatGPT?** Yes — [docs/SETUP_CHATGPT.md](docs/SETUP_CHATGPT.md).

## License

MIT — see [LICENSE](LICENSE).

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc. "Meta", "Facebook" and "Instagram" are trademarks of Meta Platforms, Inc., used here only to identify the platform this connector reads.*
