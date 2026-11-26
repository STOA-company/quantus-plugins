# 설치 · Install — Quantus Cloud


서버 등록은 **플러그인이 하는 한 곳뿐**이다. 플러그인을 쓸 때 `claude mcp add` 를 따로 하지 않는다(같은 서버가 두 번 등록되어 로그인을 두 번 하게 된다).

## 한국어

플러그인 이름은 `quantus-cloud` 하나다. 서버 `https://vibe-api.quantus.kr/mcp/cloud`: 조회·백테스트 · 퀀터스 클라우드 인스턴스 대여(내 코드 올리기·시작·로그·상태·멈추기 — 퀀터스 클라우드가 고객에게 열리면 보임) · 주문 확인 카드(퀀터스 화면에서 본인이 «확인» 을 눌러야 주문이 나감).

### Claude Code
    /plugin marketplace add STOA-company/quantus-plugins
    /plugin install quantus-cloud@quantus

그다음 `/mcp` → quantus-cloud → 인증(브라우저에서 퀀터스 로그인 한 번). 이제 이렇게 말해 보세요.
- «삼성전자 가장 긴 기간으로 백테스트»
- «국내 반도체 PER 하위 10종목 백테스트, 가능한 가장 긴 기간으로»
- «내 계좌로 삼성전자 1주 사 줘» → 확인 카드 링크가 나옵니다. 퀀터스 화면에서 직접 확인을 눌러야 주문이 나갑니다.
- «내 노트북 파이썬에서 퀀터스 데이터 받는 법»

다른 주소로 붙이려면 Claude Code 를 시작하기 전에 `export QUANTUS_MCP_URL=<MCP 주소>` (기본은 `https://vibe-api.quantus.kr/mcp/cloud`).
플러그인 없이 MCP 만 쓰려면 한 줄: `claude mcp add --transport http quantus-cloud https://vibe-api.quantus.kr/mcp/cloud` (플러그인과 같이 쓰지 않는다).

### Codex
    codex plugin marketplace add STOA-company/quantus-plugins
    codex plugin add quantus-cloud@quantus

설치 뒤 `codex mcp list` 에 quantus-cloud 가 «Not logged in» 으로 보이면 정상이다. 새 세션을 열고 `codex mcp login quantus-cloud` 로 로그인한다. Codex 쪽 주소는 운영 고정이다 — 환경 변수로 덮이지 않는다.

플러그인 없이 `~/.codex/config.toml` 만으로 쓰려면:

    [mcp_servers.quantus-cloud]
    url = "https://vibe-api.quantus.kr/mcp/cloud"

저장 뒤 `codex mcp login quantus-cloud` (OAuth 가 기본). 다른 주소로 붙이려면 플러그인을 깔지 않고(또는 `codex plugin remove quantus-cloud@quantus` 뒤) 위 `url` 을 그 주소로 둔다. 스킬만 쓰려면 `plugins/quantus-cloud/skills/*` 를 `~/.agents/skills/` 로 복사하거나 링크한다.

### claude.ai · Claude 데스크톱 (플러그인 없이 커넥터로)
설정 › 커넥터 › 사용자 지정 커넥터 추가 › 주소 `https://vibe-api.quantus.kr/mcp/cloud` › 추가 뒤 Connect 로 퀀터스에 로그인한다(Team/Enterprise 는 Owner 가 조직 설정 › 커넥터에서 먼저 추가). 이 길은 MCP 도구만 붙는다 — 스킬은 Claude Code·Codex 플러그인에만 있다. 근거: https://claude.com/docs/connectors/custom/add-unlisted.md

### 예전 판(quantus · quantus-research)을 깔았다면
이름이 `quantus-cloud` 하나로 바뀌었다. 예전 판이 남아 있으면 서버가 두 개로 보여 로그인을 두 번 하게 된다: `/plugin uninstall quantus@quantus`·`/plugin uninstall quantus-research@quantus`(Codex 는 `codex plugin remove quantus@quantus`·`codex plugin remove quantus-research@quantus`, 직접 붙였다면 `claude mcp remove quantus`·`claude mcp remove quantus-cloud`, claude.ai·데스크톱에 커스텀 커넥터 `…/mcp/research` 를 붙였다면 설정 › 커넥터에서 지움) 뒤 위 설치를 한다.

### 데이터 API 키 (내 파이썬용)
키는 퀀터스 웹에 로그인한 뒤 발급된다(MCP 로그인만으로는 키가 나오지 않는다). 키를 대화에 붙여 넣지 말고 환경 변수 `QUANTUS_API_KEY` 로 넣는다. 내려받기로 안내하는 것은 가격 일봉(`prices_daily`)·재무·팩터(PER·PBR·시총·모멘텀)·백테스트 결과·DART 재무 금액·공시·내부자·주문 연결이다. 응답에 `attribution`(원천 이름)이 있으면 고객에게 같이 보여 주고, `source_disabled` 를 받으면 «이 원천은 지금 제공이 멈췄습니다»라고 말하며 같은 값을 대화 표로 우회해 깔지 않는다. 이 변경 전에 발급한 키는 가격 범위가 없으니 가격이 필요하면 키를 새로 발급한다. 가격 원값 표는 대화에 깔지 않고 파이썬으로 받는 길을 안내한다 — `quantus-data` 스킬 참고.

## English
Claude Code: `/plugin marketplace add STOA-company/quantus-plugins` then `/plugin install quantus-cloud@quantus`, then `/mcp` → quantus-cloud → sign in once in the browser. Do not also run `claude mcp add` (double registration). To use another address, `export QUANTUS_MCP_URL=<MCP URL>` before starting Claude Code.

Codex: `codex plugin marketplace add STOA-company/quantus-plugins`, `codex plugin add quantus-cloud@quantus`, then `codex mcp login quantus-cloud`. Without the plugin, put `[mcp_servers.quantus-cloud]` `url = "https://vibe-api.quantus.kr/mcp/cloud"` in `~/.codex/config.toml`.

claude.ai / Claude Desktop: Settings > Connectors > Add custom connector > `https://vibe-api.quantus.kr/mcp/cloud` (tools only, no skills). Orders are only ever a confirm-card link; you press confirm on the Quantus screen. API keys: issue them on the Quantus web after login and pass them via `QUANTUS_API_KEY`, never in chat.
