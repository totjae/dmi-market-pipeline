# DMI Stage Output Template

Use the stage's original prompt schema inside these wrappers. Do not replace the original report with a summary.

```text
[DMI_RUN_META]
SCHEMA_VERSION: DMI_v7.1
DATE: YYYY-MM-DD
STAGE: HH:MM
RUN_TIME_KST: YYYY-MM-DD HH:MM:SS
[/DMI_RUN_META]

[STAGE_REPORT]
<complete original stage output>
[/STAGE_REPORT]

[STAGE_HANDOFF]
<original HANDOFF capsule; omit only when the stage has no HANDOFF>
[/STAGE_HANDOFF]

[STAGE_REVIEW_CAPSULE]
<16:30 only: original REVIEW capsule>
[/STAGE_REVIEW_CAPSULE]
```

The output path is determined by `/WORKFLOW.md`.
