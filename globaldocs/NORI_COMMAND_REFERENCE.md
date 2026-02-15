# NORI Command & Switch Reference Guide
Version: v1.0.0  
Scope: Phase 1 (Local Project Intelligence Management System)  
Audience: Vit / Operators (human) + Claude Code (executor)

---

## 0) Key Concept

NORI commands are **conversation commands** you type to Claude Code.

They are enforced by:
- `globaldocs/BOOTSTRAP.md`
- `globaldocs/NORI_Implementation_Runbook.md`
- `globaldocs/templates/prompts/PROJECT_SERVICE_PROMPT.md`
- `globaldocs/registry/PROJECT_INDEX.md`
- `globaldocs/SESSION_STATE.md`

NORI “awareness” comes from reading these files, not from memory.

---

## 1) Boot & Session Controls

### Bootstrap (Session Start)
**Purpose:** Start a governed NORI session with state awareness, audit discipline, and “pause before action.”

**Run from directory:** `E:\MyProjects\NORI\`

**Recommended command to type in Claude Code:**
- `Read globaldocs/BOOTSTRAP.md and follow it strictly for this session.`

**What it must do:**
- Read runbook, prompt router, registry, session state
- Summarize current state + health
- Ask whether to resume/review/start fresh
- Wait for confirmation before making changes

---

### End-of-Session Protocol (Implicit)
**Purpose:** Ensure the session ends with continuity and audit integrity.

**What happens at session close:**
- Global log updated (append-only)
- Project logs updated (if touched)
- `SESSION_STATE.md` updated:
  - last session date
  - active project
  - last command executed
  - pending next action
  - system health
  - last log path

---

## 2) Core Project Service Switch

### `/project`
**Purpose:** Enter "Project Service Mode." Shows the operator menu and routes to workflows.

**Expected behavior:**
- Always reads `PROJECT_INDEX.md` first
- Presents menu options
- Executes selected workflow end-to-end
- Logs actions
- Updates `SESSION_STATE.md` at end of session

---

## 3) Project Creation & Management

### `/project new`
**Purpose:** Create a new project with NORI scaffold and register it.

**Does:**
- Prompts for project name/outcome/success metrics/constraints
- Generates slug
- Creates `projects/<slug>/` + standard subfolders
- Copies scaffold files
- Populates PROJECT.md + STATUS.md
- Adds row to PROJECT_INDEX
- Creates project creation log + global session log

---

### `/project list`
**Purpose:** Show all projects and their current status from the registry.

**Does:**
- Reads `PROJECT_INDEX.md`
- Displays table
- Offers to open a project, do daily check-in, or manage ideas

---

### `/project open <slug>`
**Purpose:** Open a specific project and bring it into focus.

**Does:**
- Validates slug exists in PROJECT_INDEX
- Reads `PROJECT.md` and `STATUS.md`
- Summarizes:
  - phase/state
  - next action (<30m)
  - blockers
- Offers next step options:
  - execute next action
  - update status
  - add decision
  - add risk
  - log session notes

---

### `/project status <slug>`
**Purpose:** Quick status review/update without full open workflow.

**Does:**
- Reads STATUS.md
- Optionally updates Last Updated / Next Action / Priorities
- Updates registry Last Touched and Next Action (minimal diff)
- Logs change

---

## 4) Big Ideas (Idea Intake & Promotion)

### `/project idea add`
**Purpose:** Capture a new idea without creating a project.

**Does:**
- Prompts for:
  - title
  - why it matters
  - first tiny step (<30m)
  - promotion criteria
- Appends to BIG_IDEAS.md
- Logs action

---

### `/project idea list`
**Purpose:** Review Big Ideas.

**Does:**
- Displays Inbox/Promoted/Archived sections (high-level)
- Offers:
  - promote to project
  - archive idea

---

### Promote Idea → Project (workflow within idea list)
**Purpose:** Convert idea into a full project.

**Does:**
- Requires explicit confirmation
- Uses idea content to prefill PROJECT.md fields
- Runs `/project new` flow
- Moves idea entry from Inbox → Promoted (never deletes)
- Logs promotion

---

## 5) Daily Guidance & Momentum

### `/project daily`
**Purpose:** Daily check-in that suggests the best next action across active projects.

**Does:**
- Asks:
  - energy (1–10)
  - focus (low/med/high)
- Ranks projects based on:
  - state=active
  - next action exists
  - staleness (last touched)
  - cognitive load match
- Proposes top 3 options
- User selects one → routes to `/project open <slug>`
- Logs outcome

---

## 6) Archiving & Lifecycle Hygiene

### `/project archive <slug>`
**Purpose:** Retire a project safely without deletion.

**Does:**
- Requires explicit confirmation
- Moves folder to:
  - `src/_archive/<slug>/YYYY-MM-DD/`
- Updates PROJECT_INDEX:
  - state=archived
  - last touched=today
  - next action=—
- Logs archive event

---

## 7) Validation & Audit

### `/project validate`
**Purpose:** Run full integrity + governance + documentation drift audit.

**Validates:**
1) Registry integrity (missing/duplicates/orphans)
2) Project structure compliance (required files/folders exist)
3) Documentation drift (schema/commands/templates aligned with docs)
4) Governance enforcement (logging, session state updates, archive policy)
5) Outputs health states:
   - OK / Warning / Critical

**Rules:**
- Do not auto-fix without approval
- If Critical: halt structural operations until resolved
- Log validation event in globaldocs/logs

---

## 8) Health & State Definitions

### System Health (SESSION_STATE.md)
- **OK:** No known issues
- **Warning:** Minor drift or missing non-critical items
- **Critical:** Registry mismatch, missing required structure, undocumented schema/behavior

**Critical rule:** If Critical, run validation and correct before continuing structural work.

---

## 9) Governance Rules (Always-On)

### Always true:
- No deleting (archive only)
- Ask before overwriting
- Minimal diffs
- Logs are append-only
- All projects in `projects/` must be in `PROJECT_INDEX.md`
- All projects must have NORI wrapper files (legacy projects get wrapped, not refactored)

---

## 10) Future / Reserved Commands (Not Implemented Yet)

These may be implemented in later phases:

- `/project discovery <slug>` (guided scoping interview)
- `/project brainstorm <slug>` (structured ideation capture)
- `/project directive <slug>` (convert discovery → directive)
- `/NORI assess-evolution` (system suggests next feature upgrades)
- `/project snapshot` (checkpoint snapshots for rollback without git)

Until implemented, these should be treated as placeholders only.

---

## 11) Quick “What Do I Type?” Cheatsheet

Start session:
- `Read globaldocs/BOOTSTRAP.md and follow it strictly for this session.`

Project menu:
- `/project`

Create project:
- `/project new`

See all projects:
- `/project list`

Work on a project:
- `/project open <slug>`

Capture idea:
- `/project idea add`

Daily planning:
- `/project daily`

Audit alignment:
- `/project validate`

Archive project:
- `/project archive <slug>`
