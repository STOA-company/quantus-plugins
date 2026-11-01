---
name: quantus-backtest
description: Run a Korean/US stock backtest through the Quantus MCP over the longest period the data allows ("삼성전자 가장 긴 기간으로 백테스트", "이 전략 과거에 어땠어?", "PER 낮은 종목 백테스트"). Use whenever the user wants a backtest, with or without naming a period.
---

# 퀀터스 백테스트 — 기간을 묻지 말고 가장 긴 기간부터

도구는 퀀터스 MCP(`quantus` 서버)의 것이다. 도구 목록에 아래 이름이 없으면 «`/mcp` 에서 quantus 를 로그인해 주세요. 로그인했는데도 없으면 아직 이 서버에 열리지 않은 기능입니다» 한 줄만 말하고 멈춘다(없는 도구를 부르지 않는다).
말투는 쉬운 한국어, 고객이 영어면 영어.

## 기본 원칙
- 고객이 기간을 말하지 않았으면 **묻지 않고 가장 긴 기간**으로 돌린다. 기간을 말했으면 그대로 쓴다.
- 시작일·연수를 기억이나 추측으로 쓰지 않는다. 아래 «시작일 얻기»로 도구에서 읽은 값만 쓴다. 결과에는 실제로 쓴 시작일·종료일을 그대로 적는다.

## 시작일 얻기 (가장 긴 기간)
1. `catalog_fields` (`dataset:"prices"`, `market:"KR"` 또는 `"US"`)로 가격 필드의 제공 구간(시작·끝)을 읽는다.
2. `coverage_check` (`fields:["close"]`, `dataset:"prices"`, `market`, `start`:1에서 읽은 시작일, `end`:오늘)로 그 구간이 공개 범위 안인지 확인한다. `ok` 가 아니면 `reason`·`alternatives` 를 읽고 그 안에서 다시 잡는다.
3. 종목 하나의 실제 상장 이후 첫 거래일은 `data_prices` (`tickers:[…]`, `start`:1의 시작일, `end`: 시작일에서 가까운 날짜, `as_of`: 오늘)로 첫 유효 행을 보고 정한다. 한 번에 받는 양은 일수×종목 ≤ 10,000 이라 구간을 잘라 읽는다. 종목이 그 시작일보다 늦게 상장했으면 첫 거래일이 시작일이다.

## 실행
- **종목을 지목한 문장**(«삼성전자…»): `backtest_run`. 전략 코드는 QSDK 로 짧게 쓴다(고객이 전략을 말하지 않았으면 «처음 사서 끝까지 보유»를 기본으로 하고 그렇게 했다고 말한다). `start`=위에서 얻은 시작일, `end`=오늘, `universe`={티커: 시장}. 신호 자산이 있으면 첫 호출은 확인 필요 응답이다 — 고지 내용을 고객에게 보여 주고, 같은 입력에 `confirm=true`·`accept_modeled_notice=true`·받은 `draft_id` 를 더해 다시 부른다.
- **조건으로 종목을 고르는 문장**(«국내 반도체 PER 하위 10종목»): `run_selection_backtest` (문장에 종목명을 넣지 않는다, KR). 조건이 모호하면 먼저 `check_selection_rule`·`list_metrics` 로 지표 이름을 확인한다. 이 도구가 기간을 잘라 돌려주면 응답의 사유를 그대로 전한다.
- 위 도구가 안 맞는 말이면 `quantus_ask` 에 고객 문장을 그대로 넘긴다(큐 크레딧·요금제가 본인 계정으로 적용된다).
- 더 보고 싶다는 말이면 `backtest_inspect` 로 결정(`decisions`)·거래 건수 위주로 보여 준다. 거래 가격·곡선의 가격 칸(`curve`·`trades` 의 가격)은 대화에 옮기지 않는다 — 수익률·MDD 같은 요약 지표로 말한다.

## 보고
수익률·MDD 등 도구가 준 지표, 쓴 기간, 쓴 전략 가정을 먼저. 도구가 주지 않은 숫자는 만들지 않는다. 가격 원값 시계열은 대화에 옮기지 않는다(요약 지표만).
다음 칸: 결과가 마음에 들면 «첫 매수 한 건을 확인 카드로 만들까요, 아니면 전략 자동 운용으로 할까요?» 하고 묻는다. 한 건이면 `quantus-order`, 자동 운용이면 `quantus-order` 의 «전략 자동 운용» 절을 따른다.
크레딧이 소진됐다는 응답(`credits_exhausted`)이면 안내된 `pricing_url`·`resets_at` 을 그대로 전한다.

## 하지 않는 것
고객 대신 주문하지 않는다(주문은 `quantus-order`) · 데이터 범위를 확인하지 않고 «몇 년부터 됩니다» 같은 말을 하지 않는다.
