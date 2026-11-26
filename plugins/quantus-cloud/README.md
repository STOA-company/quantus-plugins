# Quantus Cloud

Quantus Cloud connects Claude Code, Claude and Codex to your Quantus account through one remote MCP server, `quantus-cloud` (`https://vibe-api.quantus.kr/mcp/cloud`). Sign in once in the browser (OAuth). No key is stored in any plugin file.

What you can ask in plain words:

- **Test an idea on real data** — "backtest the 10 Korean stocks with the lowest PER, rebalanced monthly, over the longest period". You get the return, the maximum drawdown and the exact dates used.
- **Look up data** — Korean and US stock metrics, prices, factors and data coverage.
- **Rent a Quantus Cloud instance for your own code** — upload your code to an instance, start it, read its logs and status, and stop it. Instances are in preparation; these tools appear once Quantus Cloud opens to customers.
- **Turn an order sentence into a confirm card** — "buy 1 share of Samsung Electronics in my account" returns a confirm link. Nothing is ordered from the chat. Orders go out only after you press confirm on the Quantus screen; they are then placed in your own brokerage account (Korea Investment & Securities or DB Securities) through the official brokerage API you connected in Quantus.

Install on Claude Code: `/plugin marketplace add STOA-company/quantus-plugins`, then `/plugin install quantus-cloud@quantus`, then `/mcp` and sign in. On Codex: `codex plugin marketplace add STOA-company/quantus-plugins`, `codex plugin add quantus-cloud@quantus`, `codex mcp login quantus-cloud`. Full steps: [docs/INSTALL.md](../../docs/INSTALL.md).

## Additional first-party endpoints referenced by skills

In chat, all tool calls go only to the declared remote MCP server `quantus-cloud` (`https://vibe-api.quantus.kr/mcp/cloud`) via OAuth. This plugin contains no local scripts, hooks, or executable code.

- **Quantus Data API (`https://vibe-api.quantus.kr/v1/...`)** — When a user asks to download raw daily prices or datasets into their own local Python environment, the `quantus-data` skill provides example Python snippets for the first-party Quantus Data API using a Quantus API key configured locally by the user (never pasted into chat, stored in plugin files, or sent to `/mcp/cloud`).
- **Quantus web pages (`https://www.quantus.kr/ko/q`, `https://www.quantus.kr/en/q`, `https://www.quantus.kr/ko/support`)** — Skills link users to Quantus Q for interactive analysis or automated strategies and to Quantus Support when needed.

Past backtest results do not guarantee future returns, and Quantus does not give investment advice. Support: https://www.quantus.kr/ko/support · Terms: https://www.quantus.kr/ko/terms · Privacy: https://stoa-investment.notion.site/21861431004880568c23d62d5421b2c5
