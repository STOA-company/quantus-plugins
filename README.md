# Quantus plugins — check a stock idea against real data, in your AI chat

**Quantus Research** lets Claude and Codex users test an investing idea on real Korean and US market data without writing code. Sign in to Quantus once, then ask in plain words — "backtest the 10 Korean stocks with the lowest PER, rebalanced monthly, over the longest period" — and get returns, drawdown and the exact period used. It is read-only: it never places orders, moves money or changes accounts. Past backtest results do not guarantee future returns, and Quantus does not give investment advice.

퀀터스 리서치는 Claude·Codex 안에서 투자 생각을 실제 국내·미국 데이터로 바로 검증합니다. 퀀터스에 한 번 로그인하고 «PER 낮은 국내 10종목 매달 바꾸면 가장 긴 기간 동안 어땠어?» 처럼 말하면, 수익률·최대 낙폭·실제로 쓴 기간을 보여 줍니다. 조회 전용이라 주문·이체·계좌 변경을 하지 않습니다. 과거 백테스트 결과는 미래 수익을 보장하지 않으며, 투자 권유가 아닌 정보 도구입니다.

## See it work (76 s)

[docs/demo/quantus-research-demo.mp4](docs/demo/quantus-research-demo.mp4) — Claude Code connected only to `quantus-research` (production): a Samsung Electronics backtest over the longest period, the 10 lowest-PER Korean stocks rebalanced monthly, and an order request that it declines because it has no order tools.

## Two plugins, one engine

| Plugin | Server | What it does | Where |
|---|---|---|---|
| `quantus-research` | `https://vibe-api.quantus.kr/mcp/research` | Read-only: backtests, metrics, prices, factors, data coverage | Official directories (Claude, ChatGPT/Codex) and this marketplace |
| `quantus` | `https://vibe-api.quantus.kr/mcp` | Everything above, plus turning an order sentence into a confirm-card link. Orders are never sent from chat: you press confirm on the Quantus screen yourself. | This marketplace only |

Install one of them, not both (the same account would sign in twice).

## Install

Claude Code:
```
/plugin marketplace add STOA-company/quantus-plugins
/plugin install quantus-research@quantus
```
Then `/mcp` → quantus-research → sign in once in the browser.

Codex:
```
codex plugin marketplace add STOA-company/quantus-plugins
codex plugin add quantus-research@quantus
codex mcp login quantus-research
```

claude.ai / Claude Desktop (tools only, no skills): Settings › Connectors › Add custom connector › `https://vibe-api.quantus.kr/mcp/research`.

More: [docs/INSTALL.md](docs/INSTALL.md) · Web guide: https://www.quantus.kr/ko/mcp

## Support and policies

Support https://www.quantus.kr/ko/support · Terms https://www.quantus.kr/ko/terms · Privacy https://stoa-investment.notion.site/21861431004880568c23d62d5421b2c5

No API keys or secrets are stored in this repository: sign-in is OAuth in your browser. Plugin files are MIT-licensed (see [LICENSE](LICENSE)); Quantus data and service are covered by the Quantus Terms.
