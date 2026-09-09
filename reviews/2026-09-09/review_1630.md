[DMI_REVIEW_META]
SCHEMA_VERSION: DMI_REVIEW_v1.1
DATE: 2026-09-09
PREDICTION_RUN_TIMES_KST: [03:30, 08:30]
REVIEW_TIME_KST: 16:30
STARTED_AT_KST: 2026-09-09 16:28:32 KST
REPORT_COMPLETED_AT_KST: 2026-09-09 16:30:53 KST
DATA_CUTOFF_KST: 2026-09-09 16:30:53 KST
SOURCE_MANIFEST: 본문의 입력 검증 표 참조
RUN_TYPE: NORMAL
RERUN_SEQUENCE: 0
[/DMI_REVIEW_META]

[REVIEW_REPORT]
# DMI Two-Agent Review

## 1. 입력과 검증 상태

2026-09-09는 수요일이며, KRX 공식 자료는 주식시장이 월요일부터 금요일까지 열리고 정규장 거래시간이 09:00~15:30이라고 안내한다. KRX 공식 사이트의 대상일 휴장 공지를 검색했으나 2026-09-09 휴장 공지는 확인되지 않았다. 따라서 `SKIPPED_NON_TRADING_DAY`를 적용하지 않았다.

- KRX 거래 안내: https://global.krx.co.kr/contents/GLB/01/0109/0109000000/guide_to_trading_in_the_korean_stock_market.pdf
- KRX 공식 사이트: https://www.krx.co.kr/

| Agent | Slot | 확인 경로 | SHA / 최초 저장시각 | 상태 | 채택·제외 사유 |
|---|---:|---|---|---|---|
| AGENT_1 | 03:30 | `totjae/dmi-agent-1/runs/2026-09-09/0330.md` 및 날짜 경로 검색 | N/A | UNAVAILABLE | 기본 파일 404, 해당 날짜 경로 검색 결과 없음, 저장 commit 없음 |
| AGENT_2 | 03:30 | `totjae/dmi-agent-2/runs/2026-09-09/0330.md` 및 날짜 경로 검색 | N/A | UNAVAILABLE | 기본 파일 404, 해당 날짜 경로 검색 결과 없음, 저장 commit 없음 |
| AGENT_1 | 08:30 | `totjae/dmi-agent-1/runs/2026-09-09/0830.md` 및 날짜 경로 검색 | N/A | UNAVAILABLE | 기본 파일 404, 해당 날짜 경로 검색 결과 없음, 저장 commit 없음 |
| AGENT_2 | 08:30 | `totjae/dmi-agent-2/runs/2026-09-09/0830.md` 및 날짜 경로 검색 | N/A | UNAVAILABLE | 기본 파일 404, 해당 날짜 경로 검색 결과 없음, 저장 commit 없음 |

네 조합 모두 선택 가능한 결과가 없어 wrapper·날짜·슬롯·cutoff·본문/캡슐 일치 여부와 장전 최초 저장시각을 검증할 입력 자체가 없다. 다른 날짜 결과, 에이전트 프롬프트·WORKFLOW, legacy는 읽지 않았다.

## 2. 시장 Ground Truth

공식 입력 후보가 총 0개이므로 종목별 Previous Close, Open, High, Low, Close를 조회하거나 계산할 대상이 없다. 미확정 값을 추정하지 않았으며 모든 후보 성과 지표는 `N/A (n=0)`이다.

## 3. 후보별 실제 성과

- 03:30: AGENT_1 0개가 아니라 입력 부재, AGENT_2 0개가 아니라 입력 부재.
- 08:30: AGENT_1 0개가 아니라 입력 부재, AGENT_2 0개가 아니라 입력 부재.
- 후보 없음 결과로 해석하지 않았고, 누락을 0점 또는 실패로 집계하지 않았다.

## 4. 에이전트별 KPI

| Slot | Agent | 유효 입력 | 유효 후보 표본 | TOP1 FE/OFE | TOP3 평균 FE/OFE/AE | 전체 평균 FE/OFE/AE | FE3/FE5/FE10 | Rank-FE Spearman |
|---|---|---:|---:|---|---|---|---|---|
| 03:30 | AGENT_1 | 없음 | n=0 | N/A | N/A | N/A | N/A | N/A |
| 03:30 | AGENT_2 | 없음 | n=0 | N/A | N/A | N/A | N/A | N/A |
| 08:30 | AGENT_1 | 없음 | n=0 | N/A | N/A | N/A | N/A | N/A |
| 08:30 | AGENT_2 | 없음 | n=0 | N/A | N/A | N/A | N/A | N/A |

Expected Move, Confidence 보정 및 조건부 매매 성과도 평가 가능한 예측 필드가 없어 N/A이다.

## 5. 슬롯별 Agent 1 vs Agent 2

### 03:30

두 입력 모두 UNAVAILABLE이므로 성과 비교와 승자 선정이 불가능하다. 누락을 0점으로 치환하지 않았다.

### 08:30

두 입력 모두 UNAVAILABLE이므로 성과 비교와 승자 선정이 불가능하다. 03:30 결과로 대체하거나 오류 복구 실행으로 간주하지 않았다.

## 6. 같은 에이전트의 03:30 vs 08:30

AGENT_1과 AGENT_2 모두 두 슬롯 입력이 전부 없어 시간대 간 변화, 새 정보 반영 효과, 순위 변화 및 성과 차이를 평가할 수 없다. 슬롯 후보를 합치지 않았다.

## 7. 성공·오류 분석

발굴 성공이나 종목 판단 오류를 분석할 표본은 없다. 오늘 확인된 운영상 사실은 두 예약 슬롯과 두 에이전트에서 결과 파일이 생성되지 않았다는 점이다. 다만 이번 리뷰만으로 원인을 단정할 수 없으며, 누락을 에이전트 예측 실패로 해석하지 않는다.

## 8. 개선 후보

- 관찰 증거: 4개 필수 입력 모두 UNAVAILABLE.
- 후보: 예측 예약의 거래일 확인 및 저장 단계가 실제로 완료되는지 다음 실행에서 검증.
- 기대효과: 최소한의 공식 비교 표본 확보.
- 부작용/주의: 단일 누락일만으로 프롬프트나 활성 규칙을 자동 변경하면 원인 오판 가능성이 있다.
- 상태: 제안만 기록. 자동 활성화·문서 수정 없음.

## 9. 최종 요약

오늘은 거래일로 처리했으나 공식 예측 입력 4개가 모두 누락되어 KPI와 승자를 산출하지 않았다. 리뷰 자체는 입력 부재를 보존하는 정상 결과이며, 에이전트 프롬프트·결과·운영 문서와 예약은 변경하지 않았다.

[REVIEW_RESULT]
SCHEMA_VERSION: DMI_REVIEW_v1.1
DATE: 2026-09-09
PREDICTION_RUN_TIME_KST: 03:30
AGENT_1_STATUS: UNAVAILABLE
AGENT_2_STATUS: UNAVAILABLE
AGENT_1_COUNT: N/A
AGENT_2_COUNT: N/A
AGENT_1_TOP1_FE: N/A
AGENT_2_TOP1_FE: N/A
AGENT_1_TOP3_AVG_FE: N/A
AGENT_2_TOP3_AVG_FE: N/A
AGENT_1_FE3_HIT_RATE: N/A
AGENT_2_FE3_HIT_RATE: N/A
AGENT_1_FE5_HIT_RATE: N/A
AGENT_2_FE5_HIT_RATE: N/A
AGENT_1_RANK_FE_SPEARMAN: N/A
AGENT_2_RANK_FE_SPEARMAN: N/A
BEST_AGENT: N/A
BEST_PICK: N/A
PRIMARY_SUCCESS_PATTERN: N/A
PRIMARY_ERROR_PATTERN: BOTH_INPUTS_UNAVAILABLE
IMPROVEMENT_CANDIDATE: 예측 예약의 거래일 확인 및 저장 완료 여부 검증
[/REVIEW_RESULT]

[REVIEW_RESULT]
SCHEMA_VERSION: DMI_REVIEW_v1.1
DATE: 2026-09-09
PREDICTION_RUN_TIME_KST: 08:30
AGENT_1_STATUS: UNAVAILABLE
AGENT_2_STATUS: UNAVAILABLE
AGENT_1_COUNT: N/A
AGENT_2_COUNT: N/A
AGENT_1_TOP1_FE: N/A
AGENT_2_TOP1_FE: N/A
AGENT_1_TOP3_AVG_FE: N/A
AGENT_2_TOP3_AVG_FE: N/A
AGENT_1_FE3_HIT_RATE: N/A
AGENT_2_FE3_HIT_RATE: N/A
AGENT_1_FE5_HIT_RATE: N/A
AGENT_2_FE5_HIT_RATE: N/A
AGENT_1_RANK_FE_SPEARMAN: N/A
AGENT_2_RANK_FE_SPEARMAN: N/A
BEST_AGENT: N/A
BEST_PICK: N/A
PRIMARY_SUCCESS_PATTERN: N/A
PRIMARY_ERROR_PATTERN: BOTH_INPUTS_UNAVAILABLE
IMPROVEMENT_CANDIDATE: 예측 예약의 거래일 확인 및 저장 완료 여부 검증
[/REVIEW_RESULT]
[/REVIEW_REPORT]
