# DMI v8 Workflow

이 문서는 DMI v8 pipeline의 **운영 계약**이다.
분석 방법은 각 canonical prompt와 Playbook이 정의하며, 이 문서는 실행 순서·독립성·파일 선택·저장·검증 규칙만 정의한다.

## 1. Target
- Repository: `totjae/dmi-market-pipeline`
- Branch: `main`
- Timezone: `Asia/Seoul`
- Output root: `runs/YYYY-MM-DD/`
- Schema: `DMI_v8`

실행 날짜는 반드시 한국시간 기준 실행 당일 `YYYY-MM-DD`로 확정한다.

## 2. Objective
DMI v8의 목적은 KRX 정규장에서 **당일 단타 기회가 될 정도로 큰 상승 움직임이 발생할 가능성이 높은 종목을 개장 전에 찾는 것**이다.
단순 UP/DOWN 적중률보다 Big-Move 포착, FE와 실제 개장 후 기회(OFE)를 중요하게 평가한다.

## 3. Canonical documents
- Simple Prediction: `/prompt/v8_simple_prediction.md`
- Deep Prediction: `/prompt/v8_deep_prediction.md`
- Daily Review: `/prompt/v8_daily_review.md`
- Prediction-safe Playbook: `/DMI_PLAYBOOK_v8.md`
- Learning Ledger: `/DMI_LEARNING_v8.md`
- Output Template: `/templates/STAGE_OUTPUT_v8.md`

Prediction 자동화는 시간대별 복제 프롬프트를 사용하지 않는다.
03:30/08:30의 차이는 자동화가 지정하는 실행 시각과 그 시점까지 이용 가능한 정보뿐이다.
같은 유형(Simple 또는 Deep)은 동일 canonical prompt를 사용한다.

## 4. Stage map / normal paths
1. `03:30_SIMPLE`
   - Prompt: `/prompt/v8_simple_prediction.md`
   - Normal path: `runs/YYYY-MM-DD/v8_01_0330_simple.md`
2. `03:30_DEEP`
   - Prompt: `/prompt/v8_deep_prediction.md`
   - Normal path: `runs/YYYY-MM-DD/v8_02_0330_deep.md`
3. `08:30_SIMPLE`
   - Prompt: `/prompt/v8_simple_prediction.md`
   - Normal path: `runs/YYYY-MM-DD/v8_03_0830_simple.md`
4. `08:30_DEEP`
   - Prompt: `/prompt/v8_deep_prediction.md`
   - Normal path: `runs/YYYY-MM-DD/v8_04_0830_deep.md`
5. `16:30_REVIEW`
   - Prompt: `/prompt/v8_daily_review.md`
   - Normal path: `runs/YYYY-MM-DD/v8_05_1630_review.md`

## 5. Required read order — Prediction
Prediction은 **분석 단계**와 **저장 단계**를 분리한다.

### 분석 전
1. `/WORKFLOW_v8.md`
2. 해당 canonical Prediction prompt
3. `/DMI_PLAYBOOK_v8.md` 전체

`DMI_PLAYBOOK_v8.md`는 Prediction-safe 문서이므로 OBJECTIVE와 ACTIVE_RULES 및 rule governance만 포함한다.
Prediction은 `/DMI_LEARNING_v8.md`, 과거 Review 및 과거 run을 읽지 않는다.

### 저장 직전
4. `/templates/STAGE_OUTPUT_v8.md`

Stage Output은 분석 판단 문서가 아니라 저장 계약이므로 후보 생성·Rank·Score가 끝난 뒤 저장 단계에서 확인한다.

## 6. Prediction independence
네 Prediction stage는 서로 완전히 독립이다.

- 같은 날짜의 다른 Prediction run을 분석 전에 읽지 않는다.
- 08:30은 03:30 결과를 읽지 않는다.
- Simple은 Deep 결과를 읽지 않는다.
- Deep은 Simple 결과를 읽지 않는다.
- 다른 Prediction의 후보·섹터·Rank·Score·Confidence·시장방향을 힌트, seed, confirmation, tie-breaker로 사용하지 않는다.
- 과거 날짜의 Prediction run을 후보 생성·Rank·Score·시장판단의 직접 입력으로 사용하지 않는다.
- 과거 Prediction 후보를 오늘의 candidate seed로 사용하지 않는다.
- 과거 Review의 개별 종목 결과를 직접 읽지 않는다. 리뷰 기반 개선은 승인된 Playbook ACTIVE_RULES를 통해서만 Prediction에 전달된다.
- 다른 stage가 실패했거나 없더라도 현재 Prediction을 대신 재구성하지 않는다.

Prediction 독립성은 **후속 비교를 위한 실험 조건**이므로 편의를 위해 완화하지 않는다.

## 7. Required read order — Review
16:30 Review는 다음 순서로 수행한다.

### 분석 전
1. `/WORKFLOW_v8.md`
2. `/prompt/v8_daily_review.md`
3. `/DMI_PLAYBOOK_v8.md` 전체
4. 같은 날짜의 각 Prediction stage에 대해 §9 규칙으로 선택한 최신 유효 파일의 실제 `[STAGE_REPORT]`와 `[STAGE_HANDOFF]`
5. 그 후 Review prompt가 요구하는 KRX Ground Truth 조사

Ground Truth를 먼저 보고 오전 예측을 재구성하거나 선택하지 않는다.
Prediction stage가 없거나 유효 파일이 없으면 `PREVIOUS_STAGE_UNAVAILABLE`로 처리한다.

### 저장 직전
6. `/templates/STAGE_OUTPUT_v8.md`

## 8. Rerun naming
정상 파일이 이미 존재하면 덮어쓰거나 삭제하지 않는다.

Rerun path:
`<normal-stem>_rerun_XX.md`

- 첫 rerun: `_rerun_01`
- 두 번째: `_rerun_02`
- 이후 가장 큰 기존 sequence + 1
- sequence는 두 자리 zero-padding을 기본으로 하며 99를 초과하면 필요한 자릿수로 확장한다.

예:
- `v8_04_0830_deep.md`
- `v8_04_0830_deep_rerun_01.md`
- `v8_04_0830_deep_rerun_02.md`

Rerun은 이전 파일을 수정하는 것이 아니라 **새 독립 실행 파일**이다.

### Official rerun policy
`runs/YYYY-MM-DD/` 아래 저장되는 rerun은 모두 **공식 대체 실행**으로 간주한다.
테스트·프롬프트 실험·형식 검증 목적 실행은 official run 경로에 저장하지 않는다.
테스트 결과가 `runs/`에 들어오면 Review의 latest valid 선택을 오염시킬 수 있으므로 금지한다.

## 9. Valid run / latest valid selection
파일이 존재한다는 이유만으로 valid run으로 간주하지 않는다.

Prediction run의 최소 유효 조건:
- `[DMI_RUN_META]` 존재 및 닫힘
- `SCHEMA_VERSION: DMI_v8`
- 요청한 DATE와 STAGE_ID 일치
- `[STAGE_REPORT]` 존재 및 닫힘
- `[STAGE_HANDOFF]` 존재 및 닫힘
- REPORT 내부 `[HANDOFF]`와 STAGE_HANDOFF가 verbatim duplicate
- wrapper와 원본 prompt의 필수 출력 구조가 명백히 깨져 있지 않음

Review run의 최소 유효 조건:
- `[DMI_RUN_META]`, `[STAGE_REPORT]`, `[STAGE_REVIEW_CAPSULE]` 존재 및 닫힘
- SCHEMA_VERSION / DATE / STAGE_ID 일치
- REPORT 내부 `[REVIEW]`와 STAGE_REVIEW_CAPSULE이 verbatim duplicate

`INVALID_OUTPUT`인 파일은 latest valid 후보에서 제외한다.

### Latest valid 선택 알고리즘
같은 날짜·같은 stage에서:
1. normal 파일과 모든 rerun 파일을 식별한다.
2. 각 파일을 위 유효 조건으로 검증한다.
3. 유효 파일만 남긴다.
4. 유효 rerun이 하나 이상이면 가장 큰 rerun sequence의 파일을 사용한다.
5. 유효 rerun이 없고 normal이 유효하면 normal을 사용한다.
6. 유효 파일이 하나도 없으면 `PREVIOUS_STAGE_UNAVAILABLE`.

단순 파일 수정시간이나 목록 반환순서만으로 latest를 결정하지 않는다.

## 10. Stage Output / metadata
모든 결과는 `/templates/STAGE_OUTPUT_v8.md` envelope로 저장한다.
원본 prompt의 필드명, enum, 순서, HANDOFF/REVIEW 구조를 임의 변경하거나 축약하지 않는다.

`DMI_RUN_META`의:
- DATE
- STAGE_ID
- STAGE_TIME_KST
- MODEL_TYPE
- ANALYSIS_TIME_KST
- DATA_CUTOFF_KST
- RUN_TYPE
- RERUN_SEQUENCE
- PROMPT_PATH
- PROMPT_VERSION
- PROMPT_COMMIT

을 실제 실행 조건에 맞게 기록한다.

`DATA_CUTOFF_KST`는 분석 정보의 시간적 상한이다. 미래 정보를 사용하지 않는다.
`PROMPT_COMMIT`은 확인 가능하면 실제 실행 시 읽은 prompt를 식별하는 commit SHA를 기록하고, 확인할 수 없으면 `N/A`.

## 11. Write boundaries / immutability
Pipeline 실행 중에는:
- 해당 stage의 새 run 파일만 생성한다.
- 기존 정상 run과 rerun을 수정·삭제하지 않는다.
- 다른 stage의 run을 수정하지 않는다.
- canonical prompt, workflow, template, playbook을 수정하지 않는다.
- 기존 v7.1 파일과 과거 run을 수정·삭제하지 않는다.

Prompt/Workflow/Template/Playbook 변경은 **pipeline 실행과 분리된 명시적 maintenance 작업**에서만 수행한다.

### Prompt versioning
canonical prompt의 판단 로직, 필수 출력 필드, enum, Score rubric, 평가 목표 등 **실질적 동작이 변경되면 `PROMPT_VERSION`을 증가**시킨다.
문구 정리·오탈자 수정처럼 의미가 바뀌지 않는 변경은 version 증가 없이 commit SHA만 달라질 수 있다.

현재 v8 canonical prompt의 시작 버전은:
- Simple: `DMI_v8.0`
- Deep: `DMI_v8.0`
- Review: `DMI_v8.0`

장기 calibration에서는 `PROMPT_VERSION`과 `PROMPT_COMMIT`을 함께 보존한다.

## 12. Failure / partial output
분석 중 데이터 일부가 없다는 이유만으로 전체 run을 임의 실패시키지 않는다.
Prompt가 허용한 `N/A`, `UNVERIFIED`, `PREVIOUS_STAGE_UNAVAILABLE`, `NOT_COMPARABLE`을 사용한다.

다만 다음은 정상 완료로 간주하지 않는다.
- GitHub write 실패
- 필수 wrapper 누락/미종결
- 잘못된 DATE 또는 STAGE_ID
- Prediction HANDOFF verbatim 불일치
- Review capsule verbatim 불일치
- 원본 prompt의 핵심 출력 구조가 저장 과정에서 손실됨

저장되지 않은 분석을 저장 성공이라고 주장하지 않는다.

## 13. Save verification
GitHub write가 성공한 직후 저장 파일을 다시 읽는다.

검증:
1. 실제 repository path가 의도한 path와 일치
2. DMI_RUN_META의 DATE / STAGE_ID / MODEL_TYPE / RUN_TYPE / RERUN_SEQUENCE 일치
3. 필수 wrapper 존재 및 닫힘
4. Prediction은 REPORT 내부 HANDOFF와 STAGE_HANDOFF의 verbatim 일치
5. Review는 REPORT 내부 REVIEW와 STAGE_REVIEW_CAPSULE의 verbatim 일치

검증 실패 시 해당 파일을 정상 run으로 보고하지 않는다.
이미 생성된 잘못된 파일을 덮어쓰거나 삭제해 숨기지 않는다. 실패 사실과 실제 생성된 path를 보고하고, 필요하면 다음 rerun sequence로 새 실행한다.

## 14. Completion report
stage 완료 보고에는 최소한 다음을 포함한다.
- DATE
- STAGE_ID
- RUN_TYPE / RERUN_SEQUENCE
- 실제 저장 repository path
- save verification 결과

GitHub 저장과 재검증이 모두 성공한 경우에만 `SUCCESS`로 보고한다.

## 15. Review preservation
16:30 Review는 오전 Prediction을 평가할 뿐 수정하지 않는다.
Review가 생성한 `OBSERVATION`, `IMPROVEMENT_CANDIDATE`, `ACTIVE_RULE_CHANGE_PROPOSED`는 해당 Review 파일에만 저장한다.

Daily Review는 `DMI_PLAYBOOK_v8.md`와 `DMI_LEARNING_v8.md`를 직접 변경하지 않는다.

- Daily Review → 해당 날짜 Review run 안에 Observation / Improvement Candidate 기록
- Rolling Calibration / Rule Review maintenance → 여러 Review를 읽고 `DMI_LEARNING_v8.md`를 갱신
- 사용자 승인 → 승인된 Rule Proposal만 `DMI_PLAYBOOK_v8.md` ACTIVE_RULES에 반영

Prediction은 Learning Ledger를 읽지 않으므로 아직 승인되지 않은 가설이 당일 판단에 섞이지 않는다.
