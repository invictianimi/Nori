# NORI Project OS — Enterprise Implementation Runbook (Claude Code)
**Purpose:** Implement NORI as a local, personal, AI-enabled project manager/advisor on Windows using Claude Code.  
**Canonical truth:** filesystem + markdown registries (no “memory-only” behavior).  
**Safety:** archive-not-delete, ask-before-overwrite.  
**Adaptive note:** NORI is expected to evolve. If you discover new requirements mid-implementation, log them as decisions and update the implementation docs via controlled amendments rather than ad-hoc edits.

---

## 0) Hard Rules (Non-Negotiable)

1. **Never delete** files/folders. Default to **archive**.
2. **Ask before overwriting** any existing file. If unsure, write a new file with `_v2` suffix.
3. **Markdown is canonical.** DOCX/PDF are generated later from markdown (not in this phase).
4. **Log everything**: every Project Service session + every structural change.
5. **Keep changes minimal** (“diff mindset”): update only what changed, don’t rewrite entire docs.
6. **Project awareness = registry awareness**: always read `PROJECT_INDEX.md` before listing projects or suggesting actions.
7. **Legacy projects (ATAS, Certification-Center, KinderGaurd)**: add wrappers only. Do not refactor or restructure existing code.

---

## 1) Target Directories

Root:
- `E:\MyProjects\NORI\`

Existing:
- `E:\MyProjects\NORI\globaldocs\`
- `E:\MyProjects\NORI\src\`

Create/ensure (global):
- `E:\MyProjects\NORI\globaldocs\registry\`
- `E:\MyProjects\NORI\globaldocs\templates\project_scaffold\`
- `E:\MyProjects\NORI\globaldocs\templates\prompts\`
- `E:\MyProjects\NORI\globaldocs\governance\`
- `E:\MyProjects\NORI\globaldocs\branding\`
- `E:\MyProjects\NORI\globaldocs\logs\`

Create/ensure (projects):
- `E:\MyProjects\NORI\src\_archive\`

---

## 2) Branding + Palette (Reference Only)

Logo path (already provided or placeholder):
- `E:\MyProjects\NORI\globaldocs\branding\NORI-logo.png`

Create:
- `E:\MyProjects\NORI\globaldocs\branding\README.md`

README must state:
- Use logo without credentials
- White page background for docs is fine
- Accent color = “cyan/ice-blue from logo”
- No destructive edits to the logo file

---

## 3) Canonical Registries

### 3.1 Create Registry Files

Create:
- `E:\MyProjects\NORI\globaldocs\registry\PROJECT_INDEX.md`
- `E:\MyProjects\NORI\globaldocs\registry\BIG_IDEAS.md`

#### PROJECT_INDEX.md — Required Table
Create a markdown table with these columns:

| Project | Slug | State | Phase | Last Touched | Next Action (<30m) | Cognitive Load (S/M/L) | AI Autonomy (0–3) | AI Enabled (Y/N) |
|---|---|---|---|---|---|---|---|---|

Populate initial rows for:
- ATAS
- Certification-Center
- KinderGaurd

Defaults:
- State: `active`
- Phase: `Discovery`
- Last Touched: today’s date (YYYY-MM-DD)
- Next Action: `Add NORI wrapper files`
- Cognitive Load: `M`
- AI Autonomy: `1`
- AI Enabled: `Y`

#### BIG_IDEAS.md — Required Sections

- Inbox Ideas
- Promoted to Projects
- Archived Ideas


Idea template:
- Title:
- Date Added:
- Why it matters:
- First Tiny Step (<30m):
- Promotion Criteria:

---

## 4) Governance Files (Minimum Viable Governance)

Create:
- `E:\MyProjects\NORI\globaldocs\governance\LIFECYCLE.md`
- `E:\MyProjects\NORI\globaldocs\governance\VERSIONING.md`

### LIFECYCLE.md must include:
- Phase list (Spark → Ops & Iteration)
- 1–2 line purpose per phase
- Required outputs (brief)
- Placeholder headings:
  - Phase Skip Criteria
  - Decision Gates
  - Governance Triggers

### VERSIONING.md must include:
- Version format (v0.1.0)
- Change log rules
- Amendment authority = Vit (for now)
- Archive-not-delete policy
- Template/schema evolution policy (no silent breaking changes)

---

## 5) Project Scaffold Templates (Canonical Project Files)

Inside:
- `E:\MyProjects\NORI\globaldocs\templates\project_scaffold\`

Create these templates:

### PROJECT.md
Include fields:
- Project Name:
- Slug:
- Blueprint Type:
- Purpose:
- Desired Outcomes:
- Success Metrics:
- Constraints:
- Stakeholders:
- Current Phase:
- State:
- AI Enabled (Y/N):
- AI Autonomy Level (0–3):
- Allowed AI Actions:
- Disallowed AI Actions:
- Links:

### STATUS.md
Include fields:
- Last Updated:
- Current Phase:
- Top 3 Priorities:
- Next Action (<30m):
- Blockers:
- Momentum Score (1–5):
- Cognitive Load (S/M/L):
- Notes:

### DECISIONS.md
Template:
- Date:
- Decision:
- Rationale:
- Owner:
- Impact:
- Links:

### RISKS.md
Template:
- Risk:
- Likelihood (L/M/H):
- Impact (L/M/H):
- Mitigation:
- Trigger:
- Owner:

### README_NORI.md
Explain:
- This project is managed under NORI Project OS
- Which files are canonical
- Where logs are stored
- How `/project` works
- Archive-not-delete policy

Also document these required folders (created per project):
- `logs\`
- `kb\`
- `artifacts\` (optional but recommended)

---

## 6) Project Service Router (This is the “Awareness Engine”)

Create:
- `E:\MyProjects\NORI\globaldocs\templates\prompts\PROJECT_SERVICE_PROMPT.md`

It must implement the command behavior below.

### Supported Commands
- `/project` (menu)
- `/project new`
- `/project list`
- `/project open <slug>`
- `/project status <slug>`
- `/project idea add`
- `/project idea list`
- `/project daily`
- `/project archive <slug>`
- `/project validate` (integrity checks)

### `/project` Menu
When user types `/project`, show:
1) Start New Project  
2) List Projects + Status  
3) Open Project  
4) Big Ideas (Add/List/Promote)  
5) Daily Check-in  
6) Validate Integrity  
7) Archive Project  
8) Exit

**Mandatory behavior:** always read `PROJECT_INDEX.md` first.

---

## 7) Project Creation Workflow (`/project new`)

### Prompt the user for:
- Project Name
- Desired Outcome (1 sentence)
- Success Metrics
- Constraints (time/money/tools)
- Blueprint Type (optional)
- Cognitive Load (S/M/L) default M
- AI Enabled (Y/N) default Y
- AI Autonomy (0–3) default 1

### Then execute:
1. Create slug (lowercase, hyphen-separated)
2. Create folder: `E:\MyProjects\NORI\src\<slug>\`
3. Create subfolders:
   - `logs\`
   - `kb\`
   - `artifacts\`
4. Copy scaffold files into the new folder:
   - PROJECT.md, STATUS.md, DECISIONS.md, RISKS.md, README_NORI.md
5. Populate `PROJECT.md` and `STATUS.md` with the user’s answers:
   - STATUS Next Action must be <30 minutes and single-step
   - If unsure, set Next Action = `Write Framing statement (problem + goal)`
6. Append project row to `PROJECT_INDEX.md`
7. Create initial log:
   - `src\<slug>\logs\YYYY-MM-DD_project-created.md`
8. Log the Project Service session in:
   - `globaldocs\logs\YYYY-MM-DD_projects-session.md`
9. Ask whether to init git in the project folder (optional, see Section 11)

---

## 8) Listing + Opening Projects (`/project list`, `/project open <slug>`)

### `/project list`
- Read `PROJECT_INDEX.md`
- Display the table
- Ask user if they want:
  - open a project
  - do daily check-in
  - add a big idea

### `/project open <slug>`
- Validate slug exists in registry
- Read:
  - `src/<slug>/STATUS.md`
  - `src/<slug>/PROJECT.md`
- Summarize to user:
  - Current phase/state
  - Next Action
  - Blockers
- Ask:
  - “Do you want to execute Next Action now, or update STATUS?”

Any edits must:
- update `STATUS.md` (minimal diff)
- update `PROJECT_INDEX.md` (Last Touched, Next Action if changed)
- create a log entry in:
  - `src/<slug>/logs/YYYY-MM-DD_<short-session-name>.md`
  - `globaldocs/logs/YYYY-MM-DD_projects-session.md`

---

## 9) Big Ideas (`/project idea add`, `/project idea list`, Promote)

### `/project idea add`
- Ask for:
  - Title
  - Why it matters
  - First tiny step (<30m)
  - Promotion criteria
- Append to `BIG_IDEAS.md`
- Log the action

### `/project idea list`
- Display sections and idea titles
- Offer:
  - promote an idea → project (requires user confirmation)
  - archive an idea

### Promote Idea → Project
- Copy the idea content into `PROJECT.md` fields where relevant
- Run `/project new` workflow (but prefilled)
- Move idea entry from Inbox → Promoted section (do not delete)
- Log the promotion

---

## 10) Daily Check-in (`/project daily`)

Ask:
- Energy (1–10)
- Focus (low/med/high)

Then:
- Read `PROJECT_INDEX.md`
- Rank projects based on:
  - State=active
  - Next Action exists
  - Last Touched oldest first (staleness)
  - Cognitive load matched to energy:
    - energy <=4 → prefer S
    - 5–7 → S/M
    - 8–10 → any
- Propose top 3 project options:
  - show slug + Next Action (<30m) + Cognitive Load
- User selects one → run `/project open <slug>`

Log the check-in result.

---

## 11) Archive Policy (`/project archive <slug>`)

Archive = move, never delete.

### Steps:
1. Confirm with user
2. Move folder to:
   - `E:\MyProjects\NORI\src\_archive\<slug>\YYYY-MM-DD\`
3. Update registry row:
   - State=archived
   - Last Touched=today
   - Next Action blank or “—”
4. Log archive event in:
   - `globaldocs\logs\YYYY-MM-DD_archive.md`
5. Do not modify old project logs (preserve history)

---

## 12) Integrity Validation (`/project validate`)

This is required for enterprise-grade stability.

### Validation checks:
1. Registry file exists
2. For each registry row (excluding archived):
   - Folder exists in `src\`
   - Required files exist:
     - PROJECT.md, STATUS.md, DECISIONS.md, RISKS.md, README_NORI.md
   - logs folder exists
3. Detect orphan projects:
   - folders in `src\` not present in registry (excluding `_archive`)
4. If mismatch found:
   - Report findings
   - Ask user for permission before auto-fixing
   - Log discrepancy + resolution

---

## 13) NORI Self-Instantiation (Dogfooding)

Create a project:
- `E:\MyProjects\NORI\src\NORI-Project-OS\`

Use the scaffold.
Set:
- State: `active`
- Phase: `Planning` (or `Discovery` if you prefer conservative)
- AI autonomy: `2` (only for low-risk doc updates, never destructive)
- Next Action: `Finalize Project Service prompt and validate registries`

Add this project to `PROJECT_INDEX.md` like any other.

---

## 14) Git (Recommended, Ask First)

### Option A — Single repo at NORI root (recommended)
- Initialize git at `E:\MyProjects\NORI\`
- Commit baseline structure
- Future commits reflect registry + project changes

### Option B — Per-project repos (optional)
- Only if you want each project isolated

**Ask the user before initializing git.**  
If user approves:
- Create `.gitignore` (ignore build artifacts, caches, etc.)
- Commit message: `Initial NORI Project OS scaffold`

---

## 15) Logging Standard (Required)

### Global Project Service Log
File:
- `globaldocs\logs\YYYY-MM-DD_projects-session.md`

Must include:
- Commands run
- Files changed (list)
- Decisions made
- Next recommended action

### Per-Project Log
File:
- `src/<slug>/logs/YYYY-MM-DD_<session-title>.md`

Must include:
- Context
- What changed
- Decisions
- Next action

**Logs are append-only.** If mistake is found, add a correction entry.

---

## 16) Milestone Validation Checklist (Phase 1 Completion)

Phase 1 is “done” when:
- Registry exists and is correct
- Big Ideas exists and is usable
- Templates exist and are used for project creation
- `/project` router works reliably
- Legacy projects have wrappers
- NORI-Project-OS exists as a project
- Archive workflow works
- Validate workflow works
- Logs are consistently created

---

## 17) Controlled Evolution Clause (Important)

If new needs are discovered during implementation:
1. Record them in `DECISIONS.md` (NORI-Project-OS)
2. Update the relevant governance or template file (minimal diff)
3. Increment version in VERSIONING.md if it’s structural
4. Log the change in globaldocs/logs
5. Do not “silently change” schema without recording it

---

# EXECUTION INSTRUCTIONS (What to do now)

1) Implement Sections 1–6 (structure + registries + templates + router)  
2) Implement `/project validate`  
3) Wrap legacy projects (Section 7/8/9)  
4) Create NORI-Project-OS project (Section 13)  
5) Run `/project validate` again  
6) Create session logs for everything  

Proceed step-by-step and pause after each major section with a brief summary of what was created/changed.

---

## 18) Operational Continuity & Rollback Doctrine

NORI must support session continuity, controlled recovery, and rollback without destructive operations.

### Session Continuity

- SESSION_STATE.md represents the live operational pointer.
- It must be updated at the end of every session.
- Bootstrap must read it at the beginning of every session.
- Resume decisions must be user-confirmed.

### Rollback Procedure

Rollback must NEVER involve deleting files.

If rollback is required:

1. Identify last stable checkpoint (git commit or archived snapshot).
2. Create a backup of current state before modifying anything.
3. Restore from:
   - Git reset (if repository exists), OR
   - Archived snapshot directory.
4. Log rollback event in:
   - globaldocs/logs/YYYY-MM-DD_rollback.md
5. Update SESSION_STATE.md.
6. Run integrity validation (/project validate).

Rollback events must always be logged.
No silent recovery actions are allowed.

### System Health Levels

System Health in SESSION_STATE.md must be one of:

- OK — No inconsistencies detected.
- Warning — Minor inconsistencies detected but non-blocking.
- Critical — Structural corruption or registry mismatch detected.

If Critical:
- Halt execution until user confirms corrective action.

---

## 19) Documentation Governance & Drift Prevention

Documentation in NORI is considered operational infrastructure.

It must remain synchronized with system behavior.

### Documentation Update Triggers

Documentation must be reviewed and updated when:

- Registry schema changes
- Template fields are added or removed
- New commands are added to PROJECT_SERVICE_PROMPT.md
- Governance policies are modified
- Rollback or recovery procedures change
- Folder structure changes
- Logging format changes

If structural change occurs and documentation is not updated,
the system is considered in Warning state.

---

### Documentation Review Gate (Per Milestone)

At the completion of any milestone:

1. Review:
   - NORI_Implementation_Runbook.md
   - PROJECT_SERVICE_PROMPT.md
   - BOOTSTRAP.md
   - VERSIONING.md
   - Templates

2. Confirm:
   - All behaviors described match current implementation.
   - No new commands are undocumented.
   - No schema fields exist in practice but not in documentation.

3. Log review completion.

---

### Version Alignment Rule

If documentation structure changes:

- Increment version in VERSIONING.md.
- Log the version change.
- Note reason for update.
- Update As-Built document if structural.

No silent documentation drift allowed.

---

### End-of-Session Documentation Check

Before closing any session:

1. Ask:
   - Did any structural behavior change?
   - Were new commands introduced?
   - Was any schema modified?

2. If yes:
   - Update relevant documentation.
   - Log update.
   - Update VERSIONING.md if structural.

3. Confirm documentation state with user.

---

### Documentation Health States

Documentation health mirrors system health:

- OK — Documentation synchronized.
- Warning — Minor drift detected.
- Critical — Schema or behavior undocumented.

Critical documentation drift halts structural changes
until resolved.

---

## 20) Universal Project Governance Requirement

All projects under NORI must comply with NORI governance standards.

This includes:

- Use of scaffold structure.
- Presence of required project files.
- Logging discipline.
- Registry inclusion.
- Session state tracking.
- Archive-not-delete policy.

No project may exist in src\ without:

- A registry entry.
- Required scaffold files.
- Compliance with audit standards.

Legacy projects must be wrapped to comply.

---

### Governance Enforcement Rule

If a project is detected that:

- Lacks required files
- Is not in registry
- Has undocumented structural changes
- Violates archive policy

The system must:

1. Flag during /project validate
2. Require remediation before further structural changes
3. Log the violation
4. Update SESSION_STATE.md with Warning or Critical status

---

### Governance Expansion Clause

If governance rules evolve:

- All active projects must be reviewed for compliance.
- Required changes must be logged.
- Documentation must be updated.
- VERSIONING.md must reflect structural update.

No partial governance allowed.

All projects must operate under the same standards.

