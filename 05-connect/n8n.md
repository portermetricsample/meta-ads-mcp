# Connect Meta Ads to n8n

## 1. Add an MCP Client node

In your workflow, add **MCP Client Tool** (`@n8n/n8n-nodes-langchain.mcpClientTool`).

## 2. Configure it

| Field | Value |
|---|---|
| Endpoint | `https://mcp.portermetrics.com/mcp` |
| Server Transport | HTTP Streamable |
| Authentication | None (Porter handles OAuth in-flow) |

A ready-made node is in [`configs/n8n_workflow.json`](../configs/n8n_workflow.json) — import it.

## 3. Attach it to an agent

Connect the MCP Client node to an **AI Agent** node's tool input. The agent can now call Porter's tools.

## 4. Example automation

**Schedule Trigger** (daily 08:00) → **AI Agent** + Porter MCP →
`"Pull yesterday's Meta Ads spend, impressions and link clicks by campaign"` →
**Slack** / **Google Sheets**.

## Troubleshooting

**Node reports no tools.** Check the endpoint has no trailing slash and the transport is HTTP Streamable, not SSE.

**Authorization loop.** The OAuth flow must be completed once interactively before an unattended schedule can use it.
