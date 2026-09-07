# Meta Ads MCP — Facebook & Instagram ads for Claude, ChatGPT, Cursor and n8n

Ask your AI assistant a question in plain language and get real numbers out of your Meta ad account — or have it build, edit and pause campaigns without you opening Ads Manager. 500 metrics, 167 dimensions, full campaign create/edit/delete. OAuth login, no API keys, no Meta developer token, no server to run.

> [!IMPORTANT]
> **This is not a standalone MCP server.** It is the field, action and troubleshooting reference for the **Meta Ads connector inside the Porter Metrics MCP** — one hosted server, 30+ connectors. You install it once, at:
>
> ```
> https://mcp.portermetrics.com/mcp
> ```
>
> There is nothing in this repo to clone, install or run.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![MCP Protocol](https://img.shields.io/badge/MCP-Protocol-blue)](https://modelcontextprotocol.io)
[![Meta Ads](https://img.shields.io/badge/Meta%20Ads-Marketing%20API%20v25-0081FB?logo=meta&logoColor=white)](06-reference/all-fields.md)
[![Powered by Porter](https://img.shields.io/badge/Powered%20by-Porter%20Metrics-6C5CE7)](https://portermetrics.com)
[![Verified](https://img.shields.io/badge/catalog%20verified-2026--09--07-brightgreen)](06-reference/all-fields.md)

---

## Start here

Pick the job you actually have today. Every file inside is one job: the prompt to paste, the shape of what comes back, how to read it, and the one thing that quietly makes the answer wrong.

| Section | What it is for |
|---|---|
| **[01 · Reporting](01-reporting/)** | The work that runs on a schedule — last week's numbers by campaign, budget pacing, creative fatigue, alerts, and one question that spans Meta, Google and TikTok at once. |
| **[02 · Auditing](02-auditing/)** | Something is wrong, or an account you did not build just landed on your desk — where the money goes, what is working, who converts, whether the pixel is really firing, why delivery stopped. |
| **[03 · Research](03-research/)** | Reading ads you do not own. Any brand's live Meta ads by name, from the public Ad Library — no login, no partner access, nothing for them to approve. |
| **[04 · Ad management](04-ad-management/)** | Changing things instead of reading them — launch a campaign, move budgets and bids, pause and restart, build audiences and lookalikes, upload creative. Writes go to your account, created paused. |

## Connect it to your assistant

Same URL for every client. You sign in with the Facebook account that already has a role on the ad account.

| Client | Setup |
|---|---|
| Claude Desktop | [05-connect/claude-desktop.md](05-connect/claude-desktop.md) |
| Claude Code | [05-connect/claude-code.md](05-connect/claude-code.md) |
| ChatGPT | [05-connect/chatgpt.md](05-connect/chatgpt.md) |
| Cursor | [05-connect/cursor.md](05-connect/cursor.md) |
| Windsurf | [05-connect/windsurf.md](05-connect/windsurf.md) |
| n8n | [05-connect/n8n.md](05-connect/n8n.md) |

Paste-ready config files live in [`configs/`](configs/). Full walkthrough: [05-connect/](05-connect/).

## What it can read

**500 metrics and 167 dimensions** for Meta Ads alone — spend and delivery, four different click counts, roughly sixty cost variants, all ten standard pixel events each with a revenue twin, around eighty deduplicated `unique_*` fields, the full video funnel down to second-by-second retention, plus quality rankings, messaging, offline conversions and parsed UTMs.

The exact names, grouped by what they measure: [06-reference/all-fields.md](06-reference/all-fields.md).
What the connector can *do* — read, create, update, delete, upload, research: [06-reference/all-actions.md](06-reference/all-actions.md).

It is also not Meta-only. The same server covers Google Ads, GA4, Search Console, TikTok, LinkedIn, Shopify, HubSpot and 25+ other connectors, so "compare Meta and Google spend this month" is one question rather than two exports and a spreadsheet.

## What it cannot do

**[06-reference/what-it-cannot-do.md](06-reference/what-it-cannot-do.md)** — the verified list, each item with the workaround.

Publishing that list is deliberate. Finding out mid-build that something is missing costs more than reading it up front, and a feature list that only says yes is not worth trusting.

## FAQ

### Is there an MCP for Meta ads?
Yes — this one, and Meta ships an official one of its own. Side-by-side, including where this one loses: [06-reference/vs-meta-official.md](06-reference/vs-meta-official.md).

### Does Meta have an official MCP?
Yes, released April 2026. It is Meta-only and gated to accounts Meta has enabled. This one covers Meta plus 25 other connectors and is not subject to that rollout.

### Is there an MCP for Facebook ads?
Facebook and Instagram ads live in the same Meta ad account, so yes — this is it.

### Do I need a Meta developer token or an app review?
No. You log in with OAuth once.

### Does it work with ChatGPT?
Yes, on a paid plan with Developer mode on: [05-connect/chatgpt.md](05-connect/chatgpt.md).

### Can it create and edit campaigns, or only read?
Both. Campaigns, ad sets and ads are created paused, so nothing spends until you deliberately turn it on: [04-ad-management/](04-ad-management/).

### Can I see a competitor's ads without access to their account?
Yes, from Meta's public Ad Library — you get the ads, not their spend or results: [03-research/](03-research/).

### Something came back as an error. Where do I look?
Real Meta errors and subcodes with the fix: [06-reference/errors.md](06-reference/errors.md).

## Found something wrong?

Field descriptions drift and platforms change. If a prompt here fails, a field behaves differently than documented, or a limit we publish is no longer true — [open an issue](../../issues) with the question you asked and the response you got.

## License

MIT — see [LICENSE](LICENSE).

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc. "Meta", "Facebook" and "Instagram" are trademarks of Meta Platforms, Inc., used here only to identify the platform this connector reads.*
