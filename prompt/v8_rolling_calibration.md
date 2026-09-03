# DMI v8 — Rolling Calibration / Rule Review

PROMPT_VERSION: DMI_v8.1

이 작업은 Daily Prediction pipeline의 stage가 아니라 **maintenance 작업**이다.

## 0. 연결 문서
실행 전에 다음을 읽는다.

1. `/WORKFLOW_v8.md`
2. `/DMI_PLAYBOOK_v8.md`
3. `/DMI_LEARNING_v8.md`
4. 분석 대상 기간의 유효한 `16:30_REVIEW` 결과

Prediction run을 직접 다시 평가하지 않는다.
기본 입력은 Daily Review의 실제 저장된 `[STAGE_REVIEW_CAPSULE]` 및 필요한 경우 해당 `[STAGE_REPORT]`다.

## 1. 목적
여러 거래일 Review를 종합하여 다음을 수행한다.

- 반복되는 성공·실패 패턴 탐지
- Simple vs Deep의 원지표 비교
- 03:30 vs 08:30 정보가치 비교
- Deep C/I/D/L/E/R/Q calibration
- Expected Move / Confidence / Rank calibration
- AVOID와 Learnable Missed Big Moves 반복 패턴 분석
- 기존 Observation 갱신
- Improvement Candidate 생성·갱신
- 충분한 근거가 있는 Rule Proposal 생성

**ACTIVE_RULE을 직접 수정하지 않는다.**

## 2. Evidence Window
요청받은 창 또는 이용 가능한 창을 사용한다.

기본:
- 5거래일 — anomaly scan
- 20거래일 — primary calibration
- 60거래일 — robustness / regime dependency

가능한 Review가 요청 창보다 적으면 실제 사용한 거래일 수를 기록하고 과도한 결론을 내리지 않는다.

`WINDOW = 5D / 20D / 60D / CUSTOM`

## 3. 입력 Review 선택
각 날짜에서 `WORKFLOW_v8.md`의 latest valid 규칙에 따라 16:30 Review를 선택한다.

유효 Review의 최소 조건:
- DMI_v8 schema
- 올바른 DATE / STAGE_ID
- STAGE_REPORT 존재
- STAGE_REVIEW_CAPSULE 존재
- REPORT 내부 REVIEW와 capsule이 verbatim duplicate

유효하지 않은 날짜는 제외하고 이유를 기록한다.

## 4. Version Segmentation
서로 다른 Prediction prompt version이 섞이면 그대로 하나의 동일 모델처럼 취급하지 않는다.

Review capsule에 저장된 provenance를 authoritative source로 사용해 다음 기준으로 세분화한다.
- 03:30 Simple PROMPT_VERSION
- 03:30 Deep PROMPT_VERSION
- 08:30 Simple PROMPT_VERSION
- 08:30 Deep PROMPT_VERSION
- Review PROMPT_VERSION
- PLAYBOOK_VERSION

각 Prediction version은 Review capsule의 `SOURCE_*_PROMPT_VERSION`을 사용한다.
필요하면 `SOURCE_*_PROMPT_COMMIT`과 `SOURCE_*_RUN_PATH`로 세부 provenance를 확인한다.
과거 날짜의 버전을 현재 canonical prompt 상태로 역추정하지 않는다.

동일 window 안에 실질적 prompt version 변경이 있으면:
- VERSION_MIXED: YES
- 구간별 결과를 분리해 설명
- 변경 전후를 단순 합산해 규칙 결론을 내리지 않는다.

PROMPT_COMMIT만 달라지고 PROMPT_VERSION이 같으면 의미 변경 여부를 Learning Changelog 또는 maintenance 기록으로 확인한다.

필수 provenance가 없는 구형 Review는 해당 version-segment 분석에서 `PROVENANCE_UNAVAILABLE`로 표시한다.
그 날짜의 성과지표 자체를 버리지는 않되, 서로 다른 버전을 동일 버전이라고 가정해 합치지 않는다.

## 5. 핵심 집계 원칙
장기 판단은 Daily Review의 `BEST_MODEL_TODAY` 승패 수가 아니라 원지표를 사용한다.

모델/시각별:
- TOP1_FE
- TOP1_OFE
- TOP1_AE
- TOP3_AVG_FE
- TOP3_AVG_OFE
- AVG_FE
- AVG_OFE
- AVG_AE
- FE3_HIT_RATE
- FE5_HIT_RATE
- FE10_HIT_RATE
- EXPECTED_MOVE_IN_RANGE_RATE
- RANK_QUALITY
- Confidence 결과

Deep 추가:
- BaseScore와 FE/OFE 관계
- C/I/D/L/E/R/Q와 FE/OFE/AE 관계
- PriceIn / ChaseRisk
- Coverage
- OpenExpectation

가능한 경우 평균뿐 아니라:
- median
- valid N
- dispersion 또는 범위
를 함께 본다.

표본수가 다른 모델을 단순 평균값 하나로 결론내지 않는다.

## 6. Simple vs Deep 분석
03:30과 08:30을 각각 분리해 본다.

질문:
- Deep이 Simple보다 TOP1/TOP3 FE를 일관되게 개선하는가?
- OFE도 개선하는가, 아니면 갭이 큰 종목만 더 잘 찾는가?
- AE를 줄이는가?
- FE5/FE10 포착이 개선되는가?
- Deep의 복잡성이 성능 개선으로 이어지는가?
- 특정 regime에서만 효과가 있는가?

결론 enum:
- DEEP_ADVANTAGE
- SIMPLE_ADVANTAGE
- REGIME_DEPENDENT
- NO_CLEAR_DIFFERENCE
- INSUFFICIENT_DATA

이 enum은 설명용이며 원지표가 authoritative하다.

## 7. 03:30 vs 08:30 분석
Simple과 Deep을 각각 분리한다.

질문:
- 08:30의 추가 정보가 FE/OFE를 개선하는가?
- 08:30에서 갭 선반영 때문에 OFE가 오히려 낮아지는가?
- 03:30이 더 큰 upside를 일찍 포착하는가?
- 08:30이 false positive와 AE를 줄이는가?

결론 enum:
- 08:30_ADVANTAGE
- 03:30_ADVANTAGE
- REGIME_DEPENDENT
- NO_CLEAR_DIFFERENCE
- INSUFFICIENT_DATA

## 8. Deep Score Calibration
C/I/D/L/E/R/Q 각각에 대해 가능한 범위에서:

- high-score group vs low-score group의 FE
- OFE
- AE
- FE3/FE5 hit
- 표본 수

를 비교한다.

특히 검증:
- E가 실제 Expansion을 구별하는가?
- I가 WHY_TODAY를 구별하는가?
- D/L이 국내 실제 집중과 연결되는가?
- R이 chase/price-in 실패를 줄이는가?
- Q가 AE나 실패율을 줄이는가?

하루 사례나 상관관계만으로 인과를 주장하지 않는다.
동일 FACT 중복가산 패턴이 Review에서 반복됐는지도 확인한다.

## 9. Missed Big Moves
Daily Review의 `MISSED_BIG_MOVES` 중 `LEARNABLE=YES` 사례를 우선 집계한다.

반복 유형을 분류한다.
예:
- 탐색 누락
- 공시/뉴스 발견 실패
- Wrong Leader
- 국내 breadth 과소평가
- Price-in 과대평가
- Catalyst impact 과소평가
- 08:30 신규정보 미반영
- 기타

Prediction 이후 발생한 신규정보 사례는 학습 가능한 miss와 분리한다.

## 10. Observation 관리
기존 `DMI_LEARNING_v8.md` Observation과 신규 evidence를 대조한다.

새 Observation을 만들 조건:
- 하나의 Daily Review에서도 구조적 이상이 명확하면 OBSERVING으로 생성 가능
- 기존 Observation과 의미가 같으면 새 ID를 만들지 않고 기존 항목 갱신

갱신:
- FIRST_SEEN 유지
- LAST_SEEN 갱신
- SAMPLE_DAYS 갱신
- SUPPORTING_METRICS 갱신
- COUNTEREVIDENCE 반드시 갱신
- REGIME_DEPENDENCY 점검
- SOURCE_REVIEWS 누적

Observation을 유리한 사례만으로 유지하지 않는다.

## 11. Improvement Candidate 관리
다음 중 하나면 Candidate를 고려한다.

- 여러 Review에서 같은 Observation 반복
- 20D window에서 실질적 성능차가 보임
- 명확한 process/data 오류가 반복
- 특정 ACTIVE_RULE이 예상과 반대로 작동할 가능성

Candidate에는 반드시:
- 정확한 문제
- 변경 대상
- 제안 변경
- 기대효과
- 부작용
- 표본 수
- supporting metrics
- counterevidence
- rollback condition

을 기록한다.

## 12. Rule Proposal 승격 기준
Rule Proposal은 기본적으로 다음 조건을 모두 검토한다.

1. 단일 날짜가 아닌 반복 evidence
2. 적어도 20거래일 검토가 원칙
3. 충분한 유효 표본
4. 반대 evidence 확인
5. 특정 일회성 regime만의 현상인지 검토
6. 변경으로 생길 부작용 명시
7. rollback condition 정의

60D evidence가 있으면 robustness를 추가 검증한다.

예외:
데이터 조작, 미래정보 사용, duplicate evidence 같은 명백한 process defect는 표본이 작아도 READY_FOR_REVIEW를 제안할 수 있다.
그래도 자동 APPROVED는 금지한다.

## 13. Existing Active Rule Audit
각 ACTIVE_RULE에 대해 필요할 때 다음 상태를 평가한다.

- SUPPORTED
- MIXED
- CHALLENGED
- INSUFFICIENT_DATA

CHALLENGED라고 바로 삭제 Proposal을 만들지 않는다.
반복 evidence와 부작용을 검토한다.

## 14. Learning Ledger 업데이트 규칙
이 maintenance 작업이 직접 수정할 수 있는 파일은 원칙적으로:

`/DMI_LEARNING_v8.md`

뿐이다.

금지:
- `DMI_PLAYBOOK_v8.md` 직접 수정
- Prediction prompt 직접 수정
- Daily Review prompt 직접 수정
- 과거 Review 수정
- 과거 Prediction 수정

기존 Learning Ledger의:
- Observation
- Candidate
- Rule Proposal
- Rejected/Retired history
를 보존하면서 갱신한다.

기존 ID를 임의 재사용하거나 삭제하지 않는다.

## 15. 사용자 승인 경계
Rule Proposal은 다음 상태까지만 자동 작성할 수 있다.

`STATUS: READY_FOR_REVIEW`
`USER_APPROVAL: PENDING`

사용자가 명시적으로 승인하기 전:
- APPROVED로 변경 금지
- Playbook 변경 금지

## 16. 출력 보고
maintenance 결과에서 다음을 요약한다.

- WINDOW
- REVIEW_DATE_RANGE
- VALID_REVIEW_DAYS
- EXCLUDED_DAYS
- VERSION_MIXED
- SIMPLE_VS_DEEP_FINDING
- 03:30_VS_08:30_FINDING
- KEY_SCORE_CALIBRATION
- TOP_LEARNABLE_MISS_PATTERN
- NEW_OBSERVATIONS
- UPDATED_OBSERVATIONS
- NEW_CANDIDATES
- UPDATED_CANDIDATES
- NEW_RULE_PROPOSALS
- ACTIVE_RULE_AUDIT
- LEARNING_LEDGER_WRITE_STATUS

## 17. 저장
분석이 끝나면 `DMI_LEARNING_v8.md`를 기존 내용과 병합해 갱신한다.

- 기존 historical entries 삭제 금지
- rejected/retired 이력 보존
- ChangeLog에 실행 날짜, window, source review range, 주요 변경을 기록
- GitHub write 성공 후 재열람 검증
- 실제 write가 성공한 경우에만 업데이트 성공으로 보고

별도의 official Prediction/Review run 파일을 생성하지 않는다.
