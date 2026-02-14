# NORI Project Management

This project is managed under **NORI Project OS**.

---

## What is NORI?

NORI is a local, filesystem-based project management system designed for:
- Individual developers and small teams
- AI-augmented project workflows
- Structured decision-making and risk tracking
- Archive-not-delete philosophy
- Markdown-based canonical documentation

---

## Canonical Files

The following files are the single source of truth for this project:

| File | Purpose |
|---|---|
| [PROJECT.md](PROJECT.md) | Project definition, constraints, AI configuration |
| [STATUS.md](STATUS.md) | Current state, priorities, next actions |
| [DECISIONS.md](DECISIONS.md) | Decision log with rationale |
| [RISKS.md](RISKS.md) | Risk register and mitigation tracking |
| [README_NORI.md](README_NORI.md) | This file - NORI usage guide |

---

## Folder Structure

```
[project-slug]/
├── PROJECT.md           # Project definition
├── STATUS.md            # Current status
├── DECISIONS.md         # Decision log
├── RISKS.md             # Risk register
├── README_NORI.md       # NORI guide
├── logs/                # Session logs (append-only)
├── kb/                  # Knowledge base (docs, notes, references)
└── artifacts/           # Generated files, outputs, builds (optional)
```

---

## Working with NORI

### Starting a Session

Use the NORI Project Service commands:

```
/Projects                    # Main menu
/Projects open [slug]        # Open this project
/Projects status [slug]      # View current status
```

When you open a project, NORI will:
1. Read STATUS.md
2. Show current phase, priorities, and next action
3. Ask if you want to execute the next action or update status

---

## Logs Directory

All project sessions must be logged.

**Log Location:** `logs/`

**Log Format:** `YYYY-MM-DD_[session-name].md`

**Log Contents:**
- Session context (what you were working on)
- Actions taken
- Decisions made
- Changes to files
- Next action identified

**Logs are append-only.** Never delete logs. If a mistake is logged, add a correction entry.

---

## Archive-Not-Delete Policy

NORI follows a strict **archive-not-delete** policy.

**Never delete:**
- Project files
- Logs
- Decisions
- Old versions of documents

**Instead:**
- Move files to `_archive/` subfolder with date stamp
- Mark items as "archived" or "superseded"
- Create new files with `_v2` suffix if needed

**Why?**
- Preserves history
- Enables rollback
- Supports learning from past decisions
- Maintains audit trail

---

## AI Configuration

This project's AI settings are defined in [PROJECT.md](PROJECT.md).

**AI Autonomy Levels:**
- **0:** AI only answers questions (no autonomous actions)
- **1:** AI suggests actions, waits for approval
- **2:** AI can execute low-risk actions (read, draft, test)
- **3:** AI has full autonomy within project boundaries

**Check PROJECT.md for:**
- Current autonomy level
- Allowed AI actions
- Disallowed AI actions

---

## Registry Integration

This project is registered in:
- **Global Registry:** `E:\MyProjects\NORI\globaldocs\registry\PROJECT_INDEX.md`

The registry tracks:
- Project metadata
- Current phase and state
- Next action
- Cognitive load
- AI configuration

**Changes to STATUS.md may trigger registry updates.**

---

## Governance

This project follows NORI governance policies:

- **Lifecycle:** [globaldocs/governance/LIFECYCLE.md](../../globaldocs/governance/LIFECYCLE.md)
- **Versioning:** [globaldocs/governance/VERSIONING.md](../../globaldocs/governance/VERSIONING.md)

---

## Validation

Run `/Projects validate` to check:
- Registry consistency
- Required files present
- Structural compliance
- No orphaned projects

---

## Getting Help

- **NORI Documentation:** `E:\MyProjects\NORI\globaldocs\`
- **Implementation Runbook:** `globaldocs/NORI_Implementation_Runbook.md`
- **Bootstrap Protocol:** `globaldocs/BOOTSTRAP.md`

---

## Quick Commands Reference

| Command | Purpose |
|---|---|
| `/Projects` | Main menu |
| `/Projects list` | List all projects |
| `/Projects open [slug]` | Open a project |
| `/Projects status [slug]` | Check project status |
| `/Projects daily` | Daily check-in (suggests project based on energy) |
| `/Projects validate` | Run integrity checks |
| `/Projects idea add` | Capture a new idea |

---

## NORI Version

This project scaffold is based on:

**NORI Version:** v0.1.0

**Last Updated:** 2026-02-13
