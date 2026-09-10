# Connect it to your assistant

Open this section once, the first time you set up Meta Ads in the AI tool you already use — after that you never come back.

Every client below points at the same hosted server, so the only detail you need is this one line:

```
https://mcp.portermetrics.com/mcp
```

You sign in with the Facebook account that has a role on the ad account. No API keys, no Meta developer token, nothing to install or run.

| Client | Use this when… |
|---|---|
| [claude-desktop.md](claude-desktop.md) | You work in the Claude app on Mac or Windows — you edit one JSON file and restart. |
| [claude-code.md](claude-code.md) | You work in the terminal, or you want the server shared with a whole project via `.mcp.json`. |
| [chatgpt.md](chatgpt.md) | You work in ChatGPT — needs a paid plan and Developer mode turned on before the connector will save. |
| [cursor.md](cursor.md) | You work in Cursor — set it globally or per project, and use Agent mode so the tools actually get called. |
| [windsurf.md](windsurf.md) | You work in Windsurf — same JSON as the others, except the key is `serverUrl`. |
| [n8n.md](n8n.md) | You want this running unattended on a schedule — approve the login once by hand, then it runs on its own. |

> [!NOTE]
> After connecting, ask **"List my Meta ad accounts"** first. If nothing comes back, the login did not finish or that Facebook user has no role on any ad account in Business Manager.

## Videos & guides

| | |
|---|---|
| [![How to install the Meta Ads MCP in Claude](https://img.youtube.com/vi/m3ozKloLTko/hqdefault.jpg)](https://www.youtube.com/watch?v=m3ozKloLTko) | **[How to install the Meta Ads MCP in Claude](https://www.youtube.com/watch?v=m3ozKloLTko)** — Meta's own official MCP, step by step, and where the Porter Metrics MCP fits in when you need more than one ad platform in the same conversation. |
| [![How to use the official Meta Ads MCP with ChatGPT](https://img.youtube.com/vi/c_daxGadUBM/hqdefault.jpg)](https://www.youtube.com/watch?v=c_daxGadUBM) | **[How to use the official Meta Ads MCP with ChatGPT](https://www.youtube.com/watch?v=c_daxGadUBM)** — same setup, ChatGPT's Developer Mode. |
| [![How to connect Meta Ads to Claude — no code](https://img.youtube.com/vi/ooaKTMNictw/hqdefault.jpg)](https://www.youtube.com/watch?v=ooaKTMNictw) | **[How to connect Meta Ads (Facebook Ads) to Claude — no code](https://www.youtube.com/watch?v=ooaKTMNictw)** — the Porter Metrics connector itself, this repo's own subject. |
| [![How to make Meta ads with AI](https://img.youtube.com/vi/OoOCFBbFbJQ/hqdefault.jpg)](https://www.youtube.com/watch?v=OoOCFBbFbJQ) | **[How to make Meta ads with AI](https://www.youtube.com/watch?v=OoOCFBbFbJQ)** — generating the creative itself with Claude, once the connector is live. |

Written guides on portermetrics.com:

- **[Meta Ads connector for Claude (MCP)](https://portermetrics.com/en/connectors/claude/meta-ads/)** — the product page: what it reads, what it can do.
- **[Meta Ads MCP: 5 free ways to connect Meta Ads to Claude](https://portermetrics.com/en/tutorial/claude/chat-meta-ads/)** — the full setup walkthrough this section is based on.
