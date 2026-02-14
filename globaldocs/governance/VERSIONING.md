# Versioning & Change Management

This document defines how NORI Project OS and its governed projects manage versions, changes, and evolution.

**Version:** v0.1.0
**Last Updated:** 2026-02-13
**Authority:** Vit

---

## Version Format

NORI uses **Semantic Versioning** adapted for documentation and governance.

Format: `v[MAJOR].[MINOR].[PATCH]`

Example: `v0.1.0`, `v1.2.3`

---

## Version Component Meanings

### MAJOR (v[X].0.0)

Increment when:
- Breaking changes to registry schema
- Breaking changes to template structure
- Breaking changes to command interfaces
- Incompatible governance policy changes

**Impact:** Requires review of all projects for compliance

**Example:** Changing required fields in PROJECT.md

---

### MINOR (vX.[Y].0)

Increment when:
- New features added (new commands, new templates)
- Non-breaking schema additions (new optional fields)
- New governance policies (additive)
- Significant documentation improvements

**Impact:** Existing projects unaffected but may benefit from update

**Example:** Adding `/Projects analytics` command

---

### PATCH (vX.Y.[Z])

Increment when:
- Bug fixes
- Typo corrections
- Clarifications to existing documentation
- Minor formatting improvements
- Log corrections

**Impact:** No project changes required

**Example:** Fixing typo in LIFECYCLE.md

---

## What Gets Versioned

### NORI Core (This System)

Files versioned as a cohesive unit:
- BOOTSTRAP.md
- NORI_Implementation_Runbook.md
- LIFECYCLE.md
- VERSIONING.md (this file)
- PROJECT_SERVICE_PROMPT.md
- All templates in `templates/project_scaffold/`

**Current NORI Version:** v0.1.0

---

### Individual Projects

Projects follow their own versioning (optional).

NORI does not enforce project-level versioning.

Projects may choose semantic versioning, date-based versioning, or no versioning.

---

### Templates & Schemas

Template changes trigger NORI version increments:
- New required field → MAJOR
- New optional field → MINOR
- Clarification to field description → PATCH

---

## Change Log Rules

### Required Changelog Entries

All version changes must include:
- Version number
- Date of change
- Description of changes
- Author/authority
- Rationale (for MAJOR/MINOR changes)

### Changelog Location

- **NORI Core:** Version history tables in each governance doc
- **Projects:** Optional, in project's DECISIONS.md or dedicated CHANGELOG.md

---

## Amendment Authority

**Current Authority:** Vit

Amendment process:
1. Identify need for change
2. Document proposed change in DECISIONS.md (for NORI-Project-OS)
3. Obtain approval from authority
4. Update relevant files
5. Increment version number
6. Log change in version history
7. Update SESSION_STATE.md if structural

**Delegation:** Authority may delegate specific amendment rights to AI agents (per AI Autonomy levels)

---

## Archive-Not-Delete Policy

**Core Principle:** Files are never deleted, only archived.

### Archiving Process

When a file/project becomes obsolete:

1. **Do not delete**
2. Move to appropriate archive location:
   - Projects → `src/_archive/[slug]/[YYYY-MM-DD]/`
   - Documents → `globaldocs/archive/[category]/[filename]_[YYYY-MM-DD].md`
3. Update references to point to archive or remove references
4. Log archive event with:
   - What was archived
   - Why it was archived
   - Where it was moved
   - Date of archive

### Archive Directory Structure

Create archive folders as needed:
- `src/_archive/` (projects)
- `globaldocs/archive/templates/` (deprecated templates)
- `globaldocs/archive/governance/` (superseded policies)
- `globaldocs/archive/docs/` (outdated documentation)

### Why Archive-Not-Delete

- Preserves project history
- Enables rollback if needed
- Prevents accidental loss of knowledge
- Maintains audit trail
- Supports learning from past decisions

---

## Template & Schema Evolution Policy

**No Silent Breaking Changes**

All template/schema changes must be:
1. **Documented** before implementation
2. **Versioned** appropriately (MAJOR/MINOR/PATCH)
3. **Logged** in change history
4. **Communicated** (if breaking change)
5. **Validated** via `/Projects validate` after implementation

### Template Change Process

1. Identify need for template change
2. Document proposed change in NORI-Project-OS DECISIONS.md
3. Assess impact (breaking vs. non-breaking)
4. Get approval if MAJOR change
5. Update template file
6. Update runbook/documentation to match
7. Increment NORI version
8. Log change
9. Run `/Projects validate` to check compliance

### Schema Backward Compatibility

When adding fields:
- **Required fields** → MAJOR version (breaking)
- **Optional fields** → MINOR version (non-breaking)

Existing projects:
- MAJOR changes → may require manual update
- MINOR changes → existing files remain valid

---

## Governance Version Synchronization

All governance files should maintain aligned versions.

If one governance file changes:
- Update version number in that file
- Consider if other files need updates
- Update NORI core version if structural

**Version Drift Prevention:**
- Regular validation checks
- End-of-session documentation reviews
- `/Projects validate` includes version consistency check

---

## Rollback Support

Versions enable safe rollback.

Rollback process:
1. Identify target version to restore
2. Use git history (if repository exists) OR archived snapshots
3. Create backup of current state before rollback
4. Restore files from target version
5. Log rollback event in `globaldocs/logs/[YYYY-MM-DD]_rollback.md`
6. Update SESSION_STATE.md
7. Run `/Projects validate`

**Critical:** Never rollback without backup of current state.

---

## Documentation Health

Version synchronization is part of system health.

Documentation Health states:
- **OK:** All documentation versions aligned, changes logged
- **Warning:** Minor version drift or missing changelog entries
- **Critical:** Schema implemented but undocumented, or breaking changes not versioned

Critical documentation drift halts structural changes until resolved.

---

## Governance

- **Version changes require logging:** All version increments must have changelog entry
- **Breaking changes require approval:** MAJOR versions must be approved by authority
- **Templates are infrastructure:** Template changes follow same rigor as code changes
- **Archive is permanent:** Once archived, files must not be deleted
- **No silent evolution:** All structural changes must be explicit and documented

---

## Version History

| Version | Date | Changes | Author |
|---|---|---|---|
| v0.1.0 | 2026-02-13 | Initial versioning policy defined | NORI Bootstrap |
