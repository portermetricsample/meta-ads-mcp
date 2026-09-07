# Connect Meta Ads to Windsurf

## 1. Open the MCP config

**Windsurf Settings → Cascade → Model Context Protocol → Add Server**, or edit `~/.codeium/windsurf/mcp_config.json`.

## 2. Add the server

```json
{
  "mcpServers": {
    "porter": { "serverUrl": "https://mcp.portermetrics.com/mcp" }
  }
}
```

Windsurf uses `serverUrl`, not `url`.

## 3. Refresh

Click refresh in the MCP panel. `porter` appears with its tools.

## 4. Use it

```
Show me Meta Ads performance by placement for the last 30 days.
```

## Troubleshooting

**Server not appearing.** Confirm the key is `serverUrl`. Restart Windsurf after editing the file.
