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

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
