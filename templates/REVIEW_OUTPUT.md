# Review Output Template

```text
[DMI_REVIEW_META]
SCHEMA_VERSION: DMI_REVIEW_v1.3
DATE:
PREDICTION_RUN_TIMES_KST: [03:30, 08:30]
REVIEW_TIME_KST: 16:30
STARTED_AT_KST:
REPORT_COMPLETED_AT_KST:
DATA_CUTOFF_KST:
SOURCE_MANIFEST: REVIEW_EVIDENCE.input_manifest
REVIEW_DOCUMENT_VERSIONS: REVIEW_EVIDENCE.review_document_versions
RUN_TYPE: NORMAL
RERUN_SEQUENCE: 0
[/DMI_REVIEW_META]

[REVIEW_REPORT]
# DMI Two-Agent Review

리뷰 프롬프트에 따른 전체 평가를 작성한다.

<아래 REVIEW_RESULT 블록을 요청된 슬롯마다 정확히 한 번씩 반복한다.>
[REVIEW_RESULT]
SCHEMA_VERSION: DMI_REVIEW_v1.3
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

- AGENT_n_STATUS는 공식 채택이면 OFFICIAL, 개장시각과 같거나 이후 저장이면 LATE, 저장시각·개장시각 검증 불가이면 TIMING_UNVERIFIED, 입력 없음·무효이면 UNAVAILABLE이다. manifest의 REFERENCE_ONLY는 LATE 또는 TIMING_UNVERIFIED와 대응하며 상세 원인은 selection_reason에 기록한다.
- LATE·TIMING_UNVERIFIED 그룹의 공식 성과 KPI와 공식 유효 표본 수는 모두 N/A이다. 구조가 유효하면 원래 COUNT만 보존할 수 있다. 참고 후보 관찰값을 공식 표본 수에 더하지 않는다.

- 계산 기준은 /prompt/REVIEW_PROMPT.md의 계산·집계 규칙을 따른다. 본문 KPI 표에는 FE·OFE·AE 등 각 지표의 유효 수 / 원래 대상 수와 N/A 사유를 적는다.
- AGENT_n_COUNT는 입력의 원래 TOP_COUNT이다. 유효한 후보 0개 입력은 0, 입력 없음·무효는 N/A이다.
- VALID_FE_COUNT는 전체 TOP 중 FE가 유효한 수, TOP3_VALID_FE_COUNT는 원래 상위 min(3, COUNT) 안에서 FE가 유효한 수이다. 유효 입력에 가격 자료가 전혀 없으면 두 수는 0이고 성과 값은 N/A이다. 입력 자체가 없거나 무효이면 두 수도 N/A이다.
- FE3·FE5·FE10 적중률은 같은 VALID_FE_COUNT를 분모로 사용하며 경계값을 포함한다. 분모 0은 N/A이다. 백분율에는 %를 붙인다.
- RANK_PERFORMANCE_SPEARMAN은 예측 순위와 실제 FE 내림차순 순위의 상관이다. +1이 좋은 정렬이며 단위는 없다. PAIR_COUNT는 계산에 사용할 수 있는 유효 쌍 수다. n < 2 또는 순위 분산 0이면 상관은 N/A이고 사유는 본문에 남긴다.
- v1.2는 방향이 모호한 기존 RANK_FE_SPEARMAN 필드를 위 명시적 필드로 교체한다. 과거 결과를 재해석하거나 수정하지 않는다.
- 지표별 우열이 엇갈리거나 종합 우열을 정할 기준이 없으면 BEST_AGENT=MIXED, 비교 불가능이면 N/A이다.

## 후보별 증거 기록

슬롯별 REVIEW_RESULT와 별도로, [/REVIEW_REPORT] 뒤, 보고서 끝에 [REVIEW_EVIDENCE] ... [/REVIEW_EVIDENCE] 블록을 정확히 한 번 추가한다. 내부는 아래 구조의 유효한 JSON으로 작성한다. 이 블록은 본문에 사용한 원자료와 계산값을 보존한다. 기존 리뷰 파일은 변경하지 않는다.

```json
{
  "schema_version": "DMI_REVIEW_EVIDENCE_v1",
  "review_document_versions": [],
  "input_manifest": [],
  "price_sources": [],
  "candidates": []
}
```

### 문서와 입력

- review_document_versions: 실제 읽은 리뷰 WORKFLOW, SOURCES, REVIEW_PROMPT, REVIEW_OUTPUT 각각에 대해 role, repository, path, commit_sha, blob_sha, read_at_kst, status, reason을 기록한다. blob SHA가 실제 읽은 내용과 연결되면 VERIFIED, 그렇지 않으면 UNVERIFIED이다. 확인할 수 없는 값은 null이다.
- input_manifest: 요청된 에이전트·슬롯마다 하나씩 기록한다. 필드: input_id, agent_id, date, slot_kst, repository, path, evaluated_commit_sha, evaluated_blob_sha, first_saved_commit_sha, first_saved_at_kst, selection_status, selection_reason, prediction_schema_version, prediction_document_versions, version_status.
- input_id는 이 리뷰 안에서 유일한 문자열이다. selection_status는 OFFICIAL, REFERENCE_ONLY, UNAVAILABLE 중 하나이며, selection_reason에 LATE, TIMING_UNVERIFIED, MISSING_FILE 등 실제 원인을 남긴다. OFFICIAL은 WORKFLOW의 유효성·장전 채택 검증을 통과한 경우에만 사용한다.
- evaluated_*는 실제 평가한 revision, first_saved_*는 파일 최초 생성 이력이다. 두 시점을 혼동하지 않는다. 선택하지 않은 다른 경로의 제외 근거는 기존 규칙에 따라 본문에 남긴다.
- prediction_document_versions는 입력의 DOCUMENT_VERSIONS를 그대로 보존한다. 없으면 빈 배열과 version_status=NOT_PROVIDED로 기록한다. 모두 실제 SHA를 확인한 기록이면 VERIFIED, 일부라도 미확인이면 UNVERIFIED이다. 리뷰가 에이전트 지침을 열어 새로 채우지 않는다.
- 누락 입력도 manifest는 남기고 알 수 없는 필드는 null로 둔다. 관련 candidates는 빈 집합이다. 버전 누락만으로 정상 후보 성과를 폐기하지 않는다.

### 가격 출처

price_sources의 각 객체는 source_id, provider, url, retrieved_at_kst, observation_date, venue, session, currency, adjustment_basis, status, reason을 가진다. source_id는 블록 안에서 유일하다. venue=KRX, session=REGULAR, currency=KRW를 실제 자료와 대조한다. adjustment_basis에는 원주가·수정주가와 기업행사 처리 기준을 명시한다. 확인 불가이면 null과 사유를 기록한다. 다른 시점·기준의 출처는 별도 객체로 남긴다.

### 후보별 결과

candidates의 각 객체는 다음 필드를 가진다.

- input_id, rank, code, name, market: 원래 입력과 연결한다. code는 앞자리 0을 보존하는 문자열이다. 각 input_id·rank 조합은 정확히 하나이며 후보 수는 유효 입력의 TOP_COUNT와 일치한다.
- evaluation_scope: OFFICIAL 또는 REFERENCE_ONLY. manifest와 일치한다.
- prices: previous_close, open, high, low, close 각각을 {"value": 숫자 또는 null, "source_ids": ["출처 ID"]} 구조로 기록한다. previous_close의 관측일은 해당 출처에 따로 기록한다.
- metrics_pct: c2c, o2c, fe, ofe, ae의 숫자 또는 null. 예를 들어 3.5는 3.5%이며 0.035가 아니다. 이미 검증한 가격으로 계산한 반올림 전 값을 가능한 정밀도로 보존하고 본문 표시만 반올림한다.
- hits: fe3, fe5, fe10 각각 true, false 또는 null. 실제 FE 미확인일 때 false로 쓰지 않는다.
- expected_fe_range_match: true, false 또는 null. 명시적 예상 구간과 실제 FE가 모두 유효할 때만 boolean이다.
- trade_plan: {"status": "NOT_PROVIDED / NOT_SCORABLE / NOT_TRIGGERED / SCORABLE 중 하나", "report_reference": "원문 절 위치 또는 null", "reason": "평가 근거", "evidence_urls": []}. SCORABLE이면 본문에 확인된 조건 발생 순서와 계획 평가 결과를 적고 그 절을 참조한다. NOT_TRIGGERED는 유효기간 동안 진입 조건 미충족을 자료로 확인했을 때만 사용한다.
- missing_reasons: {"field": "prices.open 등 필드 경로", "status": "NOT_PROVIDED / UNVERIFIED / NOT_APPLICABLE / UNCERTAIN 중 하나", "reason": "구체적 사유"} 객체 배열이다. 모든 null 성과 값의 사유를 남긴다. 누락이 없으면 빈 배열이다.

리뷰가 새로 작성하는 JSON의 결측값은 null, 기존 텍스트 KPI 필드의 결측값은 N/A이다. 단, prediction_document_versions는 원본을 그대로 보존하므로 원본 내부의 문자열 N/A도 그대로 유지한다. JSON에 NaN, Infinity, 주석, 자리표시자 문구를 남기지 않는다. 구조화 기록을 채우려고 미제공 예측을 계산하거나 가격·출처·SHA를 추정하지 않는다.

### 저장 전 대조

JSON 문법, input_id·source_id의 유일성과 참조 연결, 후보 수·원래 순위, 가격별 출처, 성과 단위, 결측 사유를 확인한다. 후보별 값으로 계산한 공식 집계가 각 슬롯 REVIEW_RESULT의 KPI와 유효 표본 수에 일치해야 한다. REFERENCE_ONLY는 공식 집계에서 제외한다. 입력 버전 정보와 실제 평가 revision을 서로 대체하지 않는다.
