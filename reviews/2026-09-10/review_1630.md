[DMI_REVIEW_META]
SCHEMA_VERSION: DMI_REVIEW_v1.3
DATE: 2026-09-10
PREDICTION_RUN_TIMES_KST: [03:30, 08:30]
REVIEW_TIME_KST: 16:30
STARTED_AT_KST: 2026-09-10T16:28:20+09:00
REPORT_COMPLETED_AT_KST: 2026-09-10T16:38:52+09:00
DATA_CUTOFF_KST: 2026-09-10T16:38:52+09:00
SOURCE_MANIFEST: REVIEW_EVIDENCE.input_manifest
REVIEW_DOCUMENT_VERSIONS: REVIEW_EVIDENCE.review_document_versions
RUN_TYPE: NORMAL
RERUN_SEQUENCE: 0
[/DMI_REVIEW_META]

[REVIEW_REPORT]
# DMI Two-Agent Review — 2026-09-10

## 1. 입력과 검증 상태

KRX 공식 거래 안내의 정규장 09:00~15:30 KST를 장전 판정 기준으로 사용했다. 지정 날짜·슬롯의 기본 파일과 저장 이력만 확인했으며 에이전트 프롬프트, 다른 날짜 결과, legacy는 읽지 않았다.

| 슬롯 | 에이전트 | 상태 | 공식 입력 | 최초 저장(KST) | 검증 |
|---|---|---|---|---|---|
| 03:30 | Agent 1 | OFFICIAL | `runs/2026-09-10/0330.md` @ `fbbae2b8957e48538a8c8fe35ff941569105ddaa` | 03:34:43 | v1.3 구조·본문/캡슐·날짜·cutoff 일치, 09:00 이전 |
| 03:30 | Agent 2 | OFFICIAL | `runs/2026-09-10/0330.md` @ `2706925cd584a1d8ae16583fd4a67f841b918eb1` | 04:00:22 | v1.3 구조·본문/캡슐·날짜·cutoff 일치, 09:00 이전 |
| 08:30 | Agent 1 | UNAVAILABLE | 없음 | N/A | MISSING_FILE. 후보 0개가 아니라 입력 누락이며 KPI 제외 |
| 08:30 | Agent 2 | OFFICIAL | `runs/2026-09-10/0830.md` @ `8073403308bfe22764697557b407ce5f7ee8f8e7` | 08:38:03 | v1.3 구조·본문/캡슐·날짜·cutoff 일치, 09:00 이전 |

확인된 rerun이 없어 각 공식 입력은 최초 유효 기본 파일이다. 입력 내부 문서 버전은 blob SHA가 있으나 commit SHA가 `N/A`이므로 version_status는 UNVERIFIED로 보존했다. 이는 후보 성과 집계 제외 사유는 아니다.

## 2. 시장 Ground Truth

2026-09-10 KRX 정규장 장마감 자료를 사용했다. 가격은 Npay 증권 종목 페이지가 명시한 KRX 제공 전일가·시가·고가·저가·종가이며 모두 KRW이다.

| 종목 | 전일 | 시가 | 고가 | 저가 | 종가 |
|---|---:|---:|---:|---:|---:|
| 우리로 | 6,570 | 6,660 | 7,090 | 6,400 | 6,700 |
| S-Oil | 165,900 | 168,800 | 170,800 | 151,600 | 154,900 |
| 삼성전자 | 269,500 | 269,000 | 270,500 | 263,500 | 269,000 |
| SK하이닉스 | 1,856,000 | 1,879,000 | 1,890,000 | 1,811,000 | 1,853,000 |
| 흥구석유 | 12,090 | 12,730 | 15,710 | 12,720 | 14,510 |
| SK이노베이션 | 153,500 | 155,500 | 164,700 | 150,200 | 153,100 |

정규장 운영 기준: https://global.krx.co.kr/contents/GLB/01/0109/0109000000/guide_to_trading_in_the_korean_stock_market.pdf

## 3. 후보별 실제 성과

| 슬롯·에이전트·순위 | 후보 | C2C | O2C | FE | OFE | AE | FE3/5/10 | 예상 FE 적합 | 계획 |
|---|---|---:|---:|---:|---:|---:|---|---|---|
| 03:30 A1 #1 | 우리로 | +1.98% | +0.60% | +7.91% | +6.46% | 2.59% | Y/Y/N | TRUE (+5~10%) | NOT_SCORABLE |
| 03:30 A2 #1 | S-Oil | -6.63% | -8.23% | +2.95% | +1.18% | 8.62% | N/N/N | N/A | NOT_SCORABLE |
| 03:30 A2 #2 | 삼성전자 | -0.19% | 0.00% | +0.37% | +0.56% | 2.23% | N/N/N | N/A | NOT_TRIGGERED |
| 03:30 A2 #3 | SK하이닉스 | -0.16% | -1.38% | +1.83% | +0.59% | 2.42% | N/N/N | N/A | NOT_SCORABLE |
| 08:30 A2 #1 | S-Oil | -6.63% | -8.23% | +2.95% | +1.18% | 8.62% | N/N/N | N/A | NOT_SCORABLE |
| 08:30 A2 #2 | 흥구석유 | +20.02% | +13.98% | +29.94% | +23.41% | 0.00% | Y/Y/Y | N/A | NOT_SCORABLE |
| 08:30 A2 #3 | SK이노베이션 | -0.26% | -1.54% | +7.30% | +5.92% | 2.15% | Y/Y/N | N/A | NOT_SCORABLE |

AE는 전일 종가 기준 하방폭이며 진입 후 손실이 아니다. 조건부 계획은 일봉 안의 돌파·지지·무효화 순서를 확정할 수 없어 체결이나 실현수익을 판정하지 않았다. 삼성전자는 고가가 275,000원 진입 기준에 미달해 NOT_TRIGGERED다.

## 4. 에이전트별 KPI

| 슬롯 | 에이전트 | TOP1 FE/OFE | TOP3 평균 FE/OFE/AE | 전체 평균 FE/OFE/AE | FE3/5/10 | Spearman | 유효 표본 |
|---|---|---|---|---|---|---|---|
| 03:30 | Agent 1 | 7.91% / 6.46% | 7.91% / 6.46% / 2.59% | 동일 | 100.00% / 100.00% / 0.00% | N/A (n=1) | 각 1/1 |
| 03:30 | Agent 2 | 2.95% / 1.18% | 1.72% / 0.78% / 4.42% | 동일 | 0.00% / 0.00% / 0.00% | +0.500 (n=3) | 각 3/3 |
| 08:30 | Agent 1 | N/A | N/A | N/A | N/A | N/A | 입력 누락 |
| 08:30 | Agent 2 | 2.95% / 1.18% | 13.40% / 10.17% / 3.59% | 동일 | 66.67% / 66.67% / 33.33% | -0.500 (n=3) | 각 3/3 |

Agent 1의 03:30 예상 FE 구간 적합률은 1/1, 100.00%다. Agent 2는 ExpectedMoveFE를 제공하지 않아 역산하지 않았다. 상관계수는 소표본 일일 관찰값이다.

## 5. Agent 1 vs Agent 2

### 03:30

Agent 1이 TOP1 FE(7.91% 대 2.95%), 평균 FE·OFE, AE에서 모두 우세했다. 우리로 한 종목만 제시했으므로 폭넓은 후보 탐색 비교에는 한계가 있지만, 실제 FE가 예상 +5~10% 구간에 들어와 당일 선택은 성공했다. Agent 2의 세 후보는 모두 FE3에 미달했고 특히 S-Oil은 시가 이후 급반전했다.

### 08:30

Agent 1 입력이 없어 에이전트 간 비교와 BEST_AGENT는 N/A다. 존재하는 공식 입력 중 최우수 후보는 Agent 2의 흥구석유(FE 29.94%)지만 이를 Agent 1 대비 우승으로 해석하지 않는다.

## 6. 동일 에이전트의 시간대 비교

Agent 1은 08:30 입력 누락으로 비교 불가다.

Agent 2는 08:30을 새 정보 기반 독립 분석으로 평가했다. 평균 FE가 1.72%에서 13.40%, FE3 적중률이 0.00%에서 66.67%로 개선됐다. 새로 포함한 흥구석유(FE 29.94%)와 SK이노베이션(FE 7.30%)이 개선을 만들었다. 반면 실제 FE가 가장 낮은 S-Oil(2.95%)을 계속 1순위로 두고 흥구석유를 2순위로 둬 순위 상관은 +0.500에서 -0.500으로 악화했다.

## 7. 성공·오류 분석

- Agent 1 03:30: 우리로는 FE 7.91%, OFE 6.46%, 종가 +1.98%로 한 종목 집중 발굴이 적중했다. 다만 표본 1개이고 위험도 HIGH·확신도 LOW였으므로 일반화하지 않는다.
- Agent 2 08:30: 국제유가 촉매의 국내 테마 전달경로를 확장해 흥구석유와 SK이노베이션을 추가한 판단은 성공했다. 특히 흥구석유는 AE 0.00%와 FE 29.94%를 기록했다.
- Agent 2 공통 오류: 직접 수혜 논리의 S-Oil을 1순위로 유지했지만, S-Oil은 갭 상승 뒤 C2C -6.63%, O2C -8.23%, AE 8.62%로 반전했다. 입력이 언급한 갭 소진 위험은 맞았으나 순위에 충분히 반영되지 않았다.
- SK이노베이션은 FE 7.30%와 OFE 5.92%에도 종가가 -0.26%여서, 큰 장중 움직임과 종가 지속성을 구분해야 함을 보여준다.
- 삼성전자·SK하이닉스는 각각 FE 0.37%, 1.83%로 AI/메모리 촉매가 큰 당일 가격발견으로 이어지지 않았다.

## 8. 개선 후보

관찰 근거는 Agent 2의 08:30 후보 간 성과 격차다. 후속 슬롯에서 같은 거시 촉매 후보를 정렬할 때 직접 수혜 규모만으로 기존 1순위를 유지하지 말고, 전일 선반영·시가 갭 소진·국내 테마 탄력의 상대 차이를 명시적으로 비교하는 규칙을 검토할 수 있다. 기대효과는 흥구석유 같은 잔여 가격발견 후보의 상위 배치다. 부작용은 소형 테마주의 투기성과 체결 위험을 과대평가할 수 있다는 점이다. 단일 거래일 증거이므로 프롬프트 변경이나 활성 규칙 승격은 하지 않는다.

## 9. 최종 요약

03:30 공식 비교는 Agent 1 승리이며 최우수 후보는 우리로다. 08:30은 Agent 1 입력 누락으로 에이전트 간 승자를 정할 수 없지만, Agent 2가 새 정보로 흥구석유의 큰 움직임을 포착했다. Agent 2의 후보 발굴 폭은 개선됐으나 순위 정렬은 악화했다.

[REVIEW_RESULT]
SCHEMA_VERSION: DMI_REVIEW_v1.3
DATE: 2026-09-10
PREDICTION_RUN_TIME_KST: 03:30
AGENT_1_STATUS: OFFICIAL
AGENT_2_STATUS: OFFICIAL
AGENT_1_COUNT: 1
AGENT_2_COUNT: 3
AGENT_1_TOP1_FE: 7.91%
AGENT_2_TOP1_FE: 2.95%
AGENT_1_TOP3_AVG_FE: 7.91%
AGENT_2_TOP3_AVG_FE: 1.72%
AGENT_1_FE3_HIT_RATE: 100.00%
AGENT_2_FE3_HIT_RATE: 0.00%
AGENT_1_FE5_HIT_RATE: 100.00%
AGENT_2_FE5_HIT_RATE: 0.00%
AGENT_1_FE10_HIT_RATE: 0.00%
AGENT_2_FE10_HIT_RATE: 0.00%
AGENT_1_VALID_FE_COUNT: 1
AGENT_2_VALID_FE_COUNT: 3
AGENT_1_TOP3_VALID_FE_COUNT: 1
AGENT_2_TOP3_VALID_FE_COUNT: 3
AGENT_1_RANK_PERFORMANCE_SPEARMAN: N/A
AGENT_2_RANK_PERFORMANCE_SPEARMAN: +0.500
AGENT_1_RANK_PERFORMANCE_PAIR_COUNT: 1
AGENT_2_RANK_PERFORMANCE_PAIR_COUNT: 3
BEST_AGENT: AGENT_1
BEST_PICK: 우리로(046970)
PRIMARY_SUCCESS_PATTERN: 우리로 단일 후보의 실제 FE가 예상 +5~10% 구간에 적합
PRIMARY_ERROR_PATTERN: Agent 2의 세 후보 모두 FE3 미달, S-Oil 갭 소진·급반전
IMPROVEMENT_CANDIDATE: 직접 수혜와 잔여 가격발견·갭 소진 위험을 함께 반영한 상대 순위 검토
[/REVIEW_RESULT]

[REVIEW_RESULT]
SCHEMA_VERSION: DMI_REVIEW_v1.3
DATE: 2026-09-10
PREDICTION_RUN_TIME_KST: 08:30
AGENT_1_STATUS: UNAVAILABLE
AGENT_2_STATUS: OFFICIAL
AGENT_1_COUNT: N/A
AGENT_2_COUNT: 3
AGENT_1_TOP1_FE: N/A
AGENT_2_TOP1_FE: 2.95%
AGENT_1_TOP3_AVG_FE: N/A
AGENT_2_TOP3_AVG_FE: 13.40%
AGENT_1_FE3_HIT_RATE: N/A
AGENT_2_FE3_HIT_RATE: 66.67%
AGENT_1_FE5_HIT_RATE: N/A
AGENT_2_FE5_HIT_RATE: 66.67%
AGENT_1_FE10_HIT_RATE: N/A
AGENT_2_FE10_HIT_RATE: 33.33%
AGENT_1_VALID_FE_COUNT: N/A
AGENT_2_VALID_FE_COUNT: 3
AGENT_1_TOP3_VALID_FE_COUNT: N/A
AGENT_2_TOP3_VALID_FE_COUNT: 3
AGENT_1_RANK_PERFORMANCE_SPEARMAN: N/A
AGENT_2_RANK_PERFORMANCE_SPEARMAN: -0.500
AGENT_1_RANK_PERFORMANCE_PAIR_COUNT: N/A
AGENT_2_RANK_PERFORMANCE_PAIR_COUNT: 3
BEST_AGENT: N/A
BEST_PICK: 흥구석유(024060)
PRIMARY_SUCCESS_PATTERN: Agent 2가 08:30 새 정보로 흥구석유 FE 29.94%와 SK이노베이션 FE 7.30% 포착
PRIMARY_ERROR_PATTERN: Agent 1 입력 누락으로 교차 비교 불가; Agent 2는 최저 FE의 S-Oil을 1순위로 유지
IMPROVEMENT_CANDIDATE: 후속 슬롯에서 전일 선반영·시가 갭 소진·테마 탄력의 상대 비교 검토
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
      "reason": "기본 브랜치에서 읽은 내용과 Git blob SHA가 연결됨; 조회시각은 도구 응답에서 미제공"
    },
    {
      "role": "SOURCES",
      "repository": "totjae/dmi-market-pipeline",
      "path": "config/SOURCES.md",
      "commit_sha": null,
      "blob_sha": "5c47de7afdb65f60bc81a0050058a4c71d332853",
      "read_at_kst": null,
      "status": "VERIFIED",
      "reason": "기본 브랜치에서 읽은 내용과 Git blob SHA가 연결됨; 조회시각은 도구 응답에서 미제공"
    },
    {
      "role": "REVIEW_PROMPT",
      "repository": "totjae/dmi-market-pipeline",
      "path": "prompt/REVIEW_PROMPT.md",
      "commit_sha": null,
      "blob_sha": "fbd5f2e1f490a2b5a68ae8b095b58bccbbc19cb2",
      "read_at_kst": null,
      "status": "VERIFIED",
      "reason": "기본 브랜치에서 읽은 내용과 Git blob SHA가 연결됨; 조회시각은 도구 응답에서 미제공"
    },
    {
      "role": "REVIEW_OUTPUT",
      "repository": "totjae/dmi-market-pipeline",
      "path": "templates/REVIEW_OUTPUT.md",
      "commit_sha": null,
      "blob_sha": "aced9658e7423ac059150f7d5cdf069efce21849",
      "read_at_kst": null,
      "status": "VERIFIED",
      "reason": "기본 브랜치에서 읽은 내용과 Git blob SHA가 연결됨; 조회시각은 도구 응답에서 미제공"
    }
  ],
  "input_manifest": [
    {
      "input_id": "a1_20260910_0330",
      "agent_id": "AGENT_1",
      "date": "2026-09-10",
      "slot_kst": "03:30",
      "repository": "totjae/dmi-agent-1",
      "path": "runs/2026-09-10/0330.md",
      "evaluated_commit_sha": "fbbae2b8957e48538a8c8fe35ff941569105ddaa",
      "evaluated_blob_sha": "6a74766885d21ac0ca05860c629a1d789b60fb01",
      "first_saved_commit_sha": "fbbae2b8957e48538a8c8fe35ff941569105ddaa",
      "first_saved_at_kst": "2026-09-10T03:34:43+09:00",
      "selection_status": "OFFICIAL",
      "selection_reason": "DMI_AGENT_v1.3 구조·날짜·슬롯·cutoff·본문/캡슐 일치 확인. KRX 정규장 개장 09:00 KST 이전 최초 저장된 유효 예측이며 더 이른 유효 파일 없음.",
      "prediction_schema_version": "DMI_AGENT_v1.3",
      "prediction_document_versions": [
        {
          "role": "WORKFLOW",
          "repository": "totjae/dmi-agent-1",
          "path": "WORKFLOW.md",
          "commit_sha": "N/A",
          "blob_sha": "83918da3d6630b6c3b9cdf76a8e0a911dffe0eef",
          "read_at_kst": "2026-09-10T03:31:06+09:00",
          "status": "VERIFIED"
        },
        {
          "role": "AGENT_PROMPT",
          "repository": "totjae/dmi-agent-1",
          "path": "prompt/AGENT_PROMPT.md",
          "commit_sha": "N/A",
          "blob_sha": "c000680472231d27bc5388adf55c7b05378046b5",
          "read_at_kst": "2026-09-10T03:31:06+09:00",
          "status": "VERIFIED"
        },
        {
          "role": "OUTPUT",
          "repository": "totjae/dmi-agent-1",
          "path": "templates/OUTPUT.md",
          "commit_sha": "N/A",
          "blob_sha": "d570db4d1d175e111c8d2f5c4bc3be6614ca400c",
          "read_at_kst": "2026-09-10T03:32:55+09:00",
          "status": "VERIFIED"
        }
      ],
      "version_status": "UNVERIFIED"
    },
    {
      "input_id": "a1_20260910_0830",
      "agent_id": "AGENT_1",
      "date": "2026-09-10",
      "slot_kst": "08:30",
      "repository": "totjae/dmi-agent-1",
      "path": "runs/2026-09-10/0830.md",
      "evaluated_commit_sha": null,
      "evaluated_blob_sha": null,
      "first_saved_commit_sha": null,
      "first_saved_at_kst": null,
      "selection_status": "UNAVAILABLE",
      "selection_reason": "MISSING_FILE: 기본 경로가 존재하지 않고 선택 가능한 결과가 확인되지 않음.",
      "prediction_schema_version": null,
      "prediction_document_versions": [],
      "version_status": "NOT_PROVIDED"
    },
    {
      "input_id": "a2_20260910_0330",
      "agent_id": "AGENT_2",
      "date": "2026-09-10",
      "slot_kst": "03:30",
      "repository": "totjae/dmi-agent-2",
      "path": "runs/2026-09-10/0330.md",
      "evaluated_commit_sha": "2706925cd584a1d8ae16583fd4a67f841b918eb1",
      "evaluated_blob_sha": "1360ce650d75d2a6579112e44f38c3147a0952f4",
      "first_saved_commit_sha": "2706925cd584a1d8ae16583fd4a67f841b918eb1",
      "first_saved_at_kst": "2026-09-10T04:00:22+09:00",
      "selection_status": "OFFICIAL",
      "selection_reason": "DMI_AGENT_v1.3 구조·날짜·슬롯·cutoff·본문/캡슐 일치 확인. KRX 정규장 개장 09:00 KST 이전 최초 저장된 유효 예측이며 더 이른 유효 파일 없음.",
      "prediction_schema_version": "DMI_AGENT_v1.3",
      "prediction_document_versions": [
        {
          "role": "WORKFLOW",
          "repository": "totjae/dmi-agent-2",
          "path": "WORKFLOW.md",
          "commit_sha": "N/A",
          "blob_sha": "601b0b7fde747f6e81a7bc7f0e43a86e08f3ec6a",
          "read_at_kst": "N/A",
          "status": "VERIFIED"
        },
        {
          "role": "AGENT_PROMPT",
          "repository": "totjae/dmi-agent-2",
          "path": "prompt/AGENT_PROMPT.md",
          "commit_sha": "N/A",
          "blob_sha": "bd5f67ceacc307fd629273719cc57b22720e96bc",
          "read_at_kst": "N/A",
          "status": "VERIFIED"
        },
        {
          "role": "OUTPUT",
          "repository": "totjae/dmi-agent-2",
          "path": "templates/OUTPUT.md",
          "commit_sha": "N/A",
          "blob_sha": "d570db4d1d175e111c8d2f5c4bc3be6614ca400c",
          "read_at_kst": "2026-09-10T03:58:02+09:00",
          "status": "VERIFIED"
        }
      ],
      "version_status": "UNVERIFIED"
    },
    {
      "input_id": "a2_20260910_0830",
      "agent_id": "AGENT_2",
      "date": "2026-09-10",
      "slot_kst": "08:30",
      "repository": "totjae/dmi-agent-2",
      "path": "runs/2026-09-10/0830.md",
      "evaluated_commit_sha": "8073403308bfe22764697557b407ce5f7ee8f8e7",
      "evaluated_blob_sha": "562245e671bcaf8ca43c0ea98d22dd6ccf1858df",
      "first_saved_commit_sha": "8073403308bfe22764697557b407ce5f7ee8f8e7",
      "first_saved_at_kst": "2026-09-10T08:38:03+09:00",
      "selection_status": "OFFICIAL",
      "selection_reason": "DMI_AGENT_v1.3 구조·날짜·슬롯·cutoff·본문/캡슐 일치 확인. KRX 정규장 개장 09:00 KST 이전 최초 저장된 유효 예측이며 더 이른 유효 파일 없음.",
      "prediction_schema_version": "DMI_AGENT_v1.3",
      "prediction_document_versions": [
        {
          "role": "WORKFLOW",
          "repository": "totjae/dmi-agent-2",
          "path": "WORKFLOW.md",
          "commit_sha": "N/A",
          "blob_sha": "601b0b7fde747f6e81a7bc7f0e43a86e08f3ec6a",
          "read_at_kst": "N/A",
          "status": "VERIFIED"
        },
        {
          "role": "AGENT_PROMPT",
          "repository": "totjae/dmi-agent-2",
          "path": "prompt/AGENT_PROMPT.md",
          "commit_sha": "N/A",
          "blob_sha": "bd5f67ceacc307fd629273719cc57b22720e96bc",
          "read_at_kst": "N/A",
          "status": "VERIFIED"
        },
        {
          "role": "OUTPUT",
          "repository": "totjae/dmi-agent-2",
          "path": "templates/OUTPUT.md",
          "commit_sha": "N/A",
          "blob_sha": "d570db4d1d175e111c8d2f5c4bc3be6614ca400c",
          "read_at_kst": "N/A",
          "status": "VERIFIED"
        }
      ],
      "version_status": "UNVERIFIED"
    }
  ],
  "price_sources": [
    {
      "source_id": "price_046970",
      "provider": "Npay 증권 (한국거래소 KRX 제공 종합정보)",
      "url": "https://finance.naver.com/item/main.naver?code=046970",
      "retrieved_at_kst": "2026-09-10T16:38:52+09:00",
      "observation_date": "2026-09-10",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": "동일 페이지의 2026-09-10 KRX 장마감 전일가·시가·고가·저가·종가 원자료; 별도 수정주가 혼합 없음",
      "status": "VERIFIED",
      "reason": "우리로 종목 페이지가 2026-09-10 KRX 장마감과 전일가/OHLC를 명시"
    },
    {
      "source_id": "price_010950",
      "provider": "Npay 증권 (한국거래소 KRX 제공 종합정보)",
      "url": "https://finance.naver.com/item/main.naver?code=010950",
      "retrieved_at_kst": "2026-09-10T16:38:52+09:00",
      "observation_date": "2026-09-10",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": "동일 페이지의 2026-09-10 KRX 장마감 전일가·시가·고가·저가·종가 원자료; 별도 수정주가 혼합 없음",
      "status": "VERIFIED",
      "reason": "S-Oil 종목 페이지가 2026-09-10 KRX 장마감과 전일가/OHLC를 명시"
    },
    {
      "source_id": "price_005930",
      "provider": "Npay 증권 (한국거래소 KRX 제공 종합정보)",
      "url": "https://finance.naver.com/item/main.naver?code=005930",
      "retrieved_at_kst": "2026-09-10T16:38:52+09:00",
      "observation_date": "2026-09-10",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": "동일 페이지의 2026-09-10 KRX 장마감 전일가·시가·고가·저가·종가 원자료; 별도 수정주가 혼합 없음",
      "status": "VERIFIED",
      "reason": "삼성전자 종목 페이지가 2026-09-10 KRX 장마감과 전일가/OHLC를 명시"
    },
    {
      "source_id": "price_000660",
      "provider": "Npay 증권 (한국거래소 KRX 제공 종합정보)",
      "url": "https://finance.naver.com/item/main.naver?code=000660",
      "retrieved_at_kst": "2026-09-10T16:38:52+09:00",
      "observation_date": "2026-09-10",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": "동일 페이지의 2026-09-10 KRX 장마감 전일가·시가·고가·저가·종가 원자료; 별도 수정주가 혼합 없음",
      "status": "VERIFIED",
      "reason": "SK하이닉스 종목 페이지가 2026-09-10 KRX 장마감과 전일가/OHLC를 명시"
    },
    {
      "source_id": "price_024060",
      "provider": "Npay 증권 (한국거래소 KRX 제공 종합정보)",
      "url": "https://finance.naver.com/item/main.naver?code=024060",
      "retrieved_at_kst": "2026-09-10T16:38:52+09:00",
      "observation_date": "2026-09-10",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": "동일 페이지의 2026-09-10 KRX 장마감 전일가·시가·고가·저가·종가 원자료; 별도 수정주가 혼합 없음",
      "status": "VERIFIED",
      "reason": "흥구석유 종목 페이지가 2026-09-10 KRX 장마감과 전일가/OHLC를 명시"
    },
    {
      "source_id": "price_096770",
      "provider": "Npay 증권 (한국거래소 KRX 제공 종합정보)",
      "url": "https://finance.naver.com/item/main.naver?code=096770",
      "retrieved_at_kst": "2026-09-10T16:38:52+09:00",
      "observation_date": "2026-09-10",
      "venue": "KRX",
      "session": "REGULAR",
      "currency": "KRW",
      "adjustment_basis": "동일 페이지의 2026-09-10 KRX 장마감 전일가·시가·고가·저가·종가 원자료; 별도 수정주가 혼합 없음",
      "status": "VERIFIED",
      "reason": "SK이노베이션 종목 페이지가 2026-09-10 KRX 장마감과 전일가/OHLC를 명시"
    }
  ],
  "candidates": [
    {
      "input_id": "a1_20260910_0330",
      "rank": 1,
      "code": "046970",
      "name": "우리로",
      "market": "KOSDAQ",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 6570,
          "source_ids": [
            "price_046970"
          ]
        },
        "open": {
          "value": 6660,
          "source_ids": [
            "price_046970"
          ]
        },
        "high": {
          "value": 7090,
          "source_ids": [
            "price_046970"
          ]
        },
        "low": {
          "value": 6400,
          "source_ids": [
            "price_046970"
          ]
        },
        "close": {
          "value": 6700,
          "source_ids": [
            "price_046970"
          ]
        }
      },
      "metrics_pct": {
        "c2c": 1.97869101978691,
        "o2c": 0.6006006006006006,
        "fe": 7.91476407914764,
        "ofe": 6.456456456456457,
        "ae": 2.5875190258751903
      },
      "hits": {
        "fe3": true,
        "fe5": true,
        "fe10": false
      },
      "expected_fe_range_match": true,
      "trade_plan": {
        "status": "NOT_SCORABLE",
        "report_reference": "AGENT_1 03:30 STAGE_REPORT 후보 1 무효화 조건",
        "reason": "6,570원 회복·지지 및 갭 실패의 시간순서를 일봉 OHLC만으로 확인할 수 없음",
        "evidence_urls": [
          "https://finance.naver.com/item/main.naver?code=046970"
        ]
      },
      "missing_reasons": []
    },
    {
      "input_id": "a2_20260910_0330",
      "rank": 1,
      "code": "010950",
      "name": "S-Oil",
      "market": "KOSPI",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 165900,
          "source_ids": [
            "price_010950"
          ]
        },
        "open": {
          "value": 168800,
          "source_ids": [
            "price_010950"
          ]
        },
        "high": {
          "value": 170800,
          "source_ids": [
            "price_010950"
          ]
        },
        "low": {
          "value": 151600,
          "source_ids": [
            "price_010950"
          ]
        },
        "close": {
          "value": 154900,
          "source_ids": [
            "price_010950"
          ]
        }
      },
      "metrics_pct": {
        "c2c": -6.630500301386377,
        "o2c": -8.234597156398104,
        "fe": 2.9535864978902953,
        "ofe": 1.1848341232227488,
        "ae": 8.61965039180229
      },
      "hits": {
        "fe3": false,
        "fe5": false,
        "fe10": false
      },
      "expected_fe_range_match": null,
      "trade_plan": {
        "status": "NOT_SCORABLE",
        "report_reference": "AGENT_2 03:30 STAGE_REPORT Rank 1 진입 계획",
        "reason": "168,600원 돌파와 168,700원 이상 지지의 시간순서를 일봉 OHLC만으로 확인할 수 없음",
        "evidence_urls": [
          "https://finance.naver.com/item/main.naver?code=010950"
        ]
      },
      "missing_reasons": [
        {
          "field": "expected_fe_range_match",
          "status": "NOT_PROVIDED",
          "reason": "입력에 ExpectedMoveFE 수치 구간이 제공되지 않음"
        }
      ]
    },
    {
      "input_id": "a2_20260910_0330",
      "rank": 2,
      "code": "005930",
      "name": "삼성전자",
      "market": "KOSPI",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 269500,
          "source_ids": [
            "price_005930"
          ]
        },
        "open": {
          "value": 269000,
          "source_ids": [
            "price_005930"
          ]
        },
        "high": {
          "value": 270500,
          "source_ids": [
            "price_005930"
          ]
        },
        "low": {
          "value": 263500,
          "source_ids": [
            "price_005930"
          ]
        },
        "close": {
          "value": 269000,
          "source_ids": [
            "price_005930"
          ]
        }
      },
      "metrics_pct": {
        "c2c": -0.1855287569573284,
        "o2c": 0,
        "fe": 0.3710575139146568,
        "ofe": 0.5576208178438662,
        "ae": 2.2263450834879404
      },
      "hits": {
        "fe3": false,
        "fe5": false,
        "fe10": false
      },
      "expected_fe_range_match": null,
      "trade_plan": {
        "status": "NOT_TRIGGERED",
        "report_reference": "AGENT_2 03:30 STAGE_REPORT Rank 2 진입 계획",
        "reason": "정규장 고가 270,500원으로 진입 조건인 275,000원 돌파에 미달",
        "evidence_urls": [
          "https://finance.naver.com/item/main.naver?code=005930"
        ]
      },
      "missing_reasons": [
        {
          "field": "expected_fe_range_match",
          "status": "NOT_PROVIDED",
          "reason": "입력에 ExpectedMoveFE 수치 구간이 제공되지 않음"
        }
      ]
    },
    {
      "input_id": "a2_20260910_0330",
      "rank": 3,
      "code": "000660",
      "name": "SK하이닉스",
      "market": "KOSPI",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 1856000,
          "source_ids": [
            "price_000660"
          ]
        },
        "open": {
          "value": 1879000,
          "source_ids": [
            "price_000660"
          ]
        },
        "high": {
          "value": 1890000,
          "source_ids": [
            "price_000660"
          ]
        },
        "low": {
          "value": 1811000,
          "source_ids": [
            "price_000660"
          ]
        },
        "close": {
          "value": 1853000,
          "source_ids": [
            "price_000660"
          ]
        }
      },
      "metrics_pct": {
        "c2c": -0.16163793103448276,
        "o2c": -1.3837147418839808,
        "fe": 1.8318965517241377,
        "ofe": 0.5854177754124534,
        "ae": 2.4245689655172415
      },
      "hits": {
        "fe3": false,
        "fe5": false,
        "fe10": false
      },
      "expected_fe_range_match": null,
      "trade_plan": {
        "status": "NOT_SCORABLE",
        "report_reference": "AGENT_2 03:30 STAGE_REPORT Rank 3 진입 계획",
        "reason": "1,883,000원 돌파 가격 접촉은 있었으나 지지·거래량과 시간순서를 일봉 OHLC만으로 확인할 수 없음",
        "evidence_urls": [
          "https://finance.naver.com/item/main.naver?code=000660"
        ]
      },
      "missing_reasons": [
        {
          "field": "expected_fe_range_match",
          "status": "NOT_PROVIDED",
          "reason": "입력에 ExpectedMoveFE 수치 구간이 제공되지 않음"
        }
      ]
    },
    {
      "input_id": "a2_20260910_0830",
      "rank": 1,
      "code": "010950",
      "name": "S-Oil",
      "market": "KOSPI",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 165900,
          "source_ids": [
            "price_010950"
          ]
        },
        "open": {
          "value": 168800,
          "source_ids": [
            "price_010950"
          ]
        },
        "high": {
          "value": 170800,
          "source_ids": [
            "price_010950"
          ]
        },
        "low": {
          "value": 151600,
          "source_ids": [
            "price_010950"
          ]
        },
        "close": {
          "value": 154900,
          "source_ids": [
            "price_010950"
          ]
        }
      },
      "metrics_pct": {
        "c2c": -6.630500301386377,
        "o2c": -8.234597156398104,
        "fe": 2.9535864978902953,
        "ofe": 1.1848341232227488,
        "ae": 8.61965039180229
      },
      "hits": {
        "fe3": false,
        "fe5": false,
        "fe10": false
      },
      "expected_fe_range_match": null,
      "trade_plan": {
        "status": "NOT_SCORABLE",
        "report_reference": "AGENT_2 08:30 STAGE_REPORT Rank 1 진입 계획",
        "reason": "168,600원 돌파와 이후 지지의 시간순서를 일봉 OHLC만으로 확인할 수 없음",
        "evidence_urls": [
          "https://finance.naver.com/item/main.naver?code=010950"
        ]
      },
      "missing_reasons": [
        {
          "field": "expected_fe_range_match",
          "status": "NOT_PROVIDED",
          "reason": "입력에 ExpectedMoveFE 수치 구간이 제공되지 않음"
        }
      ]
    },
    {
      "input_id": "a2_20260910_0830",
      "rank": 2,
      "code": "024060",
      "name": "흥구석유",
      "market": "KOSDAQ",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 12090,
          "source_ids": [
            "price_024060"
          ]
        },
        "open": {
          "value": 12730,
          "source_ids": [
            "price_024060"
          ]
        },
        "high": {
          "value": 15710,
          "source_ids": [
            "price_024060"
          ]
        },
        "low": {
          "value": 12720,
          "source_ids": [
            "price_024060"
          ]
        },
        "close": {
          "value": 14510,
          "source_ids": [
            "price_024060"
          ]
        }
      },
      "metrics_pct": {
        "c2c": 20.016542597187758,
        "o2c": 13.982717989002358,
        "fe": 29.942100909842846,
        "ofe": 23.409269442262374,
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
        "report_reference": "AGENT_2 08:30 STAGE_REPORT Rank 2 진입 계획",
        "reason": "12,800원 돌파 가격 접촉은 있었으나 지지·거래량과 시간순서를 일봉 OHLC만으로 확인할 수 없음",
        "evidence_urls": [
          "https://finance.naver.com/item/main.naver?code=024060"
        ]
      },
      "missing_reasons": [
        {
          "field": "expected_fe_range_match",
          "status": "NOT_PROVIDED",
          "reason": "입력에 ExpectedMoveFE 수치 구간이 제공되지 않음"
        }
      ]
    },
    {
      "input_id": "a2_20260910_0830",
      "rank": 3,
      "code": "096770",
      "name": "SK이노베이션",
      "market": "KOSPI",
      "evaluation_scope": "OFFICIAL",
      "prices": {
        "previous_close": {
          "value": 153500,
          "source_ids": [
            "price_096770"
          ]
        },
        "open": {
          "value": 155500,
          "source_ids": [
            "price_096770"
          ]
        },
        "high": {
          "value": 164700,
          "source_ids": [
            "price_096770"
          ]
        },
        "low": {
          "value": 150200,
          "source_ids": [
            "price_096770"
          ]
        },
        "close": {
          "value": 153100,
          "source_ids": [
            "price_096770"
          ]
        }
      },
      "metrics_pct": {
        "c2c": -0.26058631921824105,
        "o2c": -1.5434083601286173,
        "fe": 7.296416938110749,
        "ofe": 5.916398713826367,
        "ae": 2.1498371335504887
      },
      "hits": {
        "fe3": true,
        "fe5": true,
        "fe10": false
      },
      "expected_fe_range_match": null,
      "trade_plan": {
        "status": "NOT_SCORABLE",
        "report_reference": "AGENT_2 08:30 STAGE_REPORT Rank 3 진입 계획",
        "reason": "155,400원 돌파 가격 접촉은 있었으나 이후 지지의 시간순서를 일봉 OHLC만으로 확인할 수 없음",
        "evidence_urls": [
          "https://finance.naver.com/item/main.naver?code=096770"
        ]
      },
      "missing_reasons": [
        {
          "field": "expected_fe_range_match",
          "status": "NOT_PROVIDED",
          "reason": "입력에 ExpectedMoveFE 수치 구간이 제공되지 않음"
        }
      ]
    }
  ]
}
[/REVIEW_EVIDENCE]
