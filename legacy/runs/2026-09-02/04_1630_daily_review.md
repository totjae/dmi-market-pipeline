[DMI_RUN_META]
SCHEMA_VERSION: DMI_v7.1
DATE: 2026-09-02
STAGE: 16:30
RUN_TIME_KST: 2026-09-02 16:31:34
[/DMI_RUN_META]

[STAGE_REPORT]
# TASK 4 — 16:30 Daily Review — v7.1

## 1. 원본 및 데이터 상태

- AVAILABLE_STAGES: 03:30, 07:20, 08:25
- 세 stage 모두 같은 날짜의 정상 파일에서 실제 `[STAGE_REPORT]`와 `[STAGE_HANDOFF]`를 확인했다.
- 03:30 `REGIME_PRELIMINARY`: Risk-off; Energy/Defense relative strength; Semiconductors/Airlines/Chemicals weakness; high yields, oil and KRW weakness constrain risk appetite
- 08:25 `MARKET_VIEW_AT_SELECTION`: KOSPI와 KOSDAQ 모두 DOWN 우위, KOSPI 상대우위; Risk-off; 정유·개별 대형 수주주 유리, 반도체·항공·화학·고밸류 성장주 불리; 고유가·4.79% 미 10년물·원화 약세가 핵심 제약
- 가격 데이터: 2026-09-02 KRX 정규장 일봉. StockAnalysis의 S&P Global Market Intelligence 일봉을 동일 기준으로 사용했다. 지수는 Investing.com 일봉을 사용했다.
- 대한항공은 16:30 현재 사용한 일봉 원천에서 9월 2일 확정 행이 갱신되지 않아 N/A로 처리했다.
- Corporate Action Check: 후보군에서 당일 비교를 왜곡하는 확인된 권리락·분할·병합·무상증자 자료는 발견하지 못했다. 별도 조정가격이 확인되지 않아 전일 종가 기준이며, 확인 불가 사항은 추정하지 않았다.
- 일부 공급업체 화면의 장마감 값이 서로 달라 단일 데이터셋 내부 일관성을 우선했다.

## 2. KRX Ground Truth

- KOSPI: 6,562.72, 전일 6,835.80 대비 -3.99% (시가 6,625.47, 고가 6,694.57, 저가 6,558.30)
- KOSDAQ: 803.98, 전일 821.25 대비 -2.10% (시가 802.80, 고가 819.62, 저가 796.34)
- 실제 방향: KOSPI DOWN, KOSDAQ DOWN
- 시장 성격: 국제유가와 글로벌 국채금리 상승, 미국·이란 긴장 재확대로 아시아 전반 Risk-off. KOSPI 낙폭이 KOSDAQ보다 더 커 오전의 KOSPI 상대우위 판단은 MISS.
- 업종: 반도체·대형 기술주, 조선, 화학, 발전설비가 약했고 정유는 상대강세였다. S-Oil은 +1.19%였으나 SK이노베이션은 -0.44%로 정유 내 차별화가 나타났다.
- 실제 주도/관심: 하락 방향에서는 SK하이닉스(-4.49%), 삼성전자(-3.83%), 두산에너빌리티(-4.85%), 한화오션(-4.10%)의 낙폭이 컸다. 상승 후보군에서는 S-Oil만 뚜렷한 절대수익을 냈다.
- 외국인·기관·개인 수급: 16:30 기준 신뢰할 수 있는 최종 종합 수치를 확보하지 못해 N/A.
- USD/KRW: 우리은행 2026-09-02 매매기준율 1,370.80원. 서울외환시장 15:30 종가와 동일 개념의 값은 확인하지 못해 N/A.
- 거래대금 집중 영역: 삼성전자·SK하이닉스 등 대형 반도체와 삼성전기에서 높은 거래대금이 확인됐으나, 시장 전체 순위표는 확보하지 못해 정량 순위는 N/A.
- 장중 중요 뉴스: 미국·이란 충돌과 호르무즈 공급 우려, Brent 약 95.45달러, 미 10년물 4.81%대가 핵심 위험요인이었다.

출처:
- KOSPI 일봉: https://kr.investing.com/indices/kospi-historical-data
- KOSDAQ 일봉: https://kr.investing.com/indices/kosdaq-historical-data
- 후보 OHLC: https://stockanalysis.com/
- 글로벌 장중 배경: https://www.reuters.com/world/china/global-markets-wrapup-1-2026-09-02/
- 환율: https://spot.wooribank.com/pot/Dream?withyou=FXXRT0014

## 3. TASK 2 객관적 지수 방향 검증

- KOSPI_DIRECTION_FORECAST: DOWN
- KOSPI_DIRECTION_ACTUAL: DOWN
- KOSPI_DIRECTION_HIT: HIT
- KOSDAQ_DIRECTION_FORECAST: DOWN
- KOSDAQ_DIRECTION_ACTUAL: DOWN
- KOSDAQ_DIRECTION_HIT: HIT

두 지수 모두 -0.20% 이하이므로 고정 규칙상 DOWN이다.

## 4. 07:20 Market Regime Review

- Direction: HIT — 양 지수 모두 큰 폭 하락.
- Volatility: HIT — KOSPI 장중 범위 약 2.08%, KOSDAQ 약 2.92%.
- Risk Sentiment: HIT — 글로벌 주식·채권 동반 매도와 유가 상승의 Risk-off.
- KOSPI/KOSDAQ 상대강도: MISS — 실제로 KOSPI -3.99%, KOSDAQ -2.10%로 KOSDAQ이 상대우위.
- 강세 섹터: PARTIAL — 정유 중 S-Oil은 상승했지만 SK이노베이션은 하락했고 방산·조선은 절대 약세.
- 약세 섹터: HIT — 반도체·화학·고밸류 성장주가 약세. 대한항공은 확정 일봉 부재로 평가 제외.

## 5. Stage별 성과

### 03:30 UP

- Candidate Count: 4
- Direction Hit Valid N: 4
- Direction Hit Rate: 25.00%
- 평균 Directional Return: -0.94%
- 평균 BADR: +3.05%
- UP TOP3 평균 Directional Return: -0.25%
- UP TOP3 평균 BADR: +3.74%
- 평균 FE: 1.03%
- 평균 AE: 2.99%
- O2C Hit Rate: N/A — 모든 O2C 예측이 UNCERTAIN

S-Oil만 절대 방향 HIT였다. 다만 네 후보 모두 KOSPI보다 나아 평균 BADR은 양수였다.

### 03:30 DOWN

- Candidate Count: 5
- Direction Hit Valid N: 4
- Direction Hit Rate: 100.00%
- 평균 Directional Return: +3.97%
- 평균 BADR: -0.02%
- DOWN TOP3 평균 Directional Return: +4.00% (확정 가능한 TOP2와 Rank4 사용이 아니라 TOP3 중 대한항공 N/A를 포함하므로 통계 계산은 실제 유효 2개 기준)
- DOWN TOP3 평균 BADR: +0.17% (SK하이닉스·삼성전자 유효 2개)
- 평균 FE: 4.58%
- 평균 AE: 0.80%
- O2C Hit Rate: N/A — 모든 O2C 예측이 UNCERTAIN

방향 적중은 강했지만 평균 BADR은 거의 0으로, 상당 부분은 시장 급락을 맞힌 결과였다.

### 08:25 UP

- Candidate Count: 5
- Direction Hit Valid N: 5
- Direction Hit Rate: 20.00%
- 평균 Directional Return: -1.86%
- 평균 BADR: +2.13%
- UP TOP3 평균 Directional Return: -3.38%
- UP TOP3 평균 BADR: +0.61%
- 평균 FE: 0.94%
- 평균 AE: 3.66%
- O2C Hit Rate: 100.00% (유효 예측 1개: 삼성전기)

신규 대형 계약주 4개 중 절대 상승한 종목은 없었다. S-Oil만 HIT였고, 계약 직접성이 시장 급락을 이기지 못했다.

### 08:25 DOWN

- Candidate Count: 5
- Direction Hit Valid N: 4
- Direction Hit Rate: 100.00%
- 평균 Directional Return: +3.73%
- 평균 BADR: +0.21%
- DOWN TOP3 평균 Directional Return: +3.79% (대한항공 N/A, 롯데케미칼·LG화학 유효 2개)
- DOWN TOP3 평균 BADR: -0.21% (대한항공 N/A, 롯데케미칼·LG화학 유효 2개)
- 평균 FE: 4.46%
- 평균 AE: 0.80%
- O2C Hit Rate: N/A — 대한항공만 DOWN 예측이었으나 실제값 N/A

하락 후보의 방향은 모두 맞았지만 BADR은 제한적이었다. 에코프로비엠과 SK하이닉스가 양의 BADR을 냈다.

## 6. Churn / Retention

- UP_RETENTION_RATE: 25.00% (S-Oil 1/4)
- DOWN_RETENTION_RATE: 80.00% (SK하이닉스·대한항공·롯데케미칼·LG화학 4/5)
- UP_CHURN_RATE: 75.00%
- DOWN_CHURN_RATE: 20.00%
- MAINTAINED_AVG_BADR: +1.32% (성과 확인 가능한 S-Oil·SK하이닉스·롯데케미칼·LG화학)
- NEW_AVG_BADR: +1.24%
- REMOVED_ACTUAL_BADR: +1.72%
- 잘 추가한 후보: 에코프로비엠 — DOWN 방향 HIT, BADR +0.74%.
- 잘못 추가한 후보: 삼성전기·한화오션·두산에너빌리티·유한양행 — 모두 UP 방향 MISS.
- 잘 제거한 후보: 삼성전자 — 03:30 DOWN 후보에서 제거됐으나 08:25 하락 후보군의 추가 상대성과는 제한적이었다. 단, 절대 방향은 계속 하락했으므로 완전한 성공으로 보기는 어렵다.
- 잘못 제거한 후보: 한국항공우주·한화에어로스페이스는 UP 예측 자체는 실패했으나 KOSPI 대비 BADR은 양수였다.
- 결론: UP 교체율이 높았지만 NEW 평균 BADR이 REMOVED보다 낮아, 장 마감 후 계약 공시로의 교체가 성과를 개선하지 못했다.

## 7. Rank Quality / Score Calibration

- 03:30 UP Score-Rank Concordance: EXACT
- 03:30 DOWN Score-Rank Concordance: LOW — Rank 2 삼성전자의 Base Score가 Rank 3 대한항공보다 낮아 Score와 Rank가 완전 정렬되지 않음.
- 08:25 UP Score-Rank Concordance: EXACT
- 08:25 DOWN Score-Rank Concordance: EXACT
- #1 품질: 03:30 UP #1 S-Oil은 해당 SIDE 최고 Directional Return과 BADR로 우수. 03:30 DOWN #1 SK하이닉스도 확인 가능한 후보 중 최고 Directional Return과 BADR. 08:25 UP #1 삼성전기는 S-Oil보다 열위. 08:25 DOWN #1 대한항공은 N/A.
- TOP3 품질: 08:25 UP TOP3는 #4~5보다 Directional Return과 BADR이 모두 나빠 Rank 품질이 낮았다.
- Spearman: 표본이 작고 대한항공 N/A가 있어 성과와 Score의 엄밀 상관계수는 N/A.
- SCORE_CALIBRATION_03_30: UP에서는 #1이 유효했으나 나머지 높은 점수는 절대 방향을 보장하지 못했다. DOWN은 방향 적중률이 높지만 BADR은 거의 0.
- SCORE_CALIBRATION_08_25: 높은 UP 점수와 직접 계약 촉매가 실제 수익으로 이어지지 않았다. DOWN 점수는 방향에는 유효했으나 상대성과 차이는 작았다.
- Confidence: 모든 후보가 MEDIUM이므로 Confidence 단조성은 평가 불가.
- Coverage: 03:30의 낮은 Coverage 후보와 08:25의 90% Coverage 후보 모두 UP 방향 실패가 많아 오늘 하루만으로 Coverage의 예측력을 확인할 수 없다.
- Price-in: 전 후보 UNVERIFIED. 높은 계약 직접성에도 갭 상승이 형성되지 않아 사전 가격·예상체결 검증 부재가 핵심 과정 위험으로 드러났다.

## 8. Scenario / Invalidation Review

- 시간순서가 필요한 자연어 Scenario는 신뢰할 수 있는 분봉 자료를 확보하지 못했다.
- SCENARIO: NOT SCORED — INTRADAY SEQUENCE DATA UNAVAILABLE
- OHLC만으로 갭 이후의 정확한 시간순서를 추정하지 않았다.
- 다만 고정 OpenExpectation은 기계적으로 평가했다. 03:30 S-Oil의 GAP_UP만 HIT, SK이노베이션 GAP_UP은 MISS, SK하이닉스·삼성전자 GAP_DOWN은 HIT. 08:25의 다섯 UP 후보 GAP_UP 중 S-Oil만 HIT했고, 네 확인 가능한 DOWN 후보의 GAP_DOWN은 모두 HIT했다.
- Invalidation은 당시 원문을 보존해 검토했으나, 시간순서·실시간 유가·업종 상대강도의 완결 자료가 없어 별도 점수화하지 않았다.

## 9. Error / Success Analysis

- BEST_CALL: 03:30 SK하이닉스 DOWN — C2C -4.49%, Directional Return +4.49%, FE 4.78%.
- WORST_CALL: 08:25 두산에너빌리티 UP — C2C -4.85%, Directional Return -4.85%, BADR -0.86%.
- PRIMARY_SUCCESS_PATTERN: Global Peer Lead와 Market Regime Fit. 반도체 약세와 전체 Risk-off 방향이 가장 안정적으로 작동했다.
- PRIMARY_ERROR_CLASS: CATALYST_ERROR
- PRIMARY_ERROR_SUBTYPE: Catalyst Overestimated
- 성공: S-Oil은 원유 급등의 직접 전달경로가 절대 상승으로 연결됐다. 하락 후보군은 Risk-off와 글로벌 반도체 약세가 방향 적중을 만들었다.
- 실패: 삼성전기·한화오션·두산에너빌리티·유한양행의 계약 촉매가 시장 급락과 갭 부재를 이기지 못했다. 03:30 방산 UP 후보도 직접 신규 촉매 없이 지정학 테마만으로는 부족했다.
- Evidence Double Counting: 08:25 신규 계약주에서 Catalyst와 Freshness가 모두 높게 반영됐으나, 실제 예상체결·기술 위치가 N/A인 상태에서 계약 직접성이 Rank에 과도하게 기여했을 가능성이 있다.

## 10. WATCH 효과

- 03:30 WATCH는 별도 구조화 WATCH 목록이 없어 후보군 기준 정성 평가.
- 08:25 WATCH 10개 중 대한항공을 제외한 9개에서 평균 절대 C2C는 2.76%, 평균 Intraday Range는 4.25%.
- 거래대금 상위권 진입 여부는 통합 시장 순위를 확보하지 못해 N/A.
- WATCH_EFFECTIVENESS_NOTE: 변동성 포착은 유효했으나 방향성은 하락 후보에 집중됐다. UP WATCH의 계약주들은 높은 관심에도 절대 방향 성과가 부진했다.

## 11. 오늘의 학습과 요약

- 가장 잘한 판단: 양 지수 DOWN, Risk-off, 반도체·화학 약세, S-Oil 상대강세.
- 가장 큰 오판: 직접 대형 계약 공시를 08:25 UP Rank 상단에 배치한 것. 시장 충격과 갭 부재를 충분히 할인하지 못했다.
- BETTER_STAGE: 03:30 — UP #1과 DOWN #1 품질, UP 평균 BADR에서 08:25보다 우수. 단, DOWN 방향 성과는 두 stage 모두 강했다.
- 가장 유효한 신호: SOXX·EWY 약세, 미국 10년물 상승, 유가 급등이 결합된 글로벌 전달경로.
- 가장 위험한 함정: 직접 공시의 신선도를 시장 레짐과 가격 확인보다 우선한 것.
- 강화할 기준: 개장 전 실제 갭·예상체결과 시장 충격 강도를 촉매 점수와 별도로 확인.
- 경계할 기준: 신규 계약 규모만으로 Risk-off에서 절대 상승을 가정하는 것.
- 추가 관찰: DOWN 후보의 높은 Hit Rate가 실제 종목선정력인지 시장 beta인지 BADR로 계속 분리.
- CARRY_FORWARD: 유가·미 10년물·USD/KRW와 외국인 반도체 수급. S-Oil의 상대강세 지속 여부와 계약주들의 갭 실패 후 후속 반응을 다음 거래일에 확인한다.
- 단 하루 결과로 규칙을 변경하지 않는다.

[REVIEW]
SCHEMA_VERSION: DMI_v7.1
DATE: 2026-09-02
AVAILABLE_STAGES: 03:30; 07:20; 08:25

03:30_REGIME_PRELIMINARY: Risk-off; Energy/Defense relative strength; Semiconductors/Airlines/Chemicals weakness; high yields, oil and KRW weakness constrain risk appetite
08:25_MARKET_VIEW_AT_SELECTION: KOSPI와 KOSDAQ 모두 DOWN 우위, KOSPI 상대우위; Risk-off; 정유·개별 대형 수주주 유리, 반도체·항공·화학·고밸류 성장주 불리; 고유가·4.79% 미 10년물·원화 약세가 핵심 제약

KOSPI_RETURN: -3.99%
KOSDAQ_RETURN: -2.10%
KOSPI_DIRECTION_FORECAST: DOWN
KOSPI_DIRECTION_ACTUAL: DOWN
KOSPI_DIRECTION_HIT: HIT
KOSDAQ_DIRECTION_FORECAST: DOWN
KOSDAQ_DIRECTION_ACTUAL: DOWN
KOSDAQ_DIRECTION_HIT: HIT

MARKET_REGIME_NOTE: Risk-off와 고변동성 및 반도체·화학 약세는 적중; KOSPI 상대우위와 방산·조선 강세는 실패; 정유는 S-Oil 중심 부분 적중

03:30_UP_COUNT: 4
03:30_UP_HIT_VALID_N: 4
03:30_UP_HIT_RATE: 25.00%
03:30_UP_AVG_DIRECTIONAL_RETURN: -0.94%
03:30_UP_AVG_BADR: +3.05%
03:30_UP_TOP3_DIRECTIONAL_RETURN: -0.25%
03:30_UP_TOP3_BADR: +3.74%

03:30_DOWN_COUNT: 5
03:30_DOWN_HIT_VALID_N: 4
03:30_DOWN_HIT_RATE: 100.00%
03:30_DOWN_AVG_DIRECTIONAL_RETURN: +3.97%
03:30_DOWN_AVG_BADR: -0.02%
03:30_DOWN_TOP3_DIRECTIONAL_RETURN: +4.16%
03:30_DOWN_TOP3_BADR: +0.17%

03:30_AVG_FE: 2.80%
03:30_AVG_AE: 1.89%
03:30_O2C_HIT_RATE: N/A

08:25_UP_COUNT: 5
08:25_UP_HIT_VALID_N: 5
08:25_UP_HIT_RATE: 20.00%
08:25_UP_AVG_DIRECTIONAL_RETURN: -1.86%
08:25_UP_AVG_BADR: +2.13%
08:25_UP_TOP3_DIRECTIONAL_RETURN: -3.38%
08:25_UP_TOP3_BADR: +0.61%

08:25_DOWN_COUNT: 5
08:25_DOWN_HIT_VALID_N: 4
08:25_DOWN_HIT_RATE: 100.00%
08:25_DOWN_AVG_DIRECTIONAL_RETURN: +3.73%
08:25_DOWN_AVG_BADR: +0.21%
08:25_DOWN_TOP3_DIRECTIONAL_RETURN: +3.79%
08:25_DOWN_TOP3_BADR: -0.21%

08:25_AVG_FE: 2.50%
08:25_AVG_AE: 2.39%
08:25_O2C_HIT_RATE: 100.00%

UP_RETENTION_RATE: 25.00%
DOWN_RETENTION_RATE: 80.00%
UP_CHURN_RATE: 75.00%
DOWN_CHURN_RATE: 20.00%
MAINTAINED_AVG_BADR: +1.32%
NEW_AVG_BADR: +1.24%
REMOVED_ACTUAL_BADR: +1.72%

03:30_UP_SCORE_RANK_CONCORDANCE: EXACT
03:30_DOWN_SCORE_RANK_CONCORDANCE: LOW
08:25_UP_SCORE_RANK_CONCORDANCE: EXACT
08:25_DOWN_SCORE_RANK_CONCORDANCE: EXACT

BETTER_STAGE: 03:30

RESULTS_03_30:
SIDE|RANK|종목|Code|Market|BaseScore|RawScore|AvailableMax|Coverage|Breakdown|Confidence|FreshGrade|PriceInCheck|OpenExpectation|OpenActual|OpenHit|O2CForecast|O2CActual|O2CHit|PriceIn|PrimaryCatalystType|SecondaryCatalystType|C2C|DirectionalReturn|BADR|HIT-MISS-FLAT|FE|AE|SuccessFactor|ErrorClass|ErrorSubtype
UP|1|S-Oil|010950|KOSPI|87.7|57|65|65%|20/15/13/N/A/N/A/9/N/A|MEDIUM|S|UNVERIFIED|GAP_UP|GAP_UP|HIT|UNCERTAIN|-1.03%|N/A|MEDIUM|Macro_FX_Commodity|Supply_Demand|+1.19%|+1.19%|+5.18%|HIT|3.43%|2.50%|Catalyst Strength|N/A|N/A
UP|2|SK이노베이션|096770|KOSPI|84.6|55|65|65%|19/15/12/N/A/N/A/9/N/A|MEDIUM|S|UNVERIFIED|GAP_UP|GAP_DOWN|MISS|UNCERTAIN|+0.82%|N/A|MEDIUM|Macro_FX_Commodity|Sector_Theme|-0.44%|-0.44%|+3.55%|MISS|0.67%|2.88%|N/A|PRICING_ERROR|Profit Taking
UP|3|한화에어로스페이스|012450|KOSPI|72.3|47|65|65%|14/15/9/N/A/N/A/9/N/A|MEDIUM|S|UNVERIFIED|UNCERTAIN|GAP_DOWN|N/A|UNCERTAIN|-0.57%|N/A|HIGH|Sector_Theme|Policy_Regulation|-1.51%|-1.51%|+2.48%|MISS|0.00%|2.17%|N/A|CATALYST_ERROR|Catalyst Overestimated
UP|4|한국항공우주|047810|KOSPI|69.2|45|65|65%|13/15/9/N/A/N/A/8/N/A|MEDIUM|S|UNVERIFIED|UNCERTAIN|GAP_DOWN|N/A|UNCERTAIN|-1.36%|N/A|HIGH|Sector_Theme|Policy_Regulation|-2.99%|-2.99%|+1.00%|MISS|0.00%|4.40%|N/A|CATALYST_ERROR|Catalyst Overestimated
DOWN|1|SK하이닉스|000660|KOSPI|85.0|68|80|80%|17/15/13/14/N/A/9/N/A|MEDIUM|S|UNVERIFIED|GAP_DOWN|GAP_DOWN|HIT|UNCERTAIN|-0.80%|N/A|MEDIUM|Global_Peer|Macro_FX_Commodity|-4.49%|+4.49%|+0.50%|HIT|4.78%|0.00%|Global Peer Lead|N/A|N/A
DOWN|2|삼성전자|005930|KOSPI|81.3|65|80|80%|15/15/13/14/N/A/8/N/A|MEDIUM|S|UNVERIFIED|GAP_DOWN|GAP_DOWN|HIT|UNCERTAIN|-0.40%|N/A|MEDIUM|Global_Peer|Macro_FX_Commodity|-3.83%|+3.83%|-0.16%|HIT|4.41%|0.00%|Market Regime Fit|N/A|N/A
DOWN|3|대한항공|003490|KOSPI|83.1|54|65|65%|18/15/12/N/A/N/A/9/N/A|MEDIUM|S|UNVERIFIED|GAP_DOWN|N/A|N/A|UNCERTAIN|N/A|N/A|MEDIUM|Macro_FX_Commodity|Supply_Demand|N/A|N/A|N/A|NOT_COMPARABLE|N/A|N/A|N/A|N/A|N/A
DOWN|4|롯데케미칼|011170|KOSPI|76.9|50|65|65%|16/15/11/N/A/N/A/8/N/A|MEDIUM|S|UNVERIFIED|UNCERTAIN|GAP_DOWN|N/A|UNCERTAIN|-2.53%|N/A|MEDIUM|Macro_FX_Commodity|Sector_Theme|-3.67%|+3.67%|-0.32%|HIT|4.50%|0.00%|Market Regime Fit|N/A|N/A
DOWN|5|LG화학|051910|KOSPI|73.8|48|65|65%|15/15/10/N/A/N/A/8/N/A|MEDIUM|S|UNVERIFIED|UNCERTAIN|GAP_DOWN|N/A|UNCERTAIN|-2.52%|N/A|MEDIUM|Macro_FX_Commodity|Sector_Theme|-3.90%|+3.90%|-0.09%|HIT|4.61%|3.19%|Market Regime Fit|N/A|N/A

RESULTS_08_25:
SIDE|RANK|종목|Code|Market|BaseScore|RawScore|AvailableMax|Coverage|Breakdown|Confidence|FreshGrade|PriceInCheck|OpenExpectation|OpenActual|OpenHit|O2CForecast|O2CActual|O2CHit|PriceIn|ChaseRisk|PrimaryCatalystType|SecondaryCatalystType|C2C|DirectionalReturn|BADR|HIT-MISS-FLAT|FE|AE|SuccessFactor|ErrorClass|ErrorSubtype
UP|1|삼성전기|009150|KOSPI|88.9|80|90|90%|23/15/11/10/N/A/8/8|MEDIUM|S|UNVERIFIED|GAP_UP|GAP_DOWN|MISS|UP|+2.32%|HIT|MEDIUM|HIGH|Contract_Order|Sector_Theme|-1.19%|-1.19%|+2.80%|MISS|0.56%|4.27%|N/A|CATALYST_ERROR|Catalyst Overestimated
UP|2|한화오션|042660|KOSPI|84.4|76|90|90%|21/15/11/9/N/A/9/6|MEDIUM|S|UNVERIFIED|GAP_UP|GAP_DOWN|MISS|UNCERTAIN|-0.71%|N/A|MEDIUM|HIGH|Contract_Order|Supply_Demand|-4.10%|-4.10%|-0.11%|MISS|0.00%|4.55%|N/A|MARKET_CONTEXT_ERROR|Market Regime Misread
UP|3|두산에너빌리티|034020|KOSPI|82.2|74|90|90%|20/15/11/9/N/A/9/6|MEDIUM|S|UNVERIFIED|GAP_UP|GAP_DOWN|MISS|UNCERTAIN|-1.71%|N/A|HIGH|VERY_HIGH|Contract_Order|Sector_Theme|-4.85%|-4.85%|-0.86%|MISS|0.00%|5.28%|N/A|PRICING_ERROR|Already Priced-in
UP|4|S-Oil|010950|KOSPI|81.1|73|90|90%|20/15/13/9/N/A/9/7|MEDIUM|S|UNVERIFIED|GAP_UP|GAP_UP|HIT|UNCERTAIN|-1.03%|N/A|MEDIUM|HIGH|Macro_FX_Commodity|Supply_Demand|+1.19%|+1.19%|+5.18%|HIT|3.43%|2.50%|Catalyst Strength|N/A|N/A
UP|5|유한양행|000100|KOSPI|77.8|70|90|90%|18/15/7/8/N/A/7/8|MEDIUM|S|UNVERIFIED|GAP_UP|FLAT|MISS|UNCERTAIN|-0.36%|N/A|LOW|MEDIUM|Contract_Order|Other|-0.36%|-0.36%|+3.63%|MISS|0.73%|1.69%|N/A|CATALYST_ERROR|Catalyst Overestimated
DOWN|1|대한항공|003490|KOSPI|84.4|76|90|90%|21/15/13/9/N/A/9/9|MEDIUM|S|UNVERIFIED|GAP_DOWN|N/A|N/A|DOWN|N/A|N/A|MEDIUM|MEDIUM|Macro_FX_Commodity|Supply_Demand|N/A|N/A|N/A|NOT_COMPARABLE|N/A|N/A|N/A|N/A|N/A
DOWN|2|롯데케미칼|011170|KOSPI|80.0|72|90|90%|19/15/12/8/N/A/9/9|MEDIUM|S|UNVERIFIED|GAP_DOWN|GAP_DOWN|HIT|UNCERTAIN|-2.53%|N/A|MEDIUM|MEDIUM|Macro_FX_Commodity|Sector_Theme|-3.67%|+3.67%|-0.32%|HIT|4.50%|0.00%|Market Regime Fit|N/A|N/A
DOWN|3|LG화학|051910|KOSPI|76.7|69|90|90%|17/15/11/8/N/A/9/9|MEDIUM|S|UNVERIFIED|GAP_DOWN|GAP_DOWN|HIT|UNCERTAIN|-2.52%|N/A|MEDIUM|MEDIUM|Macro_FX_Commodity|Sector_Theme|-3.90%|+3.90%|-0.09%|HIT|4.61%|3.19%|Market Regime Fit|N/A|N/A
DOWN|4|SK하이닉스|000660|KOSPI|74.4|67|90|90%|17/15/13/11/N/A/8/3|MEDIUM|S|UNVERIFIED|GAP_DOWN|GAP_DOWN|HIT|UNCERTAIN|-0.80%|N/A|HIGH|HIGH|Global_Peer|Macro_FX_Commodity|-4.49%|+4.49%|+0.50%|HIT|4.78%|0.00%|Global Peer Lead|N/A|N/A
DOWN|5|에코프로비엠|247540|KOSDAQ|70.0|63|90|90%|14/15/10/8/N/A/9/7|MEDIUM|S|UNVERIFIED|GAP_DOWN|GAP_DOWN|HIT|UNCERTAIN|+1.16%|N/A|MEDIUM|MEDIUM|Macro_FX_Commodity|Sector_Theme|-2.84%|+2.84%|+0.74%|HIT|3.96%|0.00%|Market Regime Fit|N/A|N/A

WATCH_EFFECTIVENESS_NOTE: 08:25 WATCH 중 확인 가능한 9개 평균 절대 C2C 2.76%, 평균 Intraday Range 4.25%; 변동성 포착은 유효했으나 UP 계약주의 방향성은 부진

BEST_CALL: 03:30 SK하이닉스 DOWN; Directional Return +4.49%; BADR +0.50%
WORST_CALL: 08:25 두산에너빌리티 UP; Directional Return -4.85%; BADR -0.86%
PRIMARY_SUCCESS_PATTERN: Global Peer Lead and Market Regime Fit
PRIMARY_ERROR_CLASS: CATALYST_ERROR
PRIMARY_ERROR_SUBTYPE: Catalyst Overestimated

SCORE_CALIBRATION_03_30: UP #1 S-Oil과 DOWN #1 SK하이닉스는 우수했으나 DOWN 평균 BADR은 거의 0으로 시장 beta 영향이 큼
SCORE_CALIBRATION_08_25: UP 고점수 직접 계약주가 절대 방향을 만들지 못했고 TOP3가 하위 Rank보다 부진
CONFIDENCE_CALIBRATION_03_30: 모든 후보 MEDIUM으로 단조성 평가 불가
CONFIDENCE_CALIBRATION_08_25: 모든 후보 MEDIUM으로 단조성 평가 불가
COVERAGE_CALIBRATION_NOTE: 65~80%와 90% Coverage 모두 UP 실패가 있어 하루 결과로 예측력 판단 불가
PRICE_IN_VERIFICATION_NOTE: 전 후보 UNVERIFIED; 개장 전 가격 확인 부재가 계약주 과대평가 위험으로 나타남
EVIDENCE_DOUBLE_COUNTING_NOTE: 신규 계약의 Catalyst와 Freshness가 동시 고득점이었으나 기술·예상체결 N/A를 충분히 상쇄하지 못했을 가능성
CARRY_FORWARD: 유가·미 10년물·USD/KRW·외국인 반도체 수급, S-Oil 상대강세와 계약주 후속 반응 확인
[/REVIEW]
[/STAGE_REPORT]

[STAGE_REVIEW_CAPSULE]
[REVIEW]
SCHEMA_VERSION: DMI_v7.1
DATE: 2026-09-02
AVAILABLE_STAGES: 03:30; 07:20; 08:25

03:30_REGIME_PRELIMINARY: Risk-off; Energy/Defense relative strength; Semiconductors/Airlines/Chemicals weakness; high yields, oil and KRW weakness constrain risk appetite
08:25_MARKET_VIEW_AT_SELECTION: KOSPI와 KOSDAQ 모두 DOWN 우위, KOSPI 상대우위; Risk-off; 정유·개별 대형 수주주 유리, 반도체·항공·화학·고밸류 성장주 불리; 고유가·4.79% 미 10년물·원화 약세가 핵심 제약

KOSPI_RETURN: -3.99%
KOSDAQ_RETURN: -2.10%
KOSPI_DIRECTION_FORECAST: DOWN
KOSPI_DIRECTION_ACTUAL: DOWN
KOSPI_DIRECTION_HIT: HIT
KOSDAQ_DIRECTION_FORECAST: DOWN
KOSDAQ_DIRECTION_ACTUAL: DOWN
KOSDAQ_DIRECTION_HIT: HIT

MARKET_REGIME_NOTE: Risk-off와 고변동성 및 반도체·화학 약세는 적중; KOSPI 상대우위와 방산·조선 강세는 실패; 정유는 S-Oil 중심 부분 적중

03:30_UP_COUNT: 4
03:30_UP_HIT_VALID_N: 4
03:30_UP_HIT_RATE: 25.00%
03:30_UP_AVG_DIRECTIONAL_RETURN: -0.94%
03:30_UP_AVG_BADR: +3.05%
03:30_UP_TOP3_DIRECTIONAL_RETURN: -0.25%
03:30_UP_TOP3_BADR: +3.74%

03:30_DOWN_COUNT: 5
03:30_DOWN_HIT_VALID_N: 4
03:30_DOWN_HIT_RATE: 100.00%
03:30_DOWN_AVG_DIRECTIONAL_RETURN: +3.97%
03:30_DOWN_AVG_BADR: -0.02%
03:30_DOWN_TOP3_DIRECTIONAL_RETURN: +4.16%
03:30_DOWN_TOP3_BADR: +0.17%

03:30_AVG_FE: 2.80%
03:30_AVG_AE: 1.89%
03:30_O2C_HIT_RATE: N/A

08:25_UP_COUNT: 5
08:25_UP_HIT_VALID_N: 5
08:25_UP_HIT_RATE: 20.00%
08:25_UP_AVG_DIRECTIONAL_RETURN: -1.86%
08:25_UP_AVG_BADR: +2.13%
08:25_UP_TOP3_DIRECTIONAL_RETURN: -3.38%
08:25_UP_TOP3_BADR: +0.61%

08:25_DOWN_COUNT: 5
08:25_DOWN_HIT_VALID_N: 4
08:25_DOWN_HIT_RATE: 100.00%
08:25_DOWN_AVG_DIRECTIONAL_RETURN: +3.73%
08:25_DOWN_AVG_BADR: +0.21%
08:25_DOWN_TOP3_DIRECTIONAL_RETURN: +3.79%
08:25_DOWN_TOP3_BADR: -0.21%

08:25_AVG_FE: 2.50%
08:25_AVG_AE: 2.39%
08:25_O2C_HIT_RATE: 100.00%

UP_RETENTION_RATE: 25.00%
DOWN_RETENTION_RATE: 80.00%
UP_CHURN_RATE: 75.00%
DOWN_CHURN_RATE: 20.00%
MAINTAINED_AVG_BADR: +1.32%
NEW_AVG_BADR: +1.24%
REMOVED_ACTUAL_BADR: +1.72%

03:30_UP_SCORE_RANK_CONCORDANCE: EXACT
03:30_DOWN_SCORE_RANK_CONCORDANCE: LOW
08:25_UP_SCORE_RANK_CONCORDANCE: EXACT
08:25_DOWN_SCORE_RANK_CONCORDANCE: EXACT

BETTER_STAGE: 03:30

RESULTS_03_30:
SIDE|RANK|종목|Code|Market|BaseScore|RawScore|AvailableMax|Coverage|Breakdown|Confidence|FreshGrade|PriceInCheck|OpenExpectation|OpenActual|OpenHit|O2CForecast|O2CActual|O2CHit|PriceIn|PrimaryCatalystType|SecondaryCatalystType|C2C|DirectionalReturn|BADR|HIT-MISS-FLAT|FE|AE|SuccessFactor|ErrorClass|ErrorSubtype
UP|1|S-Oil|010950|KOSPI|87.7|57|65|65%|20/15/13/N/A/N/A/9/N/A|MEDIUM|S|UNVERIFIED|GAP_UP|GAP_UP|HIT|UNCERTAIN|-1.03%|N/A|MEDIUM|Macro_FX_Commodity|Supply_Demand|+1.19%|+1.19%|+5.18%|HIT|3.43%|2.50%|Catalyst Strength|N/A|N/A
UP|2|SK이노베이션|096770|KOSPI|84.6|55|65|65%|19/15/12/N/A/N/A/9/N/A|MEDIUM|S|UNVERIFIED|GAP_UP|GAP_DOWN|MISS|UNCERTAIN|+0.82%|N/A|MEDIUM|Macro_FX_Commodity|Sector_Theme|-0.44%|-0.44%|+3.55%|MISS|0.67%|2.88%|N/A|PRICING_ERROR|Profit Taking
UP|3|한화에어로스페이스|012450|KOSPI|72.3|47|65|65%|14/15/9/N/A/N/A/9/N/A|MEDIUM|S|UNVERIFIED|UNCERTAIN|GAP_DOWN|N/A|UNCERTAIN|-0.57%|N/A|HIGH|Sector_Theme|Policy_Regulation|-1.51%|-1.51%|+2.48%|MISS|0.00%|2.17%|N/A|CATALYST_ERROR|Catalyst Overestimated
UP|4|한국항공우주|047810|KOSPI|69.2|45|65|65%|13/15/9/N/A/N/A/8/N/A|MEDIUM|S|UNVERIFIED|UNCERTAIN|GAP_DOWN|N/A|UNCERTAIN|-1.36%|N/A|HIGH|Sector_Theme|Policy_Regulation|-2.99%|-2.99%|+1.00%|MISS|0.00%|4.40%|N/A|CATALYST_ERROR|Catalyst Overestimated
DOWN|1|SK하이닉스|000660|KOSPI|85.0|68|80|80%|17/15/13/14/N/A/9/N/A|MEDIUM|S|UNVERIFIED|GAP_DOWN|GAP_DOWN|HIT|UNCERTAIN|-0.80%|N/A|MEDIUM|Global_Peer|Macro_FX_Commodity|-4.49%|+4.49%|+0.50%|HIT|4.78%|0.00%|Global Peer Lead|N/A|N/A
DOWN|2|삼성전자|005930|KOSPI|81.3|65|80|80%|15/15/13/14/N/A/8/N/A|MEDIUM|S|UNVERIFIED|GAP_DOWN|GAP_DOWN|HIT|UNCERTAIN|-0.40%|N/A|MEDIUM|Global_Peer|Macro_FX_Commodity|-3.83%|+3.83%|-0.16%|HIT|4.41%|0.00%|Market Regime Fit|N/A|N/A
DOWN|3|대한항공|003490|KOSPI|83.1|54|65|65%|18/15/12/N/A/N/A/9/N/A|MEDIUM|S|UNVERIFIED|GAP_DOWN|N/A|N/A|UNCERTAIN|N/A|N/A|MEDIUM|Macro_FX_Commodity|Supply_Demand|N/A|N/A|N/A|NOT_COMPARABLE|N/A|N/A|N/A|N/A|N/A
DOWN|4|롯데케미칼|011170|KOSPI|76.9|50|65|65%|16/15/11/N/A/N/A/8/N/A|MEDIUM|S|UNVERIFIED|UNCERTAIN|GAP_DOWN|N/A|UNCERTAIN|-2.53%|N/A|MEDIUM|Macro_FX_Commodity|Sector_Theme|-3.67%|+3.67%|-0.32%|HIT|4.50%|0.00%|Market Regime Fit|N/A|N/A
DOWN|5|LG화학|051910|KOSPI|73.8|48|65|65%|15/15/10/N/A/N/A/8/N/A|MEDIUM|S|UNVERIFIED|UNCERTAIN|GAP_DOWN|N/A|UNCERTAIN|-2.52%|N/A|MEDIUM|Macro_FX_Commodity|Sector_Theme|-3.90%|+3.90%|-0.09%|HIT|4.61%|3.19%|Market Regime Fit|N/A|N/A

RESULTS_08_25:
SIDE|RANK|종목|Code|Market|BaseScore|RawScore|AvailableMax|Coverage|Breakdown|Confidence|FreshGrade|PriceInCheck|OpenExpectation|OpenActual|OpenHit|O2CForecast|O2CActual|O2CHit|PriceIn|ChaseRisk|PrimaryCatalystType|SecondaryCatalystType|C2C|DirectionalReturn|BADR|HIT-MISS-FLAT|FE|AE|SuccessFactor|ErrorClass|ErrorSubtype
UP|1|삼성전기|009150|KOSPI|88.9|80|90|90%|23/15/11/10/N/A/8/8|MEDIUM|S|UNVERIFIED|GAP_UP|GAP_DOWN|MISS|UP|+2.32%|HIT|MEDIUM|HIGH|Contract_Order|Sector_Theme|-1.19%|-1.19%|+2.80%|MISS|0.56%|4.27%|N/A|CATALYST_ERROR|Catalyst Overestimated
UP|2|한화오션|042660|KOSPI|84.4|76|90|90%|21/15/11/9/N/A/9/6|MEDIUM|S|UNVERIFIED|GAP_UP|GAP_DOWN|MISS|UNCERTAIN|-0.71%|N/A|MEDIUM|HIGH|Contract_Order|Supply_Demand|-4.10%|-4.10%|-0.11%|MISS|0.00%|4.55%|N/A|MARKET_CONTEXT_ERROR|Market Regime Misread
UP|3|두산에너빌리티|034020|KOSPI|82.2|74|90|90%|20/15/11/9/N/A/9/6|MEDIUM|S|UNVERIFIED|GAP_UP|GAP_DOWN|MISS|UNCERTAIN|-1.71%|N/A|HIGH|VERY_HIGH|Contract_Order|Sector_Theme|-4.85%|-4.85%|-0.86%|MISS|0.00%|5.28%|N/A|PRICING_ERROR|Already Priced-in
UP|4|S-Oil|010950|KOSPI|81.1|73|90|90%|20/15/13/9/N/A/9/7|MEDIUM|S|UNVERIFIED|GAP_UP|GAP_UP|HIT|UNCERTAIN|-1.03%|N/A|MEDIUM|HIGH|Macro_FX_Commodity|Supply_Demand|+1.19%|+1.19%|+5.18%|HIT|3.43%|2.50%|Catalyst Strength|N/A|N/A
UP|5|유한양행|000100|KOSPI|77.8|70|90|90%|18/15/7/8/N/A/7/8|MEDIUM|S|UNVERIFIED|GAP_UP|FLAT|MISS|UNCERTAIN|-0.36%|N/A|LOW|MEDIUM|Contract_Order|Other|-0.36%|-0.36%|+3.63%|MISS|0.73%|1.69%|N/A|CATALYST_ERROR|Catalyst Overestimated
DOWN|1|대한항공|003490|KOSPI|84.4|76|90|90%|21/15/13/9/N/A/9/9|MEDIUM|S|UNVERIFIED|GAP_DOWN|N/A|N/A|DOWN|N/A|N/A|MEDIUM|MEDIUM|Macro_FX_Commodity|Supply_Demand|N/A|N/A|N/A|NOT_COMPARABLE|N/A|N/A|N/A|N/A|N/A
DOWN|2|롯데케미칼|011170|KOSPI|80.0|72|90|90%|19/15/12/8/N/A/9/9|MEDIUM|S|UNVERIFIED|GAP_DOWN|GAP_DOWN|HIT|UNCERTAIN|-2.53%|N/A|MEDIUM|MEDIUM|Macro_FX_Commodity|Sector_Theme|-3.67%|+3.67%|-0.32%|HIT|4.50%|0.00%|Market Regime Fit|N/A|N/A
DOWN|3|LG화학|051910|KOSPI|76.7|69|90|90%|17/15/11/8/N/A/9/9|MEDIUM|S|UNVERIFIED|GAP_DOWN|GAP_DOWN|HIT|UNCERTAIN|-2.52%|N/A|MEDIUM|MEDIUM|Macro_FX_Commodity|Sector_Theme|-3.90%|+3.90%|-0.09%|HIT|4.61%|3.19%|Market Regime Fit|N/A|N/A
DOWN|4|SK하이닉스|000660|KOSPI|74.4|67|90|90%|17/15/13/11/N/A/8/3|MEDIUM|S|UNVERIFIED|GAP_DOWN|GAP_DOWN|HIT|UNCERTAIN|-0.80%|N/A|HIGH|HIGH|Global_Peer|Macro_FX_Commodity|-4.49%|+4.49%|+0.50%|HIT|4.78%|0.00%|Global Peer Lead|N/A|N/A
DOWN|5|에코프로비엠|247540|KOSDAQ|70.0|63|90|90%|14/15/10/8/N/A/9/7|MEDIUM|S|UNVERIFIED|GAP_DOWN|GAP_DOWN|HIT|UNCERTAIN|+1.16%|N/A|MEDIUM|MEDIUM|Macro_FX_Commodity|Sector_Theme|-2.84%|+2.84%|+0.74%|HIT|3.96%|0.00%|Market Regime Fit|N/A|N/A

WATCH_EFFECTIVENESS_NOTE: 08:25 WATCH 중 확인 가능한 9개 평균 절대 C2C 2.76%, 평균 Intraday Range 4.25%; 변동성 포착은 유효했으나 UP 계약주의 방향성은 부진

BEST_CALL: 03:30 SK하이닉스 DOWN; Directional Return +4.49%; BADR +0.50%
WORST_CALL: 08:25 두산에너빌리티 UP; Directional Return -4.85%; BADR -0.86%
PRIMARY_SUCCESS_PATTERN: Global Peer Lead and Market Regime Fit
PRIMARY_ERROR_CLASS: CATALYST_ERROR
PRIMARY_ERROR_SUBTYPE: Catalyst Overestimated

SCORE_CALIBRATION_03_30: UP #1 S-Oil과 DOWN #1 SK하이닉스는 우수했으나 DOWN 평균 BADR은 거의 0으로 시장 beta 영향이 큼
SCORE_CALIBRATION_08_25: UP 고점수 직접 계약주가 절대 방향을 만들지 못했고 TOP3가 하위 Rank보다 부진
CONFIDENCE_CALIBRATION_03_30: 모든 후보 MEDIUM으로 단조성 평가 불가
CONFIDENCE_CALIBRATION_08_25: 모든 후보 MEDIUM으로 단조성 평가 불가
COVERAGE_CALIBRATION_NOTE: 65~80%와 90% Coverage 모두 UP 실패가 있어 하루 결과로 예측력 판단 불가
PRICE_IN_VERIFICATION_NOTE: 전 후보 UNVERIFIED; 개장 전 가격 확인 부재가 계약주 과대평가 위험으로 나타남
EVIDENCE_DOUBLE_COUNTING_NOTE: 신규 계약의 Catalyst와 Freshness가 동시 고득점이었으나 기술·예상체결 N/A를 충분히 상쇄하지 못했을 가능성
CARRY_FORWARD: 유가·미 10년물·USD/KRW·외국인 반도체 수급, S-Oil 상대강세와 계약주 후속 반응 확인
[/REVIEW]
[/STAGE_REVIEW_CAPSULE]
