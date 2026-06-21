# CLAUDE.md — [PROJECT NAME]

## Native Memory
MEMORY.md is supplemental. The authoritative memory for this project is the `.claude/` files. Do not duplicate into MEMORY.md what is already captured here.

## Session Start (always run in this exact order)
1. Read `.claude/STATE.md` — active tasks and blockers only
2. Read `## Index` in `.claude/DECISIONS.md` and `.claude/FAILURES.md` — index only
3. Read `## Summary` in `.claude/ARCH-backend.md` or `.claude/ARCH-frontend.md` — summary only, based on task type. Load both summaries if the task spans both.
4. Load a full file only if: (a) the index or summary shows something relevant to the current task, (b) making an architecture decision, or (c) investigating a failure
5. Report in 2 lines: what's active, what's next. Then proceed.
6. STATE.md should be in .gitignore

## Mid-Session Write Rules (write when the event happens — not at session end)

| Event | What to write | Where |
|---|---|---|
| Decision made with a rejected alternative | Append index line + full entry | `DECISIONS.md` |
| Something tried that failed or was abandoned | Append index line + full entry | `FAILURES.md` |
| Active task completes | Delete task from STATE.md | `STATE.md` |
| Architecture changes (new file, new dep, new pattern, refactor) | Replace/update affected entry | `ARCH-backend.md` or `ARCH-frontend.md` |
| Spec approved | Add row to Build_Plan.md, create phase plan | see Spec workflow |
| Phase completes | Mark Done in phase plan, append one-liner to DECISIONS.md | `Docs/` + `DECISIONS.md` |

**Why mid-session:** Auto-compact can fire at any time. Write on the event, not at the end.

## ARCH File Rules
- Two files: `ARCH-backend.md` for server/DB/API/infra. `ARCH-frontend.md` for UI/components/state/routing.
- Each file has a `## Summary` section at the top — 5 lines max. Claude reads Summary first.
- **Replace/update existing entries when things change. Do not append stale info.**
- ARCH files describe the current system only. History belongs in DECISIONS.md.
- Constraints sections are firewalls. Never violate without explicit user approval.

## STATE.md Rules
- Active tasks only. No history, no log, no completed items.
- Hard limit: 60 lines. If exceeded, too many active tasks — ask user to scope down.
- When a task completes: delete it. Do not archive here.

## DECISIONS.md Rules
- Top section is always `## Index` — one line per entry: `[date] [D-NNN] [title]`
- Full entries below the index. Append-only — never edit or delete past entries.
- One entry per decision. Required: date, decision, rejected alternative, reason.

## FAILURES.md Rules
- Top section is always `## Index` — one line per entry: `[date] [F-NNN] [title] [status]`
- Full entries below the index. Append-only — never edit or delete past entries.
- One entry per failure. Required: date, what was tried, what happened, root cause, status.
- Status values: `abandoned` | `worked-around` | `resolved` | `open`

## Feedback Evaluation Rule
Before acting on any feedback on a spec or phase plan:
1. Check `Build_Plan.md` and `.claude/DECISIONS.md` — if the feedback belongs to a future phase, name that phase and do not add it to the current scope.
2. Evaluate whether the feedback is practical, technically sound, consistent with the architecture, and appropriate for the active phase.
3. Push back explicitly if it creates scope creep, conflicts with existing decisions, duplicates planned work, or introduces phase-order violations.
4. Produce a Review Response Table in chat before touching any file. One row per comment. Columns: `Comment | Decision (Accept/Modify/Reject/Defer) | Technical reasoning | Architecture impact | Phase impact | Required doc update`. Every row must show full reasoning — especially Reject and Defer decisions. Do not edit any file until the table is visible in chat and the user can challenge it.
5. After applying changes, append the Review Response Table to the `## Review Log` section at the bottom of the reviewed file. One entry per pass, append-only.

Do not treat feedback as automatically correct. Validate first, then update.

## Spec and Phase Plan Workflow

### Source Header Rule
Every spec and phase plan must open with this block immediately after the title and status lines:
```
Sources:      [Arch_Spec_Final/ docs or reference files used]
Decisions:    [D-NNN entries that apply — or — none]
Related spec: [spec file path — or — — if this is a spec]
Related plan: [phase plan file path — or — — if this is a phase plan]
Scope note:   [one sentence: what this covers and what it explicitly does not]
```
Only list sources and decisions that were actually consulted. Missing block = spec defect.

### Deferred Items Rule
Every spec and phase plan must include a `## Deferred Items` table for anything intentionally excluded:
```
| Item | Moved to | Reason |
```
Each row is one item. `Moved to` must name the specific future feature (e.g. F004). Reason must explain why it cannot or should not be done now. Missing table = spec defect.

### Step 1 — Spec (before any code)
- Create `Docs/F[NNN]-[slug]-spec.md` using `Docs/SPEC_TEMPLATE.md` as the template, add row to `Build_Plan.md` as `Spec Ready` with the spec file path in the Spec column
- Include source header block and deferred items table
- Include `## What Comes Next — F[NNN+1]` section before the Review Log: one paragraph on what the next feature builds on top of this one
- Stop. Wait for explicit user approval.

### Step 2 — Phase Plan (after spec approval)
- Create `Docs/F[NNN]-[slug]-phases.md` using `Docs/PHASE_PLAN_TEMPLATE.md`
- Include source header block and deferred items table
- Update `Build_Plan.md` to `Approved`
- Stop. Wait for explicit user approval before writing any code.

### Step 3 — Build (phase by phase)
- Update `Build_Plan.md` to `In Progress`
- One phase at a time. Do not start next phase until current is marked Done with notes.
- Write phase `Notes` mid-task as things happen — not at the end.
- Before marking a phase Done: confirm tests pass for that phase's scope. If tests fail at phase close, log an open entry in FAILURES.md — do not mark Done with silent failures.
- - On phase complete: Read the phase plan file first, then update: (1) top-level `Status:` line, (2) phase `**Status:** Done`, (3) tick all `- [ ]` task checkboxes to `- [x]`, (4) fill Notes. Then append one-liner to DECISIONS.md.
- On full feature complete: update `Build_Plan.md` to `Done`.

### Memory rules for specs/phases
- DECISIONS.md: one pointer when spec approved (name, date, paths). One outcome per phase complete.
- FAILURES.md: one entry per failed/abandoned attempt during a build.
- Spec and phase plan files hold full detail. Memory files hold pointers and outcomes only.

### Build_Plan.md status flow
`Planned` → `Spec Ready` → `Approved` → `In Progress` → `Done`
Never remove entries.

## What We Are Building
[Fill this in]

## Current Direction
[Fill this in]

## Stack
[Fill this in — one line each for frontend, backend, DB, auth, hosting]

## Color Palette (hard rule — only these colors)
- `--paper: #ece6d9` — background
- `--panel: #e4ddcc` — panels, sidebars, cards
- `--ink: #211d17` — primary text
- `--ink-soft: #544d41` — secondary text
- `--muted: #928873` — muted/placeholder text and icons
- `--line: #c6bba4` — borders, dividers, hover fills
- `--accent: #9a4b25` — primary accent
- `--accent-2: #5c6b3a` — secondary accent

Derive tints/shades using rgba with opacity. Do not introduce new base colors.
