[DMI_REVIEW_META]
SCHEMA_VERSION: DMI_REVIEW_v1.3
DATE: 2026-09-14
PREDICTION_RUN_TIMES_KST: [03:30, 08:30]
REVIEW_TIME_KST: 16:30
STARTED_AT_KST: 2026-09-14T16:34:26+09:00
REPORT_COMPLETED_AT_KST: 2026-09-14T16:42:31+09:00
DATA_CUTOFF_KST: 2026-09-14T16:42:14+09:00
SOURCE_MANIFEST: REVIEW_EVIDENCE.input_manifest
REVIEW_DOCUMENT_VERSIONS: REVIEW_EVIDENCE.review_document_versions
RUN_TYPE: NORMAL
RERUN_SEQUENCE: 0
[/DMI_REVIEW_META]

[REVIEW_REPORT]
# DMI Two-Agent Review — 2026-09-14
## 1. 공식 입력 검증
[한국거래소 공식 거래안내](https://global.krx.co.kr/contents/GLB/01/0109/0109000000/guide_to_trading_in_the_korean_stock_market.pdf)에 따르면 당일 통상 정규장은 **09:00~15:30 KST**이고 시간외 거래는 별도다. 월요일 9월 14일 정규 거래 기준으로 입력의 GitHub 최초 *생성* commit 및 당시 본문을 확인했다. 아래 입력의 자체기입 완료시각은 채택 근거로 사용하지 않았다.

| 슬롯 | Agent 1 | Agent 2 | 공식 비교 |
|---|---|---|---|
| 03:30 | UNAVAILABLE, COUNT N/A: 9월 14일 저장 폴더에 0330 및 rerun 파일 없음 | UNAVAILABLE, COUNT N/A: 같은 사유 | N/A, 양쪽 유효 표본 0그룹 |
| 08:30 | OFFICIAL, TOP 2: [처음 추가한 commit](https://github.com/totjae/dmi-agent-1/commit/2269b4530883cfcf9f70de111b57943c7adb67a7) 08:28:04 KST, [검증한 본문](https://github.com/totjae/dmi-agent-1/blob/2269b4530883cfcf9f70de111b57943c7adb67a7/runs/2026-09-14/0830.md) | OFFICIAL, TOP 1: [처음 추가한 commit](https://github.com/totjae/dmi-agent-2/commit/693b7f24920442dd357469732f5edd1f84c46fd1) 08:32:03 KST, [검증한 본문](https://github.com/totjae/dmi-agent-2/blob/693b7f24920442dd357469732f5edd1f84c46fd1/runs/2026-09-14/0830.md) | 유효 2그룹·총 3후보 |

두 저장소의 지정 날짜 디렉터리에는 0830.md만 있었고 그 파일의 전체 path별 commit 이력은 각각 위 신규 추가 1건뿐이다. 따라서 동일 슬롯의 선택에서 배제할 rerun/수정본은 발견되지 않았다. 두 입력은 v1.3의 META/REPORT/RESULT와 DATE·RUN_TIME, TOP_COUNT, 순위·코드·이름 및 요약/본문 정합성을 통과했다. 입력 원문 DOCUMENT_VERSIONS는 아래 evidence에 그대로 보존했다. 각각 문서 blob SHA만 확인돼 있고 입력 자체는 문서 commit·열람시각이 N/A여서 **문서 버전 묶음은 UNVERIFIED**; 공식 입력의 장전 저장·가격 평가 자격을 이 사실만으로 없애지 않는다.

## 2. 정규장 Ground Truth
가격은 원화 명목 표시 가격이며, 서로 다른 거래소의 NXT 가격이나 15:30 이후 단일가를 정규장 종가로 혼합하지 않았다. 단위 원; FE는 전일 정규장 종가 대비 **당일 고가**, 매매 수익률이 아니다. 자료제공자 원시 KRX 추출 파일과 기업행사 이력은 별도 대조하지 않았으나 당일 표시 전일가가 전 거래일의 일별 종가와 일치한다.

| 종목 (코드) | 9/11 종가 P | 9/14 시가 O | 고가 H | 저가 L | 정규장 종가 C | 가격 근거 |
|---|---:|---:|---:|---:|---:|---|
| 삼성전기 (009150) | 1,400,000 | 1,355,000 | 1,360,000 | 1,318,000 | 1,337,000 | [회사 IR 9/11](https://m.samsungsem.com/kr/about-us/investor-relations/stock.do), [Google KRX 9/14 15:30:21](https://www.google.com/finance/quote/009150:KRX?hl=ko) |
| 삼화콘덴서 (001820) | 137,400 | 132,600 | 143,700 | 130,600 | 139,200 | [9/11 일별 자료](https://alphasquare.co.kr/home/stock-summary?code=001820), [Google KRX 9/14 15:30:16](https://www.google.com/finance/quote/001820:KRX?hl=ko) |
| 흥아해운 (003280) | 1,878 | 1,909 | 1,961 | 1,831 | 1,836 | [MK KRX 9/14 15:33, 15:30:01 종가 체결](https://stock.mk.co.kr/price/home/KR7003280005) |

삼성전기 회사 IR의 16:15 표시 1,329,000원, 삼화콘덴서의 변동하는 장후 실시간 표시값은 **9/14 정규장 종가로 채택하지 않았다**. 정규장 종료 시각이 명시된 시세를 우선했다. 날짜·세션·관측시각·가격별 링크는 REVIEW_EVIDENCE.price_sources와 candidates.prices에 있다. 코스피는 [MK 시장 화면](https://stock.mk.co.kr/price/home/KR7003280005) 기준 9/14 약 3.3% 하락해 광범위한 위험회피 환경이었다.

## 3. 후보별 성과 — 08:30 공식 입력만
| 에이전트·원래 Rank | 후보·예상 FE·확신도 | C2C | O2C | FE | OFE | AE | FE3/5/10 | 예상구간 적합 |
|---|---|---:|---:|---:|---:|---:|---|---|
| A1·1 | 삼성전기 +3~5%, LOW·관찰 | -4.50% | -1.33% | -2.86% | 0.37% | 5.86% | 실패/실패/실패 | 불일치: 실제 FE가 음수 |
| A1·2 | 삼화콘덴서 +5~10%, LOW·고위험 관찰 | 1.31% | 4.98% | 4.59% | 8.37% | 4.95% | 적중/실패/실패 | 불일치: FE 5% 미만 |
| A2·1 | 흥아해운 UNCERTAIN, LOW·관찰 | -2.24% | -3.82% | 4.42% | 2.72% | 2.50% | 적중/실패/실패 | N/A (예상 FE 미제공) |

C2C=(C−P)/P, O2C=(C−O)/O, FE=(H−P)/P, OFE=(H−O)/O, AE=max(0,(P−L)/P); % 표시만 소수 둘째 자리 반올림. AE는 전일 종가 기준 낙폭이지 실제 거래 손실이 아니다. **관찰** 상태는 종목 발굴 표본에는 들어가나 매수·체결을 뜻하지 않는다. 모든 후보의 조건부 계획은 일봉만으로 거래량·시간순서·진입/목표/손절 충족을 확정할 수 없으므로 NOT_SCORABLE; A2의 2,080원은 저항 참고값, 예상 FE나 목표가가 아니다.

## 4. 에이전트별 KPI — 08:30
아래 평균 FE/OFE/AE는 전체 후보 및 TOP3에 **동일**하다. 두 후보군 모두 TOP_COUNT≤3이기 때문이며 원래 후보 수를 줄이지 않았다. 각 평균의 유효수는 Agent 1 FE/OFE/AE 모두 2/2, Agent 2 모두 1/1이다. TOP1 OFE는 Agent 1 0.37%, Agent 2 2.72%.

| 08:30 공식 입력 | TOP1 FE | TOP3=전체 평균 FE | 평균 OFE | 평균 AE | FE3 | FE5 | FE10 | Rank-FE Spearman |
|---|---:|---:|---:|---:|---:|---:|---:|---|
| Agent 1 (n=2) | -2.86% | 0.86% | 4.37% | 5.40% | 1/2 (50.00%) | 0/2 | 0/2 | -1.000 (2쌍) |
| Agent 2 (n=1) | 4.42% | 4.42% | 2.72% | 2.50% | 1/1 (100.00%) | 0/1 | 0/1 | N/A (1쌍) |

TOP1 유효 FE/OFE는 A1 1/1, A2 1/1. FE 적중률 분모 A1=2, A2=1. A1의 Rank-실제 FE 순서는 1·2 vs 2·1로 Spearman -1.000 (2쌍), A2는 1쌍뿐이므로 N/A이며 0으로 취급하지 않는다. 예상구간 적합은 A1 0/2=0.00%, A2는 예상값 UNCERTAIN으로 0/0=N/A. LOW 확신도 발굴 관찰은 A1 n=2 (FE 평균 0.86%), A2 n=1 (FE 4.42%); LOW를 예측확률로 바꾸지 않는다. 03:30은 입력 자체가 없어 양 에이전트 COUNT와 공식 유효 FE 수 및 전 성과지표 N/A(후보 0개를 뜻하지 않음).

## 5. 비교, 판단 오류와 개선 후보
**03:30 Agent 1 vs Agent 2:** 양쪽 입력 없음 → N/A, 승자 없음. **08:30:** A2가 TOP1/전체 FE(4.42% 대 -2.86% / 0.86%) 및 더 낮은 AE(2.50% 대 5.40%)에서 앞선 반면, A1은 시가 이후 OFE 평균(4.37% 대 2.72%)과 단일 최상위 FE 후보(삼화콘덴서 4.59%)를 확보했다. A1 TOP1 판단은 하위 후보보다 FE가 낮아 순위 반전이고, A2 종가는 시가보다 낮다. 서로 다른 n과 지표별 우열 교차로 **BEST_AGENT=MIXED**, 사전 정의되지 않은 종합 점수/당일 승자를 강제하지 않는다.

**같은 에이전트 03:30 vs 08:30:** 양쪽 다 오전 첫 슬롯 결과가 없어 시간대 간 정량 성능 비교 N/A. 두 번째 슬롯은 신규 정보 기반 독립 분석이지 첫 번째의 오류 복구나 대체가 아니다. 03:30과 08:30 후보는 합치지 않았다.

A1의 섹터 기대를 삼성전기 Rank 1로 전이한 가정은 당일 FE -2.86%와 종가 -4.50%로 지지받지 못했다. 반면 직전 거래 집중을 포착한 삼화콘덴서는 FE 4.59% 및 OFE 8.37%가 있었지만 예상 최소 +5%에는 못 미쳤다. A2의 해운 뉴스는 흥아해운 FE 4.42%라는 장중 관심 가능성과 부합하지만 종가는 -2.24%로 밀렸고 실제 운임 수혜·매매 성공은 입증하지 않는다. 모두 가격 반영과 개장 후 남은 여력을 구분할 필요가 있다.

**검토만 할 개선 후보:** (1) 테마 업황 근거를 개별 기업 종가 보합에 곧바로 확대하기 전에 상대강도·시장 전체 위험회피를 별도 평가. 기대효과: 삼성전기형 상위 순위 오판 줄일 수 있음; 부작용: 지연 반등 첫날을 놓칠 수 있음. (2) 장전 범위 예측에서 직전 큰 거래·고가 후 후퇴와 갭/시가 대비 여력을 별개 변수로 두기. 기대효과: FE와 실제 매매 가능성 혼동 감소; 부작용: 유효한 강세 지속을 과소평가할 수 있음. **한 거래일의 관찰만으로 프롬프트·규칙을 바꾸거나 자동 적용하지 않는다.**

## 6. 요약
공식 4조합 중 08:30 2조합만 유효(총 3후보), 03:30 2조합은 누락이다. 단일 최상위 FE는 A1의 삼화콘덴서 4.59%이나 A2의 좁은 1개 후보 집합과 A1의 2개 후보 집합의 전체 FE를 함께 볼 때 지표 우열이 섞여 일일 우승자를 확정할 수 없다. 종가·고가는 거래 실현 수익이 아니며 시간외 가격을 정규장 종가로 대체하지 않았다.

[REVIEW_RESULT]
SCHEMA_VERSION: DMI_REVIEW_v1.3
DATE: 2026-09-14
PREDICTION_RUN_TIME_KST: 03:30
AGENT_1_STATUS: UNAVAILABLE
AGENT_2_STATUS: UNAVAILABLE
AGENT_1_COUNT: N/A
AGENT_2_COUNT: N/A
AGENT_1_TOP1_FE: N/A
AGENT_2_TOP1_FE: N/A
AGENT_1_TOP3_AVG_FE: N/A
AGENT_2_TOP3_AVG_FE: N/A
AGENT_1_FE3_HIT_RATE: N/A
AGENT_2_FE3_HIT_RATE: N/A
AGENT_1_FE5_HIT_RATE: N/A
AGENT_2_FE5_HIT_RATE: N/A
AGENT_1_FE10_HIT_RATE: N/A
AGENT_2_FE10_HIT_RATE: N/A
AGENT_1_VALID_FE_COUNT: N/A
AGENT_2_VALID_FE_COUNT: N/A
AGENT_1_TOP3_VALID_FE_COUNT: N/A
AGENT_2_TOP3_VALID_FE_COUNT: N/A
AGENT_1_RANK_PERFORMANCE_SPEARMAN: N/A
AGENT_2_RANK_PERFORMANCE_SPEARMAN: N/A
AGENT_1_RANK_PERFORMANCE_PAIR_COUNT: N/A
AGENT_2_RANK_PERFORMANCE_PAIR_COUNT: N/A
BEST_AGENT: N/A
BEST_PICK: N/A
PRIMARY_SUCCESS_PATTERN: N/A (공식 입력 0/2그룹)
PRIMARY_ERROR_PATTERN: 03:30 입력 2개 누락; 성과 실패 또는 TOP_COUNT=0으로 간주하지 않음
IMPROVEMENT_CANDIDATE: 입력 생성·저장 누락 원인 점검 제안만; 자동 변경 없음
[/REVIEW_RESULT]

[REVIEW_RESULT]
SCHEMA_VERSION: DMI_REVIEW_v1.3
DATE: 2026-09-14
PREDICTION_RUN_TIME_KST: 08:30
AGENT_1_STATUS: OFFICIAL
AGENT_2_STATUS: OFFICIAL
AGENT_1_COUNT: 2
AGENT_2_COUNT: 1
AGENT_1_TOP1_FE: -2.86%
AGENT_2_TOP1_FE: 4.42%
AGENT_1_TOP3_AVG_FE: 0.86%
AGENT_2_TOP3_AVG_FE: 4.42%
AGENT_1_FE3_HIT_RATE: 50.00%
AGENT_2_FE3_HIT_RATE: 100.00%
AGENT_1_FE5_HIT_RATE: 0.00%
AGENT_2_FE5_HIT_RATE: 0.00%
AGENT_1_FE10_HIT_RATE: 0.00%
AGENT_2_FE10_HIT_RATE: 0.00%
AGENT_1_VALID_FE_COUNT: 2
AGENT_2_VALID_FE_COUNT: 1
AGENT_1_TOP3_VALID_FE_COUNT: 2
AGENT_2_TOP3_VALID_FE_COUNT: 1
AGENT_1_RANK_PERFORMANCE_SPEARMAN: -1.000
AGENT_2_RANK_PERFORMANCE_SPEARMAN: N/A
AGENT_1_RANK_PERFORMANCE_PAIR_COUNT: 2
AGENT_2_RANK_PERFORMANCE_PAIR_COUNT: 1
BEST_AGENT: MIXED
BEST_PICK: 삼화콘덴서(001820), FE 4.59% (개별 후보 최고 FE이며 실행 매수 제안 아님)
PRIMARY_SUCCESS_PATTERN: A1 하위 후보의 MLCC 후속 변동 및 A2 해운주 FE3 발굴
PRIMARY_ERROR_PATTERN: A1 1순위 실제 FE 음수와 순위 반전; A2 종가 시가 하회, 매매 계획 미평가
IMPROVEMENT_CANDIDATE: 가격반영·시장 위험회피와 개장 후 여력 분리 평가 검토만; 자동 적용 없음
[/REVIEW_RESULT]
[/REVIEW_REPORT]

[REVIEW_EVIDENCE]
{
  "schema_version": "DMI_REVIEW_EVIDENCE_v1",
  "review_document_versions": [
    {
      "role": "WORKFLOW",
      "repository": "totjae/dmi-market-pipeline",
      "path": "WORKFLOW.md",
      "commit_sha": null,
      "blob_sha": "f7d593b7f558c95df45ad802b1489591cb726151",
      "read_at_kst": null,
      "status": "VERIFIED",
      "reason": "Path and blob SHA verified on default branch; exact read time and document commit not captured."
    },
    {
      "role": "SOURCES",
      "repository": "totjae/dmi-market-pipeline",
      "path": "config/SOURCES.md",
      "commit_sha": null,
      "blob_sha": "5c47de7afdb65f60bc81a0050058a4c71d332853",
      "read_at_kst": null,
      "status": "VERIFIED",
      "reason": "Path and blob SHA verified on default branch; exact read time and document commit not captured."
    },
    {
      "role": "REVIEW_PROMPT",
      "repository": "totjae/dmi-market-pipeline",
      "path": "prompt/REVIEW_PROMPT.md",
      "commit_sha": null,
      "blob_sha": "fbd5f2e1f490a2b5a68ae8b095b58bccbbc19cb2",
      "read_at_kst": null,
      "status": "VERIFIED",
      "reason": "Path and blob SHA verified on default branch; exact read time and document commit not captured."
    },
    {
      "role": "REVIEW_OUTPUT",
      "repository": "totjae/dmi-market-pipeline",
      "path": "templates/REVIEW_OUTPUT.md",
      "commit_sha": null,
      "blob_sha": "aced9658e7423ac059150f7d5cdf069efce21849",
      "read_at_kst": null,
      "status": "VERIFIED",
      "reason": "Path and blob SHA verified on default branch; exact read time and document commit not captured."
    }
  ],
  "input_manifest": [
    {
      "input_id": "A1_0330",
      "agent_id": "AGENT_1",
      "date": "2026-09-14",
      "slot_kst": "03:30",
      "repository": "totjae/dmi-agent-1",
      "path": "runs/2026-09-14/0330.md",
      "evaluated_commit_sha": null,
      "evaluated_blob_sha": null,
      "first_saved_commit_sha": null,
      "first_saved_at_kst": null,
      "selection_status": "UNAVAILABLE",
      "selection_reason": "MISSING_FILE; DATE_SLOT_DIRECTORY_CONTAINS_ONLY_0830_FILE",
      "prediction_schema_version": null,
      "prediction_document_versions": null,
      "version_status": null
    },
    {
      "input_id": "A1_0830",
      "agent_id": "AGENT_1",
      "date": "2026-09-14",
      "slot_kst": "08:30",
      "repository": "totjae/dmi-agent-1",
      "path": "runs/2026-09-14/0830.md",
      "evaluated_commit_sha": "2269b4530883cfcf9f70de111b57943c7adb67a7",
      "evaluated_blob_sha": "da027cdf91450a7d0b1b7d3151b1016f415b419e",
      "first_saved_commit_sha": "2269b4530883cfcf9f70de111b57943c7adb67a7",
      "first_saved_at_kst": "2026-09-14T08:28:04+09:00",
      "selection_status": "OFFICIAL",
      "selection_reason": "FIRST_VALID_FILE; ADDED_AT_COMMIT; BEFORE_KRX_OPEN_09:00; NO_OTHER_DATE_SLOT_FILES",
      "prediction_schema_version": "DMI_AGENT_v1.3",
      "prediction_document_versions": [
        {
          "role": "WORKFLOW",
          "repository": "totjae/dmi-agent-1",
          "path": "WORKFLOW.md",
          "commit_sha": "N/A",
          "blob_sha": "8a25e4fe9ce2e66b516a189b78def10ba4281ad1",
          "read_at_kst": "N/A",
          "status": "VERIFIED",
          "reason": "NONE"
        },
        {
          "role": "AGENT_PROMPT",
          "repository": "totjae/dmi-agent-1",
          "path": "prompt/AGENT_PROMPT.md",
          "commit_sha": "N/A",
          "blob_sha": "a44b95f40710db6c56b8916b8aabce89d1654633",
          "read_at_kst": "N/A",
          "status": "VERIFIED",
          "reason": "NONE"
        },
        {
          "role": "OUTPUT",
          "repository": "totjae/dmi-agent-1",
          "path": "templates/OUTPUT.md",
          "commit_sha": "N/A",
          "blob_sha": "cafb325fcc6f5497c631849517849f7c24ae7a3d",
          "read_at_kst": "N/A",
          "status": "VERIFIED",
          "reason": "NONE"
        }
      ],
      "version_status": "UNVERIFIED"
    },
    {
      "input_id": "A2_0330",
      "agent_id": "AGENT_2",
      "date": "2026-09-14",
      "slot_kst": "03:30",
      "repository": "totjae/dmi-agent-2",
      "path": "runs/2026-09-14/0330.md",
      "evaluated_commit_sha": null,
      "evaluated_blob_sha": null,
      "first_saved_commit_sha": null,
      "first_saved_at_kst": null,
      "selection_status": "UNAVAILABLE",
      "selection_reason": "MISSING_FILE; DATE_SLOT_DIRECTORY_CONTAINS_ONLY_0830_FILE",
      "prediction_schema_version": null,
      "prediction_document_versions": null,
      "version_status": null
    },
    {
      "input_id": "A2_0830",
      "agent_id": "AGENT_2",
      "date": "2026-09-14",
      "slot_kst": "08:30",
      "repository": "totjae/dmi-agent-2",
      "path": "runs/2026-09-14/0830.md",
      "evaluated_commit_sha": "693b7f24920442dd357469732f5edd1f84c46fd1",
      "evaluated_blob_sha": "dba1029b15a2c2c2b215c3ceea5c7e0ff68a43d0",
      "first_saved_commit_sha": "693b7f24920442dd357469732f5edd1f84c46fd1",
      "first_saved_at_kst": "2026-09-14T08:32:03+09:00",
      "selection_status": "OFFICIAL",
      "selection_reason": "FIRST_VALID_FILE; ADDED_AT_COMMIT; BEFORE_KRX_OPEN_09:00; NO_OTHER_DATE_SLOT_FILES",
      "prediction_schema_version": "DMI_AGENT_v1.3",
      "prediction_document_versions": [
        {
          "role": "WORKFLOW",
          "repository": "totjae/dmi-agent-2",
          "path": "WORKFLOW.md",
          "commit_sha": "N/A",
          "blob_sha": "1f863cf6d2ce2fc3b347609845906d1d0ed56815",
          "read_at_kst": "N/A",
          "status": "VERIFIED",
          "reason": "NONE"
        },
        {
          "role": "AGENT_PROMPT",
          "repository": "totjae/dmi-agent-2",
          "path": "prompt/AGENT_PROMPT.md",
          "commit_sha": "N/A",
          "blob_sha": "4da3d7554ee7da9bec1af8f74ccea24b824854bb",
          "read_at_kst": "N/A",
          "status": "VERIFIED",
          "reason": "NONE"
        },
        {
          "role": "OUTPUT",
          "repository": "totjae/dmi-agent-2",
          "path": "templates/OUTPUT.md",
          "commit_sha": "N/A",
          "blob_sha": "cafb325fcc6f5497c631849517849f7c24ae7a3d",
          "read_at_kst": "N/A",
          "status": "VERIFIED",
          "reason": "NONE"
        }
      ],
      "version_status": "UNVERIFIED"
    }
  ],
  "price_sources": [
    {
      "source_id": "SEM_0911",
      "provider": "삼성전기 공식 IR",
      "url": "https://m.samsungsem.com/kr/about-us/investor-relations/stock.do",
      "retrieved_at_kst": null,
      "observation_date": "2026-09-11",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": "Displayed nominal KRW price (not separately adjusted); previous close reconciled with same-day previous/change or dated prior quote; no corporate-action discrepancy observed.",
      "status": "VERIFIED",
      "reason": "일자별시세 26/09/11 종가 1,400,000원; exchange raw file and corporate-action history not independently audited. Exact lookup timestamp was not recorded; quotes display dated session time."
    },
    {
      "source_id": "SEM_0914",
      "provider": "Google Finance, 009150:KRX",
      "url": "https://www.google.com/finance/quote/009150:KRX?hl=ko",
      "retrieved_at_kst": null,
      "observation_date": "2026-09-14",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": "Displayed nominal KRW price (not separately adjusted); previous close reconciled with same-day previous/change or dated prior quote; no corporate-action discrepancy observed.",
      "status": "VERIFIED",
      "reason": "9월 14일 15:30:21 KST 표기 현재가 1,337,000원 및 시가/고가/저가; exchange raw file and corporate-action history not independently audited. Exact lookup timestamp was not recorded; quotes display dated session time."
    },
    {
      "source_id": "SHA_0911",
      "provider": "알파스퀘어 KRX 일별시세",
      "url": "https://alphasquare.co.kr/home/stock-summary?code=001820",
      "retrieved_at_kst": null,
      "observation_date": "2026-09-11",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": "Displayed nominal KRW price (not separately adjusted); previous close reconciled with same-day previous/change or dated prior quote; no corporate-action discrepancy observed.",
      "status": "VERIFIED",
      "reason": "2026.09.11 일별시세 종가 137,400원; exchange raw file and corporate-action history not independently audited. Exact lookup timestamp was not recorded; quotes display dated session time."
    },
    {
      "source_id": "SHA_0914",
      "provider": "Google Finance, 001820:KRX",
      "url": "https://www.google.com/finance/quote/001820:KRX?hl=ko",
      "retrieved_at_kst": null,
      "observation_date": "2026-09-14",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": "Displayed nominal KRW price (not separately adjusted); previous close reconciled with same-day previous/change or dated prior quote; no corporate-action discrepancy observed.",
      "status": "VERIFIED",
      "reason": "9월 14일 15:30:16 KST 표기 현재가 139,200원 및 시가/고가/저가; exchange raw file and corporate-action history not independently audited. Exact lookup timestamp was not recorded; quotes display dated session time."
    },
    {
      "source_id": "HEU_0914",
      "provider": "매일경제 마켓 KRX 시세",
      "url": "https://stock.mk.co.kr/price/home/KR7003280005",
      "retrieved_at_kst": null,
      "observation_date": "2026-09-14",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": "Displayed nominal KRW price (not separately adjusted); previous close reconciled with same-day previous/change or dated prior quote; no corporate-action discrepancy observed.",
      "status": "VERIFIED",
      "reason": "09.14 15:33 KST, 전일·시가·고가·저가·종가 및 15:30:01 종가 체결 기록; exchange raw file and corporate-action history not independently audited. Exact lookup timestamp was not recorded; quotes display dated session time."
    }
  ],
  "candidates": [
    {
      "input_id": "A1_0830",
      "rank": 1,
      "code": "009150",
      "name": "삼성전기",
      "market": "KOSPI",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 1400000,
          "source_ids": [
            "SEM_0911"
          ]
        },
        "open": {
          "value": 1355000,
          "source_ids": [
            "SEM_0914"
          ]
        },
        "high": {
          "value": 1360000,
          "source_ids": [
            "SEM_0914"
          ]
        },
        "low": {
          "value": 1318000,
          "source_ids": [
            "SEM_0914"
          ]
        },
        "close": {
          "value": 1337000,
          "source_ids": [
            "SEM_0914"
          ]
        }
      },
      "metrics_pct": {
        "c2c": -4.5,
        "o2c": -1.3284132841328413,
        "fe": -2.857142857142857,
        "ofe": 0.36900369003690037,
        "ae": 5.857142857142858
      },
      "hits": {
        "fe3": false,
        "fe5": false,
        "fe10": false
      },
      "expected_fe_range_match": false,
      "trade_plan": {
        "status": "NOT_SCORABLE",
        "report_reference": "STAGE_REPORT > 후보별 근거 > 1. 삼성전기; STAGE_RESULT > CANDIDATE_DETAIL Rank 1",
        "reason": "Observation-only; no executable entry, target or stop, and daily OHLC cannot establish intraday condition sequence or fills.",
        "evidence_urls": []
      },
      "missing_reasons": []
    },
    {
      "input_id": "A1_0830",
      "rank": 2,
      "code": "001820",
      "name": "삼화콘덴서",
      "market": "KOSPI",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 137400,
          "source_ids": [
            "SHA_0911"
          ]
        },
        "open": {
          "value": 132600,
          "source_ids": [
            "SHA_0914"
          ]
        },
        "high": {
          "value": 143700,
          "source_ids": [
            "SHA_0914"
          ]
        },
        "low": {
          "value": 130600,
          "source_ids": [
            "SHA_0914"
          ]
        },
        "close": {
          "value": 139200,
          "source_ids": [
            "SHA_0914"
          ]
        }
      },
      "metrics_pct": {
        "c2c": 1.3100436681222707,
        "o2c": 4.97737556561086,
        "fe": 4.585152838427948,
        "ofe": 8.3710407239819,
        "ae": 4.9490538573508
      },
      "hits": {
        "fe3": true,
        "fe5": false,
        "fe10": false
      },
      "expected_fe_range_match": false,
      "trade_plan": {
        "status": "NOT_SCORABLE",
        "report_reference": "STAGE_REPORT > 후보별 근거 > 2. 삼화콘덴서; STAGE_RESULT > CANDIDATE_DETAIL Rank 2",
        "reason": "Observation-only; no executable entry, target or stop, and daily OHLC cannot establish intraday condition sequence or fills.",
        "evidence_urls": []
      },
      "missing_reasons": []
    },
    {
      "input_id": "A2_0830",
      "rank": 1,
      "code": "003280",
      "name": "흥아해운",
      "market": "KOSPI",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 1878,
          "source_ids": [
            "HEU_0914"
          ]
        },
        "open": {
          "value": 1909,
          "source_ids": [
            "HEU_0914"
          ]
        },
        "high": {
          "value": 1961,
          "source_ids": [
            "HEU_0914"
          ]
        },
        "low": {
          "value": 1831,
          "source_ids": [
            "HEU_0914"
          ]
        },
        "close": {
          "value": 1836,
          "source_ids": [
            "HEU_0914"
          ]
        }
      },
      "metrics_pct": {
        "c2c": -2.2364217252396164,
        "o2c": -3.823991618648507,
        "fe": 4.419595314164004,
        "ofe": 2.7239392352016765,
        "ae": 2.5026624068157615
      },
      "hits": {
        "fe3": true,
        "fe5": false,
        "fe10": false
      },
      "expected_fe_range_match": null,
      "trade_plan": {
        "status": "NOT_SCORABLE",
        "report_reference": "STAGE_REPORT > 종목별 판단 > 1. 흥아해운; STAGE_RESULT > CANDIDATE_DETAIL Rank 1",
        "reason": "Observation-only conditional rebound; no verified intraday sequence, volume, executable entry, stop or target; daily OHLC cannot establish fills.",
        "evidence_urls": []
      },
      "missing_reasons": [
        {
          "field": "expected_fe_range_match",
          "status": "UNCERTAIN",
          "reason": "Agent 2 explicitly marked ExpectedMoveFE as UNCERTAIN; reference price/resistance must not be converted to forecast range."
        }
      ]
    }
  ]
}
[/REVIEW_EVIDENCE]
