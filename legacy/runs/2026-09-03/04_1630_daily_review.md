[DMI_RUN_META]
SCHEMA_VERSION: DMI_v7.1
DATE: 2026-09-03
STAGE: 16:30
RUN_TIME_KST: 2026-09-03 16:27:42
[/DMI_RUN_META]

[STAGE_REPORT]
DATE: 2026-09-03
STAGE: 16:30 Daily Review
GROUND_TRUTH_TIME: 2026-09-03 16:22 KST
DATA_STATUS: KRX 정규장 종가 확정; 투자자 수급은 16:22 공개값

## 1. 예측 원본 상태
- 03:30 REPORT/HANDOFF: AVAILABLE
- 07:20 REPORT/HANDOFF: AVAILABLE
- 08:25 REPORT/HANDOFF: PREVIOUS_STAGE_UNAVAILABLE
- 08:25 후보·Rank·Score·시장전망은 사후 재구성하지 않았다.
- 정상 Review 파일은 실행 전 존재하지 않아 정상 경로를 사용한다.

## 2. 실제 시장 Ground Truth
- KOSPI 6,579.48, +0.26%; KOSDAQ 790.21, -1.71%. KOSPI 상승 424·하락 433, KOSDAQ 상승 520·하락 1,079로 시장 내부는 KOSDAQ 중심 약세였다.
- KOSPI 수급: 개인 -9,551.6억원, 기관 -2,152.7억원, 외국인 -4,231.9억원. KOSDAQ: 개인 +2,950.8억원, 기관 -1,846.3억원, 외국인 -1,075.3억원. 기타법인 등 미표시 주체 영향 때문에 표시 수급 합계와 지수 방향을 단순 등치하지 않는다.
- 실제 강세 테마는 보험·금융, 건설기계, 철강과 일부 조선이었다. 삼성중공업 +8.07%, HD현대중공업 +3.08%가 조선 breadth를 확인했다.
- 원/달러는 1,350원대로 하락했고, 장중 미국 금리·전쟁 불안이 상승폭을 제한했다.
- 지수·수급·테마 출처: [알파스퀘어 시장요약, 2026-09-03 16:23](https://alphasquare.co.kr/home/market-summary)
- 오전에는 KOSPI·KOSDAQ 모두 1%대 상승 출발했으나 KOSDAQ이 먼저 하락 전환했다. Broadcom 시간외 약세와 고유가가 상단을 제약했다. [연합뉴스, 2026-09-03](https://www.yna.co.kr/view/AKR20260903047900008)
- 종목 OHLC는 각 회사 IR·Google Finance·매일경제·알파스퀘어의 15:30~15:33 KRX 정규장 값을 교차확인했다. 시간외 값은 C2C에 혼합하지 않았다.

## 3. Corporate Action Check
- 평가일 당일 비교를 왜곡하는 액면분할·병합·무상증자·권리락은 후보군에서 확인되지 않았다.
- 롯데케미칼 배당락 표시는 9월 2일이며 9월 3일 Previous Close 57,300원은 이미 전일 확정가격이므로 별도 조정 없이 비교했다.
- 삼성전자·SK하이닉스 등 표시된 과거/향후 배당락일은 당일 비교를 왜곡하지 않았다.

## 4. TASK 2 지수 방향 검증
- KOSPI: UP 예측 vs +0.26% UP actual → HIT.
- KOSDAQ: UP 예측 vs -1.71% DOWN actual → MISS.
- 정성 레짐: PARTIAL. KOSPI 상대우위와 높은 변동성은 적중했으나 KOSDAQ 반등 실패, AI 하드웨어·정유 주도 실패, 항공·석유화학 약세 실패로 핵심 섹터 판단은 약했다.

## 5. 03:30 성능
- UP: 5개, 1 HIT, Hit Rate 20.0%, 평균 Directional Return -0.78%, 평균 BADR -1.03%.
- DOWN: 5개, 2 HIT, Hit Rate 40.0%, 평균 Directional Return -2.43%, 평균 BADR -2.18%.
- 전체 평균 FE 2.20%, AE 4.42%, O2C Hit Rate 33.3%.
- UP TOP3 평균 Directional Return -1.08%, DOWN TOP3 -4.67%로 양쪽 모두 상위 Rank가 하위 Rank보다 부진했다.
- 상승 #1 삼성전자는 -0.20%, 하락 #1 대한항공은 +0.87%로 두 #1 모두 MISS.
- Score-Rank 자체 정렬은 양 SIDE Spearman 0.90이나 실제 성과와의 순위 정합성은 낮았다.

## 6. 후보별 핵심 진단
- BEST: HD현대중공업 UP. +3.08%, BADR +2.83%. 조선 섹터 breadth가 실제로 확인됐다.
- WORST: LG화학 DOWN. +6.69%, BADR -6.44%. 고유가→석유화학 약세 전달 가정이 정반대로 작동했다.
- 롯데케미칼 DOWN도 +6.46%로 크게 실패해 개별종목 문제가 아니라 Sector Misread 가능성이 높다.
- 삼성전기 UP은 -3.71%로 AI 부품 follower 선택이 실패했다.
- NAVER·카카오 DOWN은 각각 -0.72%, -1.14%로 적중했다.
- SCENARIO: NOT SCORED — INTRADAY SEQUENCE DATA UNAVAILABLE. OHLC만으로 고가·저가 발생 순서를 추정하지 않았다.

## 7. 08:25 성능 및 Churn
PREVIOUS_STAGE_UNAVAILABLE. 저장된 08:25 원본이 없으므로 성능·Retention·Churn·추가/제거 효과·Score calibration을 계산하지 않았다.

## 8. Error / Success 분석
- 주요 성공요인: Sector Breadth. 조선의 동반 강세와 플랫폼 약세 지속.
- 주요 오류: MARKET_CONTEXT_ERROR / Sector Misread.
- 보조 오류: 미국 AI 주식 상승의 국내 종가 전이 실패, 고유가의 정유·항공 전달 과대평가, 삼성전기 follower 선택.
- 고유가 신호가 S-Oil·대한항공·롯데케미칼·LG화학에 반복 사용됐고 여러 Score 항목에도 반영됐다. 한 개 매크로 FACT가 다수 후보와 C·S·M을 동시에 지배한 구조는 향후 반복 여부를 점검해야 한다.

## 9. 오늘의 학습
- 강화: 개장 후 시장 breadth와 실제 외국인 수급을 글로벌 선행지표와 별도로 검증.
- 경계: 미국 반도체 반등의 국내 종가 단순 전이, 고유가의 정유 강세·항공/화학 약세 기계적 적용.
- 관찰: 갭 상승 후 O2C 약세가 삼성전자·SK하이닉스·삼성전기에서 공통 발생. Gap Exhaustion 패턴인지 다일 표본 필요.
- Carry Forward: KOSPI와 KOSDAQ 방향을 분리하고, 대형주 지수 방어와 시장 breadth 악화를 동시에 표현할 것.
- 단 하루 결과로 시스템 규칙을 변경하지 않는다.

## 10. Review 요약
- 오늘 가장 잘한 판단: HD현대중공업 상승 및 조선 상대강세.
- 오늘 가장 큰 오판: LG화학·롯데케미칼 하락 예상.
- 더 유효했던 단계: 03:30 only; 08:25 unavailable로 비교 불가.
- 가장 유효했던 신호: 실제 조선 Sector Breadth.
- 가장 위험했던 함정: 고유가 하나로 정유·항공·화학 방향을 일괄 추론한 것.
- 다음 거래일: 글로벌 종가보다 국내 개장 후 수급·O2C·breadth를 별도 확인.

[REVIEW]
SCHEMA_VERSION: DMI_v7.1
DATE: 2026-09-03
AVAILABLE_STAGES: 03:30, 07:20; 08:25 PREVIOUS_STAGE_UNAVAILABLE

03:30_REGIME_PRELIMINARY: Mixed selective rebound; KOSPI 대형 AI 하드웨어·에너지 상대우위; 항공·화학·KOSDAQ 고밸류 상대열위; 고유가·4.8% 금리·SOXX breadth 부재가 제약
08:25_MARKET_VIEW_AT_SELECTION: PREVIOUS_STAGE_UNAVAILABLE

KOSPI_RETURN: +0.26%
KOSDAQ_RETURN: -1.71%
KOSPI_DIRECTION_FORECAST: UP
KOSPI_DIRECTION_ACTUAL: UP
KOSPI_DIRECTION_HIT: HIT
KOSDAQ_DIRECTION_FORECAST: UP
KOSDAQ_DIRECTION_ACTUAL: DOWN
KOSDAQ_DIRECTION_HIT: MISS

MARKET_REGIME_NOTE: PARTIAL; KOSPI 상대우위와 높은 변동성은 적중했으나 선별적 반등은 종가 기준 매우 약했고 KOSDAQ은 상승 출발 후 -1.71%로 반전. 실제 주도는 금융·보험·건설기계·철강과 일부 조선이었고 AI 하드웨어·정유 우위 및 항공·화학 열위는 대체로 빗나감

03:30_UP_COUNT: 5
03:30_UP_HIT_VALID_N: 5
03:30_UP_HIT_RATE: 20.0%
03:30_UP_AVG_DIRECTIONAL_RETURN: -0.78%
03:30_UP_AVG_BADR: -1.03%
03:30_UP_TOP3_DIRECTIONAL_RETURN: -1.08%
03:30_UP_TOP3_BADR: -1.34%

03:30_DOWN_COUNT: 5
03:30_DOWN_HIT_VALID_N: 5
03:30_DOWN_HIT_RATE: 40.0%
03:30_DOWN_AVG_DIRECTIONAL_RETURN: -2.43%
03:30_DOWN_AVG_BADR: -2.18%
03:30_DOWN_TOP3_DIRECTIONAL_RETURN: -4.67%
03:30_DOWN_TOP3_BADR: -4.42%

03:30_AVG_FE: 2.20%
03:30_AVG_AE: 4.42%
03:30_O2C_HIT_RATE: 33.3%

08:25_UP_COUNT: PREVIOUS_STAGE_UNAVAILABLE
08:25_UP_HIT_VALID_N: N/A
08:25_UP_HIT_RATE: N/A
08:25_UP_AVG_DIRECTIONAL_RETURN: N/A
08:25_UP_AVG_BADR: N/A
08:25_UP_TOP3_DIRECTIONAL_RETURN: N/A
08:25_UP_TOP3_BADR: N/A

08:25_DOWN_COUNT: PREVIOUS_STAGE_UNAVAILABLE
08:25_DOWN_HIT_VALID_N: N/A
08:25_DOWN_HIT_RATE: N/A
08:25_DOWN_AVG_DIRECTIONAL_RETURN: N/A
08:25_DOWN_AVG_BADR: N/A
08:25_DOWN_TOP3_DIRECTIONAL_RETURN: N/A
08:25_DOWN_TOP3_BADR: N/A

08:25_AVG_FE: N/A
08:25_AVG_AE: N/A
08:25_O2C_HIT_RATE: N/A

UP_RETENTION_RATE: N/A
DOWN_RETENTION_RATE: N/A
UP_CHURN_RATE: N/A
DOWN_CHURN_RATE: N/A
MAINTAINED_AVG_BADR: N/A
NEW_AVG_BADR: N/A
REMOVED_ACTUAL_BADR: N/A

03:30_UP_SCORE_RANK_CONCORDANCE: 0.90
03:30_DOWN_SCORE_RANK_CONCORDANCE: 0.90
08:25_UP_SCORE_RANK_CONCORDANCE: N/A
08:25_DOWN_SCORE_RANK_CONCORDANCE: N/A

BETTER_STAGE: 03:30; 08:25 unavailable, so this is not a valid two-stage performance comparison

RESULTS_03_30:
SIDE|RANK|종목|Code|Market|BaseScore|RawScore|AvailableMax|Coverage|Breakdown|Confidence|FreshGrade|PriceInCheck|OpenExpectation|OpenActual|OpenHit|O2CForecast|O2CActual|O2CHit|PriceIn|PrimaryCatalystType|SecondaryCatalystType|C2C|DirectionalReturn|BADR|HIT-MISS-FLAT|FE|AE|SuccessFactor|ErrorClass|ErrorSubtype
UP|1|삼성전자|005930|KOSPI|70.0|56|80|80%|17/15/9/N/A/N/A/8/7|MEDIUM|S|UNVERIFIED|GAP_UP|GAP_UP|HIT|UP|-1.57%|MISS|MEDIUM|Global_Peer|Earnings|-0.20%|-0.20%|-0.46%|MISS|1.80%|2.99%|N/A|MARKET_CONTEXT_ERROR|Global Transmission Error
UP|2|S-Oil|010950|KOSPI|76.3|61|80|80%|19/15/12/N/A/N/A/9/6|MEDIUM|S|UNVERIFIED|GAP_UP|GAP_DOWN|MISS|UP|-0.67%|MISS|HIGH|Macro_FX_Commodity|Supply_Demand|-1.99%|-1.99%|-2.24%|MISS|2.58%|3.71%|N/A|MARKET_CONTEXT_ERROR|Global Transmission Error
UP|3|SK하이닉스|000660|KOSPI|69.0|69|100|100%|18/15/9/10/6/7/4|MEDIUM|S|VERIFIED|GAP_UP|GAP_UP|HIT|UP|-2.86%|MISS|HIGH|Global_Peer|Earnings|-1.05%|-1.05%|-1.31%|MISS|2.23%|3.41%|N/A|MARKET_CONTEXT_ERROR|Global Transmission Error
UP|4|삼성전기|009150|KOSPI|67.5|54|80|80%|15/15/8/N/A/N/A/8/8|MEDIUM|S|UNVERIFIED|GAP_UP|GAP_UP|HIT|UP|-5.87%|MISS|MEDIUM|Global_Peer|Sector_Theme|-3.71%|-3.71%|-3.97%|MISS|3.50%|6.29%|N/A|SECURITY_SELECTION_ERROR|Wrong Leader
UP|5|HD현대중공업|329180|KOSPI|62.5|50|80|80%|12/15/8/N/A/N/A/8/7|MEDIUM|S|UNVERIFIED|GAP_UP|FLAT|MISS|UP|+2.59%|HIT|MEDIUM|Sector_Theme|Macro_FX_Commodity|+3.08%|+3.08%|+2.83%|HIT|4.98%|2.13%|Sector Breadth|N/A|N/A
DOWN|1|대한항공|003490|KOSPI|66.3|53|80|80%|17/15/9/N/A/N/A/7/5|MEDIUM|S|UNVERIFIED|GAP_DOWN|FLAT|MISS|UNCERTAIN|+0.69%|N/A|MEDIUM|Macro_FX_Commodity|Other|+0.87%|-0.87%|-0.61%|MISS|1.38%|3.11%|N/A|CATALYST_ERROR|Catalyst Overestimated
DOWN|2|롯데케미칼|011170|KOSPI|67.5|54|80|80%|16/15/10/N/A/N/A/8/5|MEDIUM|S|UNVERIFIED|GAP_DOWN|FLAT|MISS|DOWN|+6.46%|MISS|MEDIUM|Macro_FX_Commodity|Supply_Demand|+6.46%|-6.46%|-6.20%|MISS|0.52%|8.55%|N/A|MARKET_CONTEXT_ERROR|Sector Misread
DOWN|3|LG화학|051910|KOSPI|63.8|51|80|80%|14/15/8/N/A/N/A/8/6|MEDIUM|S|UNVERIFIED|GAP_DOWN|GAP_UP|MISS|DOWN|+5.51%|MISS|MEDIUM|Macro_FX_Commodity|Sector_Theme|+6.69%|-6.69%|-6.44%|MISS|1.12%|9.85%|N/A|MARKET_CONTEXT_ERROR|Sector Misread
DOWN|4|NAVER|035420|KOSPI|57.5|46|80|80%|10/15/7/N/A/N/A/8/6|MEDIUM|S|UNVERIFIED|GAP_DOWN|GAP_UP|MISS|DOWN|-1.43%|HIT|MEDIUM|Macro_FX_Commodity|Technical|-0.72%|+0.72%|+0.97%|HIT|2.63%|1.20%|Technical Structure|N/A|N/A
DOWN|5|카카오|035720|KOSPI|56.3|45|80|80%|10/15/7/N/A/N/A/8/5|MEDIUM|S|UNVERIFIED|GAP_DOWN|GAP_UP|MISS|DOWN|-1.84%|HIT|MEDIUM|Macro_FX_Commodity|Technical|-1.14%|+1.14%|+1.40%|HIT|1.28%|2.99%|Market Regime Fit|N/A|N/A

RESULTS_08_25:
PREVIOUS_STAGE_UNAVAILABLE

WATCH_EFFECTIVENESS_NOTE: 03:30 TOP10을 WATCH 대용으로 보면 평균 절대 C2C 2.59%, 평균 Intraday Range 6.81%. SK하이닉스·삼성전자·삼성전기의 거래대금 집중은 컸으나 방향성은 부정적이었고 HD현대중공업만 상승 후보 중 종가 방향 적중. 08:25 WATCH는 저장 파일 부재로 평가 불가

BEST_CALL: HD현대중공업 UP; C2C +3.08%, BADR +2.83%, O2C +2.59%
WORST_CALL: LG화학 DOWN; C2C +6.69%, Directional Return -6.69%, BADR -6.44%
PRIMARY_SUCCESS_PATTERN: 조선의 실제 Sector Breadth와 플랫폼 약세의 종가 지속
PRIMARY_ERROR_CLASS: MARKET_CONTEXT_ERROR
PRIMARY_ERROR_SUBTYPE: Sector Misread

SCORE_CALIBRATION_03_30: UP 2위 S-Oil과 DOWN 2위 롯데케미칼의 높은 점수가 큰 음의 BADR로 이어졌고 양 SIDE TOP3가 4~5위보다 부진. 점수와 실제 상대성과의 일치가 약함
SCORE_CALIBRATION_08_25: N/A
CONFIDENCE_CALIBRATION_03_30: 모든 후보 MEDIUM으로 Confidence별 단조성 평가 불가
CONFIDENCE_CALIBRATION_08_25: N/A
COVERAGE_CALIBRATION_NOTE: 100% Coverage인 SK하이닉스도 MISS였고 80% 후보군은 HIT와 MISS 혼재. 단일 세션으로 Coverage 효과 판단 불가
PRICE_IN_VERIFICATION_NOTE: VERIFIED인 SK하이닉스는 MISS. UNVERIFIED 9개 중 HIT 3개. 단일 세션이며 검증 여부 자체의 예측력은 확인되지 않음
EVIDENCE_DOUBLE_COUNTING_NOTE: 고유가 하나를 C·S·M에 중첩 반영한 S-Oil·항공·화학 후보군에서 동시 실패가 발생. 향후 다일 표본에서 중복가산 여부를 추적
CARRY_FORWARD: 미국 반도체 상승을 국내 대형 반도체 종가로 단순 전이하지 말고 개장 후 외국인 수급과 O2C 유지력을 분리 검증. 고유가가 정유 강세·화학 약세로 직결된다는 가정은 제품 스프레드·환율·선반영과 함께 재검증. 단 하루 결과로 규칙 변경 금지
[/REVIEW]
[/STAGE_REPORT]

[STAGE_REVIEW_CAPSULE]
[REVIEW]
SCHEMA_VERSION: DMI_v7.1
DATE: 2026-09-03
AVAILABLE_STAGES: 03:30, 07:20; 08:25 PREVIOUS_STAGE_UNAVAILABLE

03:30_REGIME_PRELIMINARY: Mixed selective rebound; KOSPI 대형 AI 하드웨어·에너지 상대우위; 항공·화학·KOSDAQ 고밸류 상대열위; 고유가·4.8% 금리·SOXX breadth 부재가 제약
08:25_MARKET_VIEW_AT_SELECTION: PREVIOUS_STAGE_UNAVAILABLE

KOSPI_RETURN: +0.26%
KOSDAQ_RETURN: -1.71%
KOSPI_DIRECTION_FORECAST: UP
KOSPI_DIRECTION_ACTUAL: UP
KOSPI_DIRECTION_HIT: HIT
KOSDAQ_DIRECTION_FORECAST: UP
KOSDAQ_DIRECTION_ACTUAL: DOWN
KOSDAQ_DIRECTION_HIT: MISS

MARKET_REGIME_NOTE: PARTIAL; KOSPI 상대우위와 높은 변동성은 적중했으나 선별적 반등은 종가 기준 매우 약했고 KOSDAQ은 상승 출발 후 -1.71%로 반전. 실제 주도는 금융·보험·건설기계·철강과 일부 조선이었고 AI 하드웨어·정유 우위 및 항공·화학 열위는 대체로 빗나감

03:30_UP_COUNT: 5
03:30_UP_HIT_VALID_N: 5
03:30_UP_HIT_RATE: 20.0%
03:30_UP_AVG_DIRECTIONAL_RETURN: -0.78%
03:30_UP_AVG_BADR: -1.03%
03:30_UP_TOP3_DIRECTIONAL_RETURN: -1.08%
03:30_UP_TOP3_BADR: -1.34%

03:30_DOWN_COUNT: 5
03:30_DOWN_HIT_VALID_N: 5
03:30_DOWN_HIT_RATE: 40.0%
03:30_DOWN_AVG_DIRECTIONAL_RETURN: -2.43%
03:30_DOWN_AVG_BADR: -2.18%
03:30_DOWN_TOP3_DIRECTIONAL_RETURN: -4.67%
03:30_DOWN_TOP3_BADR: -4.42%

03:30_AVG_FE: 2.20%
03:30_AVG_AE: 4.42%
03:30_O2C_HIT_RATE: 33.3%

08:25_UP_COUNT: PREVIOUS_STAGE_UNAVAILABLE
08:25_UP_HIT_VALID_N: N/A
08:25_UP_HIT_RATE: N/A
08:25_UP_AVG_DIRECTIONAL_RETURN: N/A
08:25_UP_AVG_BADR: N/A
08:25_UP_TOP3_DIRECTIONAL_RETURN: N/A
08:25_UP_TOP3_BADR: N/A

08:25_DOWN_COUNT: PREVIOUS_STAGE_UNAVAILABLE
08:25_DOWN_HIT_VALID_N: N/A
08:25_DOWN_HIT_RATE: N/A
08:25_DOWN_AVG_DIRECTIONAL_RETURN: N/A
08:25_DOWN_AVG_BADR: N/A
08:25_DOWN_TOP3_DIRECTIONAL_RETURN: N/A
08:25_DOWN_TOP3_BADR: N/A

08:25_AVG_FE: N/A
08:25_AVG_AE: N/A
08:25_O2C_HIT_RATE: N/A

UP_RETENTION_RATE: N/A
DOWN_RETENTION_RATE: N/A
UP_CHURN_RATE: N/A
DOWN_CHURN_RATE: N/A
MAINTAINED_AVG_BADR: N/A
NEW_AVG_BADR: N/A
REMOVED_ACTUAL_BADR: N/A

03:30_UP_SCORE_RANK_CONCORDANCE: 0.90
03:30_DOWN_SCORE_RANK_CONCORDANCE: 0.90
08:25_UP_SCORE_RANK_CONCORDANCE: N/A
08:25_DOWN_SCORE_RANK_CONCORDANCE: N/A

BETTER_STAGE: 03:30; 08:25 unavailable, so this is not a valid two-stage performance comparison

RESULTS_03_30:
SIDE|RANK|종목|Code|Market|BaseScore|RawScore|AvailableMax|Coverage|Breakdown|Confidence|FreshGrade|PriceInCheck|OpenExpectation|OpenActual|OpenHit|O2CForecast|O2CActual|O2CHit|PriceIn|PrimaryCatalystType|SecondaryCatalystType|C2C|DirectionalReturn|BADR|HIT-MISS-FLAT|FE|AE|SuccessFactor|ErrorClass|ErrorSubtype
UP|1|삼성전자|005930|KOSPI|70.0|56|80|80%|17/15/9/N/A/N/A/8/7|MEDIUM|S|UNVERIFIED|GAP_UP|GAP_UP|HIT|UP|-1.57%|MISS|MEDIUM|Global_Peer|Earnings|-0.20%|-0.20%|-0.46%|MISS|1.80%|2.99%|N/A|MARKET_CONTEXT_ERROR|Global Transmission Error
UP|2|S-Oil|010950|KOSPI|76.3|61|80|80%|19/15/12/N/A/N/A/9/6|MEDIUM|S|UNVERIFIED|GAP_UP|GAP_DOWN|MISS|UP|-0.67%|MISS|HIGH|Macro_FX_Commodity|Supply_Demand|-1.99%|-1.99%|-2.24%|MISS|2.58%|3.71%|N/A|MARKET_CONTEXT_ERROR|Global Transmission Error
UP|3|SK하이닉스|000660|KOSPI|69.0|69|100|100%|18/15/9/10/6/7/4|MEDIUM|S|VERIFIED|GAP_UP|GAP_UP|HIT|UP|-2.86%|MISS|HIGH|Global_Peer|Earnings|-1.05%|-1.05%|-1.31%|MISS|2.23%|3.41%|N/A|MARKET_CONTEXT_ERROR|Global Transmission Error
UP|4|삼성전기|009150|KOSPI|67.5|54|80|80%|15/15/8/N/A/N/A/8/8|MEDIUM|S|UNVERIFIED|GAP_UP|GAP_UP|HIT|UP|-5.87%|MISS|MEDIUM|Global_Peer|Sector_Theme|-3.71%|-3.71%|-3.97%|MISS|3.50%|6.29%|N/A|SECURITY_SELECTION_ERROR|Wrong Leader
UP|5|HD현대중공업|329180|KOSPI|62.5|50|80|80%|12/15/8/N/A/N/A/8/7|MEDIUM|S|UNVERIFIED|GAP_UP|FLAT|MISS|UP|+2.59%|HIT|MEDIUM|Sector_Theme|Macro_FX_Commodity|+3.08%|+3.08%|+2.83%|HIT|4.98%|2.13%|Sector Breadth|N/A|N/A
DOWN|1|대한항공|003490|KOSPI|66.3|53|80|80%|17/15/9/N/A/N/A/7/5|MEDIUM|S|UNVERIFIED|GAP_DOWN|FLAT|MISS|UNCERTAIN|+0.69%|N/A|MEDIUM|Macro_FX_Commodity|Other|+0.87%|-0.87%|-0.61%|MISS|1.38%|3.11%|N/A|CATALYST_ERROR|Catalyst Overestimated
DOWN|2|롯데케미칼|011170|KOSPI|67.5|54|80|80%|16/15/10/N/A/N/A/8/5|MEDIUM|S|UNVERIFIED|GAP_DOWN|FLAT|MISS|DOWN|+6.46%|MISS|MEDIUM|Macro_FX_Commodity|Supply_Demand|+6.46%|-6.46%|-6.20%|MISS|0.52%|8.55%|N/A|MARKET_CONTEXT_ERROR|Sector Misread
DOWN|3|LG화학|051910|KOSPI|63.8|51|80|80%|14/15/8/N/A/N/A/8/6|MEDIUM|S|UNVERIFIED|GAP_DOWN|GAP_UP|MISS|DOWN|+5.51%|MISS|MEDIUM|Macro_FX_Commodity|Sector_Theme|+6.69%|-6.69%|-6.44%|MISS|1.12%|9.85%|N/A|MARKET_CONTEXT_ERROR|Sector Misread
DOWN|4|NAVER|035420|KOSPI|57.5|46|80|80%|10/15/7/N/A/N/A/8/6|MEDIUM|S|UNVERIFIED|GAP_DOWN|GAP_UP|MISS|DOWN|-1.43%|HIT|MEDIUM|Macro_FX_Commodity|Technical|-0.72%|+0.72%|+0.97%|HIT|2.63%|1.20%|Technical Structure|N/A|N/A
DOWN|5|카카오|035720|KOSPI|56.3|45|80|80%|10/15/7/N/A/N/A/8/5|MEDIUM|S|UNVERIFIED|GAP_DOWN|GAP_UP|MISS|DOWN|-1.84%|HIT|MEDIUM|Macro_FX_Commodity|Technical|-1.14%|+1.14%|+1.40%|HIT|1.28%|2.99%|Market Regime Fit|N/A|N/A

RESULTS_08_25:
PREVIOUS_STAGE_UNAVAILABLE

WATCH_EFFECTIVENESS_NOTE: 03:30 TOP10을 WATCH 대용으로 보면 평균 절대 C2C 2.59%, 평균 Intraday Range 6.81%. SK하이닉스·삼성전자·삼성전기의 거래대금 집중은 컸으나 방향성은 부정적이었고 HD현대중공업만 상승 후보 중 종가 방향 적중. 08:25 WATCH는 저장 파일 부재로 평가 불가

BEST_CALL: HD현대중공업 UP; C2C +3.08%, BADR +2.83%, O2C +2.59%
WORST_CALL: LG화학 DOWN; C2C +6.69%, Directional Return -6.69%, BADR -6.44%
PRIMARY_SUCCESS_PATTERN: 조선의 실제 Sector Breadth와 플랫폼 약세의 종가 지속
PRIMARY_ERROR_CLASS: MARKET_CONTEXT_ERROR
PRIMARY_ERROR_SUBTYPE: Sector Misread

SCORE_CALIBRATION_03_30: UP 2위 S-Oil과 DOWN 2위 롯데케미칼의 높은 점수가 큰 음의 BADR로 이어졌고 양 SIDE TOP3가 4~5위보다 부진. 점수와 실제 상대성과의 일치가 약함
SCORE_CALIBRATION_08_25: N/A
CONFIDENCE_CALIBRATION_03_30: 모든 후보 MEDIUM으로 Confidence별 단조성 평가 불가
CONFIDENCE_CALIBRATION_08_25: N/A
COVERAGE_CALIBRATION_NOTE: 100% Coverage인 SK하이닉스도 MISS였고 80% 후보군은 HIT와 MISS 혼재. 단일 세션으로 Coverage 효과 판단 불가
PRICE_IN_VERIFICATION_NOTE: VERIFIED인 SK하이닉스는 MISS. UNVERIFIED 9개 중 HIT 3개. 단일 세션이며 검증 여부 자체의 예측력은 확인되지 않음
EVIDENCE_DOUBLE_COUNTING_NOTE: 고유가 하나를 C·S·M에 중첩 반영한 S-Oil·항공·화학 후보군에서 동시 실패가 발생. 향후 다일 표본에서 중복가산 여부를 추적
CARRY_FORWARD: 미국 반도체 상승을 국내 대형 반도체 종가로 단순 전이하지 말고 개장 후 외국인 수급과 O2C 유지력을 분리 검증. 고유가가 정유 강세·화학 약세로 직결된다는 가정은 제품 스프레드·환율·선반영과 함께 재검증. 단 하루 결과로 규칙 변경 금지
[/REVIEW]
[/STAGE_REVIEW_CAPSULE]
