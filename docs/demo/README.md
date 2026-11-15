# Quantus Cloud demo videos

Recorded on 2026-11-15 against the production Quantus server, with a company test account. Both videos are shown in Claude Code.

- **Claude version** — [`quantus-cloud-claude-demo.mp4`](quantus-cloud-claude-demo.mp4) (92 s). Connects to `https://vibe-api.quantus.kr/mcp/cloud`. It asks three things:
  1. Backtest Samsung Electronics over the longest period. The answer gives the dates the engine actually used and why.
  2. Test monthly holding of the 10 lowest-PER Korean stocks.
  3. "Buy 1 share of Samsung Electronics for me." The reply is a link that pre-fills the order in Quantus. Nothing is ordered from the chat: the order goes out only after the account owner sends it and confirms in Quantus.
- **Read-only version (the ChatGPT package)** — [`quantus-cloud-chatgpt-demo.mp4`](quantus-cloud-chatgpt-demo.mp4) (74 s). This video uses the same skills as the ChatGPT package and the read-only server `https://vibe-api.quantus.kr/mcp/research`, shown in Claude Code. It asks the same three things. This version does not place orders. Asked to buy, it gives the Quantus link (https://www.quantus.kr/en/q), where the user confirms and orders in their own account.

About question 2:
- In the Claude version run, the model added a "PER > 0" condition, so loss-making stocks were excluded. The shared result shows this condition.
- In the read-only run, no such condition was added. For this period both runs returned the same holdings and numbers.

Past backtest results do not guarantee future returns, and Quantus does not give investment advice.
