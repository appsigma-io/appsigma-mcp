# AppSigma MCP — installation instructions for LLM agents

AppSigma runs two **remote** MCP servers. There is nothing to clone, install, build or run locally. Setup is a config entry per server pointing at the hosted endpoint.

| Name | URL | Use it for |
|------|-----|------------|
| `appsigma` | `https://appsigma.io/mcp` | The user's own AppSigma organization: tracked apps, keywords, positions, competitors, review analysis |
| `appsigma-data` | `https://api.appsigma.io/mcp` | Public App Store data on any app: metadata, reviews, ratings, charts, prices |

- Transport: Streamable HTTP for both.
- Auth: OAuth for both. On first use the client opens AppSigma in the browser, the user signs in (or signs up with an email) and approves. Nothing to paste.
- `appsigma-data` also accepts an `X-API-Key` header. Use the literal value `demo` if the client has no OAuth support or the user just wants to try it: it works without an account, with demo-mode limits.

## Cline

Add these entries to the `mcpServers` object in `cline_mcp_settings.json`:

```json
{
  "mcpServers": {
    "appsigma": {
      "type": "streamableHttp",
      "url": "https://appsigma.io/mcp"
    },
    "appsigma-data": {
      "type": "streamableHttp",
      "url": "https://api.appsigma.io/mcp",
      "headers": {
        "X-API-Key": "demo"
      }
    }
  }
}
```

`appsigma` needs OAuth. If the client cannot complete the OAuth sign-in, install only `appsigma-data` with the `demo` key, and replace `demo` with the user's API key from https://appsigma.io when they have one.

## Verify

- `appsigma` lists 18 tools (`get_account`, `list_tracked_apps`, `add_keywords`, …). Test call: `get_account` with no arguments.
- `appsigma-data` lists 22 tools (`get_application`, `search_applications`, `get_chart_positions`, …). Test call that works on the demo key: `get_chart_positions` with `{ "type": "FREE" }`.

A 401 error means the sign-in did not complete, or the `X-API-Key` header is missing or invalid.
