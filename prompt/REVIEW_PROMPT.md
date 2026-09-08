# DMI Two-Agent Daily Review

PROMPT_VERSION: DMI_REVIEW_v1.2

## 목표

동일한 날짜와 실행시각에 독립 실행된 AGENT_1과 AGENT_2의 종목 발굴 성과를 KRX 정규장 실제 결과로 평가한다. 예측 결과를 사후에 재구성하거나 누락된 후보를 추정하지 않는다.

## 입력 검증

각 입력 파일에서 다음 wrapper를 확인한다.
- `[DMI_RUN_META]`
- `[STAGE_REPORT]`
- `[STAGE_RESULT]`

DATE와 RUN_TIME_KST가 리뷰 대상과 일치해야 한다. TOP_COUNT와 TOP 행 수, 종목명·코드·Rank가 본문과 일치해야 한다. 유효하지 않거나 없는 입력은 `UNAVAILABLE`로 기록한다.

후보 목록·Rank는 저장된 `STAGE_RESULT`를 사용한다. 상세 근거·가격 계획·위험·무효화 조건은 같은 선택 파일의 `STAGE_REPORT`와 선택 필드에서 읽는다. 본문과 캡슐이 충돌하면 임의로 보정하지 말고 불일치를 보고한다. 에이전트 프롬프트, 다른 날짜 결과, legacy 자료를 읽지 않는다.

### 입력 형식과 선택 필드

- DMI_AGENT_v1, DMI_AGENT_v1.1 및 DMI_AGENT_v1.2를 지원한다. v1.2는 v1.1 후보 구조를 유지하며 예약·실제 실행 시각을 분리한다. 알 수 없는 버전은 UNSUPPORTED_SCHEMA로 기록하고 억지로 해석하지 않는다.
- v1.1/v1.2의 TOP 행 순서는 RowNo|Name|Code|Market|Rank|ExpectedMoveFE|Confidence|CoreReason이다. RowNo와 Rank는 같아야 한다. OPTIONAL_DETAILS는 선택 사항이고 후보 Rank로 연결한다.
- ExpectedMoveFE는 전일 KRX 종가 대비 당일 정규장 예상 고가 상승률만 뜻한다. v1에서는 다른 단위 혼입이 허용됐으므로 본문에서 정의를 확인한 값만 FE 예측 평가에 사용한다.
- Agent 2 등에서 FE 예측이 제공되지 않은 경우 목표가·진입 계획으로 FE를 역산하지 않는다. 실제 FE/OFE에 따른 종목 발굴 평가는 가능하지만 예상 FE 구간 평가는 N/A로 둔다.
- 선택 필드 부재나 NOT_PROVIDED/UNVERIFIED/NOT_APPLICABLE/UNCERTAIN은 0이나 예측 실패로 처리하지 않는다. 사유와 평가 가능한 표본 수를 함께 남긴다.
- Confidence는 낮음/보통/높음을 LOW/MEDIUM/HIGH로 대응시킨다. 그 밖의 값을 추측해 매핑하지 않는다.
- TOP 밖의 고위험 보조 관찰군은 본문에서 별도로 검토할 수 있으나 TOP 후보 수·적중률에 포함하지 않는다. TOP 안의 관찰 후보는 발굴 평가에 포함하되 상태별로 구분한다.
- 조건부 매매 계획은 공통 종목 발굴 KPI와 분리한다. 실제 진입 조건·취소 조건·목표·손절의 시간순서를 확인할 수 있을 때만 계획 성과를 평가한다. 일봉만 있거나 같은 봉 안에서 순서가 불명확하면 NOT_SCORABLE로 기록한다. 가격 접촉만으로 체결이나 실현수익을 단정하지 않는다.

## Ground Truth

동일한 기준의 신뢰 가능한 KRX 정규장 Previous Close, Open, High, Low, Close를 확보한다. corporate action, 거래정지, 가격 데이터 불일치는 별도로 확인한다. 검증할 수 없는 값은 추정하지 않고 `N/A`로 둔다.

각 후보에 대해 계산한다.
- C2C = (Close - Previous Close) / Previous Close
- O2C = (Close - Open) / Open
- FE = (High - Previous Close) / Previous Close
- OFE = (High - Open) / Open
- AE = max(0, (Previous Close - Low) / Previous Close)
- FE3 / FE5 / FE10 적중 여부
- Expected Move가 구간으로 제공된 경우 구간 적합 여부

모든 비율은 백분율로 표시한다.

## 비교

각 에이전트에 대해 다음을 평가한다.
- TOP1 FE와 OFE
- TOP3 평균 FE·OFE·AE
- 전체 평균 FE·OFE·AE
- FE3·FE5·FE10 적중률
- Rank와 FE의 Spearman 상관
- Expected Move와 Confidence의 보정 상태
- 후보 발굴 성공과 주요 오판

후보 수와 유효 표본이 다르면 원지표와 표본 수를 함께 제시한다. 표본이 부족하거나 한쪽 입력이 없으면 억지로 승자를 정하지 않는다.

## 개선 분석

성과가 좋았던 판단 과정과 반복된 오류를 구분한다. 특히 다음을 살핀다.
- 직접 촉매와 첫 가격발견
- 시장 테마의 지속과 국내 전달경로
- 거래·관심 집중
- Price-in과 개장 후 남은 여력
- 당일 상승 가능성과 매매 위험의 혼동
- 상위 Rank가 실제 큰 움직임을 제대로 정렬했는지

개선안은 관찰된 증거, 기대효과, 부작용을 함께 기록한다. 단일 거래일 결과만으로 에이전트 프롬프트를 수정하거나 활성 규칙으로 승격하지 않는다.

## 출력

1. 입력과 검증 상태
2. 시장 Ground Truth
3. 후보별 실제 성과
4. 에이전트별 KPI
5. Agent 1 vs Agent 2 비교
6. 성공·오류 분석
7. 개선 후보
8. 최종 요약

완료 후 `/templates/REVIEW_OUTPUT.md`의 machine-readable result를 본문과 일치하게 작성한다.

## 복수 슬롯 일일 리뷰

WORKFLOW의 입력 선택·장전 저장 검증을 먼저 적용한다. 03:30과 08:30 각각 위 평가를 수행하고 결과를 슬롯별로 분리한다. 각 에이전트의 시간대 간 차이는 별도 비교하며, 후행 슬롯은 새 정보가 추가된 조건임을 명시한다. 입력이 누락된 그룹을 0점으로 채우거나 다른 슬롯으로 대체하지 않는다.
