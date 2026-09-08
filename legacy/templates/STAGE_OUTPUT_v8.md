# DMI v8 Stage Output Template

이 템플릿은 DMI v8 모든 stage의 **저장 envelope**다.

원본 Prediction/Review 프롬프트가 생성한 전체 보고서를 요약하거나 재작성하지 않는다.
각 stage의 원본 출력 스키마를 아래 wrapper 안에 그대로 보존한다.

## 1. Required Run Metadata

모든 저장 파일은 다음 메타데이터를 정확히 기록한다.

```text
[DMI_RUN_META]
SCHEMA_VERSION: DMI_v8
DATE: YYYY-MM-DD
STAGE_ID: <03:30_SIMPLE / 03:30_DEEP / 08:30_SIMPLE / 08:30_DEEP / 16:30_REVIEW>
STAGE_TIME_KST: HH:MM
MODEL_TYPE: <SIMPLE / DEEP / REVIEW>
ANALYSIS_TIME_KST: YYYY-MM-DD HH:MM:SS
DATA_CUTOFF_KST: <확인 가능한 최신 시장 데이터 기준시각 또는 N/A>
RUN_TYPE: <NORMAL / RERUN>
RERUN_SEQUENCE: <0 / 1 / 2 / ...>
PROMPT_PATH: <실제로 사용한 canonical prompt path>
PROMPT_VERSION: <prompt 내부 명시 버전 또는 DMI_v8>
PROMPT_COMMIT: <실행 시 읽은 prompt의 Git commit SHA, 확인 불가 시 N/A>
WORKFLOW_PATH: /WORKFLOW_v8.md
PLAYBOOK_PATH: /DMI_PLAYBOOK_v8.md
[/DMI_RUN_META]
```

### STAGE_ID 고정값
- `03:30_SIMPLE`
- `03:30_DEEP`
- `08:30_SIMPLE`
- `08:30_DEEP`
- `16:30_REVIEW`

### MODEL_TYPE 고정값
- Simple Prediction → `SIMPLE`
- Deep Prediction → `DEEP`
- Daily Review → `REVIEW`

### Prompt identity
- `PROMPT_PATH`
  - Simple → `/prompt/v8_simple_prediction.md`
  - Deep → `/prompt/v8_deep_prediction.md`
  - Review → `/prompt/v8_daily_review.md`
- `PROMPT_VERSION`은 prompt가 명시한 버전을 기록한다. 현재 canonical v8 prompt의 시작 버전은 `DMI_v8.0`.
- `PROMPT_COMMIT`은 가능하면 실행 시점에 실제 읽은 prompt를 식별하는 Git commit SHA를 기록한다. 확인할 수 없으면 `N/A`.
- 같은 path의 prompt가 이후 수정될 수 있으므로 재현성 판단에서 path만으로 동일 prompt라고 간주하지 않는다.

### DATA_CUTOFF_KST
분석에 사용한 정보의 **시간적 상한**을 기록한다. 이 시각 이후 공개·확인된 정보는 해당 run의 판단에 사용하지 않는다.
여러 데이터 소스의 개별 timestamp를 하나로 뭉뚱그린 "최신 데이터 시각"이라는 의미로 사용하지 않는다.

정상 실행은:
- `RUN_TYPE: NORMAL`
- `RERUN_SEQUENCE: 0`

첫 번째 재실행은:
- `RUN_TYPE: RERUN`
- `RERUN_SEQUENCE: 1`

형식으로 기록한다.

## 2. Prediction Stage Envelope

03:30 Simple / 03:30 Deep / 08:30 Simple / 08:30 Deep은 반드시 다음 형식을 사용한다.

```text
[DMI_RUN_META]
<Required Run Metadata>
[/DMI_RUN_META]

[STAGE_REPORT]
<해당 canonical Prediction prompt가 요구하는 전체 원본 보고서>
[/STAGE_REPORT]

[STAGE_HANDOFF]
<해당 Prediction prompt가 생성한 원본 [HANDOFF] capsule>
[/STAGE_HANDOFF]
```

### Prediction 저장 규칙
- `[STAGE_REPORT]`에는 전체 분석 결과를 보존한다.
- TOP 후보, 상세 논리, 위험·회피 후보, Score Audit, Scenario 등 원본 prompt가 요구한 내용을 임의로 생략하지 않는다.
- `[STAGE_HANDOFF]`는 `[STAGE_REPORT]` 내부에서 생성된 원본 `[HANDOFF]...[/HANDOFF]`의 **verbatim duplicate**다.
- HANDOFF를 새로 요약·재계산·정규화하지 않는다.
- Prediction의 판단 원본은 `[STAGE_REPORT]`이며, `[STAGE_HANDOFF]`는 후속 기계적 읽기를 위한 복제 capsule이다.
- REPORT 내부 HANDOFF와 `[STAGE_HANDOFF]`가 문자 그대로 일치하지 않으면 해당 run은 `INVALID_OUTPUT`으로 취급하고 정상 run으로 사용하지 않는다.

## 3. Review Stage Envelope

16:30 Review는 반드시 다음 형식을 사용한다.

```text
[DMI_RUN_META]
<Required Run Metadata>
[/DMI_RUN_META]

[STAGE_REPORT]
<Review prompt가 요구하는 전체 원본 Review 보고서>
[/STAGE_REPORT]

[STAGE_REVIEW_CAPSULE]
<Review 보고서에서 생성한 원본 [REVIEW] capsule>
[/STAGE_REVIEW_CAPSULE]
```

Review stage에는 Prediction용 `[STAGE_HANDOFF]`를 만들지 않는다.
Review prompt가 향후 별도 HANDOFF를 정의하지 않는 한 `[STAGE_REVIEW_CAPSULE]`만 사용한다.

### Review 저장 규칙
- 오전 Prediction의 후보, Rank, 이유, Score, Expected Move를 결과를 보고 재구성하지 않는다.
- 같은 날짜의 실제 저장된 Prediction REPORT/HANDOFF만 원본으로 사용한다.
- 없는 stage나 필수 구간은 `PREVIOUS_STAGE_UNAVAILABLE`로 남긴다.
- `[STAGE_REVIEW_CAPSULE]`는 `[STAGE_REPORT]` 내부에서 생성된 원본 `[REVIEW]...[/REVIEW]`의 **verbatim duplicate**다.
- Review의 판단 원본은 `[STAGE_REPORT]`이며, `[STAGE_REVIEW_CAPSULE]`은 장기 누적·후속 읽기를 위한 복제 capsule이다.
- REPORT 내부 REVIEW와 `[STAGE_REVIEW_CAPSULE]`이 문자 그대로 일치하지 않으면 해당 run은 `INVALID_OUTPUT`으로 취급한다.

## 4. Preservation Rules

다음은 모든 stage에 공통 적용한다.

1. 원본 prompt의 필드명, enum, 순서, 표 구조를 임의 변경하지 않는다.
2. 원본 보고서를 요약본으로 대체하지 않는다.
3. 확인할 수 없는 값은 prompt 규칙에 따라 `N/A`, `UNVERIFIED`, `PREVIOUS_STAGE_UNAVAILABLE` 등을 사용한다.
4. 과거 성공 run을 덮어쓰거나 삭제하지 않는다.
5. 저장 경로와 rerun 규칙은 `/WORKFLOW_v8.md`를 따른다.
6. GitHub write가 실제 성공한 경우에만 저장 성공으로 간주한다.
7. 저장 후 파일을 다시 읽어 다음을 검증한다.
   - `[DMI_RUN_META]`
   - `[STAGE_REPORT]`
   - Prediction이면 `[STAGE_HANDOFF]`
   - Review이면 `[STAGE_REVIEW_CAPSULE]`
8. wrapper가 닫히지 않았거나 필수 구간이 빠졌으면 정상 완료로 간주하지 않는다.

## 5. Complete Prediction Example Skeleton

```text
[DMI_RUN_META]
SCHEMA_VERSION: DMI_v8
DATE: 2026-09-04
STAGE_ID: 08:30_DEEP
STAGE_TIME_KST: 08:30
MODEL_TYPE: DEEP
ANALYSIS_TIME_KST: 2026-09-04 08:31:12
DATA_CUTOFF_KST: 2026-09-04 08:29 KST
RUN_TYPE: NORMAL
RERUN_SEQUENCE: 0
PROMPT_PATH: /prompt/v8_deep_prediction.md
PROMPT_VERSION: DMI_v8.0
PROMPT_COMMIT: <commit SHA or N/A>
WORKFLOW_PATH: /WORKFLOW_v8.md
PLAYBOOK_PATH: /DMI_PLAYBOOK_v8.md
[/DMI_RUN_META]

[STAGE_REPORT]
<complete original Deep report>
[/STAGE_REPORT]

[STAGE_HANDOFF]
[HANDOFF]
<complete original Deep HANDOFF>
[/HANDOFF]
[/STAGE_HANDOFF]
```

## 6. Complete Review Example Skeleton

```text
[DMI_RUN_META]
SCHEMA_VERSION: DMI_v8
DATE: 2026-09-04
STAGE_ID: 16:30_REVIEW
STAGE_TIME_KST: 16:30
MODEL_TYPE: REVIEW
ANALYSIS_TIME_KST: 2026-09-04 16:31:08
DATA_CUTOFF_KST: 2026-09-04 16:29 KST
RUN_TYPE: NORMAL
RERUN_SEQUENCE: 0
PROMPT_PATH: /prompt/v8_daily_review.md
PROMPT_VERSION: DMI_v8.0
PROMPT_COMMIT: <commit SHA or N/A>
WORKFLOW_PATH: /WORKFLOW_v8.md
PLAYBOOK_PATH: /DMI_PLAYBOOK_v8.md
[/DMI_RUN_META]

[STAGE_REPORT]
<complete original Review report including its [REVIEW] capsule>
[/STAGE_REPORT]

[STAGE_REVIEW_CAPSULE]
[REVIEW]
<same original REVIEW capsule>
[/REVIEW]
[/STAGE_REVIEW_CAPSULE]
```

출력 파일 경로는 `/WORKFLOW_v8.md`가 결정한다.
