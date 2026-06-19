# Claude Code Memory System v3

A persistent, token-efficient memory system for Claude Code.
Built around three principles: write on the event (not at session end), read indexes before full files, and ARCH files describe now (not history).

---

## File Structure

```
your-project/
├── CLAUDE.md                        ← Project constitution. Claude reads this every session.
├── INIT_PROMPT.md                   ← Paste into Claude Code on first run only.
├── Build_Plan.md                    ← Master feature index. Never remove entries.
├── Docs/
│   ├── PHASE_PLAN_TEMPLATE.md       ← Template for every phase plan.
│   ├── F001-[slug]-spec.md          ← Per-feature spec (before any code).
│   ├── F001-[slug]-phases.md        ← Per-feature phase plan (after spec approval).
│   └── ...
└── .claude/
    ├── STATE.md                     ← Active tasks only. 60-line hard limit.
    ├── ARCH-backend.md              ← Backend architecture. Summary section read first.
    ├── ARCH-frontend.md             ← Frontend architecture. Summary section read first.
    ├── DECISIONS.md                 ← Index + append-only decision log.
    ├── FAILURES.md                  ← Index + append-only failure log.
    └── commands/
        └── memory-update.md        ← /memory-update slash command
```

---

## How Claude reads memory (token cost per session)

| File | What Claude reads | When | Approx tokens |
|---|---|---|---|
| CLAUDE.md | Full file | Every session (native) | ~600 |
| STATE.md | Full file | Every session | ~150 |
| DECISIONS.md | Index only | Every session | ~50–150 |
| FAILURES.md | Index only | Every session | ~50–150 |
| ARCH-backend.md | Summary only | Backend tasks | ~100 |
| ARCH-frontend.md | Summary only | Frontend tasks | ~100 |
| Any full file | Full content | Only when index/summary flags it relevant | ~400–800 |
| Phase plan | Full file | Only when actively building that feature | ~300–500 |

**Typical session start cost: 600–1,100 tokens.** Full file loads only happen when the task actually needs them.

---

## The three core design principles

### 1. Write on the event, not at session end
Auto-compact can fire mid-session without warning. Every write to DECISIONS.md, FAILURES.md, and ARCH files happens immediately when the event occurs. `/memory-update` is a cleanup pass for STATE.md only — not the single save point.

### 2. Index and summary sections first
DECISIONS.md and FAILURES.md have an `## Index` at the top — one line per entry. ARCH files have a `## Summary` — five lines max. Claude reads these lightweight headers first and loads the full file only if something is relevant to the current task. A year-old project with 80 decisions costs the same to start as a week-old project.

### 3. ARCH files describe now, not history
ARCH-backend.md and ARCH-frontend.md are replaced/updated when things change — not appended to. History lives in DECISIONS.md. ARCH files are a current-state snapshot, always lean, never stale.

---

## What each file answers

| Question | File |
|---|---|
| What are we working on right now? | STATE.md |
| What does the backend look like now? | ARCH-backend.md |
| What does the frontend look like now? | ARCH-frontend.md |
| Why did we build it this way? | DECISIONS.md |
| What did we try that didn't work? | FAILURES.md |
| What features are planned or in progress? | Build_Plan.md |
| What's the full spec for feature X? | Docs/F[NNN]-[slug]-spec.md |
| What's the build status and notes for feature X? | Docs/F[NNN]-[slug]-phases.md |
| What are the project rules Claude must follow? | CLAUDE.md |

---

## Feature build workflow

Every feature follows three gates. Claude cannot advance without explicit user approval at each.

```
Request → Spec → [Approval] → Phase Plan → [Approval] → Build phase by phase → Done
```

During each phase: tasks checked off mid-build, notes written as things happen, tests confirmed before marking Done, failures logged to FAILURES.md immediately.

---

## Setup

1. Copy all files into your project root.

2. Fill in `CLAUDE.md` — project name, stack summary, constraints, color palette.

3. Fill in `.claude/ARCH-backend.md` and `.claude/ARCH-frontend.md` — Summary section first, then full detail.

4. Add to `.gitignore`:
   ```
   .claude/STATE.md
   ```
   Commit everything else. ARCH files, DECISIONS.md, FAILURES.md, and Docs/ are project knowledge — version them.

5. Open VS Code, launch Claude Code, paste `INIT_PROMPT.md`. Claude initializes STATE.md and confirms session 1.

---

## Compatibility with native Claude Code memory

Claude Code's MEMORY.md auto-memory is supplemental to this system. CLAUDE.md explicitly tells Claude not to duplicate into MEMORY.md what is already captured in `.claude/` files. If Claude's auto-memory saves something additional, that's a bonus — it doesn't conflict.

---

## When to add ARCH-infra.md

Only if your infrastructure is complex enough to warrant it — multiple cloud services, non-trivial networking, custom deployment pipelines. For most projects ARCH-backend.md covers infra in its Stack and Hosting sections. Don't create the file preemptively.
