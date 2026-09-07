# Connect Meta Ads to Cursor

## 1. Open MCP settings

**Cursor Settings → MCP → Add new global MCP server**, or create `.cursor/mcp.json` in your project.

## 2. Add the server

```json
{
  "mcpServers": {
    "porter": { "url": "https://mcp.portermetrics.com/mcp" }
  }
}
```

## 3. Verify

The MCP settings panel shows `porter` with a green dot and its tool count.

## 4. Use it in Composer

```
Pull last month's Meta Ads spend by campaign and write it to a CSV.
```

Cursor asks to run the tool the first time — approve it.

## Troubleshooting

**Red dot.** Usually malformed JSON or a trailing slash on the URL.

**Tools listed but never called.** Cursor's Agent mode uses MCP tools; Chat mode may not. Switch to Agent.
