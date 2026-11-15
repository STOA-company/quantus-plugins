---
name: quantus-data
description: Look at Quantus data inside the chat and pull it into the user's own Python ("퀀터스 데이터 보여 줘", "내 노트북 파이썬에서 데이터 받기", "재무 스냅샷 보여 줘"). Use for data lookups, screening, and API-key questions.
---

# 퀀터스 데이터 — 대화 안에서 보기, 내 파이썬에서 받기

도구는 퀀터스 MCP(`quantus-cloud` 서버). 도구 목록에 없으면 «`/mcp` 에서 quantus-cloud 를 로그인해 주세요» 한 줄 하고 멈춘다.

## 대화 안에서 보기 (로그인만 있으면 됨)
- 어떤 데이터가 있는지: `catalog_fields`, `list_metrics`(`keyword`·`category`).
- 종목 하나: `get_stock_snapshot`(재무·팩터·점수). 시간에 따른 지표 값: `get_metric_history`(가격 값 지표(`price`·`week_52_high`·`week_52_low`·`bb_upper`·`bb_lower`·`market_cap` — 시세·고저가·시총을 그대로 드러내는 것)는 이 도구로 부르지 않는다 — 가격 시계열은 대화에 표로 깔지 않고 데이터 API `prices_daily` 로 받는 길을 안내한다. PER·PBR·ROE 등 밸류·재무·팩터 지표만 쓴다).
- 조건으로 고르기: `screen_stocks`(필터·정렬), 문장으로는 `check_selection_rule`.
- 한 시점 팩터 스냅샷: `data_factors`(`as_of` 한 날짜의 팩터 값, 시계열이 아니다). 유니버스 구성: `data_universe`.
- 범위 확인: `coverage_check`. 기간·시작일은 도구가 알려 준 값만 말한다.
- 말로 묻는 분석·시세 질문: 이 연결에는 대화형 분석 도구가 없다. 위 조회 도구로 답할 수 없으면 퀀터스 큐 링크를 준다: https://www.quantus.kr/ko/q
- 일봉 종가 같은 **가격 원값 시계열은 대화에 표로 깔지 않는다.** 원값이 필요하면 파이썬으로 받는 길(데이터 API `prices_daily`, 아래 «내 파이썬에서 받기»)로 안내하고, 대화에서는 요약·지표로 답한다. 가격이 필요한 분석 자체는 `quantus-backtest` 의 요약 지표로도 답한다.

## 내 파이썬에서 받기 (데이터 API 내려받기)
내려받기로 안내하는 것은 **가격 일봉(`prices_daily`)·재무·팩터(PER·PBR·시총·모멘텀, `financials_factors`)·백테스트 결과(`backtest`)·DART 재무 금액(`financials_dart`)·공시·내부자(`alerts_signals`)·주문 연결(확인 카드 제안)** 이다. 키 범위(상품) 이름은 `prices_daily`(가격 일봉)·`financials_factors`(재무·팩터)·`backtest`·`financials_dart`(DART 재무 금액)·`alerts_signals`(공시·내부자 알림)·`order_link`(주문 연결, 기본 꺼짐)·`mcp_tools`(MCP 사용권)다. 도구·엔드포인트가 실제로 열려 있는 것만 안내한다 — 서버가 «준비 중»(501)이나 404 를 주는 상품은 사실대로 그렇게 말한다.
1. **키 발급**: 도구 목록에 `quantus_data_api_key_info` 가 있으면 그 도구가 알려 주는 안내를 따른다. 없으면 «키는 퀀터스 웹에 로그인한 뒤 발급받습니다(MCP 로그인만으로는 키가 안 나옵니다)» 까지만 말하고, 발급 화면 주소는 추측하지 않는다 — 모르면 퀀터스 고객센터(`https://www.quantus.kr/ko/support`)를 안내한다.
2. **키를 대화에 붙여 넣게 하지 않는다.** 받은 키는 셸 환경 변수 `QUANTUS_API_KEY` 에 넣게 한다(`export QUANTUS_API_KEY=…` 를 고객이 직접, 셸 기록에 남기고 싶지 않으면 `.env` 파일). 키가 대화에 올라오면 «그 키는 지금 폐기하고 새로 발급하세요» 라고 말하고 값을 다시 쓰지 않는다.
3. 파이썬 예시는 환경 변수에서만 읽는 꼴로 보여 준다: `os.environ["QUANTUS_API_KEY"]`. 호출 주소·응답 칸은 도구 설명과 서버가 알려 준 응답으로 확인한 것만 쓴다(추측 금지).
4. **이 변경 전에 발급한 키는 가격 범위(`prices_daily`)가 없다** — `/v1/prices/daily` 가 `scope_missing`(403)이면 «키를 새로 발급해 주세요» 라고 안내한다.
5. 한도가 있다: 등급별 일·월 한도를 넘으면 429 와 안내 문구가 온다. 한도 숫자·가격은 정해진 값만 말한다.

## 원천 표시 · 멈춘 원천
- **응답에 `attribution`(예 «한국투자증권·LSEG»)이 있으면 고객에게 같이 보여 준다.** 가격·팩터·백테스트 응답(데이터 API 와 대화 안 MCP 도구 둘 다, 로그인 방식과 상관없이)에 `attribution` 과 원천 id(`/v1` 은 `sources`, MCP·`/api/v1` 은 `source_ids`)가 붙는다. 값이 없는 응답(목록·오류)에는 없을 수 있으니, 없으면 지어내지 않는다.
- **`source_disabled`(MCP 는 «이 원천의 데이터는 지금 제공이 멈췄습니다» 오류)를 받으면 «이 원천은 지금 제공이 멈췄습니다»라고 사실대로 말한다.** 그 응답은 한도·크레딧에 세지 않는다. **같은 값을 대화 안 표로 우회해 깔지 않는다**(`get_metric_history`·`data_factors`·`quantus_ask` 로 같은 가격·팩터 값을 다시 뽑아 보여 주기 금지). 다른 원천·다른 기간·다른 종목으로 되는 요청이 있으면 그것만 제안한다.
- 가격 값을 «받을 수 있다»고 말하는 기간·연수는 도구가 알려 준 값만 쓴다. 한 번에 받을 수 있는 기간·종목 수에는 상한이 있어, 길면 나눠 부르게 안내한다(상한이 응답으로 오면 그 숫자 그대로).
- 공시(DART) 조회는 데이터 API `alerts_signals` 로 받는 길을 안내한다. 공시(DART) 조회 전용 도구는 이 서버에 없다(MCP) — 대화로 묻는 공시 질문은 퀀터스 큐(https://www.quantus.kr/ko/q)로 넘기되 «공시를 직접 받아 드리는 도구는 없고 퀀터스 답변으로 드립니다» 라고 말한다.

## 하지 않는 것
키·토큰을 대화·코드·로그에 쓰지 않는다 · 남의 계좌 정보를 요청하지 않는다.
