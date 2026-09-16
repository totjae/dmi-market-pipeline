[DMI_REVIEW_META]
SCHEMA_VERSION: DMI_REVIEW_v1.3
DATE: 2026-09-16
PREDICTION_RUN_TIMES_KST: [03:30, 08:30]
REVIEW_TIME_KST: 16:30
STARTED_AT_KST: 2026-09-16T16:27:20+09:00
REPORT_COMPLETED_AT_KST: 2026-09-16T16:30:09+09:00
DATA_CUTOFF_KST: 2026-09-16T16:29:29+09:00
SOURCE_MANIFEST: REVIEW_EVIDENCE.input_manifest
REVIEW_DOCUMENT_VERSIONS: REVIEW_EVIDENCE.review_document_versions
RUN_TYPE: NORMAL
RERUN_SEQUENCE: 0
[/DMI_REVIEW_META]

[REVIEW_REPORT]
# DMI Two-Agent Daily Review — 2026-09-16

## 1. 입력과 검증 상태

KRX 정규장 개장시각 09:00 KST 이전에 최초 저장된 구조 유효 결과만 공식 입력으로 선정했다. 지정된 네 조합 중 3개가 공식 입력이며 Agent 1의 03:30 결과는 파일이 없어 UNAVAILABLE이다.

| 슬롯 | 에이전트 | 상태 | 공식 입력 | 최초 저장시각(KST) | 사유 |
|---|---|---|---|---|---|
| 03:30 | Agent 1 | UNAVAILABLE | 없음 | N/A | 지정 경로 및 해당 날짜 디렉터리에 0330 결과 없음 |
| 03:30 | Agent 2 | OFFICIAL | runs/2026-09-16/0330.md | 03:32:38 | 최초 저장본, 구조·날짜·슬롯·본문/캡슐 일치, 장전 저장 |
| 08:30 | Agent 1 | OFFICIAL | runs/2026-09-16/0830.md | 08:29:23 | 최초 저장본, 구조·날짜·슬롯·본문/캡슐 일치, 장전 저장 |
| 08:30 | Agent 2 | OFFICIAL | runs/2026-09-16/0830.md | 08:30:56 | 최초 저장본, 후보 0개 판단이 구조적으로 유효하며 장전 저장 |

rerun 파일은 없었고 공식 입력을 대체할 후속 revision도 없었다. 각 입력의 문서 버전 기록은 blob SHA가 있으나 commit SHA가 N/A이므로 버전 묶음 상태는 UNVERIFIED로 보존했으며, 이는 후보 성과 집계를 막지 않는다.

## 2. 시장 Ground Truth

2026-09-16 KRX 정규장은 KOSPI 6,717.97(+1.37%), KOSDAQ 815.98(+0.44%)로 마감했다. 후보 가격은 KRX 정규장 표시값만 사용했고 애프터마켓 가격은 섞지 않았다.

| 종목 | 전일 종가 | 시가 | 고가 | 저가 | 종가 |
|---|---:|---:|---:|---:|---:|
| 두산퓨얼셀 | 51,600 | 50,800 | 51,800 | 49,550 | 51,300 |
| 효성중공업 | 2,689,000 | 2,720,000 | 2,834,000 | 2,690,000 | 2,806,000 |
| 흥구석유 | 14,980 | 15,300 | 15,580 | 13,520 | 13,970 |
| S-Oil | 148,700 | 149,900 | 150,600 | 143,200 | 144,100 |

## 3. 후보별 실제 성과

| 슬롯·에이전트·순위 | 종목 | C2C | O2C | FE | OFE | AE | FE3/5/10 | 예상 FE 적합 |
|---|---|---:|---:|---:|---:|---:|---|---|
| 03:30 A2 #1 | 흥구석유 | -6.74% | -8.69% | 4.01% | 1.83% | 9.75% | Y/N/N | 실패 (+5~10%) |
| 03:30 A2 #2 | S-Oil | -3.09% | -3.87% | 1.28% | 0.47% | 3.70% | N/N/N | 실패 (+3~5%) |
| 08:30 A1 #1 | 두산퓨얼셀 | -0.58% | +0.98% | 0.39% | 1.97% | 3.97% | N/N/N | 실패 (+5~10%) |
| 08:30 A1 #2 | 효성중공업 | +4.35% | +3.16% | 5.39% | 4.19% | 0.00% | Y/Y/N | 실패 (+3~5%, 상단 초과) |

FE는 전일 종가 대비 당일 고가 상승률이고 AE는 전일 종가 기준 하방폭이다. 실제 체결수익이나 실현손익이 아니다.

Agent 2의 03:30 조건부 계획 중 흥구석유는 고가가 15,460원을 넘었지만 일봉만으로 거래 증가·재시험 지지·무효화 발생 순서를 확인할 수 없어 NOT_SCORABLE이다. S-Oil은 고가 150,600원으로 진입 기준 151,200원에 닿지 않아 NOT_TRIGGERED다. Agent 1의 08:30 후보는 관찰과 무효화 조건만 있고 진입·손절·목표의 완결된 계획이 없어 NOT_PROVIDED다.

## 4. 에이전트별 KPI

### 03:30

| 지표 | Agent 1 | Agent 2 |
|---|---:|---:|
| 입력 상태 / 후보 수 | UNAVAILABLE / N/A | OFFICIAL / 2 |
| TOP1 FE | N/A | 4.01% |
| TOP3 평균 FE | N/A | 2.64% (n=2/2) |
| TOP3 평균 OFE | N/A | 1.15% (n=2/2) |
| TOP3 평균 AE | N/A | 6.72% (n=2/2) |
| FE3 / FE5 / FE10 적중률 | N/A | 50.00% / 0.00% / 0.00% |
| 예상 FE 구간 적합률 | N/A | 0.00% (n=2/2) |
| 순위 Spearman | N/A | +1.000 (n=2) |

Agent 2는 두 후보의 실제 FE 순서를 정확히 정렬했지만, 두 예상 FE 구간을 모두 높게 잡았다. 흥구석유는 FE3에는 도달했으나 음의 C2C·O2C와 9.75% AE로 추격 위험이 현실화됐다.

### 08:30

| 지표 | Agent 1 | Agent 2 |
|---|---:|---:|
| 입력 상태 / 후보 수 | OFFICIAL / 2 | OFFICIAL / 0 |
| TOP1 FE | 0.39% | N/A |
| TOP3 평균 FE | 2.89% (n=2/2) | N/A (n=0/0) |
| TOP3 평균 OFE | 3.08% (n=2/2) | N/A |
| TOP3 평균 AE | 1.99% (n=2/2) | N/A |
| FE3 / FE5 / FE10 적중률 | 50.00% / 50.00% / 0.00% | N/A |
| 예상 FE 구간 적합률 | 0.00% (n=2/2) | N/A |
| 순위 Spearman | -1.000 (n=2) | N/A (n=0) |

Agent 1은 효성중공업의 5.39% FE를 발굴했지만 이를 2순위로 두어 실제 성과 순위와 반대로 정렬했다. Agent 2의 후보 0개는 유효한 명시적 보류이며 누락이나 0점으로 처리하지 않는다.

## 5. Agent 1 vs Agent 2 비교

- 03:30: Agent 1 입력이 없어 비교 불가. BEST_AGENT=N/A.
- 08:30: Agent 1은 5% 이상 움직인 효성중공업을 발굴했고 Agent 2는 명시적으로 후보를 선정하지 않았다. 후보 0개에 성과 점수를 부여하는 사전 기준이 없으므로 강제 승자를 정하지 않고 BEST_AGENT=N/A로 둔다.
- 당일 최고 FE 후보는 Agent 1 08:30의 효성중공업 5.39%다.

## 6. 같은 에이전트의 시간대 비교

- Agent 1: 03:30 입력이 없어 시간대 비교 불가.
- Agent 2: 03:30은 에너지 후보 2개를 제시해 평균 FE 2.64%와 FE3 1건을 기록했지만 종가 추세와 하방 위험은 좋지 않았다. 08:30은 신규 촉매·가격 여유 부족을 이유로 0개를 선택했다. 후행 슬롯은 독립적인 새 분석으로, 03:30의 오류 복구로 해석하지 않는다.
- 08:30의 보류는 약한 에너지 후속 흐름을 피한 점은 합리적이지만, 후보 0개에는 직접 비교 가능한 FE 표본이 없어 우월성을 수치화하지 않는다.

## 7. 성공·오류 분석

성공 패턴은 직접 수주 재료가 있던 효성중공업이 시장 반등과 함께 5.39% FE를 기록한 것이다. 반면 계약 규모가 더 컸던 두산퓨얼셀은 전일 선반영 뒤 FE 0.39%에 그쳐, 촉매 규모만으로 남은 가격 여력을 판단하면 안 된다는 점이 확인됐다.

에너지 후보는 국제유가 상승 재료에도 정규장 추세 지속이 약했다. 흥구석유는 시초가가 전일 종가보다 높았지만 이후 종가까지 크게 밀렸고, S-Oil도 FE 1.28%에 그쳤다. 이는 거시 재료의 방향과 국내 개별 종목의 당일 가격 경로를 동일시한 오판이다.

## 8. 개선 후보

- 전일 급등·애프터마켓 반영이 확인된 종목은 촉매 규모와 별개로 남은 가격 여력을 더 강하게 감점한다.
- 순위 결정에서 계약 규모뿐 아니라 전일 가격 거부 후 회복 가능성, 업종 상대강도, 예상 시초가 위치를 별도 확인한다.
- 국제유가 같은 거시 촉매는 개장 갭보다 정규장 지속성을 확인할 조건을 강화한다.
- 후보 0개 전략은 다일 표본에서 기회 회피 효과와 놓친 FE를 함께 추적한 뒤 평가한다.

이 개선안은 1일 관찰 결과이며 프롬프트나 활성 규칙으로 자동 반영하지 않는다.

## 9. 최종 요약

공식 입력은 3/4개였고 후보 성과 표본은 총 4개였다. 최고 FE는 효성중공업 5.39%였으며, 03:30 Agent 2는 순위를 올바르게 정렬했지만 예상폭을 과대평가했고, 08:30 Agent 1은 최고 후보를 발굴했으나 순위를 반대로 배치했다. 입력 누락과 후보 0개 때문에 두 슬롯 모두 Agent 간 공식 승자는 정하지 않았다.

[REVIEW_RESULT]
SCHEMA_VERSION: DMI_REVIEW_v1.3
DATE: 2026-09-16
PREDICTION_RUN_TIME_KST: 03:30
AGENT_1_STATUS: UNAVAILABLE
AGENT_2_STATUS: OFFICIAL
AGENT_1_COUNT: N/A
AGENT_2_COUNT: 2
AGENT_1_TOP1_FE: N/A
AGENT_2_TOP1_FE: 4.01%
AGENT_1_TOP3_AVG_FE: N/A
AGENT_2_TOP3_AVG_FE: 2.64%
AGENT_1_FE3_HIT_RATE: N/A
AGENT_2_FE3_HIT_RATE: 50.00%
AGENT_1_FE5_HIT_RATE: N/A
AGENT_2_FE5_HIT_RATE: 0.00%
AGENT_1_FE10_HIT_RATE: N/A
AGENT_2_FE10_HIT_RATE: 0.00%
AGENT_1_VALID_FE_COUNT: N/A
AGENT_2_VALID_FE_COUNT: 2
AGENT_1_TOP3_VALID_FE_COUNT: N/A
AGENT_2_TOP3_VALID_FE_COUNT: 2
AGENT_1_RANK_PERFORMANCE_SPEARMAN: N/A
AGENT_2_RANK_PERFORMANCE_SPEARMAN: +1.000
AGENT_1_RANK_PERFORMANCE_PAIR_COUNT: N/A
AGENT_2_RANK_PERFORMANCE_PAIR_COUNT: 2
BEST_AGENT: N/A
BEST_PICK: 흥구석유(024060) FE 4.01%
PRIMARY_SUCCESS_PATTERN: 에너지 후보 내 실제 FE 순위를 정확히 정렬
PRIMARY_ERROR_PATTERN: 국제유가 상승을 국내 종목의 정규장 지속 상승으로 과대 전환
IMPROVEMENT_CANDIDATE: 높은 시초가와 전일 선반영 시 남은 가격 여력 감점 강화
[/REVIEW_RESULT]

[REVIEW_RESULT]
SCHEMA_VERSION: DMI_REVIEW_v1.3
DATE: 2026-09-16
PREDICTION_RUN_TIME_KST: 08:30
AGENT_1_STATUS: OFFICIAL
AGENT_2_STATUS: OFFICIAL
AGENT_1_COUNT: 2
AGENT_2_COUNT: 0
AGENT_1_TOP1_FE: 0.39%
AGENT_2_TOP1_FE: N/A
AGENT_1_TOP3_AVG_FE: 2.89%
AGENT_2_TOP3_AVG_FE: N/A
AGENT_1_FE3_HIT_RATE: 50.00%
AGENT_2_FE3_HIT_RATE: N/A
AGENT_1_FE5_HIT_RATE: 50.00%
AGENT_2_FE5_HIT_RATE: N/A
AGENT_1_FE10_HIT_RATE: 0.00%
AGENT_2_FE10_HIT_RATE: N/A
AGENT_1_VALID_FE_COUNT: 2
AGENT_2_VALID_FE_COUNT: 0
AGENT_1_TOP3_VALID_FE_COUNT: 2
AGENT_2_TOP3_VALID_FE_COUNT: 0
AGENT_1_RANK_PERFORMANCE_SPEARMAN: -1.000
AGENT_2_RANK_PERFORMANCE_SPEARMAN: N/A
AGENT_1_RANK_PERFORMANCE_PAIR_COUNT: 2
AGENT_2_RANK_PERFORMANCE_PAIR_COUNT: 0
BEST_AGENT: N/A
BEST_PICK: 효성중공업(298040) FE 5.39%
PRIMARY_SUCCESS_PATTERN: 직접 수주 촉매 종목에서 FE5 후보 발굴
PRIMARY_ERROR_PATTERN: 촉매 규모를 우선해 실제 최고 FE 후보를 2순위로 배치
IMPROVEMENT_CANDIDATE: 계약 규모와 남은 가격 여력·가격 거부 후 회복 가능성을 분리 평가
[/REVIEW_RESULT]
[/REVIEW_REPORT]

[REVIEW_EVIDENCE]
{
  "schema_version": "DMI_REVIEW_EVIDENCE_v1",
  "review_document_versions": [
    {"role":"WORKFLOW","repository":"totjae/dmi-market-pipeline","path":"WORKFLOW.md","commit_sha":null,"blob_sha":"f7d593b7f558c95df45ad802b1489591cb726151","read_at_kst":"2026-09-16T16:29:29+09:00","status":"VERIFIED","reason":"NONE"},
    {"role":"SOURCES","repository":"totjae/dmi-market-pipeline","path":"config/SOURCES.md","commit_sha":null,"blob_sha":"5c47de7afdb65f60bc81a0050058a4c71d332853","read_at_kst":"2026-09-16T16:29:29+09:00","status":"VERIFIED","reason":"NONE"},
    {"role":"REVIEW_PROMPT","repository":"totjae/dmi-market-pipeline","path":"prompt/REVIEW_PROMPT.md","commit_sha":null,"blob_sha":"fbd5f2e1f490a2b5a68ae8b095b58bccbbc19cb2","read_at_kst":"2026-09-16T16:29:29+09:00","status":"VERIFIED","reason":"NONE"},
    {"role":"REVIEW_OUTPUT","repository":"totjae/dmi-market-pipeline","path":"templates/REVIEW_OUTPUT.md","commit_sha":null,"blob_sha":"aced9658e7423ac059150f7d5cdf069efce21849","read_at_kst":"2026-09-16T16:29:29+09:00","status":"VERIFIED","reason":"NONE"}
  ],
  "input_manifest": [
    {
      "input_id":"a1_0330","agent_id":"AGENT_1","date":"2026-09-16","slot_kst":"03:30","repository":"totjae/dmi-agent-1","path":"runs/2026-09-16/0330.md","evaluated_commit_sha":null,"evaluated_blob_sha":null,"first_saved_commit_sha":null,"first_saved_at_kst":null,"selection_status":"UNAVAILABLE","selection_reason":"MISSING_FILE","prediction_schema_version":null,"prediction_document_versions":[],"version_status":"NOT_PROVIDED"
    },
    {
      "input_id":"a2_0330","agent_id":"AGENT_2","date":"2026-09-16","slot_kst":"03:30","repository":"totjae/dmi-agent-2","path":"runs/2026-09-16/0330.md","evaluated_commit_sha":"dd0a9247414faea6818e696d271f75bcd1f32fda","evaluated_blob_sha":"3333c67cc5b9f847b08475acb0642cc031b74e5b","first_saved_commit_sha":"dd0a9247414faea6818e696d271f75bcd1f32fda","first_saved_at_kst":"2026-09-16T03:32:38+09:00","selection_status":"OFFICIAL","selection_reason":"FIRST_VALID_PREOPEN_RESULT","prediction_schema_version":"DMI_AGENT_v1.3","prediction_document_versions":[{"role":"WORKFLOW","repository":"totjae/dmi-agent-2","path":"WORKFLOW.md","commit_sha":"N/A","blob_sha":"1f863cf6d2ce2fc3b347609845906d1d0ed56815","read_at_kst":"2026-09-16T03:28:31+09:00","status":"VERIFIED","reason":"NONE"},{"role":"AGENT_PROMPT","repository":"totjae/dmi-agent-2","path":"prompt/AGENT_PROMPT.md","commit_sha":"N/A","blob_sha":"4da3d7554ee7da9bec1af8f74ccea24b824854bb","read_at_kst":"2026-09-16T03:28:31+09:00","status":"VERIFIED","reason":"NONE"},{"role":"OUTPUT","repository":"totjae/dmi-agent-2","path":"templates/OUTPUT.md","commit_sha":"N/A","blob_sha":"cafb325fcc6f5497c631849517849f7c24ae7a3d","read_at_kst":"2026-09-16T03:31:16+09:00","status":"VERIFIED","reason":"NONE"}],"version_status":"UNVERIFIED"
    },
    {
      "input_id":"a1_0830","agent_id":"AGENT_1","date":"2026-09-16","slot_kst":"08:30","repository":"totjae/dmi-agent-1","path":"runs/2026-09-16/0830.md","evaluated_commit_sha":"d936a3c3dec8e461c68d231275969017140f2dcf","evaluated_blob_sha":"bb62573306e1f160a3d5bc8f931aa3d94f905278","first_saved_commit_sha":"d936a3c3dec8e461c68d231275969017140f2dcf","first_saved_at_kst":"2026-09-16T08:29:23+09:00","selection_status":"OFFICIAL","selection_reason":"FIRST_VALID_PREOPEN_RESULT","prediction_schema_version":"DMI_AGENT_v1.3","prediction_document_versions":[{"role":"WORKFLOW","repository":"totjae/dmi-agent-1","path":"WORKFLOW.md","commit_sha":"N/A","blob_sha":"8a25e4fe9ce2e66b516a189b78def10ba4281ad1","read_at_kst":"2026-09-16T08:25:27+09:00","status":"VERIFIED","reason":"NONE"},{"role":"AGENT_PROMPT","repository":"totjae/dmi-agent-1","path":"prompt/AGENT_PROMPT.md","commit_sha":"N/A","blob_sha":"a44b95f40710db6c56b8916b8aabce89d1654633","read_at_kst":"2026-09-16T08:25:27+09:00","status":"VERIFIED","reason":"NONE"},{"role":"OUTPUT","repository":"totjae/dmi-agent-1","path":"templates/OUTPUT.md","commit_sha":"N/A","blob_sha":"cafb325fcc6f5497c631849517849f7c24ae7a3d","read_at_kst":"2026-09-16T08:28:05+09:00","status":"VERIFIED","reason":"NONE"}],"version_status":"UNVERIFIED"
    },
    {
      "input_id":"a2_0830","agent_id":"AGENT_2","date":"2026-09-16","slot_kst":"08:30","repository":"totjae/dmi-agent-2","path":"runs/2026-09-16/0830.md","evaluated_commit_sha":"2ea812787e60b1c07d3619f02b44d092718107b7","evaluated_blob_sha":"0f5260b376de478ad8157a83684e33a834680026","first_saved_commit_sha":"2ea812787e60b1c07d3619f02b44d092718107b7","first_saved_at_kst":"2026-09-16T08:30:56+09:00","selection_status":"OFFICIAL","selection_reason":"FIRST_VALID_PREOPEN_RESULT_ZERO_CANDIDATES","prediction_schema_version":"DMI_AGENT_v1.3","prediction_document_versions":[{"role":"WORKFLOW","repository":"totjae/dmi-agent-2","path":"WORKFLOW.md","commit_sha":"N/A","blob_sha":"1f863cf6d2ce2fc3b347609845906d1d0ed56815","read_at_kst":"2026-09-16T08:29:03+09:00","status":"VERIFIED","reason":"NONE"},{"role":"AGENT_PROMPT","repository":"totjae/dmi-agent-2","path":"prompt/AGENT_PROMPT.md","commit_sha":"N/A","blob_sha":"4da3d7554ee7da9bec1af8f74ccea24b824854bb","read_at_kst":"2026-09-16T08:29:03+09:00","status":"VERIFIED","reason":"NONE"},{"role":"OUTPUT","repository":"totjae/dmi-agent-2","path":"templates/OUTPUT.md","commit_sha":"N/A","blob_sha":"cafb325fcc6f5497c631849517849f7c24ae7a3d","read_at_kst":"2026-09-16T08:30:06+09:00","status":"VERIFIED","reason":"NONE"}],"version_status":"UNVERIFIED"
    }
  ],
  "price_sources": [
    {"source_id":"src_market_0916","provider":"Investing.com","url":"https://kr.investing.com/","retrieved_at_kst":"2026-09-16T16:29:29+09:00","observation_date":"2026-09-16","venue":"KRX","session":"REGULAR","currency":"KRW","adjustment_basis":"provider-displayed index close","status":"VERIFIED","reason":"KOSPI and KOSDAQ regular-session close displayed at 15:29:59 KST"},
    {"source_id":"src_df_0916","provider":"Google Finance","url":"https://www.google.com/finance/quote/336260:KRX?hl=ko","retrieved_at_kst":"2026-09-16T16:29:29+09:00","observation_date":"2026-09-16","previous_close_observation_date":"2026-09-15","venue":"KRX","session":"REGULAR","currency":"KRW","adjustment_basis":"provider-displayed unadjusted daily prices; no corporate action identified in reviewed source","status":"VERIFIED","reason":"15:30:03 KST close and daily OHLC displayed"},
    {"source_id":"src_hh_0916","provider":"Google Finance","url":"https://www.google.com/finance/quote/298040:KRX?hl=ko","retrieved_at_kst":"2026-09-16T16:29:29+09:00","observation_date":"2026-09-16","previous_close_observation_date":"2026-09-15","venue":"KRX","session":"REGULAR","currency":"KRW","adjustment_basis":"provider-displayed unadjusted daily prices; no corporate action identified in reviewed source","status":"VERIFIED","reason":"15:30:02 KST close and daily OHLC displayed"},
    {"source_id":"src_hgo_intraday_0916","provider":"Google Finance","url":"https://www.google.com/finance/quote/024060:KOSDAQ?hl=ko","retrieved_at_kst":"2026-09-16T16:29:29+09:00","observation_date":"2026-09-16","previous_close_observation_date":"2026-09-15","venue":"KRX","session":"REGULAR","currency":"KRW","adjustment_basis":"provider-displayed unadjusted daily prices; no corporate action identified in reviewed source","status":"VERIFIED","reason":"daily open/high/low and previous close displayed"},
    {"source_id":"src_hgo_close_0916","provider":"매일경제 마켓","url":"https://stock.mk.co.kr/price/news/KR7024060006","retrieved_at_kst":"2026-09-16T16:29:29+09:00","observation_date":"2026-09-16","previous_close_observation_date":"2026-09-15","venue":"KRX","session":"REGULAR","currency":"KRW","adjustment_basis":"provider-displayed unadjusted regular-session price","status":"VERIFIED","reason":"15:32 KST final close and high displayed"},
    {"source_id":"src_soil_0916","provider":"Google Finance","url":"https://www.google.com/finance/quote/010950:KRX?hl=ko","retrieved_at_kst":"2026-09-16T16:29:29+09:00","observation_date":"2026-09-16","previous_close_observation_date":"2026-09-15","venue":"KRX","session":"REGULAR","currency":"KRW","adjustment_basis":"provider-displayed unadjusted daily prices; no corporate action identified in reviewed source","status":"VERIFIED","reason":"15:30:04 KST close and daily OHLC displayed"}
  ],
  "candidates": [
    {
      "input_id":"a2_0330","rank":1,"code":"024060","name":"흥구석유","market":"KOSDAQ","evaluation_scope":"OFFICIAL",
      "prices":{"previous_close":{"value":14980,"source_ids":["src_hgo_intraday_0916","src_hgo_close_0916"]},"open":{"value":15300,"source_ids":["src_hgo_intraday_0916"]},"high":{"value":15580,"source_ids":["src_hgo_intraday_0916","src_hgo_close_0916"]},"low":{"value":13520,"source_ids":["src_hgo_intraday_0916"]},"close":{"value":13970,"source_ids":["src_hgo_close_0916"]}},
      "metrics_pct":{"c2c":-6.742323097463284,"o2c":-8.69281045751634,"fe":4.005340453938585,"ofe":1.8300653594771243,"ae":9.746328437917223},
      "hits":{"fe3":true,"fe5":false,"fe10":false},"expected_fe_range_match":false,
      "trade_plan":{"status":"NOT_SCORABLE","report_reference":"3. 후보별 실제 성과","reason":"고가가 진입 기준을 넘었으나 일봉으로 거래 증가·재시험 지지·무효화 순서를 확인할 수 없음","evidence_urls":["https://www.google.com/finance/quote/024060:KOSDAQ?hl=ko","https://stock.mk.co.kr/price/news/KR7024060006"]},
      "missing_reasons":[]
    },
    {
      "input_id":"a2_0330","rank":2,"code":"010950","name":"S-Oil","market":"KOSPI","evaluation_scope":"OFFICIAL",
      "prices":{"previous_close":{"value":148700,"source_ids":["src_soil_0916"]},"open":{"value":149900,"source_ids":["src_soil_0916"]},"high":{"value":150600,"source_ids":["src_soil_0916"]},"low":{"value":143200,"source_ids":["src_soil_0916"]},"close":{"value":144100,"source_ids":["src_soil_0916"]}},
      "metrics_pct":{"c2c":-3.093476798924008,"o2c":-3.8692461641094065,"fe":1.277740416946873,"ofe":0.46697798532354906,"ae":3.698722259583053},
      "hits":{"fe3":false,"fe5":false,"fe10":false},"expected_fe_range_match":false,
      "trade_plan":{"status":"NOT_TRIGGERED","report_reference":"3. 후보별 실제 성과","reason":"정규장 고가 150,600원이 진입 기준 151,200원에 미달","evidence_urls":["https://www.google.com/finance/quote/010950:KRX?hl=ko"]},
      "missing_reasons":[]
    },
    {
      "input_id":"a1_0830","rank":1,"code":"336260","name":"두산퓨얼셀","market":"KOSPI","evaluation_scope":"OFFICIAL",
      "prices":{"previous_close":{"value":51600,"source_ids":["src_df_0916"]},"open":{"value":50800,"source_ids":["src_df_0916"]},"high":{"value":51800,"source_ids":["src_df_0916"]},"low":{"value":49550,"source_ids":["src_df_0916"]},"close":{"value":51300,"source_ids":["src_df_0916"]}},
      "metrics_pct":{"c2c":-0.5813953488372093,"o2c":0.984251968503937,"fe":0.3875968992248062,"ofe":1.968503937007874,"ae":3.9728682170542635},
      "hits":{"fe3":false,"fe5":false,"fe10":false},"expected_fe_range_match":false,
      "trade_plan":{"status":"NOT_PROVIDED","report_reference":"3. 후보별 실제 성과","reason":"관찰과 무효화 조건만 있으며 완결된 진입·손절·목표 계획은 제공되지 않음","evidence_urls":[]},
      "missing_reasons":[]
    },
    {
      "input_id":"a1_0830","rank":2,"code":"298040","name":"효성중공업","market":"KOSPI","evaluation_scope":"OFFICIAL",
      "prices":{"previous_close":{"value":2689000,"source_ids":["src_hh_0916"]},"open":{"value":2720000,"source_ids":["src_hh_0916"]},"high":{"value":2834000,"source_ids":["src_hh_0916"]},"low":{"value":2690000,"source_ids":["src_hh_0916"]},"close":{"value":2806000,"source_ids":["src_hh_0916"]}},
      "metrics_pct":{"c2c":4.3510598735589445,"o2c":3.161764705882353,"fe":5.392339159538862,"ofe":4.191176470588235,"ae":0},
      "hits":{"fe3":true,"fe5":true,"fe10":false},"expected_fe_range_match":false,
      "trade_plan":{"status":"NOT_PROVIDED","report_reference":"3. 후보별 실제 성과","reason":"관찰과 무효화 조건만 있으며 완결된 진입·손절·목표 계획은 제공되지 않음","evidence_urls":[]},
      "missing_reasons":[]
    }
  ]
}
[/REVIEW_EVIDENCE]
