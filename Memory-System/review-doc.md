# /review-doc — Review a spec or phase plan before making changes

Use this command when asked to review and potentially update a spec or phase plan file.

---

## Step 1 — Deep review (before touching anything)

Read the target file fully. Then analyze it as a senior engineer and check for:

- Technical accuracy and feasibility
- Consistency with current architecture (read ARCH-backend.md and ARCH-frontend.md summaries)
- Alignment with active phase scope — check Build_Plan.md
- Conflicts with existing decisions — check DECISIONS.md index
- Scope creep (work that belongs to a future feature)
- Phase-order violations (dependencies on things not yet built)
- Missing requirements or unclear acceptance criteria
- Weak or untestable assumptions
- Broken logic that sounds right but would fail in practice
- Security risks or data-model gaps
- Integration issues with other services

For every issue found, provide:

- **Issue** — what is wrong
- **Why it matters** — consequence if not addressed
- **Technical reasoning** — the engineering basis
- **Recommended resolution** — what to do instead
- **Disposition** — Fix Now / Defer / Reject

If the file is solid, say so clearly and explain why.

**Do not rewrite or update any file until the review findings are visible in chat.**

---

## Step 2 — Review Response Table (after user provides feedback)

Before applying any change, produce this table in chat — one row per comment:

| Comment | Decision | Technical reasoning | Architecture impact | Phase impact | Required doc update |
|---------|----------|---------------------|---------------------|--------------|---------------------|

Decision values: `Accept` | `Modify` | `Reject` | `Defer`

Rules:
- Reject and Defer decisions require the strongest reasoning — do not cave to pushback without a technical basis.
- If a comment belongs to a future phase, name that phase and mark it Defer.
- If a comment conflicts with an existing DECISIONS.md entry, name the entry and explain the conflict.
- Do not edit any file until the table is complete and visible.

---

## Step 3 — Apply changes and append Review Log

After the user confirms the table (or challenges individual rows and those are resolved):

1. Apply only the accepted and modified changes to the target file.
2. Append the final Review Response Table to the `## Review Log` section at the bottom of the file. Format:

```
### R-[NNN] — [YYYY-MM-DD] | Status: accepted | partial | rejected

| Comment | Decision | Technical reasoning | Architecture impact | Phase impact | Required doc update |
|---------|----------|---------------------|---------------------|--------------|---------------------|
| ...     | ...      | ...                 | ...                 | ...          | ...                 |
```

Review Log entries are append-only — never edit past entries.
