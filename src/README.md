# NORI Source Code Directory

This directory contains the source code for NORI Project OS itself.

## Purpose

Unlike `projects/` which contains project metadata and management files, this `src/` directory contains:

- **NORI.Core**: C# class library providing core NORI functionality ✅ Scaffold created 2026-02-17
  - Domain model (NoriProject, ProjectRegistry, ValidationResult) — in progress
  - Project registry reader (parses PROJECT_INDEX.md)
  - Validation engine (mirrors `/project validate`)
  - File system operations

- **NORI.CLI**: Command-line interface tools (future — starts after NORI.Core tests pass)
  - Project creation utilities
  - Migration tools
  - Validation runners

## Directory Organization

```
src/
├── NORI.Core/           # Core C# library  ✅ created 2026-02-17
│   ├── NORI.Core.slnx   # .NET 10 solution format (replaces .sln)
│   ├── NORI.Core/
│   │   └── NORI.Core.csproj   (net10.0 classlib)
│   └── NORI.Core.Tests/
│       └── NORI.Core.Tests.csproj  (net10.0 xunit)
├── NORI.CLI/            # CLI tools (future — after Core tests pass)
├── .gitignore           # Excludes bin/, obj/, .vs/, TestResults/
└── README.md            # This file
```

## Build Requirements

- **.NET 8.0 SDK** or later
- **Visual Studio 2022** or VS Code with C# extension
- **Windows 10/11** (current platform)

## Git Workflow

All source code follows the NORI Git Workflow:
- See `globaldocs/NORI_GIT_WORKFLOW.md`
- Commit discipline: Small, focused commits
- Build artifacts excluded via `.gitignore`

## Build Artifacts

The following are excluded from git:
- `bin/`
- `obj/`
- `.vs/`
- `*.user`

See `src/.gitignore` for complete list.

---

**Version:** 1.1.0
**Created:** 2026-02-15
**Last Updated:** 2026-02-17
**Purpose:** NORI system source code
