[DMI_REVIEW_META]
SCHEMA_VERSION: DMI_REVIEW_v1.3
DATE: 2026-09-11
PREDICTION_RUN_TIMES_KST: [03:30, 08:30]
REVIEW_TIME_KST: 16:30
STARTED_AT_KST: 2026-09-11T16:27:10+09:00
REPORT_COMPLETED_AT_KST: 2026-09-11T16:34:02+09:00
DATA_CUTOFF_KST: 2026-09-11T15:30:30+09:00
SOURCE_MANIFEST: REVIEW_EVIDENCE.input_manifest
REVIEW_DOCUMENT_VERSIONS: REVIEW_EVIDENCE.review_document_versions
RUN_TYPE: NORMAL
RERUN_SEQUENCE: 0
[/DMI_REVIEW_META]

[REVIEW_REPORT]
# DMI Two-Agent Review — 2026-09-11

## 공식 입력 선정

네 조합 모두 파일 최초 저장이 KRX 정규장 개장(09:00 KST) 전이고 스키마·날짜·슬롯·NORMAL/0가 유효하여 공식 입력으로 채택했다. Agent 2의 03:30 파일은 03:33:26 최초 revision을 평가했으며, 36초 뒤의 출처 링크 수정 revision으로 대체하지 않았다.

| 슬롯 | 입력 | 최초 저장(KST) | 공식 평가 commit | 후보 수 |
|---|---|---:|---|---:|
| 03:30 | Agent 1 | 03:28:40 | [783714a](https://github.com/totjae/dmi-agent-1/blob/783714a66b302886ba0570b27c46c0d95e9257cc/runs/2026-09-11/0330.md) | 3 |
| 03:30 | Agent 2 | 03:33:26 | [a9006c6](https://github.com/totjae/dmi-agent-2/blob/a9006c6b91a898b9516b4e92f10d45ccd29828db/runs/2026-09-11/0330.md) | 3 |
| 08:30 | Agent 1 | 08:28:51 | [6590443](https://github.com/totjae/dmi-agent-1/blob/6590443ac391a3edba72b4ed6035447d37a48dad/runs/2026-09-11/0830.md) | 3 |
| 08:30 | Agent 2 | 08:30:59 | [aab8760](https://github.com/totjae/dmi-agent-2/blob/aab87607f57807073bf8720d7dc695cb8dafeeb5/runs/2026-09-11/0830.md) | 2 |

입력의 DOCUMENT_VERSIONS는 원문 그대로 보존했다. 각 입력은 blob SHA를 제공하지만 일부 또는 전부의 문서 commit SHA가 N/A여서 입력 버전 상태는 UNVERIFIED다. 이는 후보 성과의 공식 채택을 취소하지 않는다.

## 확인된 정규장 데이터

| 종목 | 전일종가 | 시가 | 고가 | 저가 | 종가 | C2C | O2C | FE | OFE | AE |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 한국석유(004090) | 12,740 | 14,400 | 14,580 | 12,170 | 12,320 | -3.30% | -14.44% | 14.44% | 1.25% | 4.47% |
| 흥구석유(024060) | 14,510 | 17,010 | 17,310 | 14,600 | 14,610 | 0.69% | -14.11% | 19.30% | 1.76% | 0.00% |
| S-Oil(010950) | 154,900 | 155,800 | 155,800 | 147,300 | 150,000 | -3.16% | -3.72% | 0.58% | 0.00% | 4.91% |
| 중앙에너비스(000440) | 13,550 | 15,200 | 15,250 | 13,180 | 13,200 | -2.58% | -13.16% | 12.55% | 0.33% | 2.73% |
| SK하이닉스(000660) | 1,853,000 | 1,773,000 | 1,827,000 | 1,768,000 | 1,812,000 | -2.21% | 2.20% | -1.40% | 3.05% | 4.59% |

가격은 각 종목의 Google Finance KRX venue 표시에서 2026-09-11 정규장 KRW OHLC와 전일 종가를 확인했다: [한국석유](https://www.google.com/finance/quote/004090:KRX?hl=ko), [흥구석유](https://www.google.com/finance/quote/024060:KOSDAQ?hl=ko), [S-Oil](https://www.google.com/finance/quote/010950:KRX?hl=ko), [중앙에너비스](https://www.google.com/finance/quote/000440:KOSDAQ?hl=ko), [SK하이닉스](https://www.google.com/finance/quote/000660:KRX?hl=ko). 기업행사 조정 기준은 페이지에 명시되지 않아 evidence에는 adjustment_basis=null로 남겼다.

## 03:30 슬롯 평가

두 에이전트가 동일한 세 종목을 다른 순서로 선택해 평균 FE와 적중률은 같았다. 다만 Agent 1은 한국석유를 1위에 두어 TOP1 FE 14.44%와 순위 성과 상관 0.50을 기록했고, Agent 2는 S-Oil을 1위에 두어 TOP1 FE 0.58%, 순위 상관 -1.00이었다. 따라서 이 슬롯의 우세는 Agent 1이다.

| 지표 | Agent 1 | Agent 2 |
|---|---:|---:|
| FE 평균 (유효 3/3) | 11.44% | 11.44% |
| OFE 평균 (유효 3/3) | 1.00% | 1.00% |
| AE 평균 (유효 3/3) | 3.13% | 3.13% |
| FE≥3% / ≥5% / ≥10% | 66.67% / 66.67% / 66.67% | 66.67% / 66.67% / 66.67% |
| 예상 FE 구간 일치 | 1/3 | N/A |
| 순위 성과 Spearman | 0.50 (3쌍) | -1.00 (3쌍) |

최고 실현 FE는 흥구석유 19.30%였다. 그러나 시가 대비 종가는 -14.11%여서 개장 갭을 추격하면 성과가 급격히 달라지는 날이었다. Agent 2의 S-Oil·한국석유 진입 조건은 고가가 각각 157,000원·14,880원에 미달해 NOT_TRIGGERED였다. 흥구석유는 가격 수준을 통과했지만 거래량을 동반한 돌파·유지 순서를 일일 OHLC로 검증할 수 없어 NOT_SCORABLE이다.

## 08:30 슬롯 평가

Agent 1은 중앙에너비스와 한국석유에서 두 자릿수 FE를 포착해 평균 FE 9.19%, FE 3/5/10% 적중률 모두 66.67%였다. Agent 2의 두 후보는 평균 FE -0.41%이고 세 임계값 적중이 없었다. 두 에이전트 모두 순위 상관은 -1.00으로 상위 정렬은 실제 FE와 반대였지만, 후보 발굴 성과에서 Agent 1이 우세하다.

| 지표 | Agent 1 | Agent 2 |
|---|---:|---:|
| FE 평균 (유효 수/원래 수) | 9.19% (3/3) | -0.41% (2/2) |
| OFE 평균 (유효 수/원래 수) | 0.53% (3/3) | 1.52% (2/2) |
| AE 평균 (유효 수/원래 수) | 4.04% (3/3) | 4.75% (2/2) |
| FE≥3% / ≥5% / ≥10% | 66.67% / 66.67% / 66.67% | 0.00% / 0.00% / 0.00% |
| 예상 FE 구간 일치 | 1/3 | N/A |
| 순위 성과 Spearman | -1.00 (3쌍) | -1.00 (2쌍) |

Agent 2의 SK하이닉스는 고가 1,827,000원으로 1,890,000원 회복 조건에 미달해 NOT_TRIGGERED였다. 나머지 조건부·관찰 계획은 거래량과 가격 발생 순서를 요구하므로 일일 OHLC만으로 체결이나 손익을 추정하지 않았다.

## 시간대별 비교

- Agent 1: 03:30 평균 FE 11.44%와 TOP1 FE 14.44%가 08:30의 9.19%와 0.58%보다 우수했다. 08:30은 중앙에너비스라는 새 성공 후보를 추가했지만 1위 정렬은 악화됐다.
- Agent 2: 03:30 평균 FE 11.44%, 적중률 66.67%가 08:30 평균 FE -0.41%, 적중률 0%보다 명확히 우수했다. 08:30의 SK하이닉스 신규 편입은 당일 FE로 성과를 낮췄다.
- 공통 패턴: 에너지 테마의 장중 고가 기회는 컸지만 높은 시가 뒤 종가까지 유지되지 않았다. FE만으로 추격 매매 성과를 해석하면 안 되며 O2C와 조건 발생 순서를 함께 봐야 한다.

[REVIEW_RESULT]
SCHEMA_VERSION: DMI_REVIEW_v1.3
DATE: 2026-09-11
PREDICTION_RUN_TIME_KST: 03:30
AGENT_1_STATUS: OFFICIAL
AGENT_2_STATUS: OFFICIAL
AGENT_1_COUNT: 3
AGENT_2_COUNT: 3
AGENT_1_TOP1_FE: 14.44%
AGENT_2_TOP1_FE: 0.58%
AGENT_1_TOP3_AVG_FE: 11.44%
AGENT_2_TOP3_AVG_FE: 11.44%
AGENT_1_FE3_HIT_RATE: 66.67%
AGENT_2_FE3_HIT_RATE: 66.67%
AGENT_1_FE5_HIT_RATE: 66.67%
AGENT_2_FE5_HIT_RATE: 66.67%
AGENT_1_FE10_HIT_RATE: 66.67%
AGENT_2_FE10_HIT_RATE: 66.67%
AGENT_1_VALID_FE_COUNT: 3
AGENT_2_VALID_FE_COUNT: 3
AGENT_1_TOP3_VALID_FE_COUNT: 3
AGENT_2_TOP3_VALID_FE_COUNT: 3
AGENT_1_RANK_PERFORMANCE_SPEARMAN: 0.50
AGENT_2_RANK_PERFORMANCE_SPEARMAN: -1.00
AGENT_1_RANK_PERFORMANCE_PAIR_COUNT: 3
AGENT_2_RANK_PERFORMANCE_PAIR_COUNT: 3
BEST_AGENT: AGENT_1
BEST_PICK: 흥구석유(024060), FE 19.30%
PRIMARY_SUCCESS_PATTERN: 두 에이전트 모두 장중 변동성이 큰 에너지 3종을 발굴해 FE 10% 이상 2종을 포함했다.
PRIMARY_ERROR_PATTERN: Agent 2가 실제 FE 최하위 S-Oil을 1위로 정렬했고, 높은 시가 뒤 종가 약세 위험이 현실화됐다.
IMPROVEMENT_CANDIDATE: 개장 갭 추격 위험과 전일 급락의 가격 반증을 순위에 더 강하게 반영할지 검토한다.
[/REVIEW_RESULT]

[REVIEW_RESULT]
SCHEMA_VERSION: DMI_REVIEW_v1.3
DATE: 2026-09-11
PREDICTION_RUN_TIME_KST: 08:30
AGENT_1_STATUS: OFFICIAL
AGENT_2_STATUS: OFFICIAL
AGENT_1_COUNT: 3
AGENT_2_COUNT: 2
AGENT_1_TOP1_FE: 0.58%
AGENT_2_TOP1_FE: -1.40%
AGENT_1_TOP3_AVG_FE: 9.19%
AGENT_2_TOP3_AVG_FE: -0.41%
AGENT_1_FE3_HIT_RATE: 66.67%
AGENT_2_FE3_HIT_RATE: 0.00%
AGENT_1_FE5_HIT_RATE: 66.67%
AGENT_2_FE5_HIT_RATE: 0.00%
AGENT_1_FE10_HIT_RATE: 66.67%
AGENT_2_FE10_HIT_RATE: 0.00%
AGENT_1_VALID_FE_COUNT: 3
AGENT_2_VALID_FE_COUNT: 2
AGENT_1_TOP3_VALID_FE_COUNT: 3
AGENT_2_TOP3_VALID_FE_COUNT: 2
AGENT_1_RANK_PERFORMANCE_SPEARMAN: -1.00
AGENT_2_RANK_PERFORMANCE_SPEARMAN: -1.00
AGENT_1_RANK_PERFORMANCE_PAIR_COUNT: 3
AGENT_2_RANK_PERFORMANCE_PAIR_COUNT: 2
BEST_AGENT: AGENT_1
BEST_PICK: 한국석유(004090), FE 14.44%
PRIMARY_SUCCESS_PATTERN: Agent 1이 중앙에너비스와 한국석유에서 두 자릿수 FE를 포착했다.
PRIMARY_ERROR_PATTERN: 두 에이전트 모두 실제 FE 순서와 반대로 후보를 정렬했고 Agent 2의 SK하이닉스 돌파 조건은 미충족이었다.
IMPROVEMENT_CANDIDATE: 08:30 재평가에서 새 뉴스의 강도뿐 아니라 개장 직전 가격 확장과 실제 돌파 가능성을 분리해 순위화할지 검토한다.
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
      "read_at_kst": "2026-09-11T16:30:54+09:00",
      "status": "VERIFIED",
      "reason": "Default-branch content and blob SHA were returned together; commit SHA was not exposed."
    },
    {
      "role": "SOURCES",
      "repository": "totjae/dmi-market-pipeline",
      "path": "config/SOURCES.md",
      "commit_sha": null,
      "blob_sha": "5c47de7afdb65f60bc81a0050058a4c71d332853",
      "read_at_kst": "2026-09-11T16:30:54+09:00",
      "status": "VERIFIED",
      "reason": "Default-branch content and blob SHA were returned together; commit SHA was not exposed."
    },
    {
      "role": "REVIEW_PROMPT",
      "repository": "totjae/dmi-market-pipeline",
      "path": "prompt/REVIEW_PROMPT.md",
      "commit_sha": null,
      "blob_sha": "fbd5f2e1f490a2b5a68ae8b095b58bccbbc19cb2",
      "read_at_kst": "2026-09-11T16:30:54+09:00",
      "status": "VERIFIED",
      "reason": "Default-branch content and blob SHA were returned together; commit SHA was not exposed."
    },
    {
      "role": "REVIEW_OUTPUT",
      "repository": "totjae/dmi-market-pipeline",
      "path": "templates/REVIEW_OUTPUT.md",
      "commit_sha": null,
      "blob_sha": "aced9658e7423ac059150f7d5cdf069efce21849",
      "read_at_kst": "2026-09-11T16:30:54+09:00",
      "status": "VERIFIED",
      "reason": "Default-branch content and blob SHA were returned together; commit SHA was not exposed."
    }
  ],
  "input_manifest": [
    {
      "input_id": "A1_0330",
      "agent_id": "AGENT_1",
      "date": "2026-09-11",
      "slot_kst": "03:30",
      "repository": "totjae/dmi-agent-1",
      "path": "runs/2026-09-11/0330.md",
      "evaluated_commit_sha": "783714a66b302886ba0570b27c46c0d95e9257cc",
      "evaluated_blob_sha": "b7931f5b63a03c9b68a5571951b77a35dc863f97",
      "first_saved_commit_sha": "783714a66b302886ba0570b27c46c0d95e9257cc",
      "first_saved_at_kst": "2026-09-11T03:28:40+09:00",
      "selection_status": "OFFICIAL",
      "selection_reason": "Valid DMI_AGENT_v1.3 NORMAL/0 result; first saved before the 09:00 KRX regular-session open.",
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
          "reason": "Content and blob SHA were returned together; exact read timestamp and commit SHA were not returned."
        },
        {
          "role": "AGENT_PROMPT",
          "repository": "totjae/dmi-agent-1",
          "path": "prompt/AGENT_PROMPT.md",
          "commit_sha": "N/A",
          "blob_sha": "a44b95f40710db6c56b8916b8aabce89d1654633",
          "read_at_kst": "N/A",
          "status": "VERIFIED",
          "reason": "Content and blob SHA were returned together; exact read timestamp and commit SHA were not returned."
        },
        {
          "role": "OUTPUT",
          "repository": "totjae/dmi-agent-1",
          "path": "templates/OUTPUT.md",
          "commit_sha": "N/A",
          "blob_sha": "cafb325fcc6f5497c631849517849f7c24ae7a3d",
          "read_at_kst": "2026-09-11T03:27:12+09:00",
          "status": "VERIFIED",
          "reason": "Content and blob SHA were returned together; commit SHA was not returned."
        }
      ],
      "version_status": "UNVERIFIED"
    },
    {
      "input_id": "A2_0330",
      "agent_id": "AGENT_2",
      "date": "2026-09-11",
      "slot_kst": "03:30",
      "repository": "totjae/dmi-agent-2",
      "path": "runs/2026-09-11/0330.md",
      "evaluated_commit_sha": "a9006c6b91a898b9516b4e92f10d45ccd29828db",
      "evaluated_blob_sha": "8d293e62ca07be61738f72a17e2709ff06bd9864",
      "first_saved_commit_sha": "a9006c6b91a898b9516b4e92f10d45ccd29828db",
      "first_saved_at_kst": "2026-09-11T03:33:26+09:00",
      "selection_status": "OFFICIAL",
      "selection_reason": "Valid DMI_AGENT_v1.3 NORMAL/0 result; first saved before 09:00. A later source-link-only correction was not substituted for the earliest valid revision.",
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
          "reason": "Content and blob SHA were returned together; exact read timestamp and commit SHA were not returned."
        },
        {
          "role": "AGENT_PROMPT",
          "repository": "totjae/dmi-agent-2",
          "path": "prompt/AGENT_PROMPT.md",
          "commit_sha": "N/A",
          "blob_sha": "4da3d7554ee7da9bec1af8f74ccea24b824854bb",
          "read_at_kst": "N/A",
          "status": "VERIFIED",
          "reason": "Content and blob SHA were returned together; exact read timestamp and commit SHA were not returned."
        },
        {
          "role": "OUTPUT",
          "repository": "totjae/dmi-agent-2",
          "path": "templates/OUTPUT.md",
          "commit_sha": "N/A",
          "blob_sha": "cafb325fcc6f5497c631849517849f7c24ae7a3d",
          "read_at_kst": "2026-09-11T03:32:01+09:00",
          "status": "VERIFIED",
          "reason": "Content and blob SHA were returned together; commit SHA was not returned."
        }
      ],
      "version_status": "UNVERIFIED"
    },
    {
      "input_id": "A1_0830",
      "agent_id": "AGENT_1",
      "date": "2026-09-11",
      "slot_kst": "08:30",
      "repository": "totjae/dmi-agent-1",
      "path": "runs/2026-09-11/0830.md",
      "evaluated_commit_sha": "6590443ac391a3edba72b4ed6035447d37a48dad",
      "evaluated_blob_sha": "30be46c6f18e2ce923856b0416e8ff702417e404",
      "first_saved_commit_sha": "6590443ac391a3edba72b4ed6035447d37a48dad",
      "first_saved_at_kst": "2026-09-11T08:28:51+09:00",
      "selection_status": "OFFICIAL",
      "selection_reason": "Valid independent DMI_AGENT_v1.3 NORMAL/0 second analysis; first saved before the 09:00 KRX regular-session open.",
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
          "reason": "TOOL_RESPONSE_NO_READ_TIMESTAMP"
        },
        {
          "role": "AGENT_PROMPT",
          "repository": "totjae/dmi-agent-1",
          "path": "prompt/AGENT_PROMPT.md",
          "commit_sha": "N/A",
          "blob_sha": "a44b95f40710db6c56b8916b8aabce89d1654633",
          "read_at_kst": "N/A",
          "status": "VERIFIED",
          "reason": "TOOL_RESPONSE_NO_READ_TIMESTAMP"
        },
        {
          "role": "OUTPUT",
          "repository": "totjae/dmi-agent-1",
          "path": "templates/OUTPUT.md",
          "commit_sha": "N/A",
          "blob_sha": "cafb325fcc6f5497c631849517849f7c24ae7a3d",
          "read_at_kst": "2026-09-11T08:27:29+09:00",
          "status": "VERIFIED",
          "reason": "NONE"
        }
      ],
      "version_status": "UNVERIFIED"
    },
    {
      "input_id": "A2_0830",
      "agent_id": "AGENT_2",
      "date": "2026-09-11",
      "slot_kst": "08:30",
      "repository": "totjae/dmi-agent-2",
      "path": "runs/2026-09-11/0830.md",
      "evaluated_commit_sha": "aab87607f57807073bf8720d7dc695cb8dafeeb5",
      "evaluated_blob_sha": "0237b3b47efa9fff7c3f72386036ce157de10263",
      "first_saved_commit_sha": "aab87607f57807073bf8720d7dc695cb8dafeeb5",
      "first_saved_at_kst": "2026-09-11T08:30:59+09:00",
      "selection_status": "OFFICIAL",
      "selection_reason": "Valid independent DMI_AGENT_v1.3 NORMAL/0 second analysis; first saved before the 09:00 KRX regular-session open.",
      "prediction_schema_version": "DMI_AGENT_v1.3",
      "prediction_document_versions": [
        {
          "role": "WORKFLOW",
          "repository": "totjae/dmi-agent-2",
          "path": "WORKFLOW.md",
          "commit_sha": "N/A",
          "blob_sha": "1f863cf6d2ce2fc3b347609845906d1d0ed56815",
          "read_at_kst": "2026-09-11T08:29:07+09:00",
          "status": "VERIFIED",
          "reason": "NONE"
        },
        {
          "role": "AGENT_PROMPT",
          "repository": "totjae/dmi-agent-2",
          "path": "prompt/AGENT_PROMPT.md",
          "commit_sha": "N/A",
          "blob_sha": "4da3d7554ee7da9bec1af8f74ccea24b824854bb",
          "read_at_kst": "2026-09-11T08:29:07+09:00",
          "status": "VERIFIED",
          "reason": "NONE"
        },
        {
          "role": "OUTPUT",
          "repository": "totjae/dmi-agent-2",
          "path": "templates/OUTPUT.md",
          "commit_sha": "N/A",
          "blob_sha": "cafb325fcc6f5497c631849517849f7c24ae7a3d",
          "read_at_kst": "2026-09-11T08:29:51+09:00",
          "status": "VERIFIED",
          "reason": "NONE"
        }
      ],
      "version_status": "UNVERIFIED"
    }
  ],
  "price_sources": [
    {
      "source_id": "GF_004090_PREV",
      "provider": "Google Finance (KRX venue display)",
      "url": "https://www.google.com/finance/quote/004090:KRX?hl=ko",
      "retrieved_at_kst": "2026-09-11T16:30:54+09:00",
      "observation_date": "2026-09-10",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": null,
      "status": "VERIFIED",
      "reason": "Page reported the prior close used as 2026-09-11 previous_close; corporate-action adjustment basis was not stated."
    },
    {
      "source_id": "GF_004090_DAY",
      "provider": "Google Finance (KRX venue display)",
      "url": "https://www.google.com/finance/quote/004090:KRX?hl=ko",
      "retrieved_at_kst": "2026-09-11T16:30:54+09:00",
      "observation_date": "2026-09-11",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": null,
      "status": "VERIFIED",
      "reason": "Page reported 2026-09-11 regular-session KRW OHLC; displayed last-trade time 15:05:01 KST. Corporate-action adjustment basis was not stated."
    },
    {
      "source_id": "GF_024060_PREV",
      "provider": "Google Finance (KRX venue display)",
      "url": "https://www.google.com/finance/quote/024060:KOSDAQ?hl=ko",
      "retrieved_at_kst": "2026-09-11T16:30:54+09:00",
      "observation_date": "2026-09-10",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": null,
      "status": "VERIFIED",
      "reason": "Page reported the prior close used as 2026-09-11 previous_close; corporate-action adjustment basis was not stated."
    },
    {
      "source_id": "GF_024060_DAY",
      "provider": "Google Finance (KRX venue display)",
      "url": "https://www.google.com/finance/quote/024060:KOSDAQ?hl=ko",
      "retrieved_at_kst": "2026-09-11T16:30:54+09:00",
      "observation_date": "2026-09-11",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": null,
      "status": "VERIFIED",
      "reason": "Page reported 2026-09-11 regular-session KRW OHLC; displayed last-trade time 15:19:59 KST. Corporate-action adjustment basis was not stated."
    },
    {
      "source_id": "GF_010950_PREV",
      "provider": "Google Finance (KRX venue display)",
      "url": "https://www.google.com/finance/quote/010950:KRX?hl=ko",
      "retrieved_at_kst": "2026-09-11T16:30:54+09:00",
      "observation_date": "2026-09-10",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": null,
      "status": "VERIFIED",
      "reason": "Page reported the prior close used as 2026-09-11 previous_close; corporate-action adjustment basis was not stated."
    },
    {
      "source_id": "GF_010950_DAY",
      "provider": "Google Finance (KRX venue display)",
      "url": "https://www.google.com/finance/quote/010950:KRX?hl=ko",
      "retrieved_at_kst": "2026-09-11T16:30:54+09:00",
      "observation_date": "2026-09-11",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": null,
      "status": "VERIFIED",
      "reason": "Page reported 2026-09-11 regular-session KRW OHLC; displayed last-trade time 15:30:16 KST. Corporate-action adjustment basis was not stated."
    },
    {
      "source_id": "GF_000440_PREV",
      "provider": "Google Finance (KRX venue display)",
      "url": "https://www.google.com/finance/quote/000440:KOSDAQ?hl=ko",
      "retrieved_at_kst": "2026-09-11T16:30:54+09:00",
      "observation_date": "2026-09-10",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": null,
      "status": "VERIFIED",
      "reason": "Page reported the prior close used as 2026-09-11 previous_close; corporate-action adjustment basis was not stated."
    },
    {
      "source_id": "GF_000440_DAY",
      "provider": "Google Finance (KRX venue display)",
      "url": "https://www.google.com/finance/quote/000440:KOSDAQ?hl=ko",
      "retrieved_at_kst": "2026-09-11T16:30:54+09:00",
      "observation_date": "2026-09-11",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": null,
      "status": "VERIFIED",
      "reason": "Page reported 2026-09-11 regular-session KRW OHLC; displayed last-trade time 15:30:30 KST. Corporate-action adjustment basis was not stated."
    },
    {
      "source_id": "GF_000660_PREV",
      "provider": "Google Finance (KRX venue display)",
      "url": "https://www.google.com/finance/quote/000660:KRX?hl=ko",
      "retrieved_at_kst": "2026-09-11T16:30:54+09:00",
      "observation_date": "2026-09-10",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": null,
      "status": "VERIFIED",
      "reason": "Page reported the prior close used as 2026-09-11 previous_close; corporate-action adjustment basis was not stated."
    },
    {
      "source_id": "GF_000660_DAY",
      "provider": "Google Finance (KRX venue display)",
      "url": "https://www.google.com/finance/quote/000660:KRX?hl=ko",
      "retrieved_at_kst": "2026-09-11T16:30:54+09:00",
      "observation_date": "2026-09-11",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": null,
      "status": "VERIFIED",
      "reason": "Page reported 2026-09-11 regular-session KRW OHLC; displayed last-trade time 15:30:21 KST. Corporate-action adjustment basis was not stated."
    }
  ],
  "candidates": [
    {
      "input_id": "A1_0330",
      "rank": 1,
      "code": "004090",
      "name": "한국석유",
      "market": "KOSPI",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 12740,
          "source_ids": [
            "GF_004090_PREV"
          ]
        },
        "open": {
          "value": 14400,
          "source_ids": [
            "GF_004090_DAY"
          ]
        },
        "high": {
          "value": 14580,
          "source_ids": [
            "GF_004090_DAY"
          ]
        },
        "low": {
          "value": 12170,
          "source_ids": [
            "GF_004090_DAY"
          ]
        },
        "close": {
          "value": 12320,
          "source_ids": [
            "GF_004090_DAY"
          ]
        }
      },
      "metrics_pct": {
        "c2c": -3.296703296703297,
        "o2c": -14.444444444444443,
        "fe": 14.442700156985872,
        "ofe": 1.25,
        "ae": 4.474097331240189
      },
      "hits": {
        "fe3": true,
        "fe5": true,
        "fe10": true
      },
      "expected_fe_range_match": false,
      "trade_plan": {
        "status": "NOT_PROVIDED",
        "report_reference": null,
        "reason": "No independently scorable entry/exit plan was provided for this candidate.",
        "evidence_urls": []
      },
      "missing_reasons": []
    },
    {
      "input_id": "A1_0330",
      "rank": 2,
      "code": "024060",
      "name": "흥구석유",
      "market": "KOSDAQ",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 14510,
          "source_ids": [
            "GF_024060_PREV"
          ]
        },
        "open": {
          "value": 17010,
          "source_ids": [
            "GF_024060_DAY"
          ]
        },
        "high": {
          "value": 17310,
          "source_ids": [
            "GF_024060_DAY"
          ]
        },
        "low": {
          "value": 14600,
          "source_ids": [
            "GF_024060_DAY"
          ]
        },
        "close": {
          "value": 14610,
          "source_ids": [
            "GF_024060_DAY"
          ]
        }
      },
      "metrics_pct": {
        "c2c": 0.6891798759476223,
        "o2c": -14.109347442680775,
        "fe": 19.297036526533425,
        "ofe": 1.763668430335097,
        "ae": 0
      },
      "hits": {
        "fe3": true,
        "fe5": true,
        "fe10": true
      },
      "expected_fe_range_match": true,
      "trade_plan": {
        "status": "NOT_PROVIDED",
        "report_reference": null,
        "reason": "No independently scorable entry/exit plan was provided for this candidate.",
        "evidence_urls": []
      },
      "missing_reasons": []
    },
    {
      "input_id": "A1_0330",
      "rank": 3,
      "code": "010950",
      "name": "S-Oil",
      "market": "KOSPI",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 154900,
          "source_ids": [
            "GF_010950_PREV"
          ]
        },
        "open": {
          "value": 155800,
          "source_ids": [
            "GF_010950_DAY"
          ]
        },
        "high": {
          "value": 155800,
          "source_ids": [
            "GF_010950_DAY"
          ]
        },
        "low": {
          "value": 147300,
          "source_ids": [
            "GF_010950_DAY"
          ]
        },
        "close": {
          "value": 150000,
          "source_ids": [
            "GF_010950_DAY"
          ]
        }
      },
      "metrics_pct": {
        "c2c": -3.1633311814073597,
        "o2c": -3.7227214377406934,
        "fe": 0.5810200129115558,
        "ofe": 0,
        "ae": 4.906391220142027
      },
      "hits": {
        "fe3": false,
        "fe5": false,
        "fe10": false
      },
      "expected_fe_range_match": false,
      "trade_plan": {
        "status": "NOT_PROVIDED",
        "report_reference": null,
        "reason": "No independently scorable entry/exit plan was provided for this candidate.",
        "evidence_urls": []
      },
      "missing_reasons": []
    },
    {
      "input_id": "A2_0330",
      "rank": 1,
      "code": "010950",
      "name": "S-Oil",
      "market": "KOSPI",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 154900,
          "source_ids": [
            "GF_010950_PREV"
          ]
        },
        "open": {
          "value": 155800,
          "source_ids": [
            "GF_010950_DAY"
          ]
        },
        "high": {
          "value": 155800,
          "source_ids": [
            "GF_010950_DAY"
          ]
        },
        "low": {
          "value": 147300,
          "source_ids": [
            "GF_010950_DAY"
          ]
        },
        "close": {
          "value": 150000,
          "source_ids": [
            "GF_010950_DAY"
          ]
        }
      },
      "metrics_pct": {
        "c2c": -3.1633311814073597,
        "o2c": -3.7227214377406934,
        "fe": 0.5810200129115558,
        "ofe": 0,
        "ae": 4.906391220142027
      },
      "hits": {
        "fe3": false,
        "fe5": false,
        "fe10": false
      },
      "expected_fe_range_match": null,
      "trade_plan": {
        "status": "NOT_TRIGGERED",
        "report_reference": "STAGE_REPORT > 1위 S-Oil > 거래 계획",
        "reason": "Session high 155,800 remained below the stated 157,000 recovery trigger.",
        "evidence_urls": []
      },
      "missing_reasons": [
        {
          "field": "expected_fe_range_match",
          "status": "NOT_PROVIDED",
          "reason": "The prediction did not provide an explicit expected FE interval."
        }
      ]
    },
    {
      "input_id": "A2_0330",
      "rank": 2,
      "code": "004090",
      "name": "한국석유",
      "market": "KOSPI",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 12740,
          "source_ids": [
            "GF_004090_PREV"
          ]
        },
        "open": {
          "value": 14400,
          "source_ids": [
            "GF_004090_DAY"
          ]
        },
        "high": {
          "value": 14580,
          "source_ids": [
            "GF_004090_DAY"
          ]
        },
        "low": {
          "value": 12170,
          "source_ids": [
            "GF_004090_DAY"
          ]
        },
        "close": {
          "value": 12320,
          "source_ids": [
            "GF_004090_DAY"
          ]
        }
      },
      "metrics_pct": {
        "c2c": -3.296703296703297,
        "o2c": -14.444444444444443,
        "fe": 14.442700156985872,
        "ofe": 1.25,
        "ae": 4.474097331240189
      },
      "hits": {
        "fe3": true,
        "fe5": true,
        "fe10": true
      },
      "expected_fe_range_match": null,
      "trade_plan": {
        "status": "NOT_TRIGGERED",
        "report_reference": "STAGE_REPORT > 2위 한국석유 > 거래 계획",
        "reason": "Session high 14,580 remained below the stated 14,880 breakout trigger.",
        "evidence_urls": []
      },
      "missing_reasons": [
        {
          "field": "expected_fe_range_match",
          "status": "NOT_PROVIDED",
          "reason": "The prediction did not provide an explicit expected FE interval."
        }
      ]
    },
    {
      "input_id": "A2_0330",
      "rank": 3,
      "code": "024060",
      "name": "흥구석유",
      "market": "KOSDAQ",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 14510,
          "source_ids": [
            "GF_024060_PREV"
          ]
        },
        "open": {
          "value": 17010,
          "source_ids": [
            "GF_024060_DAY"
          ]
        },
        "high": {
          "value": 17310,
          "source_ids": [
            "GF_024060_DAY"
          ]
        },
        "low": {
          "value": 14600,
          "source_ids": [
            "GF_024060_DAY"
          ]
        },
        "close": {
          "value": 14610,
          "source_ids": [
            "GF_024060_DAY"
          ]
        }
      },
      "metrics_pct": {
        "c2c": 0.6891798759476223,
        "o2c": -14.109347442680775,
        "fe": 19.297036526533425,
        "ofe": 1.763668430335097,
        "ae": 0
      },
      "hits": {
        "fe3": true,
        "fe5": true,
        "fe10": true
      },
      "expected_fe_range_match": null,
      "trade_plan": {
        "status": "NOT_SCORABLE",
        "report_reference": "STAGE_REPORT > 3위 흥구석유 > 거래 계획",
        "reason": "The 15,710 price level traded, but daily OHLC cannot verify the required volume-backed breakout and hold sequence.",
        "evidence_urls": []
      },
      "missing_reasons": [
        {
          "field": "expected_fe_range_match",
          "status": "NOT_PROVIDED",
          "reason": "The prediction did not provide an explicit expected FE interval."
        }
      ]
    },
    {
      "input_id": "A1_0830",
      "rank": 1,
      "code": "010950",
      "name": "S-Oil",
      "market": "KOSPI",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 154900,
          "source_ids": [
            "GF_010950_PREV"
          ]
        },
        "open": {
          "value": 155800,
          "source_ids": [
            "GF_010950_DAY"
          ]
        },
        "high": {
          "value": 155800,
          "source_ids": [
            "GF_010950_DAY"
          ]
        },
        "low": {
          "value": 147300,
          "source_ids": [
            "GF_010950_DAY"
          ]
        },
        "close": {
          "value": 150000,
          "source_ids": [
            "GF_010950_DAY"
          ]
        }
      },
      "metrics_pct": {
        "c2c": -3.1633311814073597,
        "o2c": -3.7227214377406934,
        "fe": 0.5810200129115558,
        "ofe": 0,
        "ae": 4.906391220142027
      },
      "hits": {
        "fe3": false,
        "fe5": false,
        "fe10": false
      },
      "expected_fe_range_match": false,
      "trade_plan": {
        "status": "NOT_SCORABLE",
        "report_reference": "STAGE_REPORT > S-Oil > 반대논리·무효화 조건",
        "reason": "Daily OHLC shows the 151,600 invalidation level traded through but cannot establish whether an entry occurred first.",
        "evidence_urls": []
      },
      "missing_reasons": []
    },
    {
      "input_id": "A1_0830",
      "rank": 2,
      "code": "000440",
      "name": "중앙에너비스",
      "market": "KOSDAQ",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 13550,
          "source_ids": [
            "GF_000440_PREV"
          ]
        },
        "open": {
          "value": 15200,
          "source_ids": [
            "GF_000440_DAY"
          ]
        },
        "high": {
          "value": 15250,
          "source_ids": [
            "GF_000440_DAY"
          ]
        },
        "low": {
          "value": 13180,
          "source_ids": [
            "GF_000440_DAY"
          ]
        },
        "close": {
          "value": 13200,
          "source_ids": [
            "GF_000440_DAY"
          ]
        }
      },
      "metrics_pct": {
        "c2c": -2.5830258302583027,
        "o2c": -13.157894736842104,
        "fe": 12.546125461254611,
        "ofe": 0.3289473684210526,
        "ae": 2.730627306273063
      },
      "hits": {
        "fe3": true,
        "fe5": true,
        "fe10": true
      },
      "expected_fe_range_match": true,
      "trade_plan": {
        "status": "NOT_SCORABLE",
        "report_reference": "STAGE_REPORT > 중앙에너비스 > 반대논리·무효화 조건",
        "reason": "Daily OHLC cannot establish the required post-gap support and theme-liquidity sequence.",
        "evidence_urls": []
      },
      "missing_reasons": []
    },
    {
      "input_id": "A1_0830",
      "rank": 3,
      "code": "004090",
      "name": "한국석유",
      "market": "KOSPI",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 12740,
          "source_ids": [
            "GF_004090_PREV"
          ]
        },
        "open": {
          "value": 14400,
          "source_ids": [
            "GF_004090_DAY"
          ]
        },
        "high": {
          "value": 14580,
          "source_ids": [
            "GF_004090_DAY"
          ]
        },
        "low": {
          "value": 12170,
          "source_ids": [
            "GF_004090_DAY"
          ]
        },
        "close": {
          "value": 12320,
          "source_ids": [
            "GF_004090_DAY"
          ]
        }
      },
      "metrics_pct": {
        "c2c": -3.296703296703297,
        "o2c": -14.444444444444443,
        "fe": 14.442700156985872,
        "ofe": 1.25,
        "ae": 4.474097331240189
      },
      "hits": {
        "fe3": true,
        "fe5": true,
        "fe10": true
      },
      "expected_fe_range_match": false,
      "trade_plan": {
        "status": "NOT_SCORABLE",
        "report_reference": "STAGE_REPORT > 한국석유 > 반대논리·무효화 조건",
        "reason": "Daily OHLC cannot establish the required post-open recovery and volume sequence.",
        "evidence_urls": []
      },
      "missing_reasons": []
    },
    {
      "input_id": "A2_0830",
      "rank": 1,
      "code": "000660",
      "name": "SK하이닉스",
      "market": "KOSPI",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 1853000,
          "source_ids": [
            "GF_000660_PREV"
          ]
        },
        "open": {
          "value": 1773000,
          "source_ids": [
            "GF_000660_DAY"
          ]
        },
        "high": {
          "value": 1827000,
          "source_ids": [
            "GF_000660_DAY"
          ]
        },
        "low": {
          "value": 1768000,
          "source_ids": [
            "GF_000660_DAY"
          ]
        },
        "close": {
          "value": 1812000,
          "source_ids": [
            "GF_000660_DAY"
          ]
        }
      },
      "metrics_pct": {
        "c2c": -2.212628170534269,
        "o2c": 2.199661590524535,
        "fe": -1.4031300593631948,
        "ofe": 3.0456852791878175,
        "ae": 4.587155963302752
      },
      "hits": {
        "fe3": false,
        "fe5": false,
        "fe10": false
      },
      "expected_fe_range_match": null,
      "trade_plan": {
        "status": "NOT_TRIGGERED",
        "report_reference": "STAGE_REPORT > 1위 SK하이닉스 > 거래 계획",
        "reason": "Session high 1,827,000 remained below the stated 1,890,000 recovery trigger.",
        "evidence_urls": []
      },
      "missing_reasons": [
        {
          "field": "expected_fe_range_match",
          "status": "NOT_PROVIDED",
          "reason": "The prediction did not provide an explicit expected FE interval."
        }
      ]
    },
    {
      "input_id": "A2_0830",
      "rank": 2,
      "code": "010950",
      "name": "S-Oil",
      "market": "KOSPI",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 154900,
          "source_ids": [
            "GF_010950_PREV"
          ]
        },
        "open": {
          "value": 155800,
          "source_ids": [
            "GF_010950_DAY"
          ]
        },
        "high": {
          "value": 155800,
          "source_ids": [
            "GF_010950_DAY"
          ]
        },
        "low": {
          "value": 147300,
          "source_ids": [
            "GF_010950_DAY"
          ]
        },
        "close": {
          "value": 150000,
          "source_ids": [
            "GF_010950_DAY"
          ]
        }
      },
      "metrics_pct": {
        "c2c": -3.1633311814073597,
        "o2c": -3.7227214377406934,
        "fe": 0.5810200129115558,
        "ofe": 0,
        "ae": 4.906391220142027
      },
      "hits": {
        "fe3": false,
        "fe5": false,
        "fe10": false
      },
      "expected_fe_range_match": null,
      "trade_plan": {
        "status": "NOT_SCORABLE",
        "report_reference": "STAGE_REPORT > 2위 S-Oil > 거래 계획",
        "reason": "Daily OHLC cannot establish the required first-pullback support and buying-recovery sequence.",
        "evidence_urls": []
      },
      "missing_reasons": [
        {
          "field": "expected_fe_range_match",
          "status": "NOT_PROVIDED",
          "reason": "The prediction did not provide an explicit expected FE interval."
        }
      ]
    }
  ]
}
[/REVIEW_EVIDENCE]
