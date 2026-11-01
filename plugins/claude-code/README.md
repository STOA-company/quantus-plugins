# Quantus plugin (Claude in Quantus · Codex in Quantus)

This plugin connects Claude Code, Claude cowork and Codex to your Quantus account through one remote MCP server, `quantus`. Log in once in the browser (OAuth). No key is stored in any plugin file.

What you can ask in plain words:

- Run a backtest over the longest period the Quantus data covers.
- Look at Korean and US stock data and financial metrics inside the chat.
- Turn an order sentence into a confirm card. You press confirm on the Quantus screen; nothing is ordered from the chat.

Install on Claude Code: `/plugin marketplace add <owner>/<repo>` then `/plugin install quantus@quantus`, then `/mcp` and log in. On Codex: `codex plugin marketplace add <owner>/<repo>`, `codex plugin add quantus@quantus`, `codex mcp login quantus`. Full steps: docs/INSTALL.md at the repository root.

Quantus is not investment advice. Backtest and mock results can differ from real-account performance. Support: https://www.quantus.kr/ko/support, info@quantus.kr.
