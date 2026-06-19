# /memory-update

Run at any point to sync memory. Safe to run multiple times — append-only files won't duplicate.

## Steps (run in order)

1. **STATE.md** — Remove completed tasks. Update STATUS and NEXT ACTION.

2. **DECISIONS.md** — For any decision made this session not yet logged:
   - Append one line to `## Index`: `[date] [D-NNN] [title]`
   - Append full entry under `## Entries`

3. **FAILURES.md** — For any failure or abandoned attempt not yet logged:
   - Append one line to `## Index`: `[date] [F-NNN] [title] [status]`
   - Append full entry under `## Entries`

4. **ARCH.md** — Append any new files, deps, constraints, or data flow changes.

5. Confirm: "Memory updated. STATE clean. [N] decisions, [N] failures, [N] arch changes logged."

## Note on auto-compact
If auto-compact fired before you ran this, decisions and failures written mid-session are already
in the files. This command catches STATE.md cleanup and anything mid-session writes may have missed.
