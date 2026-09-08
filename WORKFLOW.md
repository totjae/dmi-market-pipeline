# DMI Review Workflow

## 역할

이 저장소는 예측을 생성하지 않는다. 두 독립 에이전트가 이미 저장한 결과를 장 마감 후 평가하고 비교한다.

## 실행 입력

1. `/config/SOURCES.md`를 읽어 두 입력 저장소를 확인한다.
2. `/prompt/REVIEW_PROMPT.md`를 읽는다.
3. 자동화가 지정한 `DATE`와 `PREDICTION_RUN_TIME_KST`를 확정한다.
4. 각 저장소에서 해당 날짜와 실행시각의 결과 파일만 읽는다.
5. KRX 정규장 Ground Truth를 조사해 리뷰를 완료한다.
6. `/templates/REVIEW_OUTPUT.md` 형식으로 저장한다.

`PREDICTION_RUN_TIME_KST`가 지정되지 않았다면 임의로 실행 결과를 고르지 않고 실패 이유를 보고한다.

## 입력 선택

기본 파일:
`runs/YYYY-MM-DD/HHMM.md`

rerun이 있으면 wrapper와 필수 필드가 정상인 파일 중 가장 높은 rerun 번호를 선택한다. 파일이 없거나 유효하지 않으면 해당 에이전트를 `UNAVAILABLE`로 기록하고 다른 에이전트의 결과를 복원하거나 추정하지 않는다.

리뷰는 에이전트 저장소에서 다음만 읽는다.
- 선택된 실행 결과 파일

읽지 않는 대상:
- 에이전트 프롬프트
- 에이전트 WORKFLOW
- 다른 날짜·다른 시각의 결과
- 현재 저장소의 `legacy/**`

## 쓰기 범위

리뷰는 `totjae/dmi-market-pipeline`에만 쓴다. 에이전트 저장소의 프롬프트·결과를 수정하지 않는다.

정상 경로:
`reviews/YYYY-MM-DD/review_HHMM.md`

기존 파일이 있으면 `review_HHMM_rerun_01.md`부터 번호를 증가시키며 덮어쓰지 않는다.

저장 후 metadata, report, result wrapper와 입력 경로, 후보 수, 계산값을 재검증한다. 실제 저장과 검증이 성공한 경우에만 `SUCCESS`로 보고한다.
