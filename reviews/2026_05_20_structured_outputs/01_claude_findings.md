---

# Review Round 1 — claude

Commit under review: `9a55d92` ("chore: preserve structured podcast outputs")

**Scope**: 253 JSON data files (metadata, participants, signals, verified_signals) across ~65 episodes added to git tracking. `.gitignore` updated to whitelist these file types. `batch_progress.md` rewritten.

**Note**: The review scaffolding (`01_diff.patch`, `01_diff_stat.md`) was generated empty because changes were already committed. Review was performed against `git diff HEAD~1..HEAD`.

---

## MUST FIX

- None

## SHOULD FIX

1. **Local absolute paths leaked into committed JSON** — 96 occurrences of local Desktop project paths in `signals.json` and `verified_signals.json` `metadata.source` fields. Non-portable and leaks local directory structure into the repo. Two different base paths existed for older episodes and newer episodes, indicating different working directories at different times. Should be relative paths.

2. **Incomplete file sets for several episodes** — Some episodes are missing files that the `.gitignore` now whitelists:
   - Missing `_metadata.json`: ep193, ep219, ep221, ep242
   - Missing `_participants.json`: ep172, ep246, ep247
   
   If these don't exist locally either, `batch_progress.md` should note them as incomplete rather than listing all as COMPLETE.

3. **Participants schema inconsistency** — Two schemas coexist: older format uses `"host"` (singular, e.g., ep193) with extra fields (`episode_info`, `guest_background`, dates), newer format uses `"hosts"` (plural, e.g., ep232) with just `{"hosts": [], "guests": []}`. Pipeline code must handle both.

4. **CLAUDE.md documentation gap** — `.claude/CLAUDE.md:19-23` (Directory Conventions) does not mention `_participants.json` as a per-episode output file, though it's now tracked in git alongside the other types.

5. **Empty/stub data committed** — Several episodes (ep82, ep188, ep200, ep218, ep237) have 0-signal files and empty participants. Consider whether `batch_progress.md` should annotate which episodes have 0 signals.

## OBSERVATIONS

1. **No code changes** — Purely data + gitignore + progress doc. No functional regressions possible from code.
2. **Repo size impact** — ~40,754 lines added. Significant clone size increase, but justified for reproducibility.
3. **batch_progress.md rewrite is cleaner** — Historical per-phase checklists replaced with a more maintainable summary format.
4. **No credentials or sensitive data** — Confirmed via grep. All "token" matches are natural-language AI token references.
5. **ep193 data quality issue** — `sv101_ep193_participants.json` contains `episode_info` referencing EP184. Pre-existing pipeline bug, not introduced by this commit.

## VERDICT

- **REVIEW_PASSED**

The commit is safe to push. The SHOULD FIX items (especially #1 local paths and #2 incomplete file sets) are worth addressing in a follow-up but do not block this data preservation commit.
