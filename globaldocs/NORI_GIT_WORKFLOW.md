# NORI Git Workflow

**SCOPE:** Universal Standard - Applies to ALL projects, ALL contexts, ALL sessions

## Session Closure and Git Commit Best Practice

**This is the CANONICAL workflow for:**
- ✅ NORI Project OS
- ✅ All NORI projects (current and future)
- ✅ BIG_IDEAS.md management
- ✅ Skills development
- ✅ Any git-managed work session
- ✅ Global workflow standard

To avoid uncommitted changes after session commits, follow this order:

### Correct Order

1. **Make all session changes** (archive projects, update registries, create logs, etc.)
2. **Update SESSION_STATE.md LAST** with final session summary
3. **Stage all changes** including SESSION_STATE.md
4. **Commit everything together**
5. **Push to remote** (if desired)

### Example Workflow

```bash
# 1. All session work is done (archives, logs, registry updates, etc.)

# 2. Update SESSION_STATE.md with final state
# Edit SESSION_STATE.md to reflect:
# - Last Command Executed: (what you just did)
# - Pending Next Action: (what's next)
# - Last Log File: (path to most recent log)

# 3. Stage ALL changes INCLUDING SESSION_STATE.md
cd "e:\MyProjects\Nori"
git add .

# 4. Commit everything together
git commit -m "Session summary with all changes

Changes:
- [List all major changes]
- SESSION_STATE.md updated with session closure

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"

# 5. Push if needed
git push origin master
```

### Why This Order Matters

**Wrong way (what we did initially):**
1. Make changes
2. Commit changes
3. Update SESSION_STATE.md → **This creates uncommitted changes!**

**Right way:**
1. Make changes
2. Update SESSION_STATE.md
3. Commit everything together → **Clean working tree!**

### SESSION_STATE.md Update Timing

**Update SESSION_STATE.md:**
- ✅ AFTER all session work is complete
- ✅ BEFORE staging and committing
- ✅ With final, accurate session state

**Never update SESSION_STATE.md:**
- ❌ After committing (leaves uncommitted changes)
- ❌ During intermediate steps (use final state only)

### Checklist for Session Closure

- [ ] All work completed (archives, updates, logs created)
- [ ] SESSION_STATE.md updated with final state
- [ ] All changes staged (`git add .`)
- [ ] Commit created with descriptive message
- [ ] Working tree is clean (`git status` shows nothing to commit)
- [ ] Push to remote (optional, based on workflow)

### Quick Verification

After committing, always check:
```bash
git status
# Should show: "nothing to commit, working tree clean"
```

If you see modified files after commit, you updated SESSION_STATE.md too late!

### Recovery from Mistake

If you already committed and then updated SESSION_STATE.md:

```bash
# Amend the previous commit to include the update
git add globaldocs/SESSION_STATE.md
git commit --amend --no-edit

# Verify clean working tree
git status
```

---

## Multi-Repository Sessions

If working with multiple repositories (e.g., NORI + Skills):

1. Complete all work in ALL repositories
2. Update SESSION_STATE.md in NORI repository
3. Stage and commit NORI repository
4. Stage and commit other repositories
5. Verify all working trees are clean

---

## NORI-Specific Registry Updates

This workflow applies to ALL NORI registry and state files:

### Always Update BEFORE Committing:
- ✅ `SESSION_STATE.md` - Session closure state
- ✅ `PROJECT_INDEX.md` - Project registry updates (after archives/additions)
- ✅ `BIG_IDEAS.md` - Idea registry updates (after archives/additions)
- ✅ All log files created during session

### Example: Archiving Workflow
```bash
# 1. Archive project/idea (creates logs, moves files)
# 2. Update registry (PROJECT_INDEX.md or BIG_IDEAS.md)
# 3. Update SESSION_STATE.md with final state
# 4. Stage all: git add .
# 5. Commit everything together
# 6. Verify: git status → clean working tree
```

**Critical Rule:** NEVER commit without including final state files!

---

## Automation Consideration

For future automation (hooks, scripts):
- Ensure SESSION_STATE.md update happens in the pre-commit phase
- Or include it automatically in the commit staging
- Never update it in a post-commit hook

---

## Source Code Management

### NORI System Source Code (`src/` directory)

**Scope:** C# code in `src/NORI.Core/`, `src/NORI.CLI/`, etc.

**Workflow:**
1. Make source code changes
2. Build and test locally:
   ```bash
   cd /e/MyProjects/Nori/src/NORI.Core
   dotnet build
   dotnet test
   ```
3. Stage source files (NOT build artifacts):
   ```bash
   cd /e/MyProjects/Nori
   git add src/**/*.cs src/**/*.csproj src/**/*.sln
   # Verify build artifacts excluded:
   git status --ignored
   ```
4. Commit with descriptive message:
   ```bash
   git commit -m "Add project validation to NORI.Core

   Implemented:
   - ProjectValidator class
   - Schema validation logic
   - Unit tests for validation

   Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
   ```
5. Verify clean working tree

**Build Artifacts:** ALWAYS excluded via `.gitignore`:
- `bin/`
- `obj/`
- `.vs/`
- `*.user`

### Project-Level Source Code (`projects/<slug>/src/`)

**Scope:** Source code for individual NORI projects

**Workflow Varies by Project Type:**

**TypeScript/Node.js Projects:**
- Commit: `package.json`, `package-lock.json`, `tsconfig.json`, source files
- Exclude: `node_modules/`, `.next/`, `dist/`, `build/`
- Workspace file: COMMIT to git

**C# Projects:**
- Commit: `.sln`, `.csproj`, source files
- Exclude: `bin/`, `obj/`, `.vs/`, `*.user`
- Solution file: COMMIT to git

**Python Projects:**
- Commit: `requirements.txt`, source files
- Exclude: `__pycache__/`, `.pytest_cache/`, `venv/`

**Documentation Projects:**
- Commit: All documentation files
- No build artifacts

**Nested Git Repositories:**
- If project has nested `.git/` (like Certification-Center/WebSite-Overhaul):
  - Manage inner repo independently
  - NORI outer repo tracks project metadata only
  - Submodule reference committed in outer repo

### VS Solutions and Workspaces

**ALWAYS COMMIT:**
- `*.sln` (Visual Studio solution files)
- `*.csproj` (C# project files)
- `*.code-workspace` (VS Code workspace files)

**RATIONALE:**
- Solutions/workspaces are configuration, not artifacts
- Enable team members to open projects immediately
- Part of project structure documentation

### Archive Workflow for Source Code

When archiving a project with source code:

1. Archive INCLUDES source code and VS solutions:
   ```bash
   # Archive moves everything including src/
   mv projects/my-project projects/_archive/my-project/2026-02-15/
   ```

2. Verify nested git repos preserved:
   ```bash
   find projects/_archive/my-project/2026-02-15 -name ".git" -type d
   ```

3. Commit archive operation (solution files move with project)

4. Tag with project type:
   ```bash
   git tag -a "archive/my-project/2026-02-15" -m "Archive: MyProject (TypeScript)"
   ```

### .gitignore Strategy

**Root `.gitignore`:**
- Global exclusions for ALL projects
- Wildcard patterns: `**/bin/`, `**/node_modules/`, etc.
- Preserve nested repos: `!projects/*/src/**/.git/`

**`src/.gitignore` (NORI system code):**
- .NET-specific exclusions
- More aggressive (this is controlled code)

**Project-level `.gitignore` (in nested repos):**
- Managed by project's own git repo
- NORI doesn't interfere

---

## Governance Declaration

**This document establishes the UNIVERSAL GIT WORKFLOW STANDARD for:**

1. **NORI Project OS** - All session work and commits
2. **All NORI Projects** - Current (Certification-Center, KinderGuard, NORI-Project-OS) and future
3. **BIG_IDEAS.md Management** - Idea additions, promotions, archives
4. **PROJECT_INDEX.md Management** - Project registrations, state changes, archives
5. **Skills Development** - All skill updates and commits
6. **Global Standard** - Any git-managed work, any context, any session

**Enforcement:** This workflow is MANDATORY for all NORI operations.

**Rationale:** Ensures clean working trees, complete session state capture, and proper audit trails.

---

**Version:** 1.2.0 (Extended for Source Code)
**Last Updated:** 2026-02-15
**Status:** Active Reference - MANDATORY COMPLIANCE
