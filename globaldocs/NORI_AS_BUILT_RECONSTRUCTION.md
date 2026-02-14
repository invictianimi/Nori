# NORI — As-Built Reconstruction Document
Version: v1.0.0
Purpose: Full deterministic rebuild instructions for NORI Project OS.

This document allows NORI to be recreated from scratch without prior chat history.

---

# 1. SYSTEM OVERVIEW

NORI (Neural Optimization Research & Intelligence) is a local, filesystem-based, AI-enabled Project Operating System.

Core principles:
- Filesystem = source of truth
- Markdown = canonical format
- Logs are append-only
- Archive, never delete
- AI must operate under governance discipline
- Session continuity must be preserved

---

# 2. ROOT DIRECTORY STRUCTURE

Root:
E:\MyProjects\NORI\

Required folders:

E:\MyProjects\NORI\
│
├── globaldocs\
│   ├── registry\
│   ├── templates\
│   │   ├── project_scaffold\
│   │   └── prompts\
│   ├── governance\
│   ├── branding\
│   ├── logs\
│   ├── SESSION_STATE.md
│   ├── BOOTSTRAP.md
│   ├── NORI_Implementation_Runbook.md
│   └── NORI_AS_BUILT_RECONSTRUCTION.md
│
├── src\
│   ├── _archive\
│   └── <project folders>
│
└── (optional .git repo at root)

All directories must exist before execution begins.

---

# 3. REQUIRED CORE FILES

## 3.1 Registry Files

Location:
globaldocs/registry/

Create:

PROJECT_INDEX.md
BIG_IDEAS.md

PROJECT_INDEX table columns:

| Project | Slug | State | Phase | Last Touched | Next Action (<30m) | Cognitive Load (S/M/L) | AI Autonomy (0–3) | AI Enabled (Y/N) |

BIG_IDEAS sections:

# Inbox Ideas
# Promoted to Projects
# Archived Ideas

---

## 3.2 Governance Files

Location:
globaldocs/governance/

Create:

LIFECYCLE.md
VERSIONING.md

LIFECYCLE.md must define:
- Spark
- Framing
- Directive
- Discovery
- Validation
- Planning
- Architecture
- Design
- Specification
- Development
- Orchestration
- Execution
- Launch Readiness
- Go Live
- Operations & Iteration

VERSIONING.md must define:
- Version format (vX.Y.Z)
- Archive-not-delete policy
- Amendment authority
- Schema evolution rules

---

## 3.3 Templates

Location:
globaldocs/templates/project_scaffold/

Create:

PROJECT.md
STATUS.md
DECISIONS.md
RISKS.md
README_NORI.md

Each project folder must contain:

logs\
kb\
artifacts\

---

## 3.4 Project Service Router

Location:
globaldocs/templates/prompts/PROJECT_SERVICE_PROMPT.md

This file defines all `/Projects` command behavior.

Supported commands:

/Projects
/Projects new
/Projects list
/Projects open <slug>
/Projects idea add
/Projects idea list
/Projects daily
/Projects archive <slug>
/Projects validate

Router must:
- Always read PROJECT_INDEX.md first
- Always log actions
- Always update registry minimally

---

## 3.5 Bootstrap File

Location:
globaldocs/BOOTSTRAP.md

Must enforce:

Session Start Ritual:
1. Read:
   - NORI_Implementation_Runbook.md
   - PROJECT_SERVICE_PROMPT.md
   - PROJECT_INDEX.md
   - SESSION_STATE.md

2. Summarize:
   - Registry state
   - Last session
   - Active project
   - Pending action
   - System health

3. Confirm readiness before modifying files.

End-of-Session Protocol:
- Log all actions
- Update SESSION_STATE.md
- Confirm system health
- Confirm next action

---

## 3.6 SESSION_STATE.md

Location:
globaldocs/SESSION_STATE.md

Template:

# NORI Session State

Last Session Date:
Active Project:
Last Command Executed:
Pending Next Action:
System Health: OK | Warning | Critical
Last Log File:
Notes:

This file is updated at end of every session.

---

# 4. PROJECT CREATION WORKFLOW

When creating a project:

1. Generate slug (lowercase-hyphenated).
2. Create folder:
   src/<slug>\
3. Create subfolders:
   logs\
   kb\
   artifacts\
4. Copy scaffold templates.
5. Populate PROJECT.md and STATUS.md.
6. Append row to PROJECT_INDEX.md.
7. Create:
   src/<slug>/logs/YYYY-MM-DD_project-created.md
8. Log global session:
   globaldocs/logs/YYYY-MM-DD_projects-session.md
9. Update SESSION_STATE.md.

---

# 5. ARCHIVE POLICY

Archive, never delete.

Move project to:
src/_archive/<slug>/YYYY-MM-DD/

Update registry:
State = archived
Next Action = —

Log archive event.

---

# 6. INTEGRITY VALIDATION

Validation must confirm:

- Registry file exists
- All non-archived projects exist in src\
- Required project files exist
- No orphan folders
- No duplicate slugs

If mismatch:
- Report
- Do not auto-fix without approval
- Log discrepancy

---

# 7. LOGGING RULES

Two log layers:

1. Global:
   globaldocs/logs/YYYY-MM-DD_projects-session.md

2. Per-project:
   src/<slug>/logs/YYYY-MM-DD_<context>.md

Logs are append-only.
Corrections require new log entry.

---

# 8. ROLLBACK DOCTRINE

Rollback must:

1. Identify stable checkpoint.
2. Backup current state.
3. Restore via:
   - Git reset OR
   - Archive restore.
4. Log rollback.
5. Update SESSION_STATE.md.
6. Run validation.

Never silent rollback.
Never destructive recovery.

---

# 9. NORI SELF-INSTANTIATION

NORI must manage itself.

Create project:
src/NORI-Project-OS/

Default:
State: active
Phase: Planning
AI Autonomy: 2 (low-risk only)
Next Action: Validate system integrity

---

# 10. GIT (OPTIONAL BUT RECOMMENDED)

Initialize at NORI root.

First commit:
Initial NORI Project OS scaffold

Commit frequently after structural changes.

---

# 11. CONTROLLED EVOLUTION CLAUSE

If new requirements emerge:

1. Record decision in DECISIONS.md (NORI-Project-OS).
2. Update relevant template or governance file.
3. Increment version if structural.
4. Log change.
5. Never silently alter schema.

---

# 12. REBUILD PROCEDURE FROM SCRATCH

If full rebuild required:

1. Create directory structure.
2. Create governance files.
3. Create registry files.
4. Create scaffold templates.
5. Create router prompt file.
6. Create BOOTSTRAP.md.
7. Create SESSION_STATE.md.
8. Create NORI-Project-OS project.
9. Initialize git.
10. Run integrity validation.

System considered operational when:

- Registry valid
- Bootstrap passes
- Projects create successfully
- Logs functioning
- SESSION_STATE updates correctly

---

# END OF DOCUMENT
