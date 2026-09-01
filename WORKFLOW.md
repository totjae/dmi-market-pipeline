# DMI v7.1 Work Contract

This repository is the persistent state store for the DMI v7.1 market-analysis pipeline.

## Target

- Repository: `totjae/dmi-market-pipeline`
- Branch: `main`
- Output root: `runs/YYYY-MM-DD/`
- Schema: `DMI_v7.1`

## Stage file names

Use these sortable names for the normal scheduled run:

1. `01_0330_overnight_radar.md`
2. `02_0720_morning_macro.md`
3. `03_0825_morning_picks.md`
4. `04_1630_daily_review.md`

A normal scheduled run creates its stage file if it does not already exist. Never overwrite or delete a previous successful run just to make the current run fit.

If a stage must be rerun and its normal file already exists, create a new file instead:

`<normal-stem>_rerun_HHMMSS.md`

Example: `02_0720_morning_macro_rerun_074512.md`

When a later stage needs an earlier stage, use the latest valid file for that stage on the same date. The normal filename is valid unless a later rerun file exists.

## Independence rules

### 01 / 03:30 Overnight Radar
- Perform the stage independently.
- Do not use same-day DMI stage output as an input to candidate generation or judgment.

### 02 / 07:20 Morning Macro
- Complete the independent fresh scan first.
- Only after the independent judgment is complete, read the latest same-day 03:30 HANDOFF for comparison.
- If unavailable, use `PREVIOUS_STAGE_UNAVAILABLE`; do not reconstruct it.

### 03 / 08:25 Morning Picks
- Complete independent Fresh Scan, candidate selection, Rank, and Base Score first.
- Only after that is complete, read the latest same-day 03:30 and 07:20 HANDOFF sections for comparison.
- Missing prior-stage information is `PREVIOUS_STAGE_UNAVAILABLE`; do not infer it from current market conditions.

### 04 / 16:30 Daily Review
- Read the latest valid same-day outputs for stages 01-03.
- Use stored HANDOFF sections where the review requires handoff data and stored REPORT sections where the original full report is required.
- Do not reconstruct morning predictions using the afternoon outcome.
- Missing data remains `PREVIOUS_STAGE_UNAVAILABLE`.

## Required file envelope

Every stage output file should preserve the stage's original schema and include this outer envelope:

```text
[DMI_RUN_META]
SCHEMA_VERSION: DMI_v7.1
DATE: YYYY-MM-DD
STAGE: HH:MM
RUN_TIME_KST: YYYY-MM-DD HH:MM:SS
[/DMI_RUN_META]

[STAGE_REPORT]
<complete stage report exactly as produced>
[/STAGE_REPORT]

[STAGE_HANDOFF]
<original HANDOFF capsule exactly as produced, when applicable>
[/STAGE_HANDOFF]
```

For the 16:30 review, preserve the original final REVIEW capsule inside the report and additionally expose it as:

```text
[STAGE_REVIEW_CAPSULE]
<original REVIEW capsule>
[/STAGE_REVIEW_CAPSULE]
```

## Write boundaries

- Create files only inside `runs/YYYY-MM-DD/` unless the user explicitly requests another location.
- Do not modify prompt/source files while running the pipeline.
- Do not delete prior stage outputs.
- Do not rewrite another stage's output.
- Do not manufacture missing prior-stage values.
- Preserve the original report, field names, enum values, ordering, scores, and HANDOFF/REVIEW structure.

## Completion check

A stage is complete only when its output file has been created successfully in the expected dated directory. Report the exact repository path written. If the write does not complete, report that persistence failed rather than claiming the stage was stored.
