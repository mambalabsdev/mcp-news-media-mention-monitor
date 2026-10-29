# News and Media Mention Monitor MCP Server

[![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-news-media-mention-monitor)](https://www.npmjs.com/package/@mambalabsdev/mcp-news-media-mention-monitor) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-news-media-mention-monitor)](https://github.com/mambalabsdev/mcp-news-media-mention-monitor/blob/main/LICENSE)

<a href="https://mcprush.com/to/mcp-news-media-mention-monitor?ref=badge"><img width="380" height="200" src="https://mcprush.com/badge/mcp-news-media-mention-monitor/card.svg" alt="News and Media Mention Monitor MCP server" /></a>

An MCP server for the Mamba Labs News and Media Mention Monitor actor on Apify. Give it company names, brands, people, or topics. It reads Google News for each one and returns one row per article: headline, outlet, date, the publisher's own URL and domain, and a headline sentiment label. With only_new on, a repeat call with the same state_key returns only articles it has not returned before.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Your keys](#your-keys)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Each news.google.com link is resolved to the article's URL on the publisher's site. An article found by two of your search terms comes back once. When a run returns no article, one free summary row says why: nothing matched, everything was returned before, or Google News did not answer. All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-news-media-mention-monitor": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-news-media-mention-monitor"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `monitor_news_mentions` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "What did the news say about Gong and Salesloft this week?"
- "Find news articles about our company from the last 30 days and list the outlets."
- "Any negative headlines about Acme Robotics since my last check?"

## Tool

`monitor_news_mentions`. One tool. Example arguments:

```json
{
  "queries": ["\"Acme Robotics\""],
  "since_days": "7",
  "state_key": "acme-weekly"
}
```

## Inputs

Every buyer facing input of the actor, unchanged. Omitted inputs take the actor's own defaults. Numbers and yes or no values are sent as strings.

| Input | Type | Description |
|---|---|---|
| `queries` | array | 1 to 50 search terms. Required |
| `exclude_terms` | array | Up to 20 words to leave out |
| `since_days` | string | Days back, 1 to 90. Default 7 |
| `country` | string | Google News country edition. Default US |
| `language` | string | Language code. Default en |
| `resolve_publisher_url` | string | true (default) or false |
| `only_new` | string | true (default) or false |
| `state_key` | string | Name for this watch list |
| `max_articles` | string | Per search term, 1 to 100. Default 50 |
| `max_charge_usd` | string | Optional cap on the run's cost |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `article-row`, per article returned | $0.0023 | $0.002185 | $0.00207 | $0.001955 |
| `apify-actor-start`, per run start | $0.0015 | $0.0015 | $0.0015 | $0.0015 |

An article skipped by only_new is not charged. A summary row is free.

## Your keys

The actor needs no key and holds none. Proxy traffic adds nothing to your price: Mamba Labs pays the platform costs of the run.

## Full actor documentation

[apify.com/mambalabs/news-media-mention-monitor](https://apify.com/mambalabs/news-media-mention-monitor)

## License

MIT. See [LICENSE](LICENSE).
