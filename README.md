# DMI Market Review

`dmi-agent-1`과 `dmi-agent-2`의 독립 예측 결과를 장 마감 후 동일 기준으로 비교하는 리뷰 저장소입니다.

## 현재 구조

- `config/SOURCES.md`: 비교 대상 저장소와 입력 경로
- `prompt/REVIEW_PROMPT.md`: 리뷰 지침
- `templates/REVIEW_OUTPUT.md`: 리뷰 저장 형식
- `reviews/YYYY-MM-DD/`: 새 리뷰 결과
- `legacy/`: 이전 파이프라인의 프롬프트·결과·테스트 자료

예측 에이전트는 이 저장소를 읽지 않습니다. 리뷰 작업만 두 에이전트 저장소의 확정 결과를 읽습니다.
