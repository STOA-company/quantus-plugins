# Quantus Cloud

Quantus Cloud connects Claude Code, Claude and Codex to your Quantus account through one remote MCP server, `quantus-cloud` (`https://vibe-api.quantus.kr/mcp`). Sign in once in the browser (OAuth). No key is stored in any plugin file.

What you can ask in plain words:

- **Test an idea on real data** — "backtest the 10 Korean stocks with the lowest PER, rebalanced monthly, over the longest period". You get the return, the maximum drawdown and the exact dates used.
- **Look up data** — Korean and US stock metrics, prices, factors and data coverage.
- **Run your own trading bot on Quantus Cloud** — upload a bot bundle, start it, read its logs and status, and stop it. These tools appear once Quantus Cloud opens to customers.
- **Turn an order sentence into a confirm card** — "buy 1 share of Samsung Electronics in my account" returns a confirm link. Nothing is ordered from the chat: the order goes out only after you press confirm on the Quantus screen, in your own account.

Install on Claude Code: `/plugin marketplace add STOA-company/quantus-plugins`, then `/plugin install quantus-cloud@quantus`, then `/mcp` and sign in. On Codex: `codex plugin marketplace add STOA-company/quantus-plugins`, `codex plugin add quantus-cloud@quantus`, `codex mcp login quantus-cloud`. Full steps: [docs/INSTALL.md](../../docs/INSTALL.md).

Past backtest results do not guarantee future returns, and Quantus does not give investment advice. Support: https://www.quantus.kr/ko/support · Terms: https://www.quantus.kr/ko/terms · Privacy: https://stoa-investment.notion.site/21861431004880568c23d62d5421b2c5
