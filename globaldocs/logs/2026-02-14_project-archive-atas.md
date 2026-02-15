# Project Archive Log: ATAS

**Date:** 2026-02-14
**Time:** 2026-02-14 (session time)
**Action:** Archive Project
**Project Slug:** atas

---

## Project Details (at time of archive)

- **Project Name:** ATAS
- **Slug:** atas
- **Previous State:** active
- **New State:** archived
- **Phase:** Discovery
- **Last Touched:** 2026-02-13 (updated to 2026-02-14 on archive)
- **Previous Next Action:** Review MARC/ folder structure
- **New Next Action:** —
- **Cognitive Load:** M (Medium)
- **AI Autonomy Level:** 1 (Suggest)
- **AI Enabled:** Y

---

## Archive Location

**From:** `src/atas/`
**To:** `src/_archive/atas/2026-02-14/`

---

## Archived Contents

The following files and folders were moved to archive:

- **NORI Wrapper Files:**
  - PROJECT.md
  - STATUS.md
  - DECISIONS.md
  - RISKS.md
  - README_NORI.md

- **Project Folders:**
  - MARC/ (original project content)
  - kb/ (knowledge base)
  - logs/ (project logs)
  - artifacts/
  - .git/ (git repository)

---

## Registry Changes

**PROJECT_INDEX.md** updated:
- Removed from "Active Projects" section
- Added to "Archived Projects" section
- State changed: `active` → `archived`
- Last Touched updated: `2026-02-13` → `2026-02-14`
- Next Action changed: `Review MARC/ folder structure` → `—`

---

## Reason for Archive

User-initiated archive via `/project --archive ATAS` command.

---

## Recovery Instructions

To restore this project from archive:

1. Move folder back to active location:
   ```bash
   mv "e:\MyProjects\Nori\src\_archive\atas\2026-02-14" "e:\MyProjects\Nori\src\atas"
   ```

2. Update PROJECT_INDEX.md:
   - Move row from "Archived Projects" to "Active Projects"
   - Change state from `archived` to `active`
   - Update Last Touched date
   - Set appropriate Next Action

3. Update SESSION_STATE.md with active_project

---

## Notes

- Archive follows NORI governance: prefer archiving over deletion
- Project can be restored at any time
- All project history and content preserved in archive
- Archive retention period: 30 days minimum before eligible for deletion

---

**Archive completed successfully.**
