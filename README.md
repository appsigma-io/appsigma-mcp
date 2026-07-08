# AppSigma MCP Server

App Store intelligence for LLMs — apps, reviews, rankings, developers, in-app purchases, price history, editorial features and in-app events, straight from the [AppSigma API](https://docs.appsigma.io).

This is a **hosted (remote) MCP server** — nothing to install or run. It speaks Streamable HTTP at:

```
https://api.appsigma.io/mcp
```

Authentication is the same `X-API-Key` header the REST API uses. Try it instantly with the built-in demo key `demo` (no signup), or [get a real API key](https://appsigma.io) for full access.

## Setup

### Cline

Add to your Cline MCP settings (`cline_mcp_settings.json`):

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

Replace `demo` with your API key when you have one.

### Claude Code

```bash
claude mcp add --transport http appsigma https://api.appsigma.io/mcp --header "X-API-Key: demo"
```

### Claude Desktop / Cursor / other MCP clients

Any client that supports remote Streamable HTTP servers works with the same URL and header:

```json
{
  "mcpServers": {
    "appsigma": {
      "type": "http",
      "url": "https://api.appsigma.io/mcp",
      "headers": { "X-API-Key": "demo" }
    }
  }
}
```

## Tools

One tool per REST endpoint — every call is authenticated, rate-limited and billed credits exactly like the REST route it wraps. Credit costs are stated in each tool description.

### Search & catalog
| Tool | Description |
|------|-------------|
| `search_applications` | Search the App Store by term (proxies iTunes Search). |
| `list_applications` | List/filter the application catalog (by ids, term, filters; paginated). |

### Applications
| Tool | Description |
|------|-------------|
| `get_application` | One application by id, full detail. |
| `get_application_reviews` | Customer reviews (paginated, filterable by country). |
| `get_application_versions` | Version/release history. |
| `get_application_similars` | Similar apps. |
| `get_application_in_app_purchases` | In-app purchases. |
| `get_application_price_changes` | Price change history. |
| `get_application_editorial_items` | App Store editorial stories featuring the app. |
| `get_application_events` | In-app events of the app. |
| `get_application_chart_history` | Chart position history. |
| `get_application_rating_histogram` | Star-rating histogram over time. |
| `get_application_ratings_by_version` | Ratings broken down by version. |
| `get_application_review_histogram` | Review-count histogram. |

### Charts
| Tool | Description |
|------|-------------|
| `get_chart_positions` | Current App Store chart positions by chart/genre/country. |
| `get_chart_history` | Historical chart data across apps. |

### Developers
| Tool | Description |
|------|-------------|
| `get_developer` | One developer (publisher) by id. |
| `get_developer_applications` | A developer's applications. |
| `get_developer_events` | In-app events across a developer's apps. |

### Editorial & events
| Tool | Description |
|------|-------------|
| `get_editorial_item` | One App Store editorial story by id. |
| `get_event` | One App Store in-app event by id. |

## Demo mode

The `demo` key is free and needs no signup. It is limited to a curated set of applications and developers, a fixed set of search terms, shallow chart depth, and a per-IP rate limit — enough to explore every tool. A paid key removes all of those limits.

## Links

- API documentation: https://docs.appsigma.io
- Get an API key: https://appsigma.io
