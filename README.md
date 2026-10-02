# AutoFire plugin for Grok

Gives Grok read-only access to one car dealership's data on [AutoFire](https://www.goautofire.com): inventory, lead workflow, test drives, LotIQ follow-up priorities, and the daily insights report, through AutoFire's hosted MCP server.

## Install

**Grok Build:** install `autofire` from the xAI plugin marketplace.

**Grok on the web or mobile:** open [grok.com/connectors](https://grok.com/connectors), select **New Connector → Custom**, and enter `https://mcp.goautofire.com/mcp`.

Either way, the first connection opens AutoFire in your browser. Sign in as a dealership owner or admin, choose the dealership Grok may read, pick the permissions, and select **Allow**. There is no API key to paste.

Full guide: [docs.goautofire.com/mcp/grok](https://docs.goautofire.com/mcp/grok).

## What it ships

- `.mcp.json`: the hosted Streamable HTTP server at `https://mcp.goautofire.com/mcp`.
- `skills/autofire-dealership/SKILL.md`: how to use the tools well.

No hooks, commands, agents, or local code.

## Network endpoints and credentials

- `https://mcp.goautofire.com/mcp`: the MCP server (Streamable HTTP).
- `https://mcp.goautofire.com/.well-known/oauth-protected-resource/mcp`: OAuth discovery, which points at AutoFire's Supabase Auth issuer for dynamic client registration, authorization, token exchange, and refresh (OAuth 2.1, PKCE S256).
- `https://www.goautofire.com/oauth/consent`: where the user signs in and approves access.

Credentials: an AutoFire account that owns or administers the dealership. Tokens are short-lived and refreshed by Grok; the dealership can disconnect Grok at any time under **Dashboard → MCP & API** in AutoFire.

## Tools

| Tool | Returns |
| --- | --- |
| `get_dealership_profile` | Business profile, hours, location |
| `search_inventory` | Up to 50 vehicles per call; no VINs |
| `get_vehicle` | One vehicle's details |
| `list_leads` | Lead workflow records without contact details |
| `list_followup_priorities` | Leads due for follow-up, with reasons |
| `get_lead` | One lead with contact details, only with the Lead contact details permission |
| `list_test_drives` | Test-drive requests without customer contact details |
| `get_dealership_insights` | Recent daily insight reports |

Every tool is read-only (`readOnlyHint: true`) and fixed to the dealership chosen at sign-in.

## License

The plugin files in this repository are MIT licensed. Use of the AutoFire service is governed by the [AutoFire Terms](https://www.goautofire.com/terms) and [Privacy Policy](https://www.goautofire.com/privacy).
