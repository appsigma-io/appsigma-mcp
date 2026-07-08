# AppSigma MCP — installation instructions for LLM agents

AppSigma is a **remote** MCP server. There is nothing to clone, install, build or run locally. Setup is a single config entry pointing at the hosted endpoint.

- Transport: Streamable HTTP
- URL: `https://api.appsigma.io/mcp`
- Auth: `X-API-Key` header. Use the literal value `demo` if the user has no API key — it works without signup (with demo-mode limits).

## Cline

Add this entry to the `mcpServers` object in `cline_mcp_settings.json`:

```json
{
  "mcpServers": {
    "appsigma": {
      "type": "streamableHttp",
      "url": "https://api.appsigma.io/mcp",
      "headers": {
        "X-API-Key": "demo"
      }
    }
  }
}
```

If the user provides their own AppSigma API key, put it in place of `demo`.

## Verify

After the client reconnects, the server should list 21 tools (`get_application`, `search_applications`, `get_chart_positions`, …). A quick test call that works on the demo key:

- Tool: `get_chart_positions`
- Args: `{ "type": "FREE" }`

If tool calls return a 401 error, the `X-API-Key` header is missing or the key is invalid.
