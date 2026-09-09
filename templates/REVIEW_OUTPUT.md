# Review Output Template

```text
[DMI_REVIEW_META]
SCHEMA_VERSION: DMI_REVIEW_v1.2
DATE:
PREDICTION_RUN_TIMES_KST: [03:30, 08:30]
REVIEW_TIME_KST: 16:30
STARTED_AT_KST:
REPORT_COMPLETED_AT_KST:
DATA_CUTOFF_KST:
SOURCE_MANIFEST: <본문의 4개 에이전트·슬롯별 경로/commit/최초 저장시각/채택 상태 표>
RUN_TYPE: NORMAL
RERUN_SEQUENCE: 0
[/DMI_REVIEW_META]

[REVIEW_REPORT]
# DMI Two-Agent Review

리뷰 프롬프트에 따른 전체 평가를 작성한다.

<아래 REVIEW_RESULT 블록을 요청된 슬롯마다 정확히 한 번씩 반복한다.>
[REVIEW_RESULT]
SCHEMA_VERSION: DMI_REVIEW_v1.2
DATE:
PREDICTION_RUN_TIME_KST:
AGENT_1_STATUS:
AGENT_2_STATUS:
AGENT_1_COUNT:
AGENT_2_COUNT:
AGENT_1_TOP1_FE:
AGENT_2_TOP1_FE:
AGENT_1_TOP3_AVG_FE:
AGENT_2_TOP3_AVG_FE:
AGENT_1_FE3_HIT_RATE:
AGENT_2_FE3_HIT_RATE:
AGENT_1_FE5_HIT_RATE:
AGENT_2_FE5_HIT_RATE:
AGENT_1_FE10_HIT_RATE:
AGENT_2_FE10_HIT_RATE:
AGENT_1_VALID_FE_COUNT:
AGENT_2_VALID_FE_COUNT:
AGENT_1_TOP3_VALID_FE_COUNT:
AGENT_2_TOP3_VALID_FE_COUNT:
AGENT_1_RANK_PERFORMANCE_SPEARMAN:
AGENT_2_RANK_PERFORMANCE_SPEARMAN:
AGENT_1_RANK_PERFORMANCE_PAIR_COUNT:
AGENT_2_RANK_PERFORMANCE_PAIR_COUNT:
BEST_AGENT:
BEST_PICK:
PRIMARY_SUCCESS_PATTERN:
PRIMARY_ERROR_PATTERN:
IMPROVEMENT_CANDIDATE:
[/REVIEW_RESULT]
[/REVIEW_REPORT]
```

비교가 불가능하면 해당 값과 BEST_AGENT를 `N/A`로 둔다. 본문에 없는 판단을 result에 새로 추가하지 않는다.

일일 리뷰는 PREDICTION_RUN_TIME_KST=03:30, 08:30인 REVIEW_RESULT 블록 두 개를 둔다. 없는 입력도 상태와 N/A를 기록하여 블록을 생략하지 않는다. 각 필드는 해당 슬롯에만 속한다. 시간대 간 비교는 본문의 별도 절로 작성한다. 단일 슬롯 리뷰는 메타 목록에 그 슬롯만 쓰고 결과 블록도 하나만 둔다. DATA_CUTOFF_KST는 리뷰에 사용한 시장자료의 확인 기준시각이며 예측 cutoff와 혼동하지 않는다.

## KPI 필드 규칙

- 계산 기준은 /prompt/REVIEW_PROMPT.md의 계산·집계 규칙을 따른다. 본문 KPI 표에는 FE·OFE·AE 등 각 지표의 유효 수 / 원래 대상 수와 N/A 사유를 적는다.
- AGENT_n_COUNT는 입력의 원래 TOP_COUNT이다. 유효한 후보 0개 입력은 0, 입력 없음·무효는 N/A이다.
- VALID_FE_COUNT는 전체 TOP 중 FE가 유효한 수, TOP3_VALID_FE_COUNT는 원래 상위 min(3, COUNT) 안에서 FE가 유효한 수이다. 유효 입력에 가격 자료가 전혀 없으면 두 수는 0이고 성과 값은 N/A이다. 입력 자체가 없거나 무효이면 두 수도 N/A이다.
- FE3·FE5·FE10 적중률은 같은 VALID_FE_COUNT를 분모로 사용하며 경계값을 포함한다. 분모 0은 N/A이다. 백분율에는 %를 붙인다.
- RANK_PERFORMANCE_SPEARMAN은 예측 순위와 실제 FE 내림차순 순위의 상관이다. +1이 좋은 정렬이며 단위는 없다. PAIR_COUNT는 계산에 사용할 수 있는 유효 쌍 수다. n < 2 또는 순위 분산 0이면 상관은 N/A이고 사유는 본문에 남긴다.
- v1.2는 방향이 모호한 기존 RANK_FE_SPEARMAN 필드를 위 명시적 필드로 교체한다. 과거 결과를 재해석하거나 수정하지 않는다.
- 지표별 우열이 엇갈리거나 종합 우열을 정할 기준이 없으면 BEST_AGENT=MIXED, 비교 불가능이면 N/A이다.
