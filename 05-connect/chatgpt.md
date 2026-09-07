# Connect Meta Ads to ChatGPT

Requires a ChatGPT plan with connector support (Plus, Pro, Business or Enterprise).

## 1. Open connector settings

**Settings → Connectors → Advanced → Developer mode**, then **Create**.

## 2. Add the server

| Field | Value |
|---|---|
| Name | `Porter — Meta Ads` |
| MCP Server URL | `https://mcp.portermetrics.com/mcp` |
| Authentication | OAuth |

## 3. Connect

ChatGPT opens Porter's authorization flow. Log in with the Facebook account that has access to your ad accounts.

## 4. Use it

Enable the connector in the composer, then:

```
List my Meta ad accounts, then show last month's spend by campaign.
```

## Troubleshooting

**Connector will not save.** Developer mode must be on. The URL must be exactly `https://mcp.portermetrics.com/mcp`.

**Tools not offered in a chat.** Enable the connector explicitly for that conversation.
