[DMI_REVIEW_META]
SCHEMA_VERSION: DMI_REVIEW_v1.3
DATE: 2026-09-18
PREDICTION_RUN_TIMES_KST: [03:30, 08:30]
REVIEW_TIME_KST: 16:30
STARTED_AT_KST: 2026-09-18T16:28:36+09:00
REPORT_COMPLETED_AT_KST: 2026-09-18T16:30:31+09:00
DATA_CUTOFF_KST: 2026-09-18T16:30:12+09:00
SOURCE_MANIFEST: REVIEW_EVIDENCE.input_manifest
REVIEW_DOCUMENT_VERSIONS: REVIEW_EVIDENCE.review_document_versions
RUN_TYPE: NORMAL
RERUN_SEQUENCE: 0
[/DMI_REVIEW_META]

[REVIEW_REPORT]
# DMI Two-Agent Daily Review — 2026-09-18

## 1. 입력과 검증 상태

KRX 공식 정규장 시간은 09:00~15:30이다. 네 파일 모두 단일 저장 이력이며 최초 저장시각이 09:00 이전이고, DMI_AGENT_v1.3 wrapper·날짜·슬롯·TOP_COUNT와 결과행이 일치했다. 따라서 4/4개를 공식 입력으로 채택했다. 정규장 시간 근거: https://global.krx.co.kr/contents/GLB/06/0602/0602020204/GLB0602020204T1.jsp

| 슬롯 | 입력 | 경로 | 최초 저장시각(KST) | 상태 |
|---|---|---|---|---|
| 03:30 | Agent 1 | runs/2026-09-18/0330.md | 03:30:48 | OFFICIAL |
| 03:30 | Agent 2 | runs/2026-09-18/0330.md | 03:35:33 | OFFICIAL |
| 08:30 | Agent 1 | runs/2026-09-18/0830.md | 08:26:09 | OFFICIAL |
| 08:30 | Agent 2 | runs/2026-09-18/0830.md | 08:32:07 | OFFICIAL |

rerun은 없었으며 최신 revision으로 최초 유효 예측을 교체하지 않았다.

## 2. 시장 Ground Truth

9월 18일 KRX 정규장에서 코스피는 2.66% 상승했다. 후보 종목의 확인된 원주가 OHLC는 다음과 같다.

| 종목 | 전일 종가 | 시가 | 고가 | 저가 | 종가 |
|---|---:|---:|---:|---:|---:|
| 엘앤에프(066970) | 111,300 | 114,800 | 115,200 | 110,100 | 111,000 |
| SK하이닉스(000660) | 1,745,000 | 1,810,000 | 1,857,000 | 1,805,000 | 1,857,000 |

출처: [엘앤에프 9월 18일 KRX 정규장](https://stock.mk.co.kr/price/home/KR7066970005), [SK하이닉스 9월 18일 KRX 정규장](https://stock.mk.co.kr/price/home/KR7000660001).

## 3. 후보별 실제 성과

동일 종목도 입력별 후보를 합치지 않았다. FE는 전일 종가 대비 당일 고가, OFE는 시가 대비 고가, AE는 전일 종가 대비 당일 저가 하방폭이다.

| 슬롯·입력·순위 | 후보 | C2C | O2C | FE | OFE | AE | 예상 FE 적합 |
|---|---|---:|---:|---:|---:|---:|---|
| 03:30 A1 #1 | 엘앤에프 | -0.27% | -3.31% | 3.50% | 0.35% | 1.08% | 적합(+3~5%) |
| 03:30 A2 #1 | 엘앤에프 | -0.27% | -3.31% | 3.50% | 0.35% | 1.08% | 미달(+5~10%) |
| 03:30 A2 #2 | SK하이닉스 | 6.42% | 2.60% | 6.42% | 2.60% | 0.00% | 초과(+3~5%) |
| 08:30 A1 #1 | 엘앤에프 | -0.27% | -3.31% | 3.50% | 0.35% | 1.08% | 미달(+5~10%) |
| 08:30 A1 #2 | SK하이닉스 | 6.42% | 2.60% | 6.42% | 2.60% | 0.00% | 초과(+3~5%) |
| 08:30 A2 #1 | 엘앤에프 | -0.27% | -3.31% | 3.50% | 0.35% | 1.08% | 미달(+5~10%) |
| 08:30 A2 #2 | SK하이닉스 | 6.42% | 2.60% | 6.42% | 2.60% | 0.00% | 초과(+3~5%) |

엘앤에프는 3.14% 갭상승 시가를 형성했지만 시가 대비 고가 여력은 0.35%에 그쳤고 종가는 시가 대비 3.31% 하락했다. 직접 촉매의 첫 가격발견은 있었지만 개장 후 여력보다 갭 소진 위험이 중요했다. SK하이닉스는 시가 이후에도 OFE 2.60%를 확보하고 고가로 마감해 해외 반도체 강세의 국내 전달경로가 실제로 이어졌다.

## 4. 슬롯별 에이전트 KPI

### 03:30

| 지표 | Agent 1 | Agent 2 |
|---|---:|---:|
| 후보 수 | 1 | 2 |
| TOP1 FE | 3.50% | 3.50% |
| TOP3/전체 평균 FE | 3.50% (n=1/1) | 4.96% (n=2/2) |
| 전체 평균 OFE | 0.35% (n=1/1) | 1.47% (n=2/2) |
| 전체 평균 AE | 1.08% (n=1/1) | 0.54% (n=2/2) |
| FE3 적중률 | 100.00% (1/1) | 100.00% (2/2) |
| FE5 적중률 | 0.00% (0/1) | 50.00% (1/2) |
| FE10 적중률 | 0.00% (0/1) | 0.00% (0/2) |
| 예상 FE 구간 적합률 | 100.00% (1/1) | 0.00% (0/2) |
| 순위 Spearman | N/A (n=1) | -1.000 (n=2) |

Agent 2는 실제 최고 FE 종목인 SK하이닉스를 추가 발굴해 평균 FE와 FE5 적중률이 높았다. 다만 엘앤에프를 1위, SK하이닉스를 2위로 둬 실제 FE 순서를 반대로 정렬했고 두 예상 구간 모두 빗나갔다. Agent 1은 후보 폭은 좁았지만 엘앤에프의 +3~5% 구간을 맞췄다. 지표가 엇갈려 종합 판정은 **MIXED**다.

### 08:30

| 지표 | Agent 1 | Agent 2 |
|---|---:|---:|
| 후보 수 | 2 | 2 |
| TOP1 FE | 3.50% | 3.50% |
| TOP3/전체 평균 FE | 4.96% (n=2/2) | 4.96% (n=2/2) |
| 전체 평균 OFE | 1.47% (n=2/2) | 1.47% (n=2/2) |
| 전체 평균 AE | 0.54% (n=2/2) | 0.54% (n=2/2) |
| FE3 적중률 | 100.00% (2/2) | 100.00% (2/2) |
| FE5 적중률 | 50.00% (1/2) | 50.00% (1/2) |
| FE10 적중률 | 0.00% (0/2) | 0.00% (0/2) |
| 예상 FE 구간 적합률 | 0.00% (0/2) | 0.00% (0/2) |
| 순위 Spearman | -1.000 (n=2) | -1.000 (n=2) |

두 에이전트는 후보·순위·예상 구간이 동일해 모든 공식 KPI가 같다. 판정은 **TIE**다. 두 후보 모두 FE3에는 성공했지만, 엘앤에프는 예상보다 낮고 SK하이닉스는 예상보다 높아 변동폭 배분과 순위가 실제 결과와 반대였다.

## 5. 동일 에이전트의 03:30 vs 08:30

- **Agent 1:** 08:30에 SK하이닉스를 새로 추가하면서 평균 FE가 3.50%에서 4.96%로 높아지고 FE5 적중 후보를 확보했다. 반면 엘앤에프 예상은 +3~5%에서 +5~10%로 상향돼 적합에서 미달로 바뀌었고, 새 순위는 실제 성과와 반대였다.
- **Agent 2:** 두 슬롯의 후보와 순위가 동일해 평균 FE와 적중률은 변하지 않았다. 08:30에는 SK하이닉스 확신도를 LOW에서 MEDIUM으로 높였으나 실제 순위 오류는 수정되지 않았다. 후행 분석은 새 정보 분석으로 평가했으며 03:30의 대체나 복구로 취급하지 않았다.

## 6. 조건부 계획 평가

Agent 2의 엘앤에프 계획은 03:30에 113,800~114,500원 회복·유지와 거래 증가, 08:30에 113,800원 돌파 후 되돌림 지지를 요구했다. 실제 시가는 114,800원, 고가는 115,200원, 저가는 110,100원이었으나 일봉 OHLC만으로 거래 증가·지지 확인과 장중 발생 순서를 확정할 수 없다. 따라서 두 계획 모두 **NOT_SCORABLE**이며 접촉만으로 체결·실현수익을 단정하지 않는다. 나머지 후보는 관찰 상태로 수치 진입 계획이 없어 **NOT_PROVIDED**다.

## 7. 성공·오류 분석

- 성공: SK하이닉스는 미국 반도체 강세와 메모리 재평가라는 해외 전달경로가 실제 FE 6.42%와 고가 마감으로 이어졌다.
- 성공: 03:30 Agent 1은 엘앤에프의 공시 규모와 갭 위험을 보수적으로 평가해 실제 FE 3.50%를 구간 안에 담았다.
- 오류: 모든 2종목 입력이 엘앤에프를 SK하이닉스보다 높게 배치했지만 실제 FE는 SK하이닉스가 2.91%p 높았다.
- 오류: 엘앤에프의 공시 직접성을 당일 고가 잠재력과 과도하게 연결했다. 실제로는 높은 시가 뒤 추가 여력이 0.35%에 그치고 종가가 음전했다.
- 오류: SK하이닉스 +3~5% 예상은 실제 6.42%를 과소평가했다.

## 8. 개선 후보

- 관찰 근거: 직접 공시가 있는 엘앤에프보다 시장·업종 강세와 가격 지속성이 있는 SK하이닉스의 FE가 높았다.
- 개선 후보: 순위 결정에서 촉매의 직접성뿐 아니라 개장 전 업종 확산 강도와 전일 고가 회복 가능성을 별도 비교한다.
- 기대효과: 직접 공시 종목의 갭 소진과 업종 대표주의 추세 지속을 더 잘 구분할 수 있다.
- 부작용: 해외 업종 신호를 과대평가하면 국내 개별 종목의 미반영 공시를 놓칠 수 있다.
- 적용 상태: 단일 거래일 관찰이므로 프롬프트나 운영 규칙에 자동 반영하지 않는다.

## 9. 최종 요약

공식 입력은 4/4개다. 03:30은 Agent 2가 SK하이닉스를 추가 발굴했지만 순위·예상 구간 정확도에서 약점이 있어 **MIXED**, 08:30은 완전히 동일해 **TIE**다. 당일 최고 후보는 SK하이닉스 FE 6.42%였으며, 엘앤에프는 FE 3.50%에도 불구하고 시가 대비 종가가 3.31% 하락해 갭 추격 위험을 확인시켰다.

[REVIEW_RESULT]
SCHEMA_VERSION: DMI_REVIEW_v1.3
DATE: 2026-09-18
PREDICTION_RUN_TIME_KST: 03:30
AGENT_1_STATUS: OFFICIAL
AGENT_2_STATUS: OFFICIAL
AGENT_1_COUNT: 1
AGENT_2_COUNT: 2
AGENT_1_TOP1_FE: 3.50%
AGENT_2_TOP1_FE: 3.50%
AGENT_1_TOP3_AVG_FE: 3.50%
AGENT_2_TOP3_AVG_FE: 4.96%
AGENT_1_FE3_HIT_RATE: 100.00%
AGENT_2_FE3_HIT_RATE: 100.00%
AGENT_1_FE5_HIT_RATE: 0.00%
AGENT_2_FE5_HIT_RATE: 50.00%
AGENT_1_FE10_HIT_RATE: 0.00%
AGENT_2_FE10_HIT_RATE: 0.00%
AGENT_1_VALID_FE_COUNT: 1
AGENT_2_VALID_FE_COUNT: 2
AGENT_1_TOP3_VALID_FE_COUNT: 1
AGENT_2_TOP3_VALID_FE_COUNT: 2
AGENT_1_RANK_PERFORMANCE_SPEARMAN: N/A
AGENT_2_RANK_PERFORMANCE_SPEARMAN: -1.000
AGENT_1_RANK_PERFORMANCE_PAIR_COUNT: 1
AGENT_2_RANK_PERFORMANCE_PAIR_COUNT: 2
BEST_AGENT: MIXED
BEST_PICK: SK하이닉스(000660) FE 6.42% — Agent 2 Rank 2
PRIMARY_SUCCESS_PATTERN: Agent 2가 해외 반도체 강세의 국내 전달경로로 SK하이닉스를 추가 발굴함
PRIMARY_ERROR_PATTERN: 엘앤에프를 실제 최고 FE 종목인 SK하이닉스보다 높게 배치하고 Agent 2의 두 예상 구간이 모두 빗나감
IMPROVEMENT_CANDIDATE: 직접 촉매와 업종 추세의 개장 후 가격 지속 가능성을 분리 비교
[/REVIEW_RESULT]

[REVIEW_RESULT]
SCHEMA_VERSION: DMI_REVIEW_v1.3
DATE: 2026-09-18
PREDICTION_RUN_TIME_KST: 08:30
AGENT_1_STATUS: OFFICIAL
AGENT_2_STATUS: OFFICIAL
AGENT_1_COUNT: 2
AGENT_2_COUNT: 2
AGENT_1_TOP1_FE: 3.50%
AGENT_2_TOP1_FE: 3.50%
AGENT_1_TOP3_AVG_FE: 4.96%
AGENT_2_TOP3_AVG_FE: 4.96%
AGENT_1_FE3_HIT_RATE: 100.00%
AGENT_2_FE3_HIT_RATE: 100.00%
AGENT_1_FE5_HIT_RATE: 50.00%
AGENT_2_FE5_HIT_RATE: 50.00%
AGENT_1_FE10_HIT_RATE: 0.00%
AGENT_2_FE10_HIT_RATE: 0.00%
AGENT_1_VALID_FE_COUNT: 2
AGENT_2_VALID_FE_COUNT: 2
AGENT_1_TOP3_VALID_FE_COUNT: 2
AGENT_2_TOP3_VALID_FE_COUNT: 2
AGENT_1_RANK_PERFORMANCE_SPEARMAN: -1.000
AGENT_2_RANK_PERFORMANCE_SPEARMAN: -1.000
AGENT_1_RANK_PERFORMANCE_PAIR_COUNT: 2
AGENT_2_RANK_PERFORMANCE_PAIR_COUNT: 2
BEST_AGENT: TIE
BEST_PICK: SK하이닉스(000660) FE 6.42% — 양쪽 Rank 2
PRIMARY_SUCCESS_PATTERN: 두 에이전트 모두 FE3 이상 후보 두 개와 SK하이닉스 강세를 발굴함
PRIMARY_ERROR_PATTERN: 두 에이전트 모두 실제 성과 순서를 반대로 배치하고 예상 FE 구간 0/2 적합
IMPROVEMENT_CANDIDATE: 개장 후 남은 여력과 업종 대표주의 추세 지속성을 순위에 더 명시적으로 반영
[/REVIEW_RESULT]
[/REVIEW_REPORT]

[REVIEW_EVIDENCE]
{
  "schema_version": "DMI_REVIEW_EVIDENCE_v1",
  "review_document_versions": [
    {"role":"WORKFLOW","repository":"totjae/dmi-market-pipeline","path":"WORKFLOW.md","commit_sha":"27298b1c624573b5a1c17582e08bb12a0a3e50c8","blob_sha":"f7d593b7f558c95df45ad802b1489591cb726151","read_at_kst":"2026-09-18T16:30:12+09:00","status":"VERIFIED","reason":"NONE"},
    {"role":"SOURCES","repository":"totjae/dmi-market-pipeline","path":"config/SOURCES.md","commit_sha":"fa4f799d8d72895a638cc19caca7e6f338da8fe5","blob_sha":"5c47de7afdb65f60bc81a0050058a4c71d332853","read_at_kst":"2026-09-18T16:30:12+09:00","status":"VERIFIED","reason":"NONE"},
    {"role":"REVIEW_PROMPT","repository":"totjae/dmi-market-pipeline","path":"prompt/REVIEW_PROMPT.md","commit_sha":"f0c2f8fc512b41ba9166fa886b0c04741ddf3913","blob_sha":"fbd5f2e1f490a2b5a68ae8b095b58bccbbc19cb2","read_at_kst":"2026-09-18T16:30:12+09:00","status":"VERIFIED","reason":"NONE"},
    {"role":"REVIEW_OUTPUT","repository":"totjae/dmi-market-pipeline","path":"templates/REVIEW_OUTPUT.md","commit_sha":"445463f9f009da62fa76e143186d6af351106d66","blob_sha":"aced9658e7423ac059150f7d5cdf069efce21849","read_at_kst":"2026-09-18T16:30:12+09:00","status":"VERIFIED","reason":"NONE"}
  ],
  "input_manifest": [
    {
      "input_id":"A1_0330","agent_id":"AGENT_1","date":"2026-09-18","slot_kst":"03:30","repository":"totjae/dmi-agent-1","path":"runs/2026-09-18/0330.md",
      "evaluated_commit_sha":"c3247cb68d23758374450550b2f362635f105900","evaluated_blob_sha":"fd080babf9c35a0d440fdd18b182a253ec426d9e",
      "first_saved_commit_sha":"c3247cb68d23758374450550b2f362635f105900","first_saved_at_kst":"2026-09-18T03:30:48+09:00",
      "selection_status":"OFFICIAL","selection_reason":"VALID_SCHEMA_AND_SAVED_BEFORE_KRX_OPEN_09:00","prediction_schema_version":"DMI_AGENT_v1.3",
      "prediction_document_versions":[
        {"role":"WORKFLOW","repository":"totjae/dmi-agent-1","path":"WORKFLOW.md","commit_sha":"037d96493f9b921a8924f73a362794385d664cac","blob_sha":"8a25e4fe9ce2e66b516a189b78def10ba4281ad1","read_at_kst":"N/A","status":"VERIFIED","reason":"NONE"},
        {"role":"AGENT_PROMPT","repository":"totjae/dmi-agent-1","path":"prompt/AGENT_PROMPT.md","commit_sha":"5d550e1c78d8ce46db587f77f5d9b84b7b4aa81a","blob_sha":"a44b95f40710db6c56b8916b8aabce89d1654633","read_at_kst":"N/A","status":"VERIFIED","reason":"NONE"},
        {"role":"OUTPUT","repository":"totjae/dmi-agent-1","path":"templates/OUTPUT.md","commit_sha":"10d0d7f095df47ff74912df15d94580f3945e883","blob_sha":"cafb325fcc6f5497c631849517849f7c24ae7a3d","read_at_kst":"2026-09-18T03:29:00+09:00","status":"VERIFIED","reason":"NONE"}
      ],"version_status":"VERIFIED"
    },
    {
      "input_id":"A2_0330","agent_id":"AGENT_2","date":"2026-09-18","slot_kst":"03:30","repository":"totjae/dmi-agent-2","path":"runs/2026-09-18/0330.md",
      "evaluated_commit_sha":"c35eb42e5f1e0da891b22ed05e4e70ec0f2f6562","evaluated_blob_sha":"8eb569df24a19ada802b32dc19b62e34d99a6c09",
      "first_saved_commit_sha":"c35eb42e5f1e0da891b22ed05e4e70ec0f2f6562","first_saved_at_kst":"2026-09-18T03:35:33+09:00",
      "selection_status":"OFFICIAL","selection_reason":"VALID_SCHEMA_AND_SAVED_BEFORE_KRX_OPEN_09:00","prediction_schema_version":"DMI_AGENT_v1.3",
      "prediction_document_versions":[
        {"role":"WORKFLOW","repository":"totjae/dmi-agent-2","path":"WORKFLOW.md","commit_sha":"0daff2c0d84b0b60314d501aed3ab092a8bedc2b","blob_sha":"1f863cf6d2ce2fc3b347609845906d1d0ed56815","read_at_kst":"N/A","status":"VERIFIED","reason":"NONE"},
        {"role":"AGENT_PROMPT","repository":"totjae/dmi-agent-2","path":"prompt/AGENT_PROMPT.md","commit_sha":"3e833704e8c858df544bb8b06a5273e4ec95d26c","blob_sha":"4da3d7554ee7da9bec1af8f74ccea24b824854bb","read_at_kst":"N/A","status":"VERIFIED","reason":"NONE"},
        {"role":"OUTPUT","repository":"totjae/dmi-agent-2","path":"templates/OUTPUT.md","commit_sha":"33e0219eb1dba7fa0a89d42f38add6c2cae4ed01","blob_sha":"cafb325fcc6f5497c631849517849f7c24ae7a3d","read_at_kst":"2026-09-18T03:34:14+09:00","status":"VERIFIED","reason":"NONE"}
      ],"version_status":"VERIFIED"
    },
    {
      "input_id":"A1_0830","agent_id":"AGENT_1","date":"2026-09-18","slot_kst":"08:30","repository":"totjae/dmi-agent-1","path":"runs/2026-09-18/0830.md",
      "evaluated_commit_sha":"4ddc85abd62d32b1f83524ff02e003fcc1b50149","evaluated_blob_sha":"ef079541c090987a63c2fecf7ae63059f23bff37",
      "first_saved_commit_sha":"4ddc85abd62d32b1f83524ff02e003fcc1b50149","first_saved_at_kst":"2026-09-18T08:26:09+09:00",
      "selection_status":"OFFICIAL","selection_reason":"VALID_SCHEMA_AND_SAVED_BEFORE_KRX_OPEN_09:00","prediction_schema_version":"DMI_AGENT_v1.3",
      "prediction_document_versions":[
        {"role":"WORKFLOW","repository":"totjae/dmi-agent-1","path":"WORKFLOW.md","commit_sha":"037d96493f9b921a8924f73a362794385d664cac","blob_sha":"8a25e4fe9ce2e66b516a189b78def10ba4281ad1","read_at_kst":"N/A","status":"VERIFIED","reason":"NONE"},
        {"role":"AGENT_PROMPT","repository":"totjae/dmi-agent-1","path":"prompt/AGENT_PROMPT.md","commit_sha":"5d550e1c78d8ce46db587f77f5d9b84b7b4aa81a","blob_sha":"a44b95f40710db6c56b8916b8aabce89d1654633","read_at_kst":"N/A","status":"VERIFIED","reason":"NONE"},
        {"role":"OUTPUT","repository":"totjae/dmi-agent-1","path":"templates/OUTPUT.md","commit_sha":"10d0d7f095df47ff74912df15d94580f3945e883","blob_sha":"cafb325fcc6f5497c631849517849f7c24ae7a3d","read_at_kst":"2026-09-18T08:25:11+09:00","status":"VERIFIED","reason":"NONE"}
      ],"version_status":"VERIFIED"
    },
    {
      "input_id":"A2_0830","agent_id":"AGENT_2","date":"2026-09-18","slot_kst":"08:30","repository":"totjae/dmi-agent-2","path":"runs/2026-09-18/0830.md",
      "evaluated_commit_sha":"56cfe872b1c993ecec26e725096799411162a0ba","evaluated_blob_sha":"2edd073ed4453ccbfdaa19d12211949139f8c331",
      "first_saved_commit_sha":"56cfe872b1c993ecec26e725096799411162a0ba","first_saved_at_kst":"2026-09-18T08:32:07+09:00",
      "selection_status":"OFFICIAL","selection_reason":"VALID_SCHEMA_AND_SAVED_BEFORE_KRX_OPEN_09:00","prediction_schema_version":"DMI_AGENT_v1.3",
      "prediction_document_versions":[
        {"role":"WORKFLOW","repository":"totjae/dmi-agent-2","path":"WORKFLOW.md","commit_sha":"0daff2c0d84b0b60314d501aed3ab092a8bedc2b","blob_sha":"1f863cf6d2ce2fc3b347609845906d1d0ed56815","read_at_kst":"N/A","status":"VERIFIED","reason":"NONE"},
        {"role":"AGENT_PROMPT","repository":"totjae/dmi-agent-2","path":"prompt/AGENT_PROMPT.md","commit_sha":"3e833704e8c858df544bb8b06a5273e4ec95d26c","blob_sha":"4da3d7554ee7da9bec1af8f74ccea24b824854bb","read_at_kst":"N/A","status":"VERIFIED","reason":"NONE"},
        {"role":"OUTPUT","repository":"totjae/dmi-agent-2","path":"templates/OUTPUT.md","commit_sha":"33e0219eb1dba7fa0a89d42f38add6c2cae4ed01","blob_sha":"cafb325fcc6f5497c631849517849f7c24ae7a3d","read_at_kst":"2026-09-18T08:30:34+09:00","status":"VERIFIED","reason":"NONE"}
      ],"version_status":"VERIFIED"
    }
  ],
  "price_sources": [
    {"source_id":"PX_LNF_20260918","provider":"매일경제 마켓(KRX 시세 표시)","url":"https://stock.mk.co.kr/price/home/KR7066970005","retrieved_at_kst":"2026-09-18T16:30:12+09:00","observation_date":"2026-09-18","venue":"KRX","session":"REGULAR","currency":"KRW","adjustment_basis":"RAW_UNADJUSTED","status":"VERIFIED","reason":"09.18 15:33 표시와 전일 종가·정규장 OHLC 확인"},
    {"source_id":"PX_SKH_20260918","provider":"매일경제 마켓(KRX 시세 표시)","url":"https://stock.mk.co.kr/price/home/KR7000660001","retrieved_at_kst":"2026-09-18T16:30:12+09:00","observation_date":"2026-09-18","venue":"KRX","session":"REGULAR","currency":"KRW","adjustment_basis":"RAW_UNADJUSTED","status":"VERIFIED","reason":"09.18 15:33 표시와 전일 종가·정규장 OHLC 확인"}
  ],
  "candidates": [
    {
      "input_id":"A1_0330","rank":1,"code":"066970","name":"엘앤에프","market":"KOSPI","evaluation_scope":"OFFICIAL",
      "prices":{"previous_close":{"value":111300,"source_ids":["PX_LNF_20260918"]},"open":{"value":114800,"source_ids":["PX_LNF_20260918"]},"high":{"value":115200,"source_ids":["PX_LNF_20260918"]},"low":{"value":110100,"source_ids":["PX_LNF_20260918"]},"close":{"value":111000,"source_ids":["PX_LNF_20260918"]}},
      "metrics_pct":{"c2c":-0.2695417789757413,"o2c":-3.3101045296167246,"fe":3.5040431266846364,"ofe":0.34843205574912894,"ae":1.078167115902965},
      "hits":{"fe3":true,"fe5":false,"fe10":false},"expected_fe_range_match":true,
      "trade_plan":{"status":"NOT_PROVIDED","report_reference":"Agent 1 03:30 후보 상세 1위","reason":"관찰 상태이며 수치 진입 계획이 제공되지 않음","evidence_urls":[]},
      "missing_reasons":[]
    },
    {
      "input_id":"A2_0330","rank":1,"code":"066970","name":"엘앤에프","market":"KOSPI","evaluation_scope":"OFFICIAL",
      "prices":{"previous_close":{"value":111300,"source_ids":["PX_LNF_20260918"]},"open":{"value":114800,"source_ids":["PX_LNF_20260918"]},"high":{"value":115200,"source_ids":["PX_LNF_20260918"]},"low":{"value":110100,"source_ids":["PX_LNF_20260918"]},"close":{"value":111000,"source_ids":["PX_LNF_20260918"]}},
      "metrics_pct":{"c2c":-0.2695417789757413,"o2c":-3.3101045296167246,"fe":3.5040431266846364,"ofe":0.34843205574912894,"ae":1.078167115902965},
      "hits":{"fe3":true,"fe5":false,"fe10":false},"expected_fe_range_match":false,
      "trade_plan":{"status":"NOT_SCORABLE","report_reference":"Agent 2 03:30 CANDIDATE_DETAIL Rank 1","reason":"일봉 OHLC로 거래 증가·회복 유지·갭 추격 중단 조건의 시간순서를 판정할 수 없음","evidence_urls":["https://stock.mk.co.kr/price/home/KR7066970005"]},
      "missing_reasons":[]
    },
    {
      "input_id":"A2_0330","rank":2,"code":"000660","name":"SK하이닉스","market":"KOSPI","evaluation_scope":"OFFICIAL",
      "prices":{"previous_close":{"value":1745000,"source_ids":["PX_SKH_20260918"]},"open":{"value":1810000,"source_ids":["PX_SKH_20260918"]},"high":{"value":1857000,"source_ids":["PX_SKH_20260918"]},"low":{"value":1805000,"source_ids":["PX_SKH_20260918"]},"close":{"value":1857000,"source_ids":["PX_SKH_20260918"]}},
      "metrics_pct":{"c2c":6.418338108882521,"o2c":2.5966850828729284,"fe":6.418338108882521,"ofe":2.5966850828729284,"ae":0},
      "hits":{"fe3":true,"fe5":true,"fe10":false},"expected_fe_range_match":false,
      "trade_plan":{"status":"NOT_PROVIDED","report_reference":"Agent 2 03:30 CANDIDATE_DETAIL Rank 2","reason":"관찰 상태이며 수치 진입·손절·목표 계획을 보류함","evidence_urls":[]},
      "missing_reasons":[]
    },
    {
      "input_id":"A1_0830","rank":1,"code":"066970","name":"엘앤에프","market":"KOSPI","evaluation_scope":"OFFICIAL",
      "prices":{"previous_close":{"value":111300,"source_ids":["PX_LNF_20260918"]},"open":{"value":114800,"source_ids":["PX_LNF_20260918"]},"high":{"value":115200,"source_ids":["PX_LNF_20260918"]},"low":{"value":110100,"source_ids":["PX_LNF_20260918"]},"close":{"value":111000,"source_ids":["PX_LNF_20260918"]}},
      "metrics_pct":{"c2c":-0.2695417789757413,"o2c":-3.3101045296167246,"fe":3.5040431266846364,"ofe":0.34843205574912894,"ae":1.078167115902965},
      "hits":{"fe3":true,"fe5":false,"fe10":false},"expected_fe_range_match":false,
      "trade_plan":{"status":"NOT_PROVIDED","report_reference":"Agent 1 08:30 CANDIDATE_DETAIL Rank 1","reason":"관찰 상태이며 수치 진입 계획이 제공되지 않음","evidence_urls":[]},
      "missing_reasons":[]
    },
    {
      "input_id":"A1_0830","rank":2,"code":"000660","name":"SK하이닉스","market":"KOSPI","evaluation_scope":"OFFICIAL",
      "prices":{"previous_close":{"value":1745000,"source_ids":["PX_SKH_20260918"]},"open":{"value":1810000,"source_ids":["PX_SKH_20260918"]},"high":{"value":1857000,"source_ids":["PX_SKH_20260918"]},"low":{"value":1805000,"source_ids":["PX_SKH_20260918"]},"close":{"value":1857000,"source_ids":["PX_SKH_20260918"]}},
      "metrics_pct":{"c2c":6.418338108882521,"o2c":2.5966850828729284,"fe":6.418338108882521,"ofe":2.5966850828729284,"ae":0},
      "hits":{"fe3":true,"fe5":true,"fe10":false},"expected_fe_range_match":false,
      "trade_plan":{"status":"NOT_PROVIDED","report_reference":"Agent 1 08:30 CANDIDATE_DETAIL Rank 2","reason":"관찰 상태이며 수치 진입 계획이 제공되지 않음","evidence_urls":[]},
      "missing_reasons":[]
    },
    {
      "input_id":"A2_0830","rank":1,"code":"066970","name":"엘앤에프","market":"KOSPI","evaluation_scope":"OFFICIAL",
      "prices":{"previous_close":{"value":111300,"source_ids":["PX_LNF_20260918"]},"open":{"value":114800,"source_ids":["PX_LNF_20260918"]},"high":{"value":115200,"source_ids":["PX_LNF_20260918"]},"low":{"value":110100,"source_ids":["PX_LNF_20260918"]},"close":{"value":111000,"source_ids":["PX_LNF_20260918"]}},
      "metrics_pct":{"c2c":-0.2695417789757413,"o2c":-3.3101045296167246,"fe":3.5040431266846364,"ofe":0.34843205574912894,"ae":1.078167115902965},
      "hits":{"fe3":true,"fe5":false,"fe10":false},"expected_fe_range_match":false,
      "trade_plan":{"status":"NOT_SCORABLE","report_reference":"Agent 2 08:30 CANDIDATE_DETAIL Rank 1","reason":"일봉 OHLC로 돌파 후 되돌림 지지와 거래 증가의 시간순서를 판정할 수 없음","evidence_urls":["https://stock.mk.co.kr/price/home/KR7066970005"]},
      "missing_reasons":[]
    },
    {
      "input_id":"A2_0830","rank":2,"code":"000660","name":"SK하이닉스","market":"KOSPI","evaluation_scope":"OFFICIAL",
      "prices":{"previous_close":{"value":1745000,"source_ids":["PX_SKH_20260918"]},"open":{"value":1810000,"source_ids":["PX_SKH_20260918"]},"high":{"value":1857000,"source_ids":["PX_SKH_20260918"]},"low":{"value":1805000,"source_ids":["PX_SKH_20260918"]},"close":{"value":1857000,"source_ids":["PX_SKH_20260918"]}},
      "metrics_pct":{"c2c":6.418338108882521,"o2c":2.5966850828729284,"fe":6.418338108882521,"ofe":2.5966850828729284,"ae":0},
      "hits":{"fe3":true,"fe5":true,"fe10":false},"expected_fe_range_match":false,
      "trade_plan":{"status":"NOT_SCORABLE","report_reference":"Agent 2 08:30 CANDIDATE_DETAIL Rank 2","reason":"일봉 OHLC로 거래량 증가와 1,785,000원 회복·지지의 시간순서를 판정할 수 없음","evidence_urls":["https://stock.mk.co.kr/price/home/KR7000660001"]},
      "missing_reasons":[]
    }
  ]
}
[/REVIEW_EVIDENCE]
