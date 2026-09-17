[DMI_REVIEW_META]
SCHEMA_VERSION: DMI_REVIEW_v1.3
DATE: 2026-09-17
PREDICTION_RUN_TIMES_KST: [03:30, 08:30]
REVIEW_TIME_KST: 16:30
STARTED_AT_KST: 2026-09-17T16:31:50+09:00
REPORT_COMPLETED_AT_KST: 2026-09-17T16:34:12+09:00
DATA_CUTOFF_KST: 2026-09-17T16:33:51+09:00
SOURCE_MANIFEST: REVIEW_EVIDENCE.input_manifest
REVIEW_DOCUMENT_VERSIONS: REVIEW_EVIDENCE.review_document_versions
RUN_TYPE: NORMAL
RERUN_SEQUENCE: 0
[/DMI_REVIEW_META]

[REVIEW_REPORT]
# DMI Two-Agent Daily Review — 2026-09-17

## 1. 입력과 검증 상태

KRX 공식 안내의 정규장 개장 09:00 KST를 기준으로 GitHub 최초 저장시각을 검증했다. 네 입력 모두 지정 날짜·슬롯, DMI_AGENT_v1.3 wrapper, TOP_COUNT와 본문/결과 캡슐 일치를 충족했고 최초 저장이 개장 전이므로 공식 입력으로 채택했다. 각 경로에는 생성 commit 하나만 확인돼 이후 rerun이나 대체 입력은 없다.

| 슬롯 | Agent | 경로 | 최초 저장 KST | 상태 |
|---|---|---|---|---|
| 03:30 | Agent 1 | runs/2026-09-17/0330.md | 03:29:13 | OFFICIAL |
| 03:30 | Agent 2 | runs/2026-09-17/0330.md | 03:33:00 | OFFICIAL |
| 08:30 | Agent 1 | runs/2026-09-17/0830.md | 08:27:20 | OFFICIAL |
| 08:30 | Agent 2 | runs/2026-09-17/0830.md | 08:31:03 | OFFICIAL |

입력에 기록된 문서 blob SHA는 보존했지만 commit_sha가 N/A이므로 prediction version_status는 UNVERIFIED로 분리했다. 이는 입력 선택과 당일 공식 KPI에는 영향을 주지 않는다.

## 2. 시장 Ground Truth

정규장 시간은 KRX 공식 안내의 09:00~15:30을 사용했다. 종목별 전일 종가와 2026-09-17 정규장 OHLC는 매일경제 마켓의 09.17 15:32 표시값으로 확인했다.

| 종목 | 전일 종가 | 시가 | 고가 | 저가 | 종가 |
|---|---:|---:|---:|---:|---:|
| 뷰티스킨(406820) | 2,540 | 2,540 | 2,830 | 2,235 | 2,310 |
| 미투온(201490) | 3,840 | 4,170 | 4,800 | 3,990 | 4,635 |
| SK하이닉스(000660) | 1,759,000 | 1,770,000 | 1,785,000 | 1,735,000 | 1,745,000 |

가격 출처:
- 뷰티스킨: https://stock.mk.co.kr/price/home/KR7406820001
- 미투온: https://stock.mk.co.kr/price/home/KR7201490000
- SK하이닉스: https://stock.mk.co.kr/price/home/KR7000660001
- KRX 정규장 시간: https://global.krx.co.kr/

## 3. 후보별 실제 성과

| 슬롯 | Agent | 후보 | C2C | O2C | FE | OFE | AE | 예상 FE 적합 |
|---|---|---|---:|---:|---:|---:|---:|---|
| 03:30 | Agent 1 | 뷰티스킨 | -9.06% | -9.06% | 11.42% | 11.42% | 12.01% | 실패 (+5~10% 상회) |
| 03:30 | Agent 2 | 미투온 | 20.70% | 11.15% | 25.00% | 15.11% | 0.00% | 실패 (+5~10% 상회) |
| 08:30 | Agent 1 | SK하이닉스 | -0.80% | -1.41% | 1.48% | 0.85% | 1.36% | 실패 (+3~5% 미달) |
| 08:30 | Agent 2 | SK하이닉스 | -0.80% | -1.41% | 1.48% | 0.85% | 1.36% | 실패 (+3~5% 미달) |

모든 후보는 TOP1 한 종목이라 TOP1·TOP3·전체 평균이 동일하다. 순위쌍 n=1이므로 Spearman은 계산할 수 없다. 조건부 거래 계획은 일봉 OHLC만으로 조건 발생 순서를 확인할 수 없어 모두 NOT_SCORABLE이며, 가격 접촉을 체결이나 실현수익으로 해석하지 않았다.

## 4. 슬롯별 Agent 비교

### 03:30

Agent 2의 미투온이 FE 25.00%, OFE 15.11%, AE 0.00%, C2C 20.70%로 Agent 1의 뷰티스킨보다 모든 방향성 지표에서 우세했다. 두 후보 모두 FE3·FE5·FE10을 충족했지만, 뷰티스킨은 고가 기준 기회가 있었던 뒤 종가 -9.06%와 AE 12.01%를 기록해 고위험 관찰 판단이 실제로 드러났다. 미투온은 전일 상한가 이후에도 추가 가격발견이 이어졌다.

03:30 BEST_AGENT는 AGENT_2다. BEST_PICK은 미투온이다.

### 08:30

두 에이전트 모두 SK하이닉스를 동일한 1순위·예상 FE +3~5%·낮은 확신도로 선정했다. 실제 FE는 1.48%로 FE3에 미달했고 종가는 전일 대비 -0.80%였다. 후보와 성과가 동일하므로 우열은 동률이다.

08:30 BEST_AGENT는 TIE, BEST_PICK은 공동 SK하이닉스다.

## 5. 에이전트별 03:30 vs 08:30

- Agent 1: 03:30 뷰티스킨 FE 11.42%가 08:30 SK하이닉스 FE 1.48%보다 높았다. 다만 뷰티스킨의 C2C·AE는 크게 악화돼 '큰 움직임 발굴'과 '종가 방향·매매 위험'이 분리됐다.
- Agent 2: 03:30 미투온 FE 25.00%가 08:30 SK하이닉스 FE 1.48%보다 높았고, C2C·OFE·AE도 03:30이 우세했다.
- 08:30은 오류 복구가 아닌 새 정보 독립 분석으로 평가했으며 후보를 시간대 사이에서 합치거나 누락값을 0으로 채우지 않았다.

## 6. 성공·오류 분석

성공 패턴은 최대주주 변경과 경영권 이전처럼 직접적이고 확정성이 높은 기업 이벤트가 전일 상한가 이후에도 후속 가격발견을 만든 미투온이다. Agent 2는 희석과 갭 추격 위험을 함께 인식하면서도 종목 발굴에는 성공했다.

주요 오류 패턴은 전일 4.08% 오른 SK하이닉스에서 탐색 단계의 협력 논의를 +3% 이상 FE로 본 점이다. 두 에이전트 모두 선반영·협상 미확정·낮은 확신도를 적절히 경고했지만, 실제 추가 고가 상승폭은 1.48%에 그쳤다.

뷰티스킨은 FE 자체는 11.42%로 강했지만 종가가 -9.06%로 반전됐다. 이는 당일 큰 움직임 가능성과 실제 추격 매매 품질을 별도로 평가해야 한다는 사례다.

## 7. 개선 후보

- 관찰 근거: 전일 상한가 종목 두 개 중 미투온은 C2C +20.70%, 뷰티스킨은 -9.06%로 갈렸다.
- 개선 후보: 후속 가격발견 판단 시 촉매의 확정성·지배구조 변화·실제 거래 집중을 전일 상한가 자체보다 우선 검토한다.
- 기대효과: 동일한 가격 선반영 상태에서도 재료 지속성이 높은 종목을 구분할 가능성이 커진다.
- 부작용: 확정성 기준을 지나치게 높이면 초기 탐색 단계의 대형 재료를 놓칠 수 있다.
- 적용 상태: 단일 거래일 관찰이므로 프롬프트나 운영 규칙에 자동 반영하지 않는다.

## 8. 최종 요약

공식 입력은 4/4개다. 03:30은 Agent 2가 우세했고 미투온이 당일 최고 FE 25.00%를 기록했다. 08:30은 두 에이전트가 동일한 SK하이닉스를 선택해 동률이며 FE는 1.48%에 그쳤다. 시간대 비교에서는 두 에이전트 모두 03:30 후보가 08:30 후보보다 높은 FE를 기록했다.

[REVIEW_RESULT]
SCHEMA_VERSION: DMI_REVIEW_v1.3
DATE: 2026-09-17
PREDICTION_RUN_TIME_KST: 03:30
AGENT_1_STATUS: OFFICIAL
AGENT_2_STATUS: OFFICIAL
AGENT_1_COUNT: 1
AGENT_2_COUNT: 1
AGENT_1_TOP1_FE: 11.42%
AGENT_2_TOP1_FE: 25.00%
AGENT_1_TOP3_AVG_FE: 11.42%
AGENT_2_TOP3_AVG_FE: 25.00%
AGENT_1_FE3_HIT_RATE: 100.00%
AGENT_2_FE3_HIT_RATE: 100.00%
AGENT_1_FE5_HIT_RATE: 100.00%
AGENT_2_FE5_HIT_RATE: 100.00%
AGENT_1_FE10_HIT_RATE: 100.00%
AGENT_2_FE10_HIT_RATE: 100.00%
AGENT_1_VALID_FE_COUNT: 1
AGENT_2_VALID_FE_COUNT: 1
AGENT_1_TOP3_VALID_FE_COUNT: 1
AGENT_2_TOP3_VALID_FE_COUNT: 1
AGENT_1_RANK_PERFORMANCE_SPEARMAN: N/A
AGENT_2_RANK_PERFORMANCE_SPEARMAN: N/A
AGENT_1_RANK_PERFORMANCE_PAIR_COUNT: 1
AGENT_2_RANK_PERFORMANCE_PAIR_COUNT: 1
BEST_AGENT: AGENT_2
BEST_PICK: 미투온(201490), FE 25.00%
PRIMARY_SUCCESS_PATTERN: 확정적 경영권 이전 촉매와 전일 상한가 이후 후속 가격발견
PRIMARY_ERROR_PATTERN: 뷰티스킨은 높은 FE 뒤 종가 반전과 큰 AE로 추격 매매 위험 노출
IMPROVEMENT_CANDIDATE: 후속 가격발견 판단에서 촉매 확정성과 지배구조 변화를 우선 검토
[/REVIEW_RESULT]

[REVIEW_RESULT]
SCHEMA_VERSION: DMI_REVIEW_v1.3
DATE: 2026-09-17
PREDICTION_RUN_TIME_KST: 08:30
AGENT_1_STATUS: OFFICIAL
AGENT_2_STATUS: OFFICIAL
AGENT_1_COUNT: 1
AGENT_2_COUNT: 1
AGENT_1_TOP1_FE: 1.48%
AGENT_2_TOP1_FE: 1.48%
AGENT_1_TOP3_AVG_FE: 1.48%
AGENT_2_TOP3_AVG_FE: 1.48%
AGENT_1_FE3_HIT_RATE: 0.00%
AGENT_2_FE3_HIT_RATE: 0.00%
AGENT_1_FE5_HIT_RATE: 0.00%
AGENT_2_FE5_HIT_RATE: 0.00%
AGENT_1_FE10_HIT_RATE: 0.00%
AGENT_2_FE10_HIT_RATE: 0.00%
AGENT_1_VALID_FE_COUNT: 1
AGENT_2_VALID_FE_COUNT: 1
AGENT_1_TOP3_VALID_FE_COUNT: 1
AGENT_2_TOP3_VALID_FE_COUNT: 1
AGENT_1_RANK_PERFORMANCE_SPEARMAN: N/A
AGENT_2_RANK_PERFORMANCE_SPEARMAN: N/A
AGENT_1_RANK_PERFORMANCE_PAIR_COUNT: 1
AGENT_2_RANK_PERFORMANCE_PAIR_COUNT: 1
BEST_AGENT: TIE
BEST_PICK: 공동 SK하이닉스(000660), FE 1.48%
PRIMARY_SUCCESS_PATTERN: 두 에이전트 모두 선반영과 낮은 확신도를 명시
PRIMARY_ERROR_PATTERN: 전일 상승 후 탐색 단계 협력 재료의 추가 FE를 과대평가
IMPROVEMENT_CANDIDATE: 전일 급등한 미확정 재료에는 첫 가격발견 잔여 여부를 더 엄격히 적용
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
      "commit_sha": "27298b1c624573b5a1c17582e08bb12a0a3e50c8",
      "blob_sha": "f7d593b7f558c95df45ad802b1489591cb726151",
      "read_at_kst": null,
      "status": "VERIFIED",
      "reason": "NONE"
    },
    {
      "role": "SOURCES",
      "repository": "totjae/dmi-market-pipeline",
      "path": "config/SOURCES.md",
      "commit_sha": "fa4f799d8d72895a638cc19caca7e6f338da8fe5",
      "blob_sha": "5c47de7afdb65f60bc81a0050058a4c71d332853",
      "read_at_kst": null,
      "status": "VERIFIED",
      "reason": "NONE"
    },
    {
      "role": "REVIEW_PROMPT",
      "repository": "totjae/dmi-market-pipeline",
      "path": "prompt/REVIEW_PROMPT.md",
      "commit_sha": "f0c2f8fc512b41ba9166fa886b0c04741ddf3913",
      "blob_sha": "fbd5f2e1f490a2b5a68ae8b095b58bccbbc19cb2",
      "read_at_kst": null,
      "status": "VERIFIED",
      "reason": "NONE"
    },
    {
      "role": "REVIEW_OUTPUT",
      "repository": "totjae/dmi-market-pipeline",
      "path": "templates/REVIEW_OUTPUT.md",
      "commit_sha": "445463f9f009da62fa76e143186d6af351106d66",
      "blob_sha": "aced9658e7423ac059150f7d5cdf069efce21849",
      "read_at_kst": null,
      "status": "VERIFIED",
      "reason": "NONE"
    }
  ],
  "input_manifest": [
    {
      "input_id": "a1_20260917_0330",
      "agent_id": "AGENT_1",
      "date": "2026-09-17",
      "slot_kst": "03:30",
      "repository": "totjae/dmi-agent-1",
      "path": "runs/2026-09-17/0330.md",
      "evaluated_commit_sha": "12ee645f95d212badd05e531d92a50989b0e676a",
      "evaluated_blob_sha": "747b794f7ec1912e8789ec8eac7c395a4bd29892",
      "first_saved_commit_sha": "12ee645f95d212badd05e531d92a50989b0e676a",
      "first_saved_at_kst": "2026-09-17T03:29:13+09:00",
      "selection_status": "OFFICIAL",
      "selection_reason": "FIRST_VALID_PREOPEN; GitHub 최초 저장이 KRX 정규장 개장 09:00 KST 이전",
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
      "input_id": "a2_20260917_0330",
      "agent_id": "AGENT_2",
      "date": "2026-09-17",
      "slot_kst": "03:30",
      "repository": "totjae/dmi-agent-2",
      "path": "runs/2026-09-17/0330.md",
      "evaluated_commit_sha": "7dfcb5c912fe151cf000e91f26f358c46bd8c897",
      "evaluated_blob_sha": "5880f6ed714076b94fac635505cb8e9fd0f88059",
      "first_saved_commit_sha": "7dfcb5c912fe151cf000e91f26f358c46bd8c897",
      "first_saved_at_kst": "2026-09-17T03:33:00+09:00",
      "selection_status": "OFFICIAL",
      "selection_reason": "FIRST_VALID_PREOPEN; GitHub 최초 저장이 KRX 정규장 개장 09:00 KST 이전",
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
    },
    {
      "input_id": "a1_20260917_0830",
      "agent_id": "AGENT_1",
      "date": "2026-09-17",
      "slot_kst": "08:30",
      "repository": "totjae/dmi-agent-1",
      "path": "runs/2026-09-17/0830.md",
      "evaluated_commit_sha": "15f383fe70214c624d6df10b7ebff4d96ae0be88",
      "evaluated_blob_sha": "6052c2dbd1221d81bcccbefd56317c9e3a6bc445",
      "first_saved_commit_sha": "15f383fe70214c624d6df10b7ebff4d96ae0be88",
      "first_saved_at_kst": "2026-09-17T08:27:20+09:00",
      "selection_status": "OFFICIAL",
      "selection_reason": "FIRST_VALID_PREOPEN; GitHub 최초 저장이 KRX 정규장 개장 09:00 KST 이전",
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
      "input_id": "a2_20260917_0830",
      "agent_id": "AGENT_2",
      "date": "2026-09-17",
      "slot_kst": "08:30",
      "repository": "totjae/dmi-agent-2",
      "path": "runs/2026-09-17/0830.md",
      "evaluated_commit_sha": "abc7625f6bae628c4216588c2c15266eb6c87191",
      "evaluated_blob_sha": "756edcccba2bd0de27ebc7aeb21701164f9f915f",
      "first_saved_commit_sha": "abc7625f6bae628c4216588c2c15266eb6c87191",
      "first_saved_at_kst": "2026-09-17T08:31:03+09:00",
      "selection_status": "OFFICIAL",
      "selection_reason": "FIRST_VALID_PREOPEN; GitHub 최초 저장이 KRX 정규장 개장 09:00 KST 이전",
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
      "source_id": "src_krx_hours",
      "provider": "Korea Exchange",
      "url": "https://global.krx.co.kr/",
      "retrieved_at_kst": "2026-09-17T16:33:51+09:00",
      "observation_date": "2026-09-17",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": "NOT_APPLICABLE",
      "status": "VERIFIED",
      "reason": "공식 안내에서 정규장 09:00-15:30 확인"
    },
    {
      "source_id": "src_beauty_20260917",
      "provider": "매일경제 마켓",
      "url": "https://stock.mk.co.kr/price/home/KR7406820001",
      "retrieved_at_kst": "2026-09-17T16:33:51+09:00",
      "observation_date": "2026-09-17",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": "페이지 표시 원주가; 별도 기업행사 조정 없음",
      "status": "VERIFIED",
      "reason": "09.17 15:32 표시 전일·시가·고가·저가·종가 확인"
    },
    {
      "source_id": "src_mituon_20260917",
      "provider": "매일경제 마켓",
      "url": "https://stock.mk.co.kr/price/home/KR7201490000",
      "retrieved_at_kst": "2026-09-17T16:33:51+09:00",
      "observation_date": "2026-09-17",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": "페이지 표시 원주가; 별도 기업행사 조정 없음",
      "status": "VERIFIED",
      "reason": "09.17 15:32 표시 전일·시가·고가·저가·종가 확인"
    },
    {
      "source_id": "src_hynix_20260917",
      "provider": "매일경제 마켓",
      "url": "https://stock.mk.co.kr/price/home/KR7000660001",
      "retrieved_at_kst": "2026-09-17T16:33:51+09:00",
      "observation_date": "2026-09-17",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": "페이지 표시 원주가; 별도 기업행사 조정 없음",
      "status": "VERIFIED",
      "reason": "09.17 15:32 표시 전일·시가·고가·저가·종가 확인"
    }
  ],
  "candidates": [
    {
      "input_id": "a1_20260917_0330",
      "rank": 1,
      "code": "406820",
      "name": "뷰티스킨",
      "market": "KOSDAQ",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 2540,
          "source_ids": [
            "src_beauty_20260917"
          ]
        },
        "open": {
          "value": 2540,
          "source_ids": [
            "src_beauty_20260917"
          ]
        },
        "high": {
          "value": 2830,
          "source_ids": [
            "src_beauty_20260917"
          ]
        },
        "low": {
          "value": 2235,
          "source_ids": [
            "src_beauty_20260917"
          ]
        },
        "close": {
          "value": 2310,
          "source_ids": [
            "src_beauty_20260917"
          ]
        }
      },
      "metrics_pct": {
        "c2c": -9.05511811023622,
        "o2c": -9.05511811023622,
        "fe": 11.41732283464567,
        "ofe": 11.41732283464567,
        "ae": 12.007874015748031
      },
      "hits": {
        "fe3": true,
        "fe5": true,
        "fe10": true
      },
      "expected_fe_range_match": false,
      "trade_plan": {
        "status": "NOT_SCORABLE",
        "report_reference": "3. 후보별 근거 / 1위 뷰티스킨",
        "reason": "일봉 OHLC만으로 거래 집중·시초가 이탈 후 회복 여부의 시간순서를 검증할 수 없음",
        "evidence_urls": [
          "https://stock.mk.co.kr/price/home/KR7406820001"
        ]
      },
      "missing_reasons": []
    },
    {
      "input_id": "a2_20260917_0330",
      "rank": 1,
      "code": "201490",
      "name": "미투온",
      "market": "KOSDAQ",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 3840,
          "source_ids": [
            "src_mituon_20260917"
          ]
        },
        "open": {
          "value": 4170,
          "source_ids": [
            "src_mituon_20260917"
          ]
        },
        "high": {
          "value": 4800,
          "source_ids": [
            "src_mituon_20260917"
          ]
        },
        "low": {
          "value": 3990,
          "source_ids": [
            "src_mituon_20260917"
          ]
        },
        "close": {
          "value": 4635,
          "source_ids": [
            "src_mituon_20260917"
          ]
        }
      },
      "metrics_pct": {
        "c2c": 20.703125,
        "o2c": 11.151079136690647,
        "fe": 25,
        "ofe": 15.107913669064748,
        "ae": 0
      },
      "hits": {
        "fe3": true,
        "fe5": true,
        "fe10": true
      },
      "expected_fe_range_match": false,
      "trade_plan": {
        "status": "NOT_SCORABLE",
        "report_reference": "1순위 — 미투온 / 매매 판단",
        "reason": "일봉 OHLC만으로 초기 지지와 눌림 회복 및 실제 체결 조건의 시간순서를 검증할 수 없음",
        "evidence_urls": [
          "https://stock.mk.co.kr/price/home/KR7201490000"
        ]
      },
      "missing_reasons": []
    },
    {
      "input_id": "a1_20260917_0830",
      "rank": 1,
      "code": "000660",
      "name": "SK하이닉스",
      "market": "KOSPI",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 1759000,
          "source_ids": [
            "src_hynix_20260917"
          ]
        },
        "open": {
          "value": 1770000,
          "source_ids": [
            "src_hynix_20260917"
          ]
        },
        "high": {
          "value": 1785000,
          "source_ids": [
            "src_hynix_20260917"
          ]
        },
        "low": {
          "value": 1735000,
          "source_ids": [
            "src_hynix_20260917"
          ]
        },
        "close": {
          "value": 1745000,
          "source_ids": [
            "src_hynix_20260917"
          ]
        }
      },
      "metrics_pct": {
        "c2c": -0.7959067652075044,
        "o2c": -1.4124293785310735,
        "fe": 1.4781125639567936,
        "ofe": 0.847457627118644,
        "ae": 1.3644115974985787
      },
      "hits": {
        "fe3": false,
        "fe5": false,
        "fe10": false
      },
      "expected_fe_range_match": false,
      "trade_plan": {
        "status": "NOT_SCORABLE",
        "report_reference": "3. 후보별 근거 / 1순위 SK하이닉스",
        "reason": "일봉 OHLC만으로 전일 종가 회복·유지와 거래 증가의 시간순서를 검증할 수 없음",
        "evidence_urls": [
          "https://stock.mk.co.kr/price/home/KR7000660001"
        ]
      },
      "missing_reasons": []
    },
    {
      "input_id": "a2_20260917_0830",
      "rank": 1,
      "code": "000660",
      "name": "SK하이닉스",
      "market": "KOSPI",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 1759000,
          "source_ids": [
            "src_hynix_20260917"
          ]
        },
        "open": {
          "value": 1770000,
          "source_ids": [
            "src_hynix_20260917"
          ]
        },
        "high": {
          "value": 1785000,
          "source_ids": [
            "src_hynix_20260917"
          ]
        },
        "low": {
          "value": 1735000,
          "source_ids": [
            "src_hynix_20260917"
          ]
        },
        "close": {
          "value": 1745000,
          "source_ids": [
            "src_hynix_20260917"
          ]
        }
      },
      "metrics_pct": {
        "c2c": -0.7959067652075044,
        "o2c": -1.4124293785310735,
        "fe": 1.4781125639567936,
        "ofe": 0.847457627118644,
        "ae": 1.3644115974985787
      },
      "hits": {
        "fe3": false,
        "fe5": false,
        "fe10": false
      },
      "expected_fe_range_match": false,
      "trade_plan": {
        "status": "NOT_SCORABLE",
        "report_reference": "매매 판단",
        "reason": "일봉 OHLC만으로 전일 종가 회복·유지와 거래대금 동반 조건의 시간순서를 검증할 수 없음",
        "evidence_urls": [
          "https://stock.mk.co.kr/price/home/KR7000660001"
        ]
      },
      "missing_reasons": []
    }
  ]
}
[/REVIEW_EVIDENCE]
