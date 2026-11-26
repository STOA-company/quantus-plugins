# Quantus Cloud — test a stock idea and confirm your orders from your AI chat

**Quantus Cloud** lets Claude and Codex users test an investing idea on real Korean and US market data without writing code and turn an order sentence into a confirm card. Cloud instance tools (rent an instance to upload and run your own code: upload, start, logs, status, stop) appear once Quantus Cloud opens to customers. Sign in to Quantus once, then ask in plain words — "backtest the 10 Korean stocks with the lowest PER, rebalanced monthly, over the longest period" — and get returns, drawdown and the exact period used. Orders go out only after you press confirm on the Quantus screen; they are then placed in your own brokerage account (Korea Investment & Securities or DB Securities) through the official brokerage API you connected in Quantus. Past backtest results do not guarantee future returns, and Quantus does not give investment advice.

퀀터스 클라우드는 Claude·Codex 안에서 투자 생각을 실제 국내·미국 데이터로 바로 검증하고, 주문 문장을 확인 카드로 바꿔 줍니다. 내 코드를 올려 돌리는 클라우드 인스턴스는 준비 중입니다. 퀀터스에 한 번 로그인하고 «PER 낮은 국내 10종목 매달 바꾸면 가장 긴 기간 동안 어땠어?» 처럼 말하면, 수익률·최대 낙폭·실제로 쓴 기간을 보여 줍니다. 주문은 퀀터스 화면에서 확인을 눌러야만 나갑니다. 그때 고객이 퀀터스에 연결한 증권사(한국투자증권·DB증권)의 공식 API를 통해 본인 계좌에서 주문이 나갑니다. 과거 백테스트 결과는 미래 수익을 보장하지 않으며, 투자 권유가 아닌 정보 도구입니다.

## What it does

| Plugin | Server | Tools |
|---|---|---|
| `quantus-cloud` | `https://vibe-api.quantus.kr/mcp/cloud` | Backtests, metrics, prices, factors, data coverage · cloud instances for your own code (upload, start, logs, status, stop — appear once Quantus Cloud opens to customers) · order confirm cards (orders go out only after you press confirm on the Quantus screen, placed in your own Korea Investment & Securities or DB Securities account through the official brokerage API you connected in Quantus) |

## Install

Claude Code:
```
/plugin marketplace add STOA-company/quantus-plugins
/plugin install quantus-cloud@quantus
```
Then `/mcp` → quantus-cloud → sign in once in the browser.

Codex:
```
codex plugin marketplace add STOA-company/quantus-plugins
codex plugin add quantus-cloud@quantus
codex mcp login quantus-cloud
```

claude.ai / Claude Desktop (tools only, no skills): Settings › Connectors › Add custom connector › `https://vibe-api.quantus.kr/mcp/cloud`.

Installed the older `quantus` or `quantus-research` plugin, or added `https://vibe-api.quantus.kr/mcp/research` as a custom connector? Remove it first, then install `quantus-cloud` (otherwise you sign in twice).

More: [docs/INSTALL.md](docs/INSTALL.md) · Web guide: https://www.quantus.kr/ko/mcp

## Support and policies

Support https://www.quantus.kr/ko/support · Terms https://www.quantus.kr/ko/terms · Privacy https://stoa-investment.notion.site/21861431004880568c23d62d5421b2c5

No API keys or secrets are stored in this repository: sign-in is OAuth in your browser. Plugin files are MIT-licensed (see [LICENSE](LICENSE)); Quantus data and service are covered by the Quantus Terms.
