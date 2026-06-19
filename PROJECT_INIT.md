# PROJECT_INIT.md
# Run this ONCE when setting up the memory system on a project.
# Works in two modes: blank workspace (scaffold only) or existing project (full init).
# After this run is complete, never use this file again.

---

You are setting up a persistent memory system. Start by detecting which mode applies.

---

## Step 0 — Detect project state

Check for the presence of any of these:
- `package.json`, `requirements.txt`, `go.mod`, `Cargo.toml`
- Any `src/`, `app/`, or `lib/` folders with actual code files
- An existing `README.md` that describes a real project (not this memory system README)

**If none of these exist → this is a blank workspace. Go to BLANK MODE.**
**If any exist → this is an existing project. Go to EXISTING MODE.**

---

## BLANK MODE — scaffold only, no questions

The project is in idea phase. Do not ask any questions. Just build the structure.

### 1. Detect the dropped folder name
The memory system files were dropped into the project as a folder. Find it:
```bash
# List top-level folders to identify the dropped memory system folder
ls -la | grep "^d"
```
The dropped folder is the one containing CLAUDE.md, PROJECT_INIT.md, and the .claude/ subfolder.
It is likely named something like `claude-memory-system` or similar.
Set that folder name as MEMORY_FOLDER for the commands below.

### 2. Create required folders at project root
```bash
mkdir -p .claude/commands
mkdir -p Docs
```

### 3. Move ALL files to their correct locations at project root
Replace `[MEMORY_FOLDER]` with the actual folder name found in step 1:
```bash
# Root-level files — move to project root
mv [MEMORY_FOLDER]/CLAUDE.md ./CLAUDE.md 2>/dev/null || true
mv [MEMORY_FOLDER]/README.md ./README.md 2>/dev/null || true
mv [MEMORY_FOLDER]/INIT_PROMPT.md ./INIT_PROMPT.md 2>/dev/null || true
mv [MEMORY_FOLDER]/Build_Plan.md ./Build_Plan.md 2>/dev/null || true

# .claude/ files — move to .claude/ at project root
mv [MEMORY_FOLDER]/.claude/STATE.md ./.claude/STATE.md 2>/dev/null || true
mv [MEMORY_FOLDER]/.claude/ARCH-backend.md ./.claude/ARCH-backend.md 2>/dev/null || true
mv [MEMORY_FOLDER]/.claude/ARCH-frontend.md ./.claude/ARCH-frontend.md 2>/dev/null || true
mv [MEMORY_FOLDER]/.claude/DECISIONS.md ./.claude/DECISIONS.md 2>/dev/null || true
mv [MEMORY_FOLDER]/.claude/FAILURES.md ./.claude/FAILURES.md 2>/dev/null || true
mv [MEMORY_FOLDER]/.claude/commands/memory-update.md ./.claude/commands/memory-update.md 2>/dev/null || true

# Docs/ files — move to Docs/ at project root
mv [MEMORY_FOLDER]/Docs/PHASE_PLAN_TEMPLATE.md ./Docs/PHASE_PLAN_TEMPLATE.md 2>/dev/null || true
```

### 4. Remove the now-empty dropped folder
```bash
# Remove the original dropped folder — it should now be empty
rm -rf [MEMORY_FOLDER]
```

### 5. Verify final structure at project root
```bash
find . -path ./node_modules -prune -o -name "*.md" -print | grep -E "(CLAUDE|INIT|PROJECT|GUIDE|Build_Plan|README|\.claude|Docs)" | sort
```

Confirm the output matches this exactly:
```
./Build_Plan.md
./CLAUDE.md
./INIT_PROMPT.md
./PROJECT_INIT.md
./README.md
./.claude/ARCH-backend.md
./.claude/ARCH-frontend.md
./.claude/DECISIONS.md
./.claude/FAILURES.md
./.claude/STATE.md
./.claude/commands/memory-update.md
./Docs/PHASE_PLAN_TEMPLATE.md
```

If any file is missing, locate it and move it before continuing.

### 6. Leave all template files as-is
Do not fill in any placeholder fields. Do not invent content.
Placeholders stay until the user is ready to fill them in.

### 7. Confirm with this exact message
"Memory scaffold ready. All files moved to project root.

Structure verified — nothing has been filled in yet.
When your project takes shape, tell me:
  - What you are building
  - Your stack
  - Your first task

I will fill in the memory files at that point.
For future sessions: Claude Code reads CLAUDE.md automatically. Use /memory-update at session end."

**Stop here. Do not ask any questions.**

---

## EXISTING MODE — full initialization

The project has real code or documentation. Work through these steps in order.

### Step 1 — Detect dropped folder and move all files first
Same as BLANK MODE steps 1-5 above — move everything into place and remove the dropped folder before doing anything else.

### Step 2 — Scan the project
Read these files before asking anything:
- `package.json` / `requirements.txt` / `go.mod` — stack and deps
- Top-level folder structure (exclude node_modules)
- `.env.example` or `config/` — integrations
- Any existing `README.md` that describes the project

Derive what you can. List findings in 5 lines or less.

### Step 3 — Ask only what the scan could not answer
One batch of questions, asked all at once. Only ask what is genuinely unknown:
- What is this project? (if README did not make it clear)
- Current phase? (greenfield / early build / active development)
- Stack gaps the scan could not determine
- Hosting / deployment target
- Constraints I must never violate
- First active task

Wait for answers before filling in any files.

### Step 4 — Populate files in order, one at a time
For each file, fill in with real information, show it to the user, wait for explicit
approval before moving to the next:

1. `CLAUDE.md` — project name, what we are building, current direction, stack
2. `.claude/ARCH-backend.md` — Summary section first, then full detail
3. `.claude/ARCH-frontend.md` — Summary section first, then full detail
4. `.claude/STATE.md` — current status, active tasks, next action, blockers
5. `Build_Plan.md` — add any known features as Planned rows

Rules:
- Write `[not yet determined]` for anything unknown — never invent content
- Show each file and wait for approval before moving on
- If corrected, update and re-show before continuing

### Step 5 — Final verification
```bash
find . -path ./node_modules -prune -o -name "*.md" -print | grep -E "(CLAUDE|INIT|PROJECT|GUIDE|Build_Plan|README|\.claude|Docs)" | sort
```

Confirm with this exact message:
"Memory system initialized for [PROJECT NAME].
Structure verified. All files populated and approved.
Do not run PROJECT_INIT.md again — use /memory-update during sessions.
Ready. What are we building today?"

---

## Rules for both modes
- Always move ALL files and remove the dropped folder before doing anything else.
- If a shell command fails, report the exact error — do not silently skip it.
- Never fill in placeholder fields with invented content.
- Blank mode: zero questions, scaffold only, done in under 60 seconds.
- Existing mode: one question batch, one file at a time, explicit approval at each step.