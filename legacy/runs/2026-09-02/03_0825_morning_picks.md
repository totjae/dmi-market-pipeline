[DMI_RUN_META]
SCHEMA_VERSION: DMI_v7.1
DATE: 2026-09-02
STAGE: 08:25
RUN_TIME_KST: 2026-09-02 08:24:35
[/DMI_RUN_META]

[STAGE_REPORT]
# TASK 3 — 08:25 Morning Picks — v7.1

## 1. 시점 및 독립 Fresh Scan

- DATE: 2026-09-02
- ANALYSIS_TIME: 08:24 KST
- SCHEMA_VERSION: DMI_v7.1
- 독립성: 후보·Rank·Base Score 확정 전 같은 날짜의 03:30·07:20 결과를 열람하지 않음
- NXT: 07:51 KST 기준 20분 지연 페이지는 확인했으나 종목별 체결표가 확보되지 않아 핵심 근거에서 제외
- 미국 지수선물: 기준시각이 명확한 종합 스냅샷을 확보하지 못해 N/A

### FACT

1. 미국 9월 1일 정규장은 S&P 500 -0.71%, Nasdaq -1.03%, Russell 2000 -1.23%로 마감했다. SOXX는 -2.13%, EWY는 -2.77%였다.
2. Brent는 $94.65(+4.6%), WTI는 $90.22(+5.2%)에 결제됐고 미국 10년물은 약 4.79%였다.
3. 9월 1일 장 마감 후 삼성전기 1조722억원 AI용 MLCC 공급계약, 한화오션 4778억원 VLGC 3척 수주, 두산에너빌리티 6658억원 하동복합발전 공사, 유한양행 1310억원 원료의약품 공급계약이 공개됐다.
4. 9월 1일 KOSPI는 +0.23%, KOSDAQ은 -1.56%로 마감했다.

### INTERPRETATION

유가와 장기금리가 동시에 오른 인플레이션형 Risk-off다. 지수·반도체·KOSDAQ에는 불리하지만, 전일 KRX 종료 후 공개된 직접 수주 공시는 시장 약세 속에서도 종목별 상대수익을 만들 수 있다. 정유는 고유가의 직접 상대수혜이며 항공·화학은 비용 측 역풍이 가장 분명하다.

### FORECAST

KOSPI와 KOSDAQ 모두 전일 종가 대비 하락 우위이며 KOSDAQ 상대약세를 예상한다. 개별 대형 수주주는 갭 상승 가능성이 높지만 지수 약세와 차익실현 때문에 시가 대비 종가 방향은 종목별로 갈릴 가능성이 있다.

## 2. Broad Scan · Evidence Test · Price-in · Counterargument

- 직접 신규 촉매 통과: 삼성전기, 한화오션, 두산에너빌리티, 유한양행.
- 거시 직접 전달경로 통과: S-Oil, 대한항공, 롯데케미칼, LG화학, SK하이닉스, 에코프로비엠.
- 제외: 일성건설·까뮤이앤씨·에스오에스랩 등은 공시의 직접성은 있으나 유동성·갭 변동·시장규모상 핵심 TOP보다 비대칭이 불리했다.
- 가격검증: 신뢰 가능한 최신 종목별 프리마켓 가격·변동성 표를 확보하지 못해 모든 TOP 후보의 T를 N/A, PRICE_IN_CHECK를 UNVERIFIED로 처리했다. 따라서 Confidence는 MEDIUM 이하이며 Base Score를 순위의 핵심 정당화로 사용하지 않았다.
- 순위 기준: 촉매의 직접성, 계약 절대규모, 당일 시장환경 전달경로, 반대논리 강도를 우선했다.

## 3. 관심종목 TOP 10

| Rank | 종목 | Code | Market | 방향 | Catalyst | Fresh Grade | Base Score | Coverage | Confidence | 핵심 Risk |
|---|---|---|---|---|---|---|---:|---:|---|---|
| 1 | 삼성전기 | 009150 | KOSPI | UP | AI용 MLCC 1조722억원 공급계약 | S | 88.9 | 90% | MEDIUM | 지수·반도체 약세와 갭 차익실현 |
| 2 | 한화오션 | 042660 | KOSPI | UP | VLGC 3척 4778억원 수주 | S | 84.4 | 90% | MEDIUM | 조선주 가격반영과 Risk-off |
| 3 | 대한항공 | 003490 | KOSPI | DOWN | 유가·항공유 급등 | S | 84.4 | 90% | MEDIUM | 유가 반락과 운임 전가 |
| 4 | 두산에너빌리티 | 034020 | KOSPI | UP | 하동복합발전 6658억원 수주 | S | 82.2 | 90% | MEDIUM | 기존 기대 선반영·갭 추격 |
| 5 | S-Oil | 010950 | KOSPI | UP | 원유·정제마진 상대수혜 | S | 81.1 | 90% | MEDIUM | 휴전 뉴스와 유가 급락 |
| 6 | 롯데케미칼 | 011170 | KOSPI | DOWN | 나프타 원가·경기민감 부담 | S | 80.0 | 90% | MEDIUM | 제품가격 동반 상승 |
| 7 | 유한양행 | 000100 | KOSPI | UP | 원료의약품 1310억원 공급계약 | S | 77.8 | 90% | MEDIUM | 계약의 이익 기여도 불확실 |
| 8 | LG화학 | 051910 | KOSPI | DOWN | 원재료·금리 동반 부담 | S | 76.7 | 90% | MEDIUM | 배터리소재 고유 호재 |
| 9 | SK하이닉스 | 000660 | KOSPI | DOWN | SOXX·EWY 약세와 고금리 | S | 74.4 | 90% | MEDIUM | Micron 공급차질 기대와 저가매수 |
| 10 | 에코프로비엠 | 247540 | KOSDAQ | DOWN | 고금리·고베타 Risk-off | S | 70.0 | 90% | MEDIUM | 개별 수주·정책 호재 |

## 4. 최종 상승 TOP 5

| Rank | 종목 | Code | Market | Base Score | Raw/Max | Coverage | Breakdown | Confidence | Fresh Grade | Price-in Check | Catalyst Type | 핵심 논리 | 반대 논리 |
|---|---|---|---|---:|---|---:|---|---|---|---|---|---|---|
| 1 | 삼성전기 | 009150 | KOSPI | 88.9 | 80/90 | 90% | 23/15/11/10/N/A/8/8 | MEDIUM | S | UNVERIFIED | Contract_Order | AI용 MLCC 대형 직접계약 | 반도체 Risk-off와 갭 차익실현 |
| 2 | 한화오션 | 042660 | KOSPI | 84.4 | 76/90 | 90% | 21/15/11/9/N/A/9/6 | MEDIUM | S | UNVERIFIED | Contract_Order | VLGC 대형 수주와 에너지운송 관심 | 높은 기대와 지수 약세 |
| 3 | 두산에너빌리티 | 034020 | KOSPI | 82.2 | 74/90 | 90% | 20/15/11/9/N/A/9/6 | MEDIUM | S | UNVERIFIED | Contract_Order | 발전소 직접 수주와 에너지안보 | 기존 기대 선반영 |
| 4 | S-Oil | 010950 | KOSPI | 81.1 | 73/90 | 90% | 20/15/13/9/N/A/9/7 | MEDIUM | S | UNVERIFIED | Macro_FX_Commodity | 유가·디젤 급등의 정유 상대수혜 | 유가 급반락 |
| 5 | 유한양행 | 000100 | KOSPI | 77.8 | 70/90 | 90% | 18/15/7/8/N/A/7/8 | MEDIUM | S | UNVERIFIED | Contract_Order | 글로벌 제약사 원료 공급계약 | 이익률·매출 인식 불확실 |

### TOP 1 삼성전기

- OPEN_EXPECTATION: GAP_UP
- O2C_EXPECTATION: UP
- Price-in: MEDIUM
- CHASE_RISK: HIGH
- Intraday Scenario: 대형 계약으로 강하게 출발하되 반도체 업종 약세가 눌림을 만들 수 있다. 갭을 절반 이상 지키고 거래가 확산되면 종가 강세 가능성이 높아진다.
- 주요 Risk: 계약 규모 대비 수익성·납품기간 세부 불확실, 기술주 전반 외국인 매도.
- Invalidation: 시가가 +0.5% 미만이거나 장 초반 갭을 전부 반납하고 반도체 업종 대비 상대약세.
- Score Audit: C 23 직접 대형계약; F 15 완료 KRX 세션 0; S 11 AI부품 연관; FL 10 공시 관심; M 8 개별 촉매 방어; A 8 계약 직접성.

### TOP 2 한화오션

- OPEN_EXPECTATION: GAP_UP
- O2C_EXPECTATION: UNCERTAIN
- Price-in: MEDIUM
- CHASE_RISK: HIGH
- Intraday Scenario: VLGC 수주와 에너지 운송 위험이 동시 부각되면 상대강세가 가능하나 갭 이후 차익실현 가능성이 크다.
- 주요 Risk: 조선업 기존 수주 기대의 가격반영, 시장 전체 Risk-off.
- Invalidation: 조선주 동반 약세와 함께 시가 갭을 전부 반납.
- Score Audit: C 21 대형 선박수주; F 15; S 11 조선·에너지운송; FL 9; M 9; A 6 선반영 위험.

### 후보 3~5 운영판

- 두산에너빌리티: GAP_UP / O2C UNCERTAIN / Price-in HIGH / CHASE_RISK VERY_HIGH. 수주 공시에도 전일종가 회복 실패 시 무효.
- S-Oil: GAP_UP / O2C UNCERTAIN / Price-in MEDIUM / CHASE_RISK HIGH. Brent $92 하회 또는 정유 동반약세 시 무효.
- 유한양행: GAP_UP / O2C UNCERTAIN / Price-in LOW / CHASE_RISK MEDIUM. 계약의 실적 기여 우려로 갭 전부 반납 시 무효.

## 5. 최종 하락 TOP 5

| Rank | 종목 | Code | Market | Base Score | Raw/Max | Coverage | Breakdown | Confidence | Fresh Grade | Price-in Check | Catalyst Type | 핵심 논리 | 반대 논리 |
|---|---|---|---|---:|---|---:|---|---|---|---|---|---|---|
| 1 | 대한항공 | 003490 | KOSPI | 84.4 | 76/90 | 90% | 21/15/13/9/N/A/9/9 | MEDIUM | S | UNVERIFIED | Macro_FX_Commodity | 항공유 비용의 직접 충격 | 유가 반락·운임 전가 |
| 2 | 롯데케미칼 | 011170 | KOSPI | 80.0 | 72/90 | 90% | 19/15/12/8/N/A/9/9 | MEDIUM | S | UNVERIFIED | Macro_FX_Commodity | 나프타와 경기민감 이중 부담 | 제품 스프레드 개선 |
| 3 | LG화학 | 051910 | KOSPI | 76.7 | 69/90 | 90% | 17/15/11/8/N/A/9/9 | MEDIUM | S | UNVERIFIED | Macro_FX_Commodity | 원가·금리·성장주 할인율 | 배터리소재 독자 촉매 |
| 4 | SK하이닉스 | 000660 | KOSPI | 74.4 | 67/90 | 90% | 17/15/13/11/N/A/8/3 | MEDIUM | S | UNVERIFIED | Global_Peer | SOXX·EWY 동반 급락 | Micron 공급차질과 방어수급 |
| 5 | 에코프로비엠 | 247540 | KOSDAQ | 70.0 | 63/90 | 90% | 14/15/10/8/N/A/9/7 | MEDIUM | S | UNVERIFIED | Macro_FX_Commodity | 고금리·KOSDAQ Risk-off | 정책·수주 고유 호재 |

### TOP 1 대한항공

- OPEN_EXPECTATION: GAP_DOWN
- O2C_EXPECTATION: DOWN
- Price-in: MEDIUM
- CHASE_RISK: MEDIUM
- Intraday Scenario: 갭 하락 뒤 유가가 $95 부근을 유지하면 비용 우려가 종가까지 이어질 수 있다.
- 주요 Risk: 유가 급락, 환율 하락, 운임 전가 기대.
- Invalidation: Brent 급락 또는 대한항공이 보합 이상 출발해 운송업 대비 상대강세.
- Score Audit: C 21 직접 비용; F 15; S 13 항공·여행 전반; FL 9; M 9; A 9.

### TOP 2 롯데케미칼

- OPEN_EXPECTATION: GAP_DOWN
- O2C_EXPECTATION: UNCERTAIN
- Price-in: MEDIUM
- CHASE_RISK: MEDIUM
- Intraday Scenario: 나프타 부담과 경기민감 매도가 겹치면 약세 지속, 다만 유가 반락 시 숏커버 가능.
- 주요 Risk: 제품가격 동반 상승과 중국 부양.
- Invalidation: 화학 업종 상대강세와 전일종가 회복.
- Score Audit: C 19 원가 직접성; F 15; S 12; FL 8; M 9; A 9.

### 후보 3~5 운영판

- LG화학: GAP_DOWN / O2C UNCERTAIN / Price-in MEDIUM / CHASE_RISK MEDIUM. 배터리소재 동반 강세 시 무효.
- SK하이닉스: GAP_DOWN / O2C UNCERTAIN / Price-in HIGH / CHASE_RISK HIGH. Micron 공급차질 기대와 방어수급 때문에 함정 위험.
- 에코프로비엠: GAP_DOWN / O2C UNCERTAIN / Price-in MEDIUM / CHASE_RISK MEDIUM. KOSDAQ 성장주 반등 시 무효.

## 6. 최종 강세·약세 섹터

- 강세: 정유; 조선·에너지운송; 발전·에너지인프라; 개별 AI부품 수주주.
- 약세: 항공·여행; 화학; 반도체·AI; KOSDAQ 고밸류 성장주.

## 7. MARKET_VIEW_AT_SELECTION

- KOSPI / KOSDAQ 상대강도: 둘 다 DOWN 우위, KOSPI 상대우위.
- Risk Sentiment: Risk-off.
- 유리한 스타일: 실적 연결성이 높은 신규 대형 수주주, 고유가 직접 수혜 가치주.
- 핵심 강세·약세: 정유·개별 수주주 강세; 항공·화학·반도체·KOSDAQ 성장주 약세.
- 핵심 제약: Brent $94.65, 미 10년물 약 4.79%, 원화 약세, EWY·SOXX 급락.
- 장 전체 Invalidation: 유가·금리·환율 동반 하락과 미국 선물 반등, 외국인 현·선물 순매수.

## 8. 이전 단계 비교

독립 판단 완료 후 같은 날짜의 실제 03:30·07:20 HANDOFF를 읽었다.

- 03:30 S-Oil: MAINTAINED, 상승 1위에서 4위로 RANK_DOWN. 장 마감 후 직접 수주주를 우선.
- 03:30 SK이노베이션·한화에어로스페이스·한국항공우주: REMOVED. 직접 신규 공시 대비 촉매 우선순위 하락.
- 삼성전기·한화오션·두산에너빌리티·유한양행: NEW.
- 대한항공: MAINTAINED, 하락 3위에서 1위로 RANK_UP.
- 롯데케미칼: MAINTAINED, 4위에서 2위로 RANK_UP.
- LG화학: MAINTAINED, 5위에서 3위로 RANK_UP.
- SK하이닉스: MAINTAINED, 1위에서 4위로 RANK_DOWN. Micron 공급 측 호재 반론 때문에 하향.
- 삼성전자: REMOVED. 개별 하락 비대칭이 SK하이닉스보다 낮음.
- 에코프로비엠: NEW. KOSDAQ 상대약세 대표 후보.
- 07:20 DOWN/DOWN, Risk-off, KOSPI 상대우위: MAINTAINED.
- 07:20 정유 강세와 반도체·항공·화학·KOSDAQ 성장주 약세: MAINTAINED.
- 변화 핵심: 거시 레짐은 유지됐지만 9월 1일 KRX 종료 후 직접 대형계약 공시를 상승 Rank 상단에 반영.

## 9. 개장 직전 핵심판

| 구분 | #1 | #2 | #3 |
|---|---|---|---|
| 상승 후보 | 삼성전기 | 한화오션 | 두산에너빌리티 |
| 하락 후보 | 대한항공 | 롯데케미칼 | LG화학 |
| 강세 섹터 | 정유 | 조선·에너지운송 | 발전·에너지인프라 |
| 약세 섹터 | 항공·여행 | 화학 | 반도체·AI |
| 시장 관심 | 삼성전기 AI용 MLCC 계약 | 국제유가 $95 부근 | 외국인 반도체 수급 |

- 오늘 가장 중요한 종목 3개: 삼성전기, 대한항공, S-Oil.
- 가장 확신 높은 상승 후보: 삼성전기.
- 가장 확신 높은 하락 후보: 대한항공.
- 가장 위험한 함정 후보: 두산에너빌리티.
- 시장 전체 전망 핵심 Invalidation: 유가·미 국채금리·USD/KRW가 동반 하락하고 미국 선물이 강하게 반등하며 외국인 현·선물 순매수가 확인되는 경우.

## 10. HANDOFF CAPSULE

[HANDOFF]
SCHEMA_VERSION: DMI_v7.1
DATE: 2026-09-02
STAGE: 08:25

MARKET_VIEW_AT_SELECTION: KOSPI와 KOSDAQ 모두 DOWN 우위, KOSPI 상대우위; Risk-off; 정유·개별 대형 수주주 유리, 반도체·항공·화학·고밸류 성장주 불리; 고유가·4.79% 미 10년물·원화 약세가 핵심 제약

UP_COUNT: 5
DOWN_COUNT: 5
WATCH_COUNT: 10

UP:
1|삼성전기|009150|KOSPI|1|88.9|80|90|90%|23/15/11/10/N/A/8/8|MEDIUM|S|UNVERIFIED|GAP_UP|UP|MEDIUM|HIGH|Contract_Order|Sector_Theme|글로벌 빅테크와 1조722억원 AI용 MLCC 공급계약
2|한화오션|042660|KOSPI|2|84.4|76|90|90%|21/15/11/9/N/A/9/6|MEDIUM|S|UNVERIFIED|GAP_UP|UNCERTAIN|MEDIUM|HIGH|Contract_Order|Supply_Demand|4778억원 규모 VLGC 3척 수주
3|두산에너빌리티|034020|KOSPI|3|82.2|74|90|90%|20/15/11/9/N/A/9/6|MEDIUM|S|UNVERIFIED|GAP_UP|UNCERTAIN|HIGH|VERY_HIGH|Contract_Order|Sector_Theme|6658억원 규모 하동복합 발전소 공사 수주
4|S-Oil|010950|KOSPI|4|81.1|73|90|90%|20/15/13/9/N/A/9/7|MEDIUM|S|UNVERIFIED|GAP_UP|UNCERTAIN|MEDIUM|HIGH|Macro_FX_Commodity|Supply_Demand|Brent 94.65달러와 디젤 강세에 따른 정유 상대수혜
5|유한양행|000100|KOSPI|5|77.8|70|90|90%|18/15/7/8/N/A/7/8|MEDIUM|S|UNVERIFIED|GAP_UP|UNCERTAIN|LOW|MEDIUM|Contract_Order|Other|글로벌 제약사와 1310억원 원료의약품 공급계약

DOWN:
1|대한항공|003490|KOSPI|1|84.4|76|90|90%|21/15/13/9/N/A/9/9|MEDIUM|S|UNVERIFIED|GAP_DOWN|DOWN|MEDIUM|MEDIUM|Macro_FX_Commodity|Supply_Demand|WTI 90.22달러와 Brent 94.65달러로 항공유 비용 부담 급증
2|롯데케미칼|011170|KOSPI|2|80.0|72|90|90%|19/15/12/8/N/A/9/9|MEDIUM|S|UNVERIFIED|GAP_DOWN|UNCERTAIN|MEDIUM|MEDIUM|Macro_FX_Commodity|Sector_Theme|유가·나프타 상승과 경기민감 Risk-off의 이중 부담
3|LG화학|051910|KOSPI|3|76.7|69|90|90%|17/15/11/8/N/A/9/9|MEDIUM|S|UNVERIFIED|GAP_DOWN|UNCERTAIN|MEDIUM|MEDIUM|Macro_FX_Commodity|Sector_Theme|원재료·장기금리·성장주 할인율 동시 부담
4|SK하이닉스|000660|KOSPI|4|74.4|67|90|90%|17/15/13/11/N/A/8/3|MEDIUM|S|UNVERIFIED|GAP_DOWN|UNCERTAIN|HIGH|HIGH|Global_Peer|Macro_FX_Commodity|SOXX -2.13%와 EWY -2.77%, 미 10년물 4.79%
5|에코프로비엠|247540|KOSDAQ|5|70.0|63|90|90%|14/15/10/8/N/A/9/7|MEDIUM|S|UNVERIFIED|GAP_DOWN|UNCERTAIN|MEDIUM|MEDIUM|Macro_FX_Commodity|Sector_Theme|고금리·Risk-off·KOSDAQ 상대약세가 고밸류 2차전지에 부담

WATCH:
1|삼성전기|009150|KOSPI|UP
2|한화오션|042660|KOSPI|UP
3|두산에너빌리티|034020|KOSPI|UP
4|S-Oil|010950|KOSPI|UP
5|유한양행|000100|KOSPI|UP
6|대한항공|003490|KOSPI|DOWN
7|롯데케미칼|011170|KOSPI|DOWN
8|LG화학|051910|KOSPI|DOWN
9|SK하이닉스|000660|KOSPI|DOWN
10|에코프로비엠|247540|KOSDAQ|DOWN

STRONG_SECTORS: 정유; 조선·에너지운송; 발전·에너지인프라; 개별 AI부품 수주주
WEAK_SECTORS: 항공·여행; 화학; 반도체·AI; KOSDAQ 고밸류 성장주
TOP_TRAP: 두산에너빌리티 — 신규 대형 수주는 강하지만 기존 원전·가스터빈 기대와 높은 가격반영으로 갭 추격 위험이 매우 높음
MARKET_INVALIDATION: 국제유가 급락과 미 국채금리 하락, USD/KRW 하락, 미국 지수선물 강한 반등이 동시에 나타나고 외국인 현·선물 순매수가 확인될 경우
[/HANDOFF]
[/STAGE_REPORT]

[STAGE_HANDOFF]
[HANDOFF]
SCHEMA_VERSION: DMI_v7.1
DATE: 2026-09-02
STAGE: 08:25

MARKET_VIEW_AT_SELECTION: KOSPI와 KOSDAQ 모두 DOWN 우위, KOSPI 상대우위; Risk-off; 정유·개별 대형 수주주 유리, 반도체·항공·화학·고밸류 성장주 불리; 고유가·4.79% 미 10년물·원화 약세가 핵심 제약

UP_COUNT: 5
DOWN_COUNT: 5
WATCH_COUNT: 10

UP:
1|삼성전기|009150|KOSPI|1|88.9|80|90|90%|23/15/11/10/N/A/8/8|MEDIUM|S|UNVERIFIED|GAP_UP|UP|MEDIUM|HIGH|Contract_Order|Sector_Theme|글로벌 빅테크와 1조722억원 AI용 MLCC 공급계약
2|한화오션|042660|KOSPI|2|84.4|76|90|90%|21/15/11/9/N/A/9/6|MEDIUM|S|UNVERIFIED|GAP_UP|UNCERTAIN|MEDIUM|HIGH|Contract_Order|Supply_Demand|4778억원 규모 VLGC 3척 수주
3|두산에너빌리티|034020|KOSPI|3|82.2|74|90|90%|20/15/11/9/N/A/9/6|MEDIUM|S|UNVERIFIED|GAP_UP|UNCERTAIN|HIGH|VERY_HIGH|Contract_Order|Sector_Theme|6658억원 규모 하동복합 발전소 공사 수주
4|S-Oil|010950|KOSPI|4|81.1|73|90|90%|20/15/13/9/N/A/9/7|MEDIUM|S|UNVERIFIED|GAP_UP|UNCERTAIN|MEDIUM|HIGH|Macro_FX_Commodity|Supply_Demand|Brent 94.65달러와 디젤 강세에 따른 정유 상대수혜
5|유한양행|000100|KOSPI|5|77.8|70|90|90%|18/15/7/8/N/A/7/8|MEDIUM|S|UNVERIFIED|GAP_UP|UNCERTAIN|LOW|MEDIUM|Contract_Order|Other|글로벌 제약사와 1310억원 원료의약품 공급계약

DOWN:
1|대한항공|003490|KOSPI|1|84.4|76|90|90%|21/15/13/9/N/A/9/9|MEDIUM|S|UNVERIFIED|GAP_DOWN|DOWN|MEDIUM|MEDIUM|Macro_FX_Commodity|Supply_Demand|WTI 90.22달러와 Brent 94.65달러로 항공유 비용 부담 급증
2|롯데케미칼|011170|KOSPI|2|80.0|72|90|90%|19/15/12/8/N/A/9/9|MEDIUM|S|UNVERIFIED|GAP_DOWN|UNCERTAIN|MEDIUM|MEDIUM|Macro_FX_Commodity|Sector_Theme|유가·나프타 상승과 경기민감 Risk-off의 이중 부담
3|LG화학|051910|KOSPI|3|76.7|69|90|90%|17/15/11/8/N/A/9/9|MEDIUM|S|UNVERIFIED|GAP_DOWN|UNCERTAIN|MEDIUM|MEDIUM|Macro_FX_Commodity|Sector_Theme|원재료·장기금리·성장주 할인율 동시 부담
4|SK하이닉스|000660|KOSPI|4|74.4|67|90|90%|17/15/13/11/N/A/8/3|MEDIUM|S|UNVERIFIED|GAP_DOWN|UNCERTAIN|HIGH|HIGH|Global_Peer|Macro_FX_Commodity|SOXX -2.13%와 EWY -2.77%, 미 10년물 4.79%
5|에코프로비엠|247540|KOSDAQ|5|70.0|63|90|90%|14/15/10/8/N/A/9/7|MEDIUM|S|UNVERIFIED|GAP_DOWN|UNCERTAIN|MEDIUM|MEDIUM|Macro_FX_Commodity|Sector_Theme|고금리·Risk-off·KOSDAQ 상대약세가 고밸류 2차전지에 부담

WATCH:
1|삼성전기|009150|KOSPI|UP
2|한화오션|042660|KOSPI|UP
3|두산에너빌리티|034020|KOSPI|UP
4|S-Oil|010950|KOSPI|UP
5|유한양행|000100|KOSPI|UP
6|대한항공|003490|KOSPI|DOWN
7|롯데케미칼|011170|KOSPI|DOWN
8|LG화학|051910|KOSPI|DOWN
9|SK하이닉스|000660|KOSPI|DOWN
10|에코프로비엠|247540|KOSDAQ|DOWN

STRONG_SECTORS: 정유; 조선·에너지운송; 발전·에너지인프라; 개별 AI부품 수주주
WEAK_SECTORS: 항공·여행; 화학; 반도체·AI; KOSDAQ 고밸류 성장주
TOP_TRAP: 두산에너빌리티 — 신규 대형 수주는 강하지만 기존 원전·가스터빈 기대와 높은 가격반영으로 갭 추격 위험이 매우 높음
MARKET_INVALIDATION: 국제유가 급락과 미 국채금리 하락, USD/KRW 하락, 미국 지수선물 강한 반등이 동시에 나타나고 외국인 현·선물 순매수가 확인될 경우
[/HANDOFF]
[/STAGE_HANDOFF]
