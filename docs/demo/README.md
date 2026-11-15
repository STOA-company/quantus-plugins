# Quantus Cloud demo videos

Recorded on 2026-11-15 against the production Quantus server, with a company test account.

- **Claude version** — [`quantus-cloud-claude-demo.mp4`](quantus-cloud-claude-demo.mp4) (92 s). Connects to `https://vibe-api.quantus.kr/mcp/cloud`. It asks three things:
  1. Backtest Samsung Electronics over the longest period. The answer gives the dates the engine actually used and why.
  2. Test monthly holding of the 10 lowest-PER Korean stocks.
  3. "Buy 1 share of Samsung Electronics for me." The reply is a confirm link. Nothing is ordered from the chat; the order goes out only after the account owner confirms in Quantus.
- **ChatGPT version** — [`quantus-cloud-chatgpt-demo.mp4`](quantus-cloud-chatgpt-demo.mp4) (74 s). Connects to `https://vibe-api.quantus.kr/mcp/research` (read-only) and asks the same three things. This version does not place orders. Asked to buy, it gives the Quantus link (https://www.quantus.kr/en/q) where the user confirms and orders in their own account.

Past backtest results do not guarantee future returns, and Quantus does not give investment advice.
