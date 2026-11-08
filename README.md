# UptimeRobot MCP server

Review monitor health then create an approved HTTP monitor. Read provider data first, then explicitly approve the selected change with operator write opt-in and a unique per-call approval key.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `UPTIMEROBOT_API_KEY`



Credential help: https://uptimerobot.com/blog/introducing-the-uptimerobot-v3-api/

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call list_monitors '{"limit":10}'
```

## Use with an MCP client

Launch `node /absolute/path/uptimerobot-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| list_monitors | Read | List monitors. |
| get_monitor | Read | Get monitor. |
| create_http_monitor | Explicit approval required | Create http monitor. |

## Concrete workflow

Review monitor health then create an approved HTTP monitor. Read provider data first, then explicitly approve the selected change with operator write opt-in and a unique per-call approval key.

1. list_monitors
2. get_monitor
3. create_http_monitor

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Import with PipMCP](https://pipmcp.com/github/start?integration=openapi-to-mcp&utm_source=github&utm_campaign=github-uptimerobot-mcp&utm_content=readme) when you want the hosted service. This provider is not currently listed as a managed template. Import selected-openapi.json (REST) or the official GraphQL schema linked in provenance, configure authentication, and review the tools before execution. Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/uptimerobot/).

## Provenance and maintenance

- https://uptimerobot.com/blog/introducing-the-uptimerobot-v3-api/
- https://raw.githubusercontent.com/uptimerobot/uptimerobot-cli/main/openapi/openapi.yaml

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
