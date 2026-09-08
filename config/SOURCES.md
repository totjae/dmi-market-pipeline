# Review Sources

| Agent ID | Repository | Prompt ownership | Run path |
|---|---|---|---|
| AGENT_1 | `totjae/dmi-agent-1` | 사용자 관리 | `runs/YYYY-MM-DD/HHMM.md` |
| AGENT_2 | `totjae/dmi-agent-2` | 사용자 관리 | `runs/YYYY-MM-DD/HHMM.md` |

리뷰 작업은 지정된 날짜·시각의 실행 결과만 읽습니다. 각 에이전트의 프롬프트와 과거 결과는 읽지 않습니다.

일일 16:30 KST 리뷰 입력 슬롯: 03:30, 08:30. 총 4개 에이전트·슬롯 조합을 각각 검증한다. HHMM은 0330 또는 0830이다. 정상 결과 선택 및 지연·복구 처리 기준은 /WORKFLOW.md를 따른다.
