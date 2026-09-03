# DMI v8 Workflow

## 1. Objective
DMI v8의 목적은 KRX 정규장에서 **당일 단타 기회가 될 정도로 큰 상승 움직임이 발생할 가능성이 높은 종목을 개장 전에 찾는 것**이다.
단순 UP/DOWN 적중률보다 상승폭, 장중 최대 상승폭(FE), 큰 상승 종목 포착률을 우선한다.

## 2. Stages
1. 03:30 Simple — 독립 자유판단 baseline
2. 03:30 Deep — 독립 심화분석
3. 08:30 Simple — 독립 자유판단 final baseline
4. 08:30 Deep — 독립 심화분석 final
5. 16:30 Review — 네 예측을 실제 KRX 결과와 비교

## 3. Independence
- 네 Prediction stage는 서로의 당일 결과를 읽지 않는다.
- 08:30 stage도 03:30 결과를 읽지 않는다.
- 후보 생성, Rank, 판단, Score에 다른 prediction stage 결과를 사용하지 않는다.
- Prediction stage는 DMI_PLAYBOOK_v8.md의 OBJECTIVE와 ACTIVE_RULES만 판단 규칙으로 사용한다.
- OBSERVATIONS, IMPROVEMENT_CANDIDATES, 과거 Review는 prediction 판단의 직접 입력으로 사용하지 않는다.
- 16:30 Review만 같은 날짜의 네 prediction 결과와 과거 review/PLAYBOOK 개선영역을 읽을 수 있다.

## 4. Source priority
공식 거래소·정부·규제기관 > 기업 공시·IR > 주요 통신사·경제매체 > 증권사·산업 전문매체.
확인 불가 데이터는 N/A. 실시간성이 중요한 값은 기준시각을 기록한다.
FACT / INTERPRETATION / FORECAST를 구분한다.

## 5. Output paths
- runs/YYYY-MM-DD/v8_01_0330_simple.md
- runs/YYYY-MM-DD/v8_02_0330_deep.md
- runs/YYYY-MM-DD/v8_03_0830_simple.md
- runs/YYYY-MM-DD/v8_04_0830_deep.md
- runs/YYYY-MM-DD/v8_05_1630_review.md

정상 파일이 이미 있으면 덮어쓰지 않는다.
rerun은 원 파일명 뒤에 _rerun_01, _rerun_02 순으로 생성한다.

## 6. Immutability
기존 v7.1 파일, 과거 run, prompt, template은 수정·삭제하지 않는다.
v8 prediction 결과도 Review 단계에서 수정하지 않는다.

## 7. Save verification
GitHub write가 실제 성공한 경우에만 저장 성공으로 간주한다.
저장 후 해당 파일을 다시 읽어 필수 섹션 존재 여부를 검증한다.
