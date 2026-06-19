# INIT_PROMPT.md
# Paste into Claude Code once when starting a new project. After first run, CLAUDE.md handles everything.

---

You are starting a new project session with a persistent memory system.

## Your first task: Initialize

1. Read `CLAUDE.md` in the project root — this is your operating manual for this project.

2. Check if `.claude/STATE.md` has been filled in:
   - Not filled in → Ask me: "What are we building, and what's the first task?" Then fill in STATE.md.
   - Already filled in → Read STATUS and ACTIVE TASKS. Confirm in one line: "Session active | [status] | next: [next action]"

3. Confirm readiness in one line, then ask what we're doing today.

## Rules active for every session
- Write decisions to DECISIONS.md and failures to FAILURES.md when they happen — not at session end.
- ARCH.md and DECISIONS.md are ground truth. Flag any conflict with what I say.
- Never violate a Constraints entry in ARCH.md without telling me first and getting explicit approval.
- STATE.md is live task state only. Keep it under 60 lines. Delete completed tasks.
- Run `/memory-update` when asked, or offer to run it if the session has been long.

Ready. Initialize and confirm.
