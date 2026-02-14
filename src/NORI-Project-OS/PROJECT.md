# Project: NORI Project OS

**Slug:** nori-project-os

**Created:** 2026-02-13

---

## Project Overview

### Purpose

Build and maintain NORI as a local, personal, AI-enabled project management system on Windows using Claude Code.

### Desired Outcomes

- Fully functional project management system based on filesystem + markdown
- All commands in PROJECT_SERVICE_PROMPT.md implemented and working
- Registry integrity maintained
- Documentation synchronized with implementation
- Stable foundation for managing personal/professional projects

### Success Metrics

- `/Projects validate` returns OK status
- All legacy projects successfully wrapped
- Documentation complete and accurate
- System passes milestone validation checklist (Phase 1)
- Able to create, manage, and archive projects reliably

---

## Project Details

### Blueprint Type

System Development / Infrastructure Project

### Stakeholders

- Vit (project owner and primary user)
- Future users of NORI (if expanded)

### Constraints

- **Time:** Bootstrap completion prioritized
- **Budget:** N/A (personal project)
- **Tools:** Claude Code, Windows filesystem, markdown, git (optional)
- **Other:** Must maintain archive-not-delete policy, minimal diff philosophy

---

## Current State

### Current Phase

Planning

### State

active

---

## AI Configuration

### AI Enabled

Y

### AI Autonomy Level

2

**Level Definitions:**
- **0:** No AI autonomy. AI only answers questions.
- **1:** AI can suggest actions but must get approval.
- **2:** AI can execute low-risk actions (read files, create drafts, run tests).
- **3:** AI has full autonomy within project boundaries (can commit, deploy if configured).

### Allowed AI Actions

- Read all NORI system files
- Create documentation
- Update templates (with logging)
- Run `/Projects validate`
- Create log entries
- Update governance docs (non-breaking changes only)
- Suggest improvements

### Disallowed AI Actions

- Delete any files (must archive instead)
- Make breaking changes to schemas without approval
- Modify registry without logging
- Skip validation after structural changes
- Auto-fix critical issues without permission
- Modify templates without version increment

---

## Links & References

- **Repository:** TBD (git init recommended)
- **Documentation:** `E:\MyProjects\NORI\globaldocs\`
- **Related Projects:** All projects in NORI are managed by this system
- **External Resources:**
  - NORI Implementation Runbook
  - Bootstrap Protocol
  - PROJECT_SERVICE_PROMPT.md

---

## Notes

**Dogfooding:** This is NORI managing itself. All decisions about NORI's development should be logged in this project's DECISIONS.md.

**Evolution:** NORI is expected to evolve. Follow controlled evolution clause - log all structural changes, version appropriately, update documentation.

**Current Phase:** Planning phase covers finalization of initial implementation and validation.

---

## Metadata

**Last Updated:** 2026-02-13

**NORI Version:** v0.1.0
