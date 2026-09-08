[DMI_RUN_META]
SCHEMA_VERSION: DMI_v7.1
DATE: 2026-09-02
STAGE: 07:20
RUN_TIME_KST: 2026-09-02 07:20:39
[/DMI_RUN_META]

[STAGE_REPORT]
# TASK 2 — 07:20 Morning Macro — v7.1

## 1. 시작 전 확인

- DATE: 2026-09-02
- ANALYSIS_TIME: 07:20 KST
- STAGE: 07:20 Morning Macro
- US_MARKET_STATUS: CLOSED
- US_DST_STATUS: ON
- US_EARLY_CLOSE_STATUS: NO
- LATEST_MARKET_DATA_TIME: 2026-09-02 07:05 KST 기준 확인 가능한 미국 정규장 최종 거래 데이터
- SCHEMA_VERSION: DMI_v7.1

## 2. 독립 Fresh Scan

03:30 결과를 열람하기 전에 현재 외부 정보만으로 판단을 완료했다.

### 글로벌 시장 FACT

| 항목 | 최종 확인값 | 시장 의미 |
|---|---:|---|
| S&P 500 | 7,631.47, -0.71% | 광범위한 위험회피 |
| Dow | 52,766.88, -0.79% | 경기·금리 부담 |
| Nasdaq Composite | 26,099.77, -1.03% | 장기금리 상승에 성장주 민감 |
| Russell 2000 | 2,920.13, -1.23% | 중소형 위험선호 약화 |
| SPY | 761.78, -0.71% | 미국 대형주 약세 확인 |
| QQQ | 707.64, -1.28% | 기술주 상대약세 |
| SOXX | 500.31, -2.13% | 한국 반도체 직접 부담 |
| EWY | 175.80, -2.77% | 한국 주식 개장 전 부정적 선행신호 |
| Bitcoin | 약 $77,199, -2.01% | 고베타 위험자산 선호 약화 |
| 미국 10년물 | 약 4.79%, 장중 4.80% 부근 | 할인율·외국인 위험선호 부담 |
| Brent | $94.65, +4.6% | 정유 우호, 항공·화학 원가 부담 |
| WTI | $90.22, +5.2% | 인플레이션 재상승 우려 |
| USD/KRW | 약 1,374원, 원화 약세 | 외국인 수급 및 성장주 부담 |

FACT: 9월 1일 미국장은 유가 급등, 장기금리 상승과 중동 긴장 속에서 S&P 500 -0.71%, Nasdaq -1.03%, Russell 2000 -1.23%로 마감했고 하락 종목 수가 상승 종목 수를 약 3대 1로 앞섰다. [Reuters](https://www.reuters.com/business/wall-st-futures-kick-off-september-under-pressure-yields-oil-prices-rise-2026-09-01/) [AP](https://apnews.com/article/61f03262bb5dfa1c414c4fb7be40772e)

FACT: Brent는 $94.65로 4.6%, WTI는 $90.22로 5.2% 상승했다. [Reuters](https://www.reuters.com/business/energy/oil-prices-rise-latest-fighting-resurrects-middle-east-supply-disruption-risks-2026-09-01/)

FACT: 미국 10년물 금리는 약 4.79%까지 상승했고, 에너지를 제외한 주요 업종은 전반적으로 약했다. 미국장 종가 부근까지 뚜렷한 위험선호 회복은 확인되지 않았다.

### INTERPRETATION

유가와 장기금리가 함께 상승한 인플레이션형 Risk-off다. 미국 지수의 약세가 소수 Mega-cap에만 국한되지 않고 시장폭과 중소형주로 확산됐으며, SOXX와 EWY가 지수보다 크게 하락했다. 한국시장에서는 정유의 상대강세 가능성이 가장 직접적이고, 반도체·KOSDAQ 성장주·항공·화학은 불리하다. 원화 약세는 수출주 환산이익보다 단기 외국인 위험축소 경로가 더 중요하다.

### FORECAST

KOSPI와 KOSDAQ 모두 약세 출발 가능성이 높다. KOSPI는 정유·방산 및 일부 대형 가치주의 완충으로 KOSDAQ보다 상대적으로 견조할 수 있지만, 대형 반도체의 비중 때문에 절대 방향은 하락 우위다. KOSDAQ은 금리·반도체·고베타 위험선호의 동시 악화로 상대약세 가능성이 더 높다.

## 3. 주요 거시변수와 한국 전달경로

1. 중동 충돌과 원유 공급위험
   - FACT: 미국·이란 충돌 재확대와 해상 공급차질 우려로 국제유가가 급등했다.
   - INTERPRETATION: 정유 재고평가·정제마진에는 우호적이나 항공유·나프타·물류비에는 부담이다.
   - FORECAST: 정유 상대강세, 항공·화학 상대약세.

2. 글로벌 장기금리 상승
   - FACT: 미국 10년물이 4.8% 부근까지 상승했다.
   - INTERPRETATION: 장기 현금흐름 의존도가 높은 성장주와 KOSDAQ의 밸류에이션 압력이 커진다.
   - FORECAST: 바이오·2차전지·AI·로봇 등 고밸류 성장주의 시장 대비 약세 가능성.

3. 반도체와 한국 ETF 동반 약세
   - FACT: SOXX -2.13%, EWY -2.77%로 마감했다.
   - INTERPRETATION: 삼성전자·SK하이닉스와 반도체 소부장에 직접적인 개장 전 부담이다.
   - FORECAST: 외국인 현·선물 매도가 동반되면 지수 하락 폭이 확대될 수 있다.

4. 원화 약세
   - FACT: USD/KRW는 약 1,374원으로 상승했다.
   - INTERPRETATION: 단기에는 외국인 위험축소와 수입 원가 부담이 우세하다.
   - FORECAST: KOSDAQ과 내수·원재료 수입 업종에 더 불리하다.

## 4. 03:30 이후 신규 이벤트

- 미국 정규장 최종 결과가 확정됐다. 03:30 장중 수치보다 낙폭은 일부 축소됐지만 S&P 500, Nasdaq, Russell 2000이 모두 하락 마감했고 시장폭도 약했다.
- Brent $94.65, WTI $90.22의 최종 결제로 원유 급등이 일시 장중 변동이 아니라 종가까지 유지됐음이 확인됐다.
- SOXX와 EWY도 큰 폭 하락으로 마감해 한국 반도체와 지수 선물에 대한 부정적 전달경로가 유지됐다.
- 03:30 이후 현재 분석 시점까지 시장 레짐을 반전시킬 중앙은행·정책·한국 산업 직접 이벤트는 신뢰 가능한 출처에서 확인되지 않았다.

## 5. 객관적 지수 방향 예측

- KOSPI_DIRECTION_FORECAST: DOWN
- KOSDAQ_DIRECTION_FORECAST: DOWN

판단 근거: EWY -2.77%, SOXX -2.13%, 원화 약세, 미국 10년물 약 4.79%, 유가 급등이 동시 발생했다. KOSDAQ은 할인율과 고베타 위험선호에 더 민감하므로 하방 확률이 KOSPI보다 높다.

## 6. Market Regime Forecast

- Direction: 약세
- Volatility: 높음
- Risk Sentiment: Risk-off
- 시장 성격: 정유·일부 방산 상대강세와 반도체·항공·화학·고밸류 성장주 약세가 공존하는 특정 산업 집중형 고변동성 장세

## 7. KOSPI 분석

### 주요 상승요인
- 유가 급등에 따른 정유 업종의 상대수혜.
- 지정학적 위험 확대에 따른 방산 관심.
- 낙폭 과대 시 대형 가치주·지수 방어수급 유입 가능성.

### 주요 하락요인
- SOXX와 EWY의 동반 급락.
- 미국 10년물 4.8% 부근과 글로벌 채권 매도.
- 원화 약세 및 외국인 현·선물 위험축소 가능성.
- 대형 반도체의 지수 비중.

### 원화·달러 영향
USD/KRW 약 1,374원의 원화 약세는 수출기업 환산효과보다 당일 외국인 수급 경로가 우선한다. 유가 상승과 결합되면 무역조건과 인플레이션 기대에도 부담이다.

### 외국인 위험선호
EWY 급락, 미국 기술주·반도체 약세, 원화 약세가 동시에 나타나 외국인 위험선호에 부정적이다. 개장 전 KOSPI200 선물과 장 초반 삼성전자·SK하이닉스 수급이 핵심 확인 항목이다.

### 예상 주도 업종
절대 상승을 보장하지 않지만 정유와 일부 방산의 상대주도가 예상된다.

### KOSDAQ 대비 상대강도
KOSPI 우위. 다만 대형 반도체 약세로 KOSPI 역시 DOWN 전망이다.

## 8. KOSDAQ 분석

KOSDAQ은 미국 장기금리 상승, Russell 2000 약세, Bitcoin 약세, SOXX 급락이 동시에 불리하게 작용한다. 반도체 장비는 글로벌 반도체 매도 영향을 직접 받고, AI·로봇·게임은 위험선호와 할인율 경로에서 부담이 크다. 바이오 고유 임상·허가 이벤트와 개별 정책 촉매가 없는 종목은 지수 방어력이 낮을 가능성이 있다. 2차전지는 원유 상승의 장기 전환 논리보다 당일 금리·위험회피·원재료 비용 경로가 우세하다.

- 예상 방향: DOWN
- 예상 상대강도: KOSPI 대비 약세
- 핵심 위험: 장 초반 신용·개인 수급이 약해질 경우 낙폭 확대
- 반대 시나리오: 미국 선물 반등, USD/KRW 급락, 외국인 코스닥 선물·현물 순매수 전환

## 9. 국내 당일 이벤트 캘린더 확인

현재 확인 가능한 신뢰도 높은 공개자료에서 2026-09-02 한국시장 전체 방향을 바꿀 만한 확정 기업 실적·정책·규제 이벤트를 확인하지 못했다. 따라서 특정 일정을 추정해 기재하지 않는다. 정부의 2026년 9월 국고채 발행 계획은 공개돼 있으나, 오늘 단일 시장 촉매로 연결할 구체적 입찰 이벤트는 N/A다. [한국 재정경제부](https://english.mofe.go.kr/)

## 10. 예상 강세 섹터

| Rank | 섹터 | 핵심 촉매 | 국내 전달경로 | 지속성 | 주요 Risk |
|---|---|---|---|---|---|
| 1 | 정유 | Brent·WTI 4.6~5.2% 급등 | 재고평가와 정제마진 기대 | 높음 | 휴전·공급 정상화 시 유가 급락 |
| 2 | 방산 | 중동 지정학 위험 확대 | 수출·수주 기대의 위험 프리미엄 | 보통 | 직접 신규 수주 부재와 높은 가격반영 |
| 3 | 일부 조선·에너지 인프라 | 에너지 안보·운송 리스크 | LNG·탱커·해양설비 관심 | 낮음~보통 | Risk-off와 선가·수주 직접 촉매 부재 |

## 11. 예상 약세 섹터

| Rank | 섹터 | 핵심 촉매 | 국내 전달경로 | 지속성 | 주요 Risk |
|---|---|---|---|---|---|
| 1 | 반도체·AI | SOXX -2.13%, 금리 상승 | 대형 반도체·소부장 외국인 매도 | 높음 | 메모리 공급차질 호재 또는 저가매수 |
| 2 | 항공·여행 | WTI $90.22, Brent $94.65 | 연료비·수요 둔화 우려 | 높음 | 유가 급반락과 운임 전가 |
| 3 | 화학 | 나프타 원가와 경기민감 위험 | 스프레드 압박 | 보통~높음 | 제품가격 동반 상승 |
| 4 | KOSDAQ 고밸류 성장주 | 10년물 약 4.79%, Risk-off | 할인율 상승과 신용위험 | 높음 | 국내 정책·개별 임상 촉매 |
| 5 | 운송·소비재 | 에너지 비용과 원화 약세 | 비용 상승·실질소득 압박 | 보통 | 원화·유가 반전 |

## 12. 03:30 대비 변화

독립 판단 완료 후 같은 날짜의 최신 유효 03:30 HANDOFF를 읽어 비교했다.

- REGIME_PRELIMINARY Risk-off: MAINTAINED
- 정유 상대강세: MAINTAINED
- 방산 상대강세: MAINTAINED
- 반도체 약세: MAINTAINED
- 항공 약세: STRENGTHENED — WTI와 Brent 급등이 최종 결제까지 유지
- 화학 약세: MAINTAINED
- 고금리·유가·원화 약세가 위험선호를 제약한다는 판단: MAINTAINED
- 미국장 미종료 불확실성: INVALIDATED — 정규장이 종료돼 최종 결과가 확정됨
- 전체 변화: 장중보다 지수 낙폭은 일부 축소됐지만 종가 시장폭, SOXX·EWY, 유가와 금리가 독립 Risk-off 판단을 확인했다.

## 13. Morning Macro 결론

- 오늘 시장 한 문장: 유가·금리·원화의 동반 부담과 미국 반도체·한국 ETF 급락으로 양 지수 약세가 예상되며, 정유·일부 방산만 상대강세를 보일 가능성이 높은 고변동성 Risk-off 장이다.
- KOSPI 방향 예측: DOWN
- KOSDAQ 방향 예측: DOWN
- KOSPI 전망: 약세, 다만 정유·방산·일부 가치주의 완충으로 KOSDAQ 대비 상대우위
- KOSDAQ 전망: 금리·반도체·고베타 위험선호 악화로 KOSPI 대비 상대약세
- 가장 강한 섹터: 정유
- 가장 약한 섹터: 반도체·AI
- 핵심 변수 3개: Brent·WTI 유지 여부; 미국 10년물과 USD/KRW; 외국인 현·선물 및 삼성전자·SK하이닉스 개장 수급
- 가장 중요한 Tail Risk: 호르무즈 공급차질 확대 또는 추가 군사 충돌로 유가·금리가 재차 급등하는 것
- 08:25까지 확인할 요소: KOSPI200·KOSDAQ150 선물, USD/KRW, 국제유가와 미국 지수선물, 외국인 예상 수급, 반도체·정유·항공의 예상체결 상대강도

[HANDOFF]
SCHEMA_VERSION: DMI_v7.1
DATE: 2026-09-02
STAGE: 07:20

KOSPI_DIRECTION_FORECAST: DOWN
KOSDAQ_DIRECTION_FORECAST: DOWN

MARKET_DIRECTION: 약세
VOLATILITY: 높음
RISK_SENTIMENT: Risk-off

KOSPI_VIEW: 약세; 정유·방산·일부 가치주 완충으로 KOSDAQ 대비 상대우위이나 대형 반도체와 외국인 수급 부담
KOSDAQ_VIEW: 약세; 금리·반도체·고베타 위험선호 악화로 KOSPI 대비 상대약세

STRONG_SECTORS: 정유; 방산; 일부 조선·에너지 인프라
WEAK_SECTORS: 반도체·AI; 항공·여행; 화학; KOSDAQ 고밸류 성장주; 운송·소비재

KEY_VARIABLES: Brent·WTI 유지 여부; 미국 10년물과 USD/KRW; 외국인 현·선물 및 대형 반도체 개장 수급
TAIL_RISK: 호르무즈 공급차질 확대 또는 추가 군사 충돌로 유가와 장기금리가 재차 급등하는 것
WATCH_UNTIL_08_25: KOSPI200·KOSDAQ150 선물; USD/KRW; 국제유가와 미국 지수선물; 외국인 예상 수급; 반도체·정유·항공 예상체결 상대강도
[/HANDOFF]
[/STAGE_REPORT]

[STAGE_HANDOFF]
[HANDOFF]
SCHEMA_VERSION: DMI_v7.1
DATE: 2026-09-02
STAGE: 07:20

KOSPI_DIRECTION_FORECAST: DOWN
KOSDAQ_DIRECTION_FORECAST: DOWN

MARKET_DIRECTION: 약세
VOLATILITY: 높음
RISK_SENTIMENT: Risk-off

KOSPI_VIEW: 약세; 정유·방산·일부 가치주 완충으로 KOSDAQ 대비 상대우위이나 대형 반도체와 외국인 수급 부담
KOSDAQ_VIEW: 약세; 금리·반도체·고베타 위험선호 악화로 KOSPI 대비 상대약세

STRONG_SECTORS: 정유; 방산; 일부 조선·에너지 인프라
WEAK_SECTORS: 반도체·AI; 항공·여행; 화학; KOSDAQ 고밸류 성장주; 운송·소비재

KEY_VARIABLES: Brent·WTI 유지 여부; 미국 10년물과 USD/KRW; 외국인 현·선물 및 대형 반도체 개장 수급
TAIL_RISK: 호르무즈 공급차질 확대 또는 추가 군사 충돌로 유가와 장기금리가 재차 급등하는 것
WATCH_UNTIL_08_25: KOSPI200·KOSDAQ150 선물; USD/KRW; 국제유가와 미국 지수선물; 외국인 예상 수급; 반도체·정유·항공 예상체결 상대강도
[/HANDOFF]
[/STAGE_HANDOFF]
