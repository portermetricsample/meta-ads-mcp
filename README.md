# Meta Ads MCP — Facebook & Instagram ads for Claude, ChatGPT, Cursor and n8n

Ask your AI assistant a question in plain language and get real numbers out of your Meta ad account — or have it build, edit and pause campaigns without you opening Ads Manager. 1,205 metrics, 167 dimensions, full campaign create/edit/delete. OAuth login, no API keys, no Meta developer token, no server to run.

<p align="center">
  <a href="https://www.youtube.com/watch?v=m3ozKloLTko">
    <img src="https://img.youtube.com/vi/m3ozKloLTko/maxresdefault.jpg" alt="Watch: connecting Meta Ads to Claude, and where Porter fits in" width="720">
  </a>
  <br>
  <sub><b>▶ Watch:</b> connecting Meta Ads to Claude, and where the Porter Metrics MCP fits in when you need more than one ad platform in the same conversation. More videos and setup guides in <a href="connect/#videos--guides">connect/</a>.</sub>
</p>

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![MCP Protocol](https://img.shields.io/badge/MCP-Protocol-blue)](https://modelcontextprotocol.io)
[![Meta Ads](https://img.shields.io/badge/Meta%20Ads-Marketing%20API%20v25-0081FB?logo=meta&logoColor=white)](reference/all-fields.md)
[![Powered by Porter](https://img.shields.io/badge/Powered%20by-Porter%20Metrics-6C5CE7)](https://portermetrics.com)
[![Verified](https://img.shields.io/badge/catalog%20verified-2026--09--10-brightgreen)](reference/all-fields.md)

> [!IMPORTANT]
> **This is not a standalone MCP server.** It is the field, action and troubleshooting reference for the **Meta Ads connector inside the Porter Metrics MCP** — one hosted server, 30+ connectors. You install it once, at:
>
> ```
> https://mcp.portermetrics.com/mcp
> ```
>
> There is nothing in this repo to clone, install or run.

---

## Connect it to your assistant

Same URL for every client. You sign in with the Facebook account that already has a role on the ad account.

| Client | Setup |
|---|---|
| Claude Desktop | [connect/claude-desktop.md](connect/claude-desktop.md) |
| Claude Code | [connect/claude-code.md](connect/claude-code.md) |
| ChatGPT | [connect/chatgpt.md](connect/chatgpt.md) |
| Cursor | [connect/cursor.md](connect/cursor.md) |
| Windsurf | [connect/windsurf.md](connect/windsurf.md) |
| n8n | [connect/n8n.md](connect/n8n.md) |

## Use cases

Pick the job you actually have today. Every file inside is one job: the prompt to paste, the shape of what comes back, how to read it, and the one thing that quietly makes the answer wrong. Each use case carries its own `skills/` folder — ready-made instructions your assistant loads before it starts, so the traps on these pages are avoided by default rather than remembered. [How to use a skill →](use-cases/README.md#how-to-use-a-skill)

| Use case | What it is for |
|---|---|
| **[Ad management](use-cases/ad-management/)** | Changing things instead of reading them — launch a campaign, move budgets and bids, pause and restart, build audiences and lookalikes, upload creative. Writes go to your account, created paused. |
| **[Reporting](use-cases/reporting/)** | The work that runs on a schedule — last week's numbers by campaign, budget pacing, creative fatigue, alerts, and one question that spans Meta, Google and TikTok at once. |
| **[Creative research](use-cases/creative-research/)** | Reading ads you do not own. Any brand's live Meta ads by name, from the public Ad Library — no login, no partner access, nothing for them to approve. |
| **[Audits](use-cases/audits/)** | Something is wrong, or an account you did not build just landed on your desk — where the money goes, what is working, who converts, whether the pixel is really firing, why delivery stopped. |


## What it can read

**1,205 metrics and 167 dimensions** for Meta Ads alone — spend and delivery, four different click counts, over 125 cost-per variants, all ten standard pixel events each with a revenue twin, 180 deduplicated `unique_*` fields, the full video funnel down to second-by-second retention, plus quality rankings, messaging, offline conversions and parsed UTMs.

The exact names, grouped by what they measure: [reference/all-fields.md](reference/all-fields.md).
What the connector can *do* — read, create, update, delete, upload, research: [reference/all-actions.md](reference/all-actions.md).

It is also not Meta-only. The same server covers Google Ads, GA4, Search Console, TikTok, LinkedIn, Shopify, HubSpot and 25+ other connectors, so "compare Meta and Google spend this month" is one question rather than two exports and a spreadsheet.

## What it cannot do

**[reference/what-it-cannot-do.md](reference/what-it-cannot-do.md)** — the verified list, each item with the workaround.

Publishing that list is deliberate. Finding out mid-build that something is missing costs more than reading it up front, and a feature list that only says yes is not worth trusting.

## FAQ

### Is there an MCP for Meta ads?
Yes — this is it: the Meta Ads connector inside the Porter Metrics MCP, one hosted server covering Meta plus 25+ other platforms.

### Does Meta have an official MCP?
Yes, released April 2026. It is Meta-only and gated to accounts Meta has enabled. This one covers Meta plus 25 other connectors and is not subject to that rollout.

### Is there an MCP for Facebook ads?
Facebook and Instagram ads live in the same Meta ad account, so yes — this is it.

### Do I need a Meta developer token or an app review?
No. You log in with OAuth once.

### Does it work with ChatGPT?
Yes, on a paid plan with Developer mode on: [connect/chatgpt.md](connect/chatgpt.md).

### Can it create and edit campaigns, or only read?
Both. Campaigns, ad sets and ads are created paused, so nothing spends until you deliberately turn it on: [use-cases/ad-management/](use-cases/ad-management/).

### Can I see a competitor's ads without access to their account?
Yes, from Meta's public Ad Library — you get the ads, not their spend or results: [use-cases/creative-research/](use-cases/creative-research/).

### Something came back as an error. Where do I look?
Real Meta errors and subcodes with the fix: [reference/errors.md](reference/errors.md).

## Found something wrong?

Field descriptions drift and platforms change. If a prompt here fails, a field behaves differently than documented, or a limit we publish is no longer true — open an issue on this repository with the question you asked and the response you got.

## License

MIT — see [LICENSE](LICENSE).

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc. "Meta", "Facebook" and "Instagram" are trademarks of Meta Platforms, Inc., used here only to identify the platform this connector reads.*
