# Quantus Research — check a stock idea against real data

Quantus Research lets you test an investing idea on real Korean and US market data from Claude or Codex, without writing code. Sign in to Quantus once, then ask in plain words — for example "backtest Samsung Electronics over the longest period" or "show me Samsung Electronics' PER over the last year" — and get returns, maximum drawdown and the exact period used, or the metric values you asked for.

It is read-only. It never places orders, moves money, or changes your accounts or strategies. Past backtest results do not guarantee future returns, and Quantus does not give investment advice.

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

claude.ai / Claude Desktop (tools only): Settings › Connectors › Add custom connector › `https://vibe-api.quantus.kr/mcp/research`.

## What you can ask

- Backtest a stock-selection rule on Korean stocks, or a strategy on Korean and US stocks, over the longest available period.
- Look up a company's metrics (PER, PBR, ROE and more) and how they changed.
- Check prices, factors, and which data fields and periods are available.

## 한국어

퀀터스 리서치는 Claude·Codex 안에서 투자 생각을 실제 국내·미국 데이터로 검증합니다. 퀀터스에 한 번 로그인하고 «삼성전자 가장 긴 기간으로 백테스트» 처럼 말하면 수익률·최대 낙폭·쓴 기간을 보여 줍니다. 조회 전용이라 주문·이체·계좌 변경을 하지 않습니다. 과거 백테스트 결과는 미래 수익을 보장하지 않으며, 투자 권유가 아닌 정보 도구입니다.

Support https://www.quantus.kr/ko/support · Terms https://www.quantus.kr/ko/terms · Privacy https://stoa-investment.notion.site/21861431004880568c23d62d5421b2c5
