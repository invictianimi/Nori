# NORI Source Code Directory

This directory contains the source code for NORI Project OS itself.

## Purpose

Unlike `projects/` which contains project metadata and management files, this `src/` directory contains:

- **NORI.Core**: C# class library providing core NORI functionality
  - Project registry management
  - Validation engine
  - File system operations
  - Schema definitions

- **NORI.CLI**: Command-line interface tools (future)
  - Project creation utilities
  - Migration tools
  - Validation runners

## Directory Organization

```
src/
├── NORI.Core/           # Core C# library
│   ├── NORI.Core.sln
│   ├── NORI.Core/
│   │   └── NORI.Core.csproj
│   └── NORI.Core.Tests/
│       └── NORI.Core.Tests.csproj
├── NORI.CLI/            # CLI tools (future)
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

**Version:** 1.0.0
**Created:** 2026-02-15
**Purpose:** NORI system source code
