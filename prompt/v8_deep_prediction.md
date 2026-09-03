# DMI v8 — Deep Big-Move Prediction

## 0. 연결 문서 / Schema Freeze
실행 전에 다음 문서를 읽는다.
- `/WORKFLOW_v8.md` — 실행·독립성·저장 규칙
- `/DMI_PLAYBOOK_v8.md` — Prediction에 허용된 OBJECTIVE와 ACTIVE_RULES
- `/templates/STAGE_OUTPUT_v8.md` — 저장 envelope

이 프롬프트는 03:30과 08:30 Deep Prediction이 공통으로 사용한다. 실행 시각만 자동화가 지정한다.

- `SCHEMA_VERSION = DMI_v8`
- 날짜: `YYYY-MM-DD`
- Code: 확인된 6자리 문자열, 확인 불가 시 `N/A`
- Market: `KOSPI / KOSDAQ`
- 확인 불가 값: `N/A` 또는 정의된 `UNVERIFIED`
- % 값은 % 단위를 명시
- enum 철자, 출력 필드명·순서, HANDOFF 구조를 임의 변경하지 않는다.
- `|` 구분 HANDOFF의 자유 텍스트 안에는 `|`를 사용하지 않는다.

## 1. 목적
오늘 KRX 정규장에서 **실제 단타 기회가 될 정도로 크게 상승할 가능성이 높은 종목**을 현재 시점 정보로 선별한다.

단순히 `종가 > 전일 종가`를 맞히는 것이 목적이 아니다. 핵심은 오늘 의미 있는 상승폭과 장중 상승 기회가 발생할 종목을 사전에 찾는 것이다.

Deep은 구조화된 검증 프레임워크를 사용한다. 다만 Score가 판단을 대신해서는 안 된다.

## 2. 분석 대상
KOSPI·KOSDAQ 상장 보통주를 폭넓게 탐색한다.
특별한 이유가 없는 한 ETF·ETN·SPAC·우선주와 정상적 가격발견이 어려울 정도의 저유동성 종목은 핵심 후보에서 제외한다.

## 3. 시점·정보·독립성
현재 실행 시각 이전에 실제 공개되었거나 확인 가능한 정보만 사용한다.
다른 DMI Prediction 결과를 읽거나 후보 생성·Rank·Score에 사용하지 않는다. 08:30 실행도 03:30 결과를 읽지 않는다.

실시간성이 중요한 데이터는 가능한 경우 기준시각을 확인한다. 아직 확정되지 않은 가격을 종가처럼 표현하지 않는다.

정보 우선순위:
1. 거래소·정부·규제기관
2. 기업 공시·공식발표·IR
3. 주요 통신사·신뢰도 높은 경제매체
4. 증권사
5. 산업 전문매체

동일 사건의 반복 보도는 여러 독립 촉매로 계산하지 않는다.
확인되지 않은 SNS·커뮤니티 루머는 핵심 근거로 사용하지 않는다.
주요 FACT에는 가능한 경우 출처를 제시한다.

## 4. FACT / INTERPRETATION / FORECAST
핵심 판단을 다음으로 구분한다.

- **FACT**: 확인된 가격·공시·기업발표·경제지표·정책·뉴스
- **INTERPRETATION**: 그 사실이 한국시장·산업·기업에 갖는 의미
- **FORECAST**: 그 결과 오늘 예상하는 가격 움직임

뉴스의 긍정·부정과 실제 주가 방향을 동일시하지 않는다.

## 5. 데이터 가용성 / N/A
존재하지 않거나 확보하지 못한 데이터를 추정하지 않는다.
이전 거래일 자료를 사용할 경우 PRIOR 정보임을 인식한다.
N/A는 실제 평가 불가능한 경우에만 사용한다. 존재하는 불리한 신호를 N/A로 제거하지 않는다.

## 6. 분석 순서
반드시 다음 순서로 수행한다.

1. **Broad Scan** — 현재 시점의 국내·글로벌 이벤트와 가능한 종목을 폭넓게 탐색
2. **Evidence Test** — 오늘 실제 움직임을 만들 근거인지 검증
3. **Big-Move Test** — 소폭 상승이 아니라 의미 있는 상승폭으로 확장될 이유 검증
4. **Price-in Check** — 재료가 이미 가격에 반영됐는지 검증
5. **Counterargument** — 예측이 틀릴 가장 강한 이유 검토
6. **Candidate Selection** — 반대논리보다 Big-Move 논리가 강한 후보만 유지
7. **Rank** — 오늘의 상승 가능성·상승폭·시급성을 종합해 순위 확정
8. **Base Score** — 후보와 Rank가 확정된 뒤 calibration/audit용으로 산출

Score를 먼저 계산해 후보를 고르지 않는다. Score가 Rank와 다르다는 이유만으로 Rank를 사후 변경하지 않는다.

## 7. Big-Move Test
각 후보는 다음 질문을 통과해야 한다.

- `WHY_THIS`: 왜 이 종목인가?
- `WHY_TODAY`: 왜 다른 날이 아니라 오늘인가?
- `WHY_BIG`: 왜 +0.x%가 아니라 단타 가치가 있는 상승폭으로 확대될 수 있는가?
- `DOMESTIC_PATH`: 핵심 재료가 한국 종목 가격으로 연결되는 실제 경로는 무엇인가?
- `ATTENTION_PATH`: 오늘 시장의 거래·관심이 이 종목으로 집중될 이유는 무엇인가?
- `MAIN_COUNTERARGUMENT`: 가장 강한 반대논리는 무엇인가?

글로벌 신호를 사용한다면 단순 Peer 동조가 아니라 국내 전달경로를 검증한다.

## 8. Base Score — 고정 Rubric
총점 100. 후보와 Rank 확정 후 기록한다.

### C = Catalyst Strength / 25
촉매가 기업가치·실적·산업구조·수급 기대에 미치는 절대 영향력.
- 0~5: 직접 방향성 촉매 거의 없음
- 6~10: 약하거나 간접적
- 11~15: 의미 있음
- 16~20: 강한 직접촉매
- 21~25: 가치·실적·산업구조·수급 기대를 크게 바꿀 수 있는 매우 강한 촉매

### F = Freshness / 15
정보 공개 후 완료된 KRX 정규세션 수 기준. Price-in을 섞지 않는다.
- 14~15: 0회
- 12~13: 1회
- 8~11: 2~3회
- 4~7: 4~10회
- 0~3: 11회 이상 또는 실질적 신규정보 없음

### S = Sector Momentum / 15
국내 확인을 우선하고 글로벌 breadth는 보조한다.
- 0~3: 고립
- 4~7: 혼재
- 8~11: 복수 관련 종목·산업 신호가 지지
- 12~13: 섹터 전반 확산
- 14~15: 시장 핵심 주도축

### FL = Flow / Market Attention / 15
실제 거래대금·수급·거래집중·검증 가능한 시장활동을 우선한다.
- 0~3: 관심·유동성 부족
- 4~7: 평상 수준
- 8~11: 실제 거래·관심 증가
- 12~13: 강한 거래집중
- 14~15: 시장 중심 종목 수준
기사 수·반복보도·소셜 buzz만으로 높이지 않는다. 실제 시장활동을 평가할 자료가 없으면 N/A.

### T = Technical Position / 10
- 0~2: 강한 역풍 또는 극단적 과열
- 3~4: 불리
- 5~6: 중립
- 7~8: 유리
- 9~10: 매우 강하게 지지

### M = Market Environment Fit / 10
- 0~2: 시장환경과 강하게 충돌
- 3~4: 불리
- 5~6: 중립
- 7~8: 부합
- 9~10: 매우 강하게 부합

### A = Big-Move Asymmetry / 10
단순 방향이 아니라 **오늘 추가 상승폭의 잠재력 대비 하방·소진 위험**을 평가한다.
- 0~2: 하방·소진 위험 압도
- 3~4: 기대구조 불리
- 5~6: 균형
- 7~8: 추가 상승 기대값 우세
- 9~10: 큰 상승 잠재력 대비 반대위험이 매우 제한적
신뢰 가능한 가격·변동성·지지저항 자료가 부족하면 N/A.

## 9. 동일 증거 중복가산 방지
하나의 FACT를 여러 항목의 독립 증거처럼 기계적으로 반복 가산하지 않는다.

- S는 breadth와 섹터 확산
- FL은 실제 거래·수급·시장활동
- M은 전체 시장환경과 스타일 적합성
- A는 추가 상승폭 대비 반대위험

을 각각 요구한다.

Global Peer 한 종목의 급등만으로 S·FL·M·A를 동시에 높이지 않는다.

## 10. Score Coverage
- `AVAILABLE_MAX` = 평가 가능한 항목 최대점수 합
- `RAW_SCORE` = 실제점수 합
- `BASE_SCORE = RAW_SCORE / AVAILABLE_MAX × 100`
- `SCORE_COVERAGE = AVAILABLE_MAX / 100 × 100%`

Coverage:
- 85~100%: NORMAL
- 70~84%: LIMITED
- <70%: LOW_COVERAGE

Coverage <70%이면 Confidence 최대 MEDIUM.
Base Score는 항상 RAW_SCORE / AVAILABLE_MAX / Coverage와 함께 기록한다.

## 11. Price-in
Price-in은 별도 Score가 아니다.

`PRICE_IN = LOW / MEDIUM / HIGH / EXTREME`
`PRICE_IN_CHECK = VERIFIED / UNVERIFIED`

Price-in은 T와 A에만 반영하며 C와 F에는 반영하지 않는다.
T 또는 A가 가격·변동성 자료 부족으로 N/A이면 PRICE_IN_CHECK = UNVERIFIED.
UNVERIFIED이면 Confidence 최대 MEDIUM.

추가로:
`CHASE_RISK = LOW / MEDIUM / HIGH / VERY_HIGH`

이미 큰 폭으로 선반영되어 추가 상승 여력이 작다면 Catalyst가 강해도 Big-Move 후보 Rank를 낮게 판단할 수 있다. 이는 Score 산출 이전의 Candidate/Rank 판단이다.

## 12. Freshness Grade
F에서 기계적으로 파생한다.
- S = 14~15
- A = 12~13
- B = 8~11
- C = 0~7

## 13. Confidence
- **VERY_HIGH**: 원출처 확인 + 여러 독립 신호 일치 + 주요 반대논리 약함
- **HIGH**: 핵심 FACT 확인 + 둘 이상의 독립 보조근거, 일부 불확실성
- **MEDIUM**: 유효한 근거가 있으나 선반영·시장환경·수급·데이터 중 큰 불확실성 존재
- **LOW**: 관찰가치는 있으나 핵심 데이터 부족 또는 binary/event risk 큼

Confidence를 임의 확률로 변환하지 않는다.

## 14. Catalyst Type
`PRIMARY_CATALYST_TYPE`:
- Earnings
- Guidance
- Contract_Order
- M&A
- Capital_Return
- Capital_Raising_Dilution
- Clinical_Approval
- Policy_Regulation
- Global_Peer
- Sector_Theme
- Supply_Demand
- Macro_FX_Commodity
- Technical
- Other

복합 촉매는 `SECONDARY_CATALYST_TYPE` 하나까지 허용한다.

## 15. 현재 시점 Market / Event Scan
현재 시점에서 오늘 한국시장에 실제 의미가 있는 변화와 이벤트를 선별한다.
숫자를 기계적으로 나열하지 말고 국내 전달 의미를 설명한다.

공시·실적·Guidance·수주·M&A·자본정책·임상/승인·정책/규제·산업 이벤트와 필요한 글로벌 시장·금리·FX·원자재·Peer 등을 폭넓게 탐색한다.

현재 시점에 신뢰할 수 있는 국내 개장 전/NXT 데이터가 실제 존재하고 최신성이 확인될 경우 활용한다. 없거나 검증되지 않으면 만들지 않으며, 데이터 부재 자체를 약세로 해석하지 않는다.

후보에 실제 관련성이 있을 때만 신용·공매도/대차·보호예수·증자/CB/BW·시간외·VI/상하한가 이력 등 추가 Risk를 확인한다.

## 16. Market View
후보 선정 시점의 시장환경 가정을 기록한다.
- 예상 Risk Sentiment
- KOSPI / KOSDAQ 또는 대형/중소형 상대환경
- 핵심 강세·약세 Theme
- 가장 중요한 시장 제약요인

## 17. Watchlist
오늘 뉴스·거래·변동성·시장 관심이 집중될 가능성이 높은 종목을 최대 10개 기록한다.
Watchlist는 TOP 상승후보와 동일하지 않다. 질 낮은 후보로 수를 채우지 않는다.

| Rank | Name | Code | Market | Direction | Catalyst | Fresh Grade | Attention | Key Risk |
|---:|---|---|---|---|---|---|---|---|

Direction: `UP / DOWN / VOLATILE / UNCERTAIN`
Attention: `LOW / MEDIUM / HIGH`

## 18. 최종 상승 TOP 5
최대 5개. 좋은 Big-Move 후보가 부족하면 수를 줄인다.

EXPECTED_MOVE:
- +1~3%
- +3~5%
- +5~10%
- 10%+
- UNCERTAIN

| Rank | Name | Code | Market | Expected Move | Base Score | Raw/Max | Coverage | Breakdown | Confidence | Fresh Grade | Price-in Check | Price-in | Chase Risk | Catalyst Type |
|---:|---|---|---|---|---:|---|---:|---|---|---|---|---|---|---|

Breakdown 순서: `C/F/S/FL/T/M/A`

각 후보:
- WHY_THIS
- WHY_TODAY
- WHY_BIG
- CORE_FACT
- INTERPRETATION
- FORECAST
- DOMESTIC_PATH
- ATTENTION_PATH
- MAIN_COUNTERARGUMENT
- 주요 Risk
- 자연어 Intraday Scenario
- Invalidation

TOP 1~2는 상세히 설명한다.

### Score Audit
각 TOP 후보의 주요 Score 항목별 근거를 짧게 기록한다.
근거 없는 숫자만 출력하지 않는다.

## 19. 위험·회피 후보
오늘 매수 관점에서 특히 위험하다고 판단되는 종목 또는 유형을 최대 5개 기록한다.
이는 하락 TOP5 예측이 아니다.

가능한 원인:
- 선반영 / 극단적 추격 위험
- 갭 상승 후 소진 가능성
- 재료 약화·소멸
- 직접 악재
- 희석·오버행
- 유동성 문제
- 비정상적 변동성
- 글로벌 재료의 국내 전달근거 부족

| Rank | Name or Type | Reason | Risk Type |
|---:|---|---|---|

후보가 없으면 NONE.

## 20. 최종 핵심판
- TOP1:
- TOP1_CORE_REASON:
- TOP1_EXPECTED_MOVE:
- PRIMARY_THEME:
- PRIMARY_UNCERTAINTY:
- MARKET_INVALIDATION:
- MOST_DANGEROUS_TRAP:

## 21. HANDOFF
[HANDOFF]
SCHEMA_VERSION: DMI_v8
DATE:
STAGE_TIME:
MODEL_TYPE: DEEP
MARKET_VIEW:
TOP_COUNT:
TOP:
1|Name|Code|Market|Rank|ExpectedMove|BaseScore|RawScore|AvailableMax|Coverage|C/F/S/FL/T/M/A|Confidence|FreshGrade|PriceInCheck|PriceIn|ChaseRisk|PrimaryCatalystType|SecondaryCatalystType|WhyToday|WhyBig|MainRisk
2|...
3|...
4|...
5|...
WATCH_COUNT:
WATCH:
1|Name|Code|Market|Direction
2|...
3|...
4|...
5|...
6|...
7|...
8|...
9|...
10|...
AVOID_COUNT:
AVOID:
1|NameOrType|Reason|RiskType
2|...
3|...
4|...
5|...
TOP1:
PRIMARY_THEME:
PRIMARY_UNCERTAINTY:
MARKET_INVALIDATION:
[/HANDOFF]

HANDOFF에는 본문에 없던 새로운 분석을 추가하지 않는다.
