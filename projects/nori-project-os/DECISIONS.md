# Decisions: [Project Name]

This log captures key decisions made throughout the project lifecycle.

**Purpose:** Preserve decision context and rationale for future reference.

---

## Decision Log

<!-- Template for new decisions:

### [Decision Title]

- **Date:** YYYY-MM-DD
- **Decision:** [What was decided]
- **Rationale:** [Why this decision was made]
- **Owner:** [Who made or approved the decision]
- **Impact:** [What this affects or changes]
- **Alternatives Considered:** [Other options that were evaluated]
- **Links:** [Related documents, discussions, or resources]

---

-->

### Big Ideas Framework Improvements (v0.2.0)

- **Date:** 2026-02-17
- **Decision:** Address gaps in Big Ideas framework identified during review
- **Rationale:** Framework review revealed four issues: (1) stats not explicitly updated in promote/archive command flows, causing drift risk; (2) no "Last Reviewed" date on inbox ideas, allowing staleness without detection; (3) no review cadence — ideas can accumulate unreviewed; (4) no tagging or status field on ideas.
- **Owner:** Vit
- **Impact:** MINOR version bump (v0.1.0 → v0.2.0). Three files updated:
  - `BIG_IDEAS.md` — three optional fields added to idea template: `Status`, `Last Reviewed`, `Tags`
  - `PROJECT_SERVICE_PROMPT.md` — stats update step added to promote and archive flows; idea staleness check added to `/project daily`
  - `VERSIONING.md` — version history entry added
- **Category:** Process / Governance
- **Alternatives Considered:**
  - Add "Under Review" as a separate BIG_IDEAS.md section (rejected — overengineered for current scale; Status field on the template achieves same result with less friction)
  - Enforce stats via code/automation (rejected — not applicable in markdown-first system; explicit steps in command definitions is the right approach)
- **Links:** `globaldocs/registry/BIG_IDEAS.md`, `globaldocs/templates/prompts/PROJECT_SERVICE_PROMPT.md`

---

### Git Session Discipline (Mandatory End-of-Session Checks)

- **Date:** 2026-02-13
- **Decision:** All NORI sessions must end with git commit + push, and start with repo sync verification
- **Rationale:** Discovered during session closure that uncommitted work exists. Need automated discipline to ensure:
  1. All session work is committed and pushed before closing
  2. Local repo matches remote before starting new work
  3. No work is lost between sessions
  4. Changes are immediately backed up to remote
- **Owner:** NORI governance / Bootstrap protocol
- **Impact:** Updates BOOTSTRAP.md End-of-Session Protocol with mandatory git checks
- **Implementation:**
  - **Session Start:** Check `git status` and `git fetch` to verify sync with remote
  - **Session End:** Check for uncommitted changes, commit all work, push to remote
  - **Automation:** Consider git hooks or checklist prompts
- **Alternatives Considered:**
  - Manual checks only (rejected - too easy to forget)
  - Auto-commit everything (rejected - need intentional commit messages)
  - Session-end reminder only (chosen - with mandatory verification)
- **Links:** BOOTSTRAP.md Section: End-of-Session Protocol

---

---

## Decision Categories

Decisions can be categorized as:

- **Architectural:** System design, technology choices, structural patterns
- **Process:** Workflow, methodology, governance changes
- **Scope:** What's in/out of scope, feature prioritization
- **Risk:** Risk acceptance, mitigation strategy choices
- **Resource:** Budget, time, people allocation
- **Technical:** Implementation details, library choices, algorithms

---

## Decision Review

Decisions should be reviewed when:
- Significant new information emerges
- Assumptions underlying the decision change
- The decision proves problematic in practice
- A major phase transition occurs

**Review Process:**
1. Reference the original decision entry
2. Create a new decision entry with "Review:" prefix
3. Note what changed and why
4. Update or supersede the original decision
5. Log the review in project logs

---

## Governance

- **Logging Required:** All significant decisions must be logged
- **Minimal Edits:** Append new decisions; don't rewrite history
- **Reversal is OK:** If a decision is reversed, log it as a new decision
- **Owner Accountability:** Decision owner is responsible for implementation oversight
- **Link to Changes:** Decisions should reference related code/doc changes

---

## Notes

Decisions are append-only. If a decision was wrong, add a new decision that reverses it.

This creates a learning trail, not a perfect history.
