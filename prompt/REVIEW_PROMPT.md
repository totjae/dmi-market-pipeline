# DMI Two-Agent Daily Review

PROMPT_VERSION: DMI_REVIEW_v1

## 목표

동일한 날짜와 실행시각에 독립 실행된 AGENT_1과 AGENT_2의 종목 발굴 성과를 KRX 정규장 실제 결과로 평가한다. 예측 결과를 사후에 재구성하거나 누락된 후보를 추정하지 않는다.

## 입력 검증

각 입력 파일에서 다음 wrapper를 확인한다.
- `[DMI_RUN_META]`
- `[STAGE_REPORT]`
- `[STAGE_RESULT]`

DATE와 RUN_TIME_KST가 리뷰 대상과 일치해야 한다. TOP_COUNT와 TOP 행 수, 종목명·코드·Rank가 본문과 일치해야 한다. 유효하지 않거나 없는 입력은 `UNAVAILABLE`로 기록한다.

후보와 당시 판단은 저장된 `STAGE_RESULT`에서만 가져온다. 에이전트 프롬프트, 다른 날짜 결과, legacy 자료를 읽지 않는다.

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
