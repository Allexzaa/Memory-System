# F[NNN] — [Feature Name]: Spec

Created: [YYYY-MM-DD]
Status: Draft | Approved | Superseded

Sources:      [reference files consulted — Arch_Spec_Final/, prior specs, etc.]
Decisions:    [D-NNN entries that apply — or — none]
Related spec: —
Related plan: Docs/F[NNN]-[slug]-phases.md (written after approval)
Scope note:   [one sentence: what this covers and what it explicitly does not]

---

<!-- INSTRUCTIONS FOR CLAUDE
- Fill every section. Write [not yet determined] for anything you cannot derive — do not invent.
- Stop after creating this file. Do not create a phase plan until the user explicitly approves this spec.
- Add a row to Build_Plan.md with status "Spec Ready" and the spec file path in the Spec column.
- If any section is blank, surface it to the user as a blocking question before proceeding.
- Include a What Comes Next section and a Review Log section at the bottom.
-->

## Problem Statement

<!-- What problem does this solve? One to three sentences. If you cannot state the problem clearly, the spec is not ready. -->
[What is broken, missing, or painful right now?]

## Target User

<!-- Who specifically experiences this problem? Not "users" — be precise. -->
[Who, in what context, doing what task?]

## Why Now

<!-- Why is this being built at this point in the project? What changes if it isn't built here? -->
[What is the forcing function or priority reason?]

---

## Success Criteria

<!-- These are the acceptance gates. A phase plan cannot be approved unless all items here are testable. -->
<!-- Each line must be falsifiable — "works correctly" is not a criterion. -->

- [ ] [Specific, observable outcome]
- [ ] [Specific, observable outcome]
- [ ] [Specific, observable outcome]

## Constraints

<!-- Hard limits — things that MUST NOT exist in this feature. These are firewalls. -->
<!-- Never violate a constraint without explicit user approval. -->

- No [X] — [reason]
- No [Y] — [reason]

## Deferred Items

<!-- Things that seem related but are explicitly excluded from this feature. -->
<!-- Moved to must name a specific future feature. Reason must explain why not now. -->

| Item | Moved to | Reason |
|------|----------|--------|
| [Item] | F[NNN] — [feature name] | [Why it cannot or should not be done now] |

---

## Approach

<!-- How will this be built at a high level? One paragraph. No implementation detail — that belongs in the phase plan. -->
[High-level approach]

## Alternatives Considered

<!-- What other approaches were evaluated and rejected? Required: at least one. -->
<!-- If no alternatives were considered, that is a risk — surface it. -->

| Option           | Why rejected |
|------------------|--------------|
| [Alternative A]  | [Reason]     |
| [Alternative B]  | [Reason]     |

---

## Risks

<!-- What could go wrong? Rate each: Low / Medium / High -->
<!-- If all risks are Low, that is suspicious — look harder. -->

| Risk               | Likelihood   | Impact       | Mitigation                   |
|--------------------|--------------|--------------|------------------------------|
| [Risk description] | Low/Med/High | Low/Med/High | [How to reduce or handle it] |

## Dependencies

<!-- What must exist or be true before this feature can be built or used? -->
<!-- Include: other features, external services, data, decisions. -->

- [Dependency — current status]
- [Dependency — current status]

---

## User Stories

<!-- At least one story per distinct user action this feature enables. -->
<!-- Format: As a [user], I want [action] so that [outcome]. -->
<!-- Each story should map to at least one Success Criterion above. -->

- As a [user], I want [action] so that [outcome].
- As a [user], I want [action] so that [outcome].

---

## Complexity Estimate

<!-- Simple / Medium / Complex — and the main reason for the rating. -->
<!-- This informs how many phases the phase plan will need. -->

**Estimate:** [Simple / Medium / Complex]
**Primary reason:** [What drives the complexity?]

## Open Questions

<!-- Anything that must be answered before or during the build. -->
<!-- Claude: surface these to the user before the phase plan is created. -->

- [ ] [Question — who needs to answer it]
- [ ] [Question — who needs to answer it]

---

## What Comes Next — F[NNN+1]

<!-- One paragraph. What does the next feature build on top of what this one delivers? -->
<!-- This section exists so the implementer understands the downstream impact of their decisions here. -->
[What F[NNN+1] inherits from this feature and what it adds.]

---

<!-- APPROVAL GATE
Do not create Docs/F[NNN]-[slug]-phases.md until the user explicitly approves this spec.
Approval message to look for: "approved", "looks good", "go ahead", or equivalent.
On approval: update Build_Plan.md status from "Spec Ready" to "Approved", then create the phase plan.
-->

## Review Log

<!-- Append-only. One entry per review pass. Never edit past entries. -->
<!-- Format below — copy per pass: -->
<!--
### R-001 — [YYYY-MM-DD] | Status: accepted | partial | rejected

| Comment | Decision | Technical reasoning | Architecture impact | Phase impact | Required doc update |
|---------|----------|---------------------|---------------------|--------------|---------------------|
| [comment] | Accept/Modify/Reject/Defer | [reasoning] | [impact or none] | [impact or none] | [file or none] |
-->
