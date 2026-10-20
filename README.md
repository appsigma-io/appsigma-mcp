# AppSigma MCP — App Store ASO for your AI agent

**[appsigma.io/agent](https://appsigma.io/agent)** · [Docs](https://docs.appsigma.io) · [Pricing](https://appsigma.io/pricing)

Connect Claude, ChatGPT, Cursor or any MCP client to your App Store data. Your agent reads your keywords, search positions, competitors and reviews, and tells you what to change to climb. It can also research any app in the store: reviews, ratings, charts, prices and release history.

Two hosted MCP servers. Nothing to install or run: add a URL, sign in, approve.

| Server | URL | What it does | Cost |
|--------|-----|--------------|------|
| **Your apps** | `https://appsigma.io/mcp` | Track apps, add keywords, follow daily search positions, manage competitors, read store activity and review analysis | Your plan limits apply; the free plan works |
| **The whole App Store** | `https://api.appsigma.io/mcp` | 22 read-only tools: metadata, reviews, ratings, chart history, prices and in-app purchases of any app | Credits, 1,000 free on a new account |

Both servers sign in with OAuth: your client opens AppSigma, you approve, done. No key to paste. The App Store server also accepts an `X-API-Key` header, and the key `demo` works without an account.

## Ask your agent

- "Which keywords am I closest to the top 10 for, and which should I add?"
- "Find the keywords I can win and rewrite my App Store subtitle with them."
- "What moved this week, and what should I change first?"
- "Compare me with my competitors and tell me where I fall behind."
- "What do the 1-star reviews of my top 3 competitors complain about?"
- "Which apps climbed the top free chart this week, and what did they change?"

## Connect

### Claude (claude.ai, Claude Desktop)

Settings → Connectors → **Add custom connector**. Paste `https://appsigma.io/mcp`, press Connect and approve. Repeat with `https://api.appsigma.io/mcp`.

### ChatGPT

Settings → Apps & Connectors (developer mode on) → add a custom connector. Paste each URL and choose OAuth. ChatGPT opens AppSigma for you to approve.

### Claude Code

```bash
claude mcp add --transport http appsigma https://appsigma.io/mcp
claude mcp add --transport http appsigma-data https://api.appsigma.io/mcp
```

Or install this repo as a plugin, which adds both servers and the `aso-teardown` skill:

```bash
claude plugin marketplace add appsigma-io/appsigma-mcp
claude plugin install appsigma@appsigma-mcp
```

### Cursor

Settings → MCP → Add new server, or add to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "appsigma": { "url": "https://appsigma.io/mcp" },
    "appsigma-data": { "url": "https://api.appsigma.io/mcp" }
  }
}
```

### Gemini CLI

```bash
gemini extensions install https://github.com/appsigma-io/appsigma-mcp
```

### Cline and other clients

Any client that supports remote Streamable HTTP servers works with the two URLs above. A client without OAuth can use the App Store server with an API key:

```json
{
  "mcpServers": {
    "appsigma-data": {
      "type": "streamableHttp",
      "url": "https://api.appsigma.io/mcp",
      "headers": { "X-API-Key": "demo" }
    }
  }
}
```

Replace `demo` with your key from [appsigma.io](https://appsigma.io) for full access.

## Tools

### Your apps — `https://appsigma.io/mcp`

Every app tool takes the App Store id of an app your organization tracks.

| Tool | Kind | What it does |
|------|------|--------------|
| `get_account` | read | Your plan, used and maximum apps and keywords, markets |
| `search_apps` | read | Find an app by name or App Store URL |
| `track_apps` | write | Start tracking apps (finds their keywords and competitors) |
| `untrack_app` | destructive | Stop tracking an app |
| `list_tracked_apps` | read | Your apps with visibility, 7-day change, average position |
| `get_app_overview` | read | ASO summary: movers, ranking distribution, top competitors |
| `suggest_keywords` | read | Keywords the app ranks for or could win, with traffic and difficulty |
| `list_keywords` | read | Tracked keywords with position, previous position, traffic, difficulty |
| `add_keywords` | write | Track up to 50 keywords |
| `remove_keywords` | destructive | Stop tracking keywords |
| `get_keyword_history` | read | Daily positions and the top apps for one search |
| `get_position_changes` | read | Keywords that moved in the last days, biggest change first |
| `list_competitors` | read | Your app and its saved competitors side by side |
| `suggest_competitors` | read | Competitor suggestions with overlapping keywords |
| `add_competitor` | write | Save a competitor |
| `remove_competitor` | destructive | Delete a saved competitor |
| `get_store_activity` | read | Versions with release notes, and in-app events |
| `get_review_insights` | read | Review analysis: sentiment, topics, praise, reviews that need a reply |

### The whole App Store — `https://api.appsigma.io/mcp`

All tools are read-only. Each call is billed in credits like the [REST endpoint](https://docs.appsigma.io) it wraps; the cost is in each tool description.

| Tool | What it does |
|------|--------------|
| `search_applications` | Search the App Store by term |
| `list_applications` | List and filter the app catalog |
| `get_application` | One app, full detail |
| `get_application_reviews` | Customer reviews, filterable by country |
| `get_application_versions` | Version and release history |
| `get_application_similars` | Similar apps |
| `get_application_in_app_purchases` | In-app purchases |
| `get_application_price_changes` | Price change history |
| `get_application_editorial_items` | App Store editorial stories featuring the app |
| `get_application_events` | In-app events of the app |
| `get_application_chart_history` | Chart position history |
| `get_application_rating_histogram` | Star-rating histogram over time |
| `get_application_ratings_by_version` | Ratings by version |
| `get_application_review_histogram` | Review-count histogram |
| `get_chart_positions` | Current chart positions by chart, genre and country |
| `get_chart_history` | Chart history across apps |
| `get_developer` | One developer |
| `get_developer_applications` | A developer's apps |
| `get_developer_events` | In-app events across a developer's apps |
| `get_editorial_item` | One editorial story |
| `get_event` | One in-app event |
| `get_usage` | Your plan, credits left and recent usage (free) |

### Demo key

`X-API-Key: demo` needs no account. It covers a curated set of apps and developers, a fixed set of search terms, shallow chart depth and a per-IP rate limit — enough to try every tool.

## Links

- Setup page: https://appsigma.io/agent
- API documentation: https://docs.appsigma.io
- Pricing: https://appsigma.io/pricing
- Privacy policy: https://appsigma.io/privacy
- Terms: https://appsigma.io/terms
- Support: mcp@appsigma.io

AppSigma is not affiliated with Apple Inc. Data comes from the public App Store.
