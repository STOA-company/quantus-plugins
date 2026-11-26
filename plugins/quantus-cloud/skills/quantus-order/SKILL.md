---
name: quantus-order
description: Turn a single buy/sell sentence into a Quantus confirmation-card link ("내 계좌로 삼성전자 1주 사 줘"), and point a strategy-running request to Quantus Q (https://www.quantus.kr/en/q), since this connection has no strategy-running tools. Nothing is ordered until the user confirms on the Quantus screen.
---

# 퀀터스 주문 — 확인 카드 링크까지만

이 스킬에는 주문을 직접 보내는 길이 없다. 주문은 고객이 **퀀터스 화면에서 직접 «확인»을 눌러야** 나간다.
도구는 퀀터스 MCP(`quantus-cloud` 서버)의 `quantus_propose_order`. 도구 목록에 없으면 «`/mcp` 화면에서 quantus-cloud 를 로그인해 주세요(이 도구는 로그인한 본인에게만 열립니다). 로그인했는데도 없으면 퀀터스에서 직접 주문하실 수 있습니다: https://www.quantus.kr/ko/q» 한 줄 하고 멈춘다.

## 순서
1. 고객이 말한 것만 담아 `quantus_propose_order` 를 부른다: `instrument`(말한 이름·티커), `side`(buy/sell), 수량(`quantity`+`unit`) 또는 금액(`amount_krw`/`amount_usd`) 중 **말한 것 하나**, `order_type`·`limit_price`·`when`·`broker`·익절/손절은 말했을 때만, `original_sentence`=고객 문장 그대로.
2. 수량·금액·증권사·시각을 임의로 채우지 않는다. 빠져서 주문을 만들 수 없으면 필요한 한 가지만 묻는다.
3. 응답의 `confirm_url`·`summary`·`notes` 를 그대로 보여 준다. 그리고 반드시 이 뜻을 말한다: «아직 주문은 나가지 않았습니다. 이 링크를 열어 퀀터스 화면에서 직접 확인을 눌러야 나갑니다. 링크는 본인 로그인으로만 열립니다.» 응답에 만료 시각(`expires_at`)이 있을 때만 «약 30분 안에» 라고 덧붙인다.
4. `link_mode` 가 `prefill` 이면 «링크를 열면 문장만 채워지고, 퀀터스 화면에서 한 번 더 보내야 합니다» 라고 사실대로 말한다.
5. 체결·접수 여부는 말하지 않는다 — 이 도구는 모른다. «체결됐나요?» 에는 퀀터스 화면(주문 내역)에서 확인하라고 안내한다.

## 전략 자동 운용 («이 전략 내 계좌로 돌려 줘»)
이것은 주문 한 건이 아니다. `quantus_propose_order` 로 한 건짜리로 줄이지 않는다.
- 이 연결(`/mcp/cloud`)에는 전략 자동 운용·조건 주문 도구가 없다. 첫 문장으로 그렇게 말하고, 퀀터스 큐에서 이어 갈 수 있다고 링크 하나를 준다: 한국어 https://www.quantus.kr/ko/q · 영어 https://www.quantus.kr/en/q.
- 고객이 직접 짠 코드를 인스턴스에 올려 돌리려는 요청이면 클라우드 인스턴스 도구(`cloud_*`)가 목록에 있을 때만 그 도구로 안내한다. 목록에 없으면 «퀀터스 클라우드 인스턴스 대여는 준비 중이며, 고객에게 열리면 이 연결에서 내 코드를 올릴 수 있다» 고 사실대로 말한다.
- 어느 쪽이든 시작됐다고 말하지 않는다.

## 하지 않는 것
고객 대신 «확인»을 누르거나 누른 것처럼 말하지 않는다 · 단건 주문을 `quantus_ask`·`propose_virtual_order` 등 다른 도구로 우회하지 않는다 · 증권사 키·계좌번호를 대화로 받지 않는다 · 남의 계좌·출금·이체는 «본인 계좌의 주문만 됩니다».
