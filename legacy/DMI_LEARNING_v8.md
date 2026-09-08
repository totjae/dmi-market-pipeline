# DMI LEARNING LEDGER v8

LEARNING_SCHEMA_VERSION: DMI_LEARNING_v8.0

이 문서는 DMI v8의 **개선 연구 및 규칙 변경 이력 저장소**다.

Prediction stage는 이 문서를 읽지 않는다.
Daily Prediction의 후보·Rank·Score에 이 문서 내용을 직접 사용하지 않는다.

Daily Review는 자신의 run 파일 안에 Observation과 Improvement Candidate를 기록한다.
이 Ledger는 이후 별도 Rolling Calibration / Rule Review maintenance 작업에서 여러 Review를 종합해 갱신한다.

## 1. 목적
Daily Review가 쌓였을 때 다음을 추적한다.

- 어떤 성공/실패 패턴이 반복되는가
- Simple과 Deep 중 어떤 판단 구조가 실제로 유효한가
- 03:30과 08:30의 정보 추가가 어떤 경우에 가치가 있는가
- Deep의 C/I/D/L/E/R/Q가 실제 FE/OFE와 어떤 관계가 있는가
- 어떤 후보를 반복적으로 놓치는가
- 어떤 ACTIVE_RULE이 유효하거나 오히려 성능을 해치는가

단일 사례의 설명을 일반 규칙으로 즉시 변환하지 않는다.

## 2. 상태 enum
Improvement Candidate와 Rule Proposal에는 다음 상태만 사용한다.

- `OBSERVING`
- `CANDIDATE`
- `READY_FOR_REVIEW`
- `APPROVED`
- `REJECTED`
- `RETIRED`

자동으로 APPROVED 상태로 변경하지 않는다.

## 3. Evidence windows
기본 집계 창:
- 5거래일 — 빠른 이상징후 탐지
- 20거래일 — 기본 개선 검토
- 60거래일 — 안정성·regime 의존성 확인

5일 결과만으로 일반 ACTIVE_RULE을 만드는 것을 기본으로 하지 않는다.
강한 구조적 오류가 있더라도 우선 CANDIDATE 또는 READY_FOR_REVIEW로 제안한다.

## 4. 핵심 장기 지표
가능한 경우 모델·시각별로 분리해 추적한다.

- TOP1_FE / TOP1_OFE / TOP1_AE
- TOP3_AVG_FE / TOP3_AVG_OFE
- AVG_FE / AVG_OFE / AVG_AE
- FE3 / FE5 / FE10 Hit Rate
- Expected Move calibration
- Rank Quality
- Confidence calibration
- Deep Score 및 C/I/D/L/E/R/Q calibration
- AVOID effectiveness
- Learnable Missed Big Moves
- Simple vs Deep 원지표
- 03:30 vs 08:30 원지표

`BEST_MODEL_TODAY` 같은 일일 종합승패는 장기 핵심 지표로 사용하지 않는다.

## 5. OBSERVATION LOG
Rolling Calibration에서 Daily Review의 Observation을 종합해 기록한다.

```text
[OBSERVATION]
ID: OBS-YYYY-NNN
STATUS: OBSERVING
FIRST_SEEN:
LAST_SEEN:
SAMPLE_DAYS:
AFFECTED_STAGE:
AFFECTED_MODEL:
PATTERN:
SUPPORTING_METRICS:
COUNTEREVIDENCE:
REGIME_DEPENDENCY:
SOURCE_REVIEWS:
NOTE:
[/OBSERVATION]
```

현재 등록 Observation: NONE

## 6. IMPROVEMENT CANDIDATES
Observation이 반복되거나 구조적 개선 가능성이 있을 때 기록한다.

```text
[IMPROVEMENT_CANDIDATE]
ID: IMP-YYYY-NNN
STATUS: CANDIDATE
RELATED_OBSERVATIONS:
TARGET: <Simple / Deep / Review / Playbook / Workflow / Score / Data>
PROBLEM:
PROPOSED_CHANGE:
EXPECTED_BENEFIT:
POSSIBLE_SIDE_EFFECT:
EVIDENCE_WINDOW:
SAMPLE_SIZE:
SUPPORTING_METRICS:
COUNTEREVIDENCE:
ROLLBACK_CONDITION:
SOURCE_REVIEWS:
[/IMPROVEMENT_CANDIDATE]
```

현재 등록 Candidate: NONE

## 7. RULE PROPOSALS
ACTIVE_RULE 변경 후보가 충분히 검증됐을 때만 생성한다.

```text
[RULE_PROPOSAL]
ID: RULE-YYYY-NNN
STATUS: READY_FOR_REVIEW
ACTION: <ADD / MODIFY / REMOVE>
TARGET_RULE:
PROPOSED_RULE_TEXT:
RATIONALE:
EVIDENCE_WINDOW:
SAMPLE_SIZE:
EXPECTED_EFFECT:
KNOWN_RISK:
ROLLBACK_CONDITION:
RELATED_CANDIDATES:
USER_APPROVAL: PENDING
[/RULE_PROPOSAL]
```

`USER_APPROVAL: APPROVED`가 되기 전에는 DMI_PLAYBOOK_v8.md를 변경하지 않는다.

현재 Rule Proposal: NONE

## 8. REJECTED / RETIRED
거절 또는 폐기한 규칙과 이유를 보존한다.
같은 실패한 아이디어가 반복 제안되는 것을 방지하기 위한 영역이다.

현재 항목: NONE

## 9. CHANGELOG
- v8.0 — Prediction-safe Playbook과 Learning Ledger를 분리.
- v8.0 — Observation → Improvement Candidate → Rule Proposal → User Approval → Active Rule 구조 도입.
- v8.0 — 5/20/60거래일 evidence window 정의.
