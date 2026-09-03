# DMI v8 Workflow

## 1. Objective
DMI v8의 목적은 KRX 정규장에서 **당일 단타 기회가 될 정도로 큰 상승 움직임이 발생할 가능성이 높은 종목을 개장 전에 찾는 것**이다.
단순 UP/DOWN 적중률보다 상승폭, 장중 최대 상승폭(FE), 큰 상승 종목 포착률을 우선한다.

## 2. Canonical documents
Prediction 자동화는 시간대별 복제 프롬프트를 사용하지 않는다.

- Simple Prediction: `/prompt/v8_simple_prediction.md`
- Deep Prediction: `/prompt/v8_deep_prediction.md`
- Daily Review: `/prompt/v8_daily_review.md`
- Common Playbook: `/DMI_PLAYBOOK_v8.md`
- Output Template: `/templates/STAGE_OUTPUT_v8.md`

03:30/08:30의 차이는 자동화가 지정하는 실행 시각뿐이다. 같은 유형(Simple 또는 Deep)은 동일한 canonical prompt를 읽는다.

## 3. Stages
1. 03:30 Simple — `v8_simple_prediction.md`
2. 03:30 Deep — `v8_deep_prediction.md`
3. 08:30 Simple — `v8_simple_prediction.md`
4. 08:30 Deep — `v8_deep_prediction.md`
5. 16:30 Review — `v8_daily_review.md`

## 4. Independence
- 네 Prediction stage는 서로의 당일 결과를 읽지 않는다.
- 08:30 stage도 03:30 결과를 읽지 않는다.
- Simple과 Deep도 서로의 결과를 읽지 않는다.
- 후보 생성, Rank, 판단, Score에 다른 Prediction 결과를 사용하지 않는다.
- Prediction stage는 `DMI_PLAYBOOK_v8.md`에서 Prediction에 허용된 OBJECTIVE와 ACTIVE_RULES만 판단 규칙으로 사용한다.
- OBSERVATIONS, IMPROVEMENT_CANDIDATES 및 과거 Review의 개별 예측 결과는 당일 후보 생성의 직접 입력으로 사용하지 않는다.
- 16:30 Review만 같은 날짜의 네 Prediction 결과를 비교 목적으로 읽을 수 있다.

## 5. Source and data integrity
공식 거래소·정부·규제기관 > 기업 공시·IR > 주요 통신사·경제매체 > 증권사·산업 전문매체 순으로 우선한다.
확인 불가 데이터는 N/A 또는 UNVERIFIED로 처리한다.
실시간성이 중요한 값은 가능한 경우 기준시각을 기록한다.
확인되지 않은 가격·수급·체결 정보를 생성하지 않는다.

## 6. Output paths
- runs/YYYY-MM-DD/v8_01_0330_simple.md
- runs/YYYY-MM-DD/v8_02_0330_deep.md
- runs/YYYY-MM-DD/v8_03_0830_simple.md
- runs/YYYY-MM-DD/v8_04_0830_deep.md
- runs/YYYY-MM-DD/v8_05_1630_review.md

## 7. Rerun
정상 파일이 이미 있으면 덮어쓰거나 삭제하지 않는다.
rerun은 원 파일명 뒤에 `_rerun_01`, `_rerun_02` 순으로 생성한다.
Review는 해당 날짜의 정상 파일 또는 최신 유효 rerun을 명시적으로 식별해 사용한다.

## 8. Immutability
- 기존 v7.1 파일과 과거 run은 수정·삭제하지 않는다.
- 실행 중 canonical prompt, workflow, template, playbook을 임의 수정하지 않는다.
- Prediction 결과를 이후 Prediction 또는 Review가 수정하지 않는다.

## 9. Stage output
모든 실행 결과는 `/templates/STAGE_OUTPUT_v8.md` envelope로 감싼다.
원본 prompt가 요구하는 필드명, enum, 순서 및 HANDOFF/REVIEW 형식을 임의 변경하거나 축약하지 않는다.

## 10. Previous stage unavailable
Review에서 필요한 Prediction 파일 또는 필수 구간이 없으면 `PREVIOUS_STAGE_UNAVAILABLE`로 처리한다.
현재 시장 결과를 이용해 과거 후보, Rank, Score, Confidence 또는 판단을 역산·재구성하지 않는다.

## 11. Save verification
GitHub write가 실제 성공한 경우에만 저장 성공으로 간주한다.
저장 후 해당 파일을 다시 읽어 필수 envelope와 HANDOFF/REVIEW 구간 존재 여부를 검증한다.
저장할 수 없으면 저장했다고 주장하지 않고 실제 실패 이유를 보고한다.
