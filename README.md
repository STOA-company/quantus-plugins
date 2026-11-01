# Quantus plugins — Claude in Quantus · Codex in Quantus

퀀터스를 Claude Code·Codex 안에서 씁니다. 한 번 로그인하면 말로 묻습니다:
- 가장 긴 기간 백테스트(«PER 낮고 ROE 높은 20종목 매달 바꾸면?»)
- 국내·미국 주식 데이터(«삼성전자 최근 5일 종가»)
- 주문 문장 → 퀀터스 화면의 확인 카드(채팅에서 주문을 내지 않습니다 — 사람이 퀀터스 화면에서 직접 확인)

## 설치
Claude Code:
```
/plugin marketplace add STOA-company/quantus-plugins
/plugin install quantus@quantus
```
Codex: `codex mcp add quantus --url https://vibe-api.quantus.kr/mcp` 또는 이 저장소의 `.agents/plugins/marketplace.json`.
자세한 안내: [docs/INSTALL.md](docs/INSTALL.md) · 웹 안내: https://www.quantus.kr/ko/mcp

## 무엇이 들어 있나
`plugins/claude-code` 한 폴더를 Claude Code·Codex 가 같이 씁니다 — 원격 MCP 서버 `quantus`(OAuth 로그인, 파일에 키 없음)와 스킬 셋(quantus-backtest·quantus-data·quantus-order).

지원 https://www.quantus.kr/ko/support · 약관 https://www.quantus.kr/ko/terms · 투자 권유가 아닌 정보 도구입니다.
