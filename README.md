# Howseen MCP server

Ask Claude, ChatGPT, Cursor or Codex how your brand shows up in AI answers, and act on it, without leaving your AI assistant.

[Howseen](https://howseen.ai) tracks which brands ChatGPT, Gemini, Perplexity, Google AI Overviews and Google AI Mode recommend on the questions your buyers ask, which sources those engines cite, and writes the content to win the spots you are missing. This repository documents its remote MCP server.

- **Server URL:** `https://app.howseen.ai/api/mcp` (Streamable HTTP, remote, nothing to install)
- **Auth:** `Authorization: Bearer <your Howseen API key>`
- **Docs:** https://howseen.ai/mcp
- **Get a key:** Howseen dashboard > Settings > API & AI assistants ([3-day free trial](https://app.howseen.ai/signup))

## Connect your AI assistant

Replace `hs_live_YOUR_KEY` with your key.

**Claude Code**

```bash
claude mcp add --scope user --transport http howseen https://app.howseen.ai/api/mcp --header "Authorization: Bearer hs_live_YOUR_KEY"
```

**Cursor** (`~/.cursor/mcp.json`)

```json
{
  "mcpServers": {
    "howseen": {
      "url": "https://app.howseen.ai/api/mcp",
      "headers": { "Authorization": "Bearer hs_live_YOUR_KEY" }
    }
  }
}
```

**Codex**

```bash
export HOWSEEN_API_KEY=hs_live_YOUR_KEY
codex mcp add howseen --url https://app.howseen.ai/api/mcp --bearer-token-env-var HOWSEEN_API_KEY
```

**Claude.ai and ChatGPT** (custom connector): these apps can only send the key inside the URL.

```
https://app.howseen.ai/api/mcp?key=hs_live_YOUR_KEY
```

Treat that URL like a password: do not share it or show it on screen, and revoke the key in Settings if it leaks.

## What you can ask

- "What is my AI visibility this month, per engine?"
- "On which buyer questions does ChatGPT name a competitor and not us?"
- "Which sites does AI cite when we lose? Where should we get listed first?"
- "What changed since the last scan?"
- "Draft an article for the question we lose the most, then publish it to our site."

## Tools

**Read** (any key)

| Tool | What it returns |
|---|---|
| `list_brands` | The brands (websites) tracked in the account |
| `get_visibility` | % of AI answers that name the brand, share of voice, average position, sentiment, per engine, with the trend |
| `list_prompts` | Tracked buyer questions with per-question visibility, engines and cited domains |
| `get_competitors` | Brand vs competitors in AI answers, overall and per engine |
| `get_top_sources` | Domains and URLs AI engines cite most on the brand's questions |
| `search_responses` | Real AI answers, with excerpts, brands named and cited URLs |
| `get_action_plan` | Prioritized actions to raise AI visibility |
| `get_prompt_gaps` | Questions where AI names a competitor but not the brand |
| `get_easiest_wins` | Third-party pages cited in the answers the brand loses, ranked |
| `get_changes` | What changed between the last two scans |
| `suggest_prompts` | Buyer questions worth tracking that are not tracked yet |
| `list_articles` | Articles Howseen wrote for the brand, with status and URL |
| `get_article_performance` | Published articles with indexing status, impressions and clicks |
| `get_usage` | Plan, quotas used and left, API limits |

**Actions** (key with actions enabled; every action previews first and only applies with `confirm: true`)

`add_prompts`, `archive_prompts`, `remove_prompts`, `add_competitor`, `remove_competitor`, `mark_action_done`, `dismiss_action`, `draft_article`, `refresh_article`, `publish_article`, `request_indexing`, `create_share_report`, `delete_article`, `restore_article`.

`publish_article` sends a written article to the brand's connected site (WordPress, Shopify, Ghost, BigCommerce, webhook) or its Howseen-hosted blog.

## REST API

The same data is available as a read-only JSON API:

```bash
curl -H "Authorization: Bearer hs_live_YOUR_KEY" https://app.howseen.ai/api/v1/brands
curl -H "Authorization: Bearer hs_live_YOUR_KEY" "https://app.howseen.ai/api/v1/brands/BRAND_ID/visibility?from=2026-09-01&engine=chatgpt"
```

## Pricing

The MCP server and the API are included in the Pro plan (79 € a month) and the Business plans, and in the 3-day free trial. See https://howseen.ai/pricing.

## Support

Questions or issues: open an issue here or write to raphael@howseen.ai.
