# Connect Meta Ads to Claude Desktop

## 1. Open your config file

- **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

Create it if it does not exist.

## 2. Add the server

```json
{
  "mcpServers": {
    "porter": { "url": "https://mcp.portermetrics.com/mcp" }
  }
}
```

Already have other MCP servers? Add `"porter"` as another key inside the existing `"mcpServers"` object — do not replace it.

## 3. Restart Claude Desktop

Quit completely and reopen. The tools icon appears in the chat input.

## 4. Connect your Meta account

Ask Claude:

```
List my Meta ad accounts
```

The first time, Porter returns an authorization link. Open it, log in with the Facebook account that has a role on the ad accounts, and grant access. Then ask again — your accounts will be listed.

## 5. First real query

```
How much did I spend on Meta ads last month, by campaign?
```

## Troubleshooting

**No tools icon.** Invalid JSON is the usual cause — check for a trailing comma. Restart fully, not just the window.

**"No accounts found".** The authorization did not complete, or the Facebook user has no role on any ad account in Business Manager. A personal profile with no assigned ad account exposes none.

**Accounts listed but queries return nothing.** Try a wider date range before concluding the account is empty — see [common errors](../reference/errors.md).
