# DMI PLAYBOOK v8

PLAYBOOK_VERSION: DMI_PLAYBOOK_v8.0

이 문서는 **Prediction-safe rulebook**이다.
03:30/08:30 Simple·Deep Prediction이 읽어도 되는 장기 규칙만 포함한다.

Daily Review의 개별 결과, 관찰, 개선 가설, 폐기된 규칙의 상세 이력은 이 문서에 넣지 않는다.
그 정보는 `/DMI_LEARNING_v8.md`에서 별도로 관리한다.

## OBJECTIVE
오늘 KRX 정규장에서 단순히 상승할 종목이 아니라 **실제 단타 기회가 될 정도로 크게 상승할 가능성이 높은 종목**을 개장 전에 찾는다.

우선순위:
1. 의미 있는 당일 Big-Move 포착
2. 오늘 움직여야 하는 이유가 있는 후보
3. 시장 관심·자금이 집중될 가능성이 있는 후보
4. 이미 대부분 선반영된 움직임보다 남은 상승 여력이 있는 후보
5. Rank가 실제 Big-Move 크기를 구별하도록 하는 것

단순 `종가 > 전일 종가` 적중은 보조적 가치만 가진다.

## ACTIVE_RULES

### AR-001 — Domestic decision first
미국 종목·미국 지수·글로벌 Peer의 움직임만으로 국내 종목 후보를 결정하지 않는다.

외부 신호가 핵심 근거라면 한국 종목으로 전달되는 구체적 경제적·산업적·수급적 경로가 있어야 한다.
국내 직접 촉매가 있다면 불필요한 글로벌 연결을 요구하지 않는다.

### AR-002 — No evidence multiplication
동일 FACT를 Catalyst, Theme, Flow, Market Environment 등 여러 개의 독립 증거처럼 반복 가산하지 않는다.

같은 사실이 여러 판단항목과 관련될 수는 있지만, 각 항목을 강하게 평가하려면 그 항목 고유의 추가 근거나 별도 논리가 있어야 한다.

### AR-003 — WHY_TODAY / WHY_BIG
후보의 핵심 질문은 다음 두 가지다.

- 왜 **오늘** 움직여야 하는가?
- 왜 단순 소폭 상승이 아니라 **의미 있는 Big-Move**가 가능한가?

좋은 회사, 장기적으로 유망한 회사, 최근 강했던 회사라는 이유만으로 후보를 선택하지 않는다.

### AR-004 — Prefer direct and current domestic evidence
현재 실행시각에 실제 확인 가능한 범위에서 국내 직접 촉매, 국내 가격반응, 관련 종목 breadth, 거래집중 등 국내 증거를 글로벌 간접 신호보다 우선한다.

해당 시각에 아직 존재하지 않는 국내 데이터를 요구하거나 추정하지 않는다.

### AR-005 — Price-in matters
재료의 긍정성이나 신선도와 별개로 이미 가격에 상당 부분 반영됐는지 확인한다.

강한 Catalyst라도 추가 상승 여력이 작거나 추격 위험이 크면 Big-Move 후보로서 낮게 평가할 수 있다.

### AR-006 — Do not fill the list
TOP5는 최대 개수다.
Big-Move 근거가 부족하면 후보 수를 줄인다.

약한 후보를 추가해 숫자를 맞추지 않는다.

### AR-007 — Score follows judgment
Deep Prediction에서 후보 선정과 Rank를 먼저 완료한다.
Score는 그 판단을 기록·검증하기 위한 calibration/audit 값이며 후보 생성이나 Rank의 사후 정당화 수단이 아니다.

### AR-008 — Unknown stays unknown
확인할 수 없는 가격·수급·NXT·예상체결·기타 실시간 데이터를 만들지 않는다.

실제 평가 불가능하면 prompt가 허용하는 `N/A` 또는 `UNVERIFIED`를 사용한다.

### AR-009 — Counterargument is mandatory in Deep
Deep Prediction에서는 각 최종 후보의 가장 강한 반대논리를 검토한다.
반대논리가 Big-Move 근거보다 강하면 후보에서 제외한다.

Simple Prediction에는 고정 검증 절차를 강제하지 않으며 자유 종합판단이라는 실험 조건을 유지한다.

## RULE GOVERNANCE
- Prediction은 이 문서의 OBJECTIVE와 ACTIVE_RULES만 적용한다.
- Daily Review 한 건으로 ACTIVE_RULE을 추가·변경·삭제하지 않는다.
- 규칙 변경은 `DMI_LEARNING_v8.md`에 축적된 근거와 Rolling Calibration을 검토한 maintenance 작업에서만 제안한다.
- 실제 ACTIVE_RULE 변경은 사용자 승인 후 수행한다.
- 규칙이 실질적으로 바뀌면 PLAYBOOK_VERSION을 증가시키고 변경 근거를 Learning Ledger에 남긴다.
