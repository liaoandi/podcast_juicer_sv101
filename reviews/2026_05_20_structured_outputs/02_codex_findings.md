# Review Round 2 - codex

Scope: unpushed changes against `origin/main` after round 1 fixes.

## MUST FIX

1. EP233 signal metadata pointed at `233_transcript_polished_gemini.json`, which is not tracked or present in the episode directory. The verified signals file had the same broken source reference.

2. Participant stub files such as EP226 and EP232 omitted date fields that `process_utils.py` reads on rerun. With audio already present, rerun could skip step0, load the stub, and overwrite metadata dates with nulls.

## Follow-Up Applied

- Normalized all signal and verified-signal `metadata.source` values to the tracked canonical transcript path.
- Backfilled participant files with both `host` and `hosts` keys plus `publish_date`, `record_date`, `date_notes`, and `guest_background` when missing, using metadata files where available.
- Revalidated all tracked JSON with `jq`.

## VERDICT

Review issues addressed in follow-up changes.
