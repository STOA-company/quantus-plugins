---
name: quantus-order
description: Turn a single buy/sell sentence into a Quantus confirmation-card link ("내 계좌로 삼성전자 1주 사 줘"), and hand a strategy-running request to the server's strategy tools. Nothing starts until the user confirms on the Quantus screen.
---

# 퀀터스 주문 — 확인 카드 링크까지만

이 스킬에는 주문을 직접 보내는 길이 없다. 주문은 고객이 **퀀터스 화면에서 직접 «확인»을 눌러야** 나간다.
도구는 퀀터스 MCP(`quantus-cloud` 서버)의 `quantus_propose_order`. 도구 목록에 없으면 «`/mcp` 에서 quantus-cloud 를 로그인해 주세요(이 도구는 로그인한 본인에게만 열립니다). 로그인했는데도 없으면 아직 이 서버에 열리지 않은 기능입니다» 한 줄 하고 멈춘다.

## 순서
1. 고객이 말한 것만 담아 `quantus_propose_order` 를 부른다: `instrument`(말한 이름·티커), `side`(buy/sell), 수량(`quantity`+`unit`) 또는 금액(`amount_krw`/`amount_usd`) 중 **말한 것 하나**, `order_type`·`limit_price`·`when`·`broker`·익절/손절은 말했을 때만, `original_sentence`=고객 문장 그대로.
2. 수량·금액·증권사·시각을 임의로 채우지 않는다. 빠져서 주문을 만들 수 없으면 필요한 한 가지만 묻는다.
3. 응답의 `confirm_url`·`summary`·`notes` 를 그대로 보여 준다. 그리고 반드시 이 뜻을 말한다: «아직 주문은 나가지 않았습니다. 이 링크를 열어 퀀터스 화면에서 직접 확인을 눌러야 나갑니다. 링크는 본인 로그인으로만 열립니다.» 응답에 만료 시각(`expires_at`)이 있을 때만 «약 30분 안에» 라고 덧붙인다.
4. `link_mode` 가 `prefill` 이면 «링크를 열면 문장만 채워지고, 퀀터스 화면에서 한 번 더 보내야 합니다» 라고 사실대로 말한다.
5. 체결·접수 여부는 말하지 않는다 — 이 도구는 모른다. «체결됐나요?» 에는 퀀터스 화면(주문 내역)에서 확인하라고 안내한다.

## 전략 자동 운용 («이 전략 내 계좌로 돌려 줘»)
이것은 주문 한 건이 아니다. `quantus_propose_order` 로 한 건짜리로 줄이지 않는다. 서버의 실제 도구로 보낸다:
- 조건으로 종목을 골라 매달 갈아타는 알고리즘: `check_selection_rule` 로 규칙을 되읽은 뒤 `propose_strategy_run`(`rule`, `notional`). `notional`(투자금)은 고객이 말한 값만 넣고, 말하지 않았으면 임의로 정하지 말고 한 가지만 묻는다. 이 도구는 **모의계좌 전용**이라 «실계좌는 아직 지원하지 않는다» 를 그대로 말한다. 확인 URL 을 사람이 열어 계좌를 고르고 승인해야 시작된다. 응답이 `proposal_created:false` 면 서버가 준 `message` 를 그대로 전하고 다른 도구로 우회하지 않는다. 이미 돌고 있는 것은 `list_strategy_runs`(인자 없음)로 보고, 끄려면 `stop_strategy_run`(`run_id`=`propose_strategy_run`·`list_strategy_runs` 가 준 값)을 쓴다.
- 실계좌 조건 주문·규칙 트레이더(코인 OKX 20일선 규칙, 국내·미국은 큐의 조건 주문): `launch_trader`(`instruction`=고객 문장, `market`). 큐 링크와 연결 가능한 증권사를 안내할 뿐 규칙을 확정하지 않는다. 이후 `list_traders`·`stop_trader`.
- 위 도구가 안 맞는 전략이면 «이 서버가 지금 자동 운용으로 이어 줄 수 있는 범위는 위 둘뿐» 이라고 사실대로 말하고, 코드 봇이면 `deploy-stocks-bot`(cloud 도구가 열린 경우).
- 어느 쪽이든 «퀀터스 화면에서 직접 확인해야 시작됩니다» 를 그대로 말하고, 시작됐다고 말하지 않는다.

## 하지 않는 것
고객 대신 «확인»을 누르거나 누른 것처럼 말하지 않는다 · 단건 주문을 `quantus_ask`·`propose_virtual_order` 등 다른 도구로 우회하지 않는다 · 증권사 키·계좌번호를 대화로 받지 않는다 · 남의 계좌·출금·이체는 «본인 계좌의 주문만 됩니다».
