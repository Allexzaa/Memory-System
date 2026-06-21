<div align="center">

<img src="./logo1.png" alt="Claude Code Memory System Logo" width="380" />

**Persistent, structured memory for Claude Code — survives session resets and auto-compact.**

<br />

![Setup](https://img.shields.io/badge/setup-~10_minutes-4285F4?style=flat-square)
![Compatible](https://img.shields.io/badge/Claude_Code-compatible-7B2FBE?style=flat-square)
![Projects](https://img.shields.io/badge/any_project-no_lock--in-34A853?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-EA4335?style=flat-square)

</div>

<br />

---

## <img src="https://api.iconify.design/material-symbols:lightbulb.svg?color=%23F4B400" width="22" align="center" /> &nbsp; What this system does

The Claude Code Memory System is a persistent project-memory framework that helps AI coding agents stay grounded, efficient, and consistent across long software builds. Instead of relying on one massive context dump, it organizes project knowledge into focused files for current state, backend architecture, frontend architecture, decisions, failures, feature plans, specs, and active tasks. The agent starts each session by reading only the highest-value summaries and indexes, then loads full details only when the task requires them. This keeps context usage lean while still preserving the project’s full reasoning trail.

The system is built for real development workflows: specs come before code, phase plans require approval, decisions are logged with rejected alternatives, failures are captured with root causes, and active work stays separated from historical notes. Architecture files describe the current system only, while decision and failure logs preserve why things changed.

The result is a coding agent that can navigate large projects with less token waste, fewer repeated explanations, and better factual grounding. It gives AI a practical map of the codebase, project rules, constraints, and build history, helping it answer questions, review plans, avoid stale assumptions, and work from existing facts instead of guessing during complex product development.


---

## <img src="https://api.iconify.design/material-symbols:folder-open.svg?color=%234285F4" width="22" align="center" /> &nbsp; Files included

| File | What it is | You edit it? |
| --- | --- | --- |
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

## <img src="https://api.iconify.design/material-symbols:rocket-launch.svg?color=%2334A853" width="22" align="center" /> &nbsp; Setup — 3 steps

<br />

**<img src="https://api.iconify.design/material-symbols:looks-one.svg?color=%234285F4" width="20" align="center" /> &nbsp; Copy files into your project**

Drop the entire folder contents into your project root. The `.claude/` folder goes at the root level alongside your `src/` or other project folders.

<br />

**<img src="https://api.iconify.design/material-symbols:looks-two.svg?color=%234285F4" width="20" align="center" /> &nbsp; Add STATE.md to .gitignore**

STATE.md is personal session state — not team-shared. Add this line to `.gitignore`:

```
.claude/STATE.md
```

Commit everything else. ARCH files, DECISIONS.md, FAILURES.md, and Docs/ are project knowledge that should be versioned and shared with your team.

<br />

**<img src="https://api.iconify.design/material-symbols:looks-3.svg?color=%234285F4" width="20" align="center" /> &nbsp; Run PROJECT_INIT.md in Claude Code**

Open your project in VS Code, launch Claude Code, and paste the full contents of `PROJECT_INIT.md` into the chat.

Claude will:
1. Scan your existing codebase
2. Ask you a single batch of questions about anything it could not determine
3. Populate all memory files with real project information
4. Show you each file for approval before moving on
5. Confirm when initialization is complete

> **Note:** This takes about 10 minutes. After it completes, delete or ignore `PROJECT_INIT.md` — you will never use it again.

---

## <img src="https://api.iconify.design/material-symbols:today.svg?color=%23EA4335" width="22" align="center" /> &nbsp; Daily use

<img src="https://api.iconify.design/material-symbols:play-circle.svg?color=%2334A853" width="18" align="center" /> &nbsp; **Starting a session** — Nothing to do. Claude Code reads `CLAUDE.md` automatically. Claude orients itself from `STATE.md` and the index sections of `DECISIONS.md` and `FAILURES.md`.

<img src="https://api.iconify.design/material-symbols:sync.svg?color=%234285F4" width="18" align="center" /> &nbsp; **During a session** — Claude writes to memory files as things happen. Decisions, failures, and architecture changes are logged mid-session automatically. You do not need to prompt it.

<img src="https://api.iconify.design/material-symbols:stop-circle.svg?color=%23EA4335" width="18" align="center" /> &nbsp; **Ending a session** — Type `/memory-update` in Claude Code. Claude cleans up `STATE.md` and confirms what was logged. Takes under 60 seconds.

<img src="https://api.iconify.design/material-symbols:manage-search.svg?color=%23F4B400" width="18" align="center" /> &nbsp; **If Claude forgot something** — Ask: `"Check DECISIONS.md / FAILURES.md / ARCH-backend.md for [topic]."` Claude will load the relevant file and find it.

---

## <img src="https://api.iconify.design/material-symbols:construction.svg?color=%23F4B400" width="22" align="center" /> &nbsp; Feature build workflow

Every feature follows three approval gates — Claude cannot advance without your sign-off:

```
Spec created  →  your approval  →  Phase plan created  →  your approval  →  Build (phase by phase)
```

Claude creates spec files in `Docs/F[NNN]-[slug]-spec.md` and phase plans in `Docs/F[NNN]-[slug]-phases.md`. `Build_Plan.md` tracks the status of all features.

---

## <img src="https://api.iconify.design/material-symbols:build.svg?color=%23EA4335" width="22" align="center" /> &nbsp; Troubleshooting

<img src="https://api.iconify.design/material-symbols:warning.svg?color=%23F4B400" width="16" align="center" /> &nbsp; **Claude is filling in placeholder values instead of real content.**  
Tell Claude: `"Do not invent content. Write [not yet determined] for anything you cannot derive from the codebase, and ask me."`

<img src="https://api.iconify.design/material-symbols:warning.svg?color=%23F4B400" width="16" align="center" /> &nbsp; **DECISIONS.md or FAILURES.md is getting long and slow to scan.**  
The Index section at the top should stay under 30 lines. If it grows beyond that, the entries are too granular — only log decisions with a meaningful rejected alternative.

<img src="https://api.iconify.design/material-symbols:warning.svg?color=%23F4B400" width="16" align="center" /> &nbsp; **Claude is not writing to memory files mid-session.**  
Remind it: `"You need to log this to DECISIONS.md / FAILURES.md now — not at session end."` If this keeps happening, start a new session and re-read `CLAUDE.md`.

<img src="https://api.iconify.design/material-symbols:warning.svg?color=%23F4B400" width="16" align="center" /> &nbsp; **A team member's STATE.md keeps conflicting with yours.**  
`STATE.md` should be in `.gitignore` — it is personal session state. Each person has their own. For shared task tracking, use `Build_Plan.md` and the phase plan files instead.

---

## <img src="https://api.iconify.design/material-symbols:help.svg?color=%234285F4" width="22" align="center" /> &nbsp; Questions

Read [Memory-System/README.md](./Memory-System/README.md) for the full technical design rationale.

---

## <img src="https://api.iconify.design/material-symbols:gavel.svg?color=%23757575" width="22" align="center" /> &nbsp; License

Released under the [MIT License](./LICENSE) — free to use, modify, and distribute with attribution.

Copyright © 2026 [Allexzaa](https://github.com/Allexzaa)
