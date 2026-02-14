# PROJECT INDEX

This is the canonical registry of all projects under NORI Project OS.

**Last Updated:** 2026-02-13

---

## Registry Schema

| Field | Description | Valid Values |
|---|---|---|
| Project | Full project name | Any string |
| Slug | URL-safe identifier | lowercase-hyphen-separated |
| State | Current operational state | `active`, `paused`, `archived` |
| Phase | Current lifecycle phase | `Spark`, `Discovery`, `Planning`, `Build`, `Test`, `Deploy`, `Ops & Iteration` |
| Last Touched | Last modification date | YYYY-MM-DD |
| Next Action (<30m) | Single, immediate next step | Brief action description |
| Cognitive Load | Complexity/mental effort | `S` (Small), `M` (Medium), `L` (Large) |
| AI Autonomy | AI decision-making level | `0` (none), `1` (suggest), `2` (execute low-risk), `3` (full autonomy) |
| AI Enabled | Whether AI assistance is active | `Y` (Yes), `N` (No) |

---

## Active Projects

| Project | Slug | State | Phase | Last Touched | Next Action (<30m) | Cognitive Load (S/M/L) | AI Autonomy (0–3) | AI Enabled (Y/N) |
|---|---|---|---|---|---|---|---|---|
| ATAS | atas | active | Discovery | 2026-02-13 | Review MARC/ folder structure | M | 1 | Y |
| Certification Center | certification-center | active | Discovery | 2026-02-13 | Review WebSite-Overhaul/ folder | M | 1 | Y |
| KinderGuard | kinderguard | active | Discovery | 2026-02-13 | Review Home_IGA_Report.docx | M | 1 | Y |
| NORI Project OS | nori-project-os | active | Planning | 2026-02-13 | Initialize git repository at NORI root | L | 2 | Y |

---

## Paused Projects

_None_

---

## Archived Projects

_None_

---

## Registry Governance

- **Archive-not-delete policy:** Projects must never be deleted, only moved to archive state
- **Slug uniqueness:** Each slug must be unique across all states (active, paused, archived)
- **Required fields:** All fields in the schema must have valid values for active/paused projects
- **Orphan detection:** All folders in `src\` (excluding `_archive`) must have registry entries
- **Structural compliance:** All registered projects must have required NORI scaffold files

---

## Validation

Last validation: 2026-02-13 — Status: ✅ OK

Run `/Projects validate` to verify registry integrity.
