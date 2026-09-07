# Connect Meta Ads to Claude Code

## Add the server

```bash
claude mcp add porter --transport http https://mcp.portermetrics.com/mcp
```

## Verify

```bash
claude mcp list
```

`porter` should appear as connected.

## Authorize

```
> List my Meta ad accounts
```

Open the authorization link Porter returns, grant access, then ask again.

## Scope it to a project

Add to `.mcp.json` in the project root to share the server with your team:

```json
{
  "mcpServers": {
    "porter": { "type": "http", "url": "https://mcp.portermetrics.com/mcp" }
  }
}
```

## Troubleshooting

**Server shows as failed.** Run `claude mcp remove porter` then re-add. Check the URL has no trailing slash.

**Tools not available mid-session.** MCP tools load at session start. Restart the session after adding.
