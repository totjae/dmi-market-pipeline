# DMI Run Storage

Scheduled ChatGPT Work runs store immutable daily stage outputs under this directory.

Path pattern:

`runs/YYYY-MM-DD/<stage-file>.md`

Normal stage files:

- `01_0330_overnight_radar.md`
- `02_0720_morning_macro.md`
- `03_0825_morning_picks.md`
- `04_1630_daily_review.md`

Reruns create a new suffixed file rather than overwriting the previous result:

`<normal-stem>_rerun_HHMMSS.md`

For execution and dependency rules, read `/WORKFLOW.md` first.
