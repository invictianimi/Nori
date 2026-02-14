# Project: NORI Testing Playground

**Slug:** nori-testing-playground

**Created:** 2026-02-13

---

## Project Overview

### Purpose

Validate `/Projects new` and `/Projects archive` command workflows by creating a temporary test project.

### Desired Outcomes

- Confirm project creation workflow functions correctly
- Verify all scaffold files are generated properly
- Test project archival process works cleanly
- Validate registry updates during create/archive operations

### Success Metrics

- Project successfully appears in registry
- All required scaffold files exist
- Can be archived without errors
- Archival preserves all data

---

## Project Details

###Blueprint Type

Test / Validation Project

### Stakeholders

- NORI system developers
- Quality assurance validation

### Constraints

- **Time:** <30 minutes (single session)
- **Budget:** N/A
- **Tools:** NORI Project OS only
- **Other:** Temporary project - will be archived after testing

---

## Current State

### Current Phase

Discovery

### State

active

---

## AI Configuration

### AI Enabled

Y

### AI Autonomy Level

1

**Level Definitions:**
- **0:** No AI autonomy. AI only answers questions.
- **1:** AI can suggest actions but must get approval.
- **2:** AI can execute low-risk actions (read files, create drafts, run tests).
- **3:** AI has full autonomy within project boundaries (can commit, deploy if configured).

### Allowed AI Actions

- Read project files
- Create log entries
- Suggest next steps
- Answer questions about project status

### Disallowed AI Actions

- Delete files
- Modify scaffold files
- Execute commands without approval
- Archive project without explicit instruction

---

## Links & References

- **Repository:** N/A (test project)
- **Documentation:** NORI Implementation Runbook
- **Related Projects:** NORI-Project-OS
- **External Resources:** N/A

---

## Notes

This is a temporary test project created to validate NORI's `/Projects new` and `/Projects archive` commands. It will be archived immediately after successful validation.

---

## Metadata

**Last Updated:** 2026-02-13

**NORI Version:** v0.1.0
