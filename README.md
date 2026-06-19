# Memory System Setup Guide

A persistent memory system for Claude Code that survives session resets and auto-compact.
Works on any project. Takes about 10 minutes to set up on a new project.

---

## What this system does

Claude Code forgets everything when a session ends. This system gives it structured,
permanent memory across sessions — what was decided, what failed, what the architecture
looks like, and what is actively being built. Claude reads the memory files at session
start and writes to them mid-session as things happen.

---

## Files included

| File | What it is | You edit it? |
|---|---|---|
| `CLAUDE.md` | Project constitution — rules, stack, palette | Once at setup, rarely after |
| `PROJECT_INIT.md` | One-time initialization prompt | Paste into Claude Code once, then never again |
| `INIT_PROMPT.md` | Session-start confirmation for sessions 2+ | Never — Claude uses it automatically |
| `Build_Plan.md` | Master feature index | Claude maintains it |
| `Docs/PHASE_PLAN_TEMPLATE.md` | Template for feature phase plans | Never — Claude uses it as a template |
| `.claude/STATE.md` | Live active tasks | Claude maintains it |
| `.claude/ARCH-backend.md` | Backend architecture reference | Claude maintains it |
| `.claude/ARCH-frontend.md` | Frontend architecture reference | Claude maintains it |
| `.claude/DECISIONS.md` | Append-only decision log | Claude maintains it |
| `.claude/FAILURES.md` | Append-only failure log | Claude maintains it |
| `.claude/commands/memory-update.md` | `/memory-update` slash command | Never |

---

## Setup — 3 steps

### Step 1 — Copy files into your project
Drop the entire folder contents into your project root. The `.claude/` folder goes
at the root level alongside your `src/` or other project folders.

### Step 2 — Add STATE.md to .gitignore
STATE.md is personal session state — not team-shared. Add this line to `.gitignore`:
```
.claude/STATE.md
```
Commit everything else. ARCH files, DECISIONS.md, FAILURES.md, and Docs/ are
project knowledge that should be versioned and shared with your team.

### Step 3 — Run PROJECT_INIT.md in Claude Code
Open your project in VS Code, launch Claude Code, and paste the full contents
of `PROJECT_INIT.md` into the chat.

Claude will:
1. Scan your existing codebase
2. Ask you a single batch of questions about anything it could not determine
3. Populate all memory files with real project information
4. Show you each file for approval before moving on
5. Confirm when initialization is complete

This takes about 10 minutes. After it completes, delete or ignore PROJECT_INIT.md —
you will never use it again.

---

## Daily use

**Starting a session:**
Nothing to do. Claude Code reads CLAUDE.md automatically. Claude orients itself
from STATE.md and the index sections of DECISIONS.md and FAILURES.md.

**During a session:**
Claude writes to memory files as things happen — you do not need to prompt it.
Decisions, failures, and architecture changes are logged mid-session automatically.

**Ending a session:**
Type `/memory-update` in Claude Code. Claude cleans up STATE.md and confirms
what was logged. Takes under 60 seconds.

**If Claude seems to have forgotten something:**
Ask: "Check DECISIONS.md / FAILURES.md / ARCH-backend.md for [topic]."
Claude will load the relevant file and find it.

---

## Feature build workflow

Every feature follows three approval gates — Claude cannot advance without your sign-off:

```
1. Spec created → your approval
2. Phase plan created → your approval
3. Build starts → phase by phase, tests required before each phase is marked Done
```

Claude creates spec files in `Docs/F[NNN]-[slug]-spec.md` and phase plans in
`Docs/F[NNN]-[slug]-phases.md`. Build_Plan.md tracks status of all features.

---

## Troubleshooting

**Claude is filling in placeholder values instead of real content.**
Stop it. Tell Claude: "Do not invent content. Write [not yet determined] for anything
you cannot derive from the codebase, and ask me."

**DECISIONS.md or FAILURES.md is getting long and slow to scan.**
The Index section at the top should stay under 30 lines for most projects. If it grows
beyond that, the entries are probably too granular. Minor implementation choices do not
need a decision log entry — only decisions with a meaningful rejected alternative.

**Claude is not writing to memory files mid-session.**
Remind it: "You need to log this to DECISIONS.md / FAILURES.md now — not at session end."
If this keeps happening, add the project to a new session and re-read CLAUDE.md.

**A team member's STATE.md keeps conflicting with yours.**
STATE.md should be in .gitignore — it is personal session state. Each person has their own.
If you want shared task tracking, use Build_Plan.md and the phase plan files instead.

---

## Questions
Read [Memory-System/README.md](./Memory-System/README.md) for the full technical design rationale.
