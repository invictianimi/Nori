# NORI Multi-Workspace Setup Guide

**SCOPE:** Setting up and synchronizing NORI across multiple computers

**VERSION:** 1.0.0
**LAST UPDATED:** 2026-02-16
**STATUS:** Active Reference

---

## Table of Contents

1. [Overview](#overview)
2. [Prerequisites](#prerequisites)
3. [Initial Setup on Primary Computer](#initial-setup-on-primary-computer)
4. [Setup on Additional Computers](#setup-on-additional-computers)
5. [Testing Your Setup](#testing-your-setup)
6. [Daily Workflow](#daily-workflow)
7. [Conflict Resolution](#conflict-resolution)
8. [Troubleshooting](#troubleshooting)
9. [Best Practices](#best-practices)

---

## Overview

NORI is designed to work seamlessly across multiple computers using Git synchronization. This guide covers:

- Setting up NORI on new computers
- Testing synchronization between workspaces
- Handling conflicts when working from multiple locations
- Best practices for multi-computer workflows

**Key Principle:** The GitHub repository is the single source of truth. Always pull before starting work, always push when finished.

---

## Prerequisites

### Required on ALL Computers

**1. Git Installation**
```bash
# Verify git is installed
git --version
# Should show: git version 2.x.x or higher
```

**2. Git Configuration**
```bash
# Set your identity (same on all computers)
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Verify configuration
git config --global --list
```

**3. GitHub Access**
- GitHub account with access to `https://github.com/invictianimi/Nori.git`
- SSH key or HTTPS credentials configured
- Test access: `ssh -T git@github.com` (for SSH) or authenticate via browser (for HTTPS)

**4. Optional but Recommended**
- Claude Code CLI installed
- Text editor (VS Code, Vim, etc.)
- `.gitignore` understanding for your OS

---

## Initial Setup on Primary Computer

**NOTE:** If you already have NORI set up on your primary computer (as you do), skip to [Setup on Additional Computers](#setup-on-additional-computers).

### Step 1: Verify Existing Setup

```bash
# Navigate to your NORI directory
cd /e/MyProjects/Nori

# Verify git repository exists
git status
# Should show: "On branch master"

# Verify remote is configured
git remote -v
# Should show: origin https://github.com/invictianimi/Nori.git
```

### Step 2: Ensure Everything is Pushed

```bash
# Check for uncommitted changes
git status

# If there are uncommitted changes, commit them
git add .
git commit -m "Sync before multi-workspace setup

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"

# Push to GitHub
git push origin master

# Verify push succeeded
git log origin/master..HEAD
# Should show: nothing (no unpushed commits)
```

### Step 3: Document Current State

```bash
# Record the latest commit ID for verification
git log -1 --oneline > ~/nori_sync_reference.txt
cat ~/nori_sync_reference.txt
# Save this commit ID - you'll verify it matches on other computers
```

---

## Setup on Additional Computers

### Computer 2, 3, 4, etc.

**Step 1: Choose Installation Location**

```bash
# Decide where to install NORI
# Common choices:
# - Windows: E:\MyProjects or C:\Users\YourName\Documents\Projects
# - macOS/Linux: ~/Projects or ~/Documents/Projects

# Create the parent directory if it doesn't exist
mkdir -p /path/to/your/workspace
cd /path/to/your/workspace
```

**Step 2: Clone the Repository**

```bash
# Clone NORI from GitHub
git clone https://github.com/invictianimi/Nori.git

# Navigate into the repository
cd Nori

# Verify the clone succeeded
ls -la
# Should see: globaldocs/, projects/, src/, .git/, etc.
```

**Step 3: Verify Remote Configuration**

```bash
# Check remote is properly configured
git remote -v
# Should show:
# origin  https://github.com/invictianimi/Nori.git (fetch)
# origin  https://github.com/invictianimi/Nori.git (push)

# Verify you're on the master branch
git branch
# Should show: * master
```

**Step 4: Verify Sync with Primary Computer**

```bash
# Check the latest commit
git log -1 --oneline
# This commit ID should MATCH the one from your primary computer

# Check repository status
git status
# Should show: "On branch master"
# Should show: "Your branch is up to date with 'origin/master'"
# Should show: "nothing to commit, working tree clean"
```

**Step 5: Test Read Access**

```bash
# Verify you can read key NORI files
ls globaldocs/
ls projects/
cat globaldocs/SESSION_STATE.md

# Verify nested repos (if any)
git submodule status
```

**Step 6: Configure Computer-Specific Settings (Optional)**

```bash
# If you have computer-specific paths or settings
# Create a local git config (NOT committed to repo)
git config --local user.name "Your Name (Laptop)"  # Optional identifier
git config --local core.autocrlf true  # Windows line endings if needed
```

---

## Testing Your Setup

### Test 1: Bidirectional Sync Test

**Objective:** Verify changes made on Computer A sync to Computer B.

#### On Computer A (Primary):

```bash
# 1. Navigate to NORI
cd /path/to/Nori

# 2. Create a test file
echo "# Multi-Workspace Sync Test

Created on: $(date)
Computer: Computer-A
Test: Bidirectional sync
" > globaldocs/TEST_SYNC.md

# 3. Commit the test file
git add globaldocs/TEST_SYNC.md
git commit -m "Test: Multi-workspace sync from Computer A

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"

# 4. Push to GitHub
git push origin master

# 5. Record the commit ID
git log -1 --oneline
# Example output: a1b2c3d Test: Multi-workspace sync from Computer A
```

#### On Computer B (Secondary):

```bash
# 1. Navigate to NORI
cd /path/to/Nori

# 2. Pull changes from GitHub
git pull origin master

# 3. Verify the test file exists
cat globaldocs/TEST_SYNC.md
# Should show the file created on Computer A

# 4. Verify commit ID matches
git log -1 --oneline
# Should show: a1b2c3d Test: Multi-workspace sync from Computer A

# 5. Add to the test file (append)
echo "
Updated on: $(date)
Computer: Computer-B
Test: Confirmed bidirectional sync works!
" >> globaldocs/TEST_SYNC.md

# 6. Commit the update
git add globaldocs/TEST_SYNC.md
git commit -m "Test: Multi-workspace sync from Computer B

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"

# 7. Push to GitHub
git push origin master
```

#### Back on Computer A:

```bash
# 1. Pull changes
git pull origin master

# 2. Verify Computer B's updates
cat globaldocs/TEST_SYNC.md
# Should show BOTH Computer A and Computer B entries

# ✅ SUCCESS: If you see both entries, sync is working!

# 3. Clean up test file
git rm globaldocs/TEST_SYNC.md
git commit -m "Test: Remove sync test file

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
git push origin master
```

#### Back on Computer B:

```bash
# Pull the cleanup
git pull origin master

# Verify test file is gone
ls globaldocs/TEST_SYNC.md
# Should show: No such file or directory

# ✅ COMPLETE: Multi-workspace sync test passed!
```

---

### Test 2: Session State Sync Test

**Objective:** Verify SESSION_STATE.md syncs correctly between computers.

#### On Computer A:

```bash
cd /path/to/Nori

# Read current SESSION_STATE
cat globaldocs/SESSION_STATE.md

# Update SESSION_STATE.md with a test session
# (In real workflow, you'd use Claude Code to do this)
# For testing, manually edit or use this:
cat >> globaldocs/SESSION_STATE.md << 'EOF'

---
## TEST SESSION (Computer A)
- Date: $(date)
- Action: Testing multi-workspace sync
- Status: In Progress
EOF

# Commit and push
git add globaldocs/SESSION_STATE.md
git commit -m "Test: Session state from Computer A

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
git push origin master
```

#### On Computer B:

```bash
cd /path/to/Nori

# Pull updates
git pull origin master

# Verify SESSION_STATE includes Computer A's test
cat globaldocs/SESSION_STATE.md | tail -10
# Should show the TEST SESSION entry

# ✅ SUCCESS: Session state syncs correctly!
```

---

### Test 3: Project Registry Sync Test

**Objective:** Verify PROJECT_INDEX.md changes sync correctly.

#### On Computer A:

```bash
cd /path/to/Nori

# View current project registry
cat globaldocs/registry/PROJECT_INDEX.md | head -20

# Note the current project count
grep "^###" globaldocs/registry/PROJECT_INDEX.md | wc -l
# Record this number

# Create a test project entry (simulated)
# In real workflow, you'd use /project new
# For testing, add a comment at the end:
echo "
<!-- Multi-workspace sync test performed on $(date) from Computer A -->
" >> globaldocs/registry/PROJECT_INDEX.md

# Commit and push
git add globaldocs/registry/PROJECT_INDEX.md
git commit -m "Test: Registry sync from Computer A

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
git push origin master
```

#### On Computer B:

```bash
cd /path/to/Nori

# Pull updates
git pull origin master

# Verify the test comment exists
tail -5 globaldocs/registry/PROJECT_INDEX.md
# Should show the comment from Computer A

# ✅ SUCCESS: Project registry syncs correctly!

# Clean up test comment
sed -i '/Multi-workspace sync test/d' globaldocs/registry/PROJECT_INDEX.md
git add globaldocs/registry/PROJECT_INDEX.md
git commit -m "Test: Clean up registry sync test

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
git push origin master
```

---

### Test 4: Conflict Resolution Test

**Objective:** Practice resolving merge conflicts (intentionally created).

#### Setup Conflict (On Computer A):

```bash
cd /path/to/Nori

# Create a test file
echo "Line 1: Original
Line 2: Original
Line 3: Original" > globaldocs/TEST_CONFLICT.md

git add globaldocs/TEST_CONFLICT.md
git commit -m "Test: Create conflict test file

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
git push origin master
```

#### On Computer B:

```bash
cd /path/to/Nori

# Pull the test file
git pull origin master

# Modify Line 2 (DO NOT PUSH YET)
echo "Line 1: Original
Line 2: Modified on Computer B
Line 3: Original" > globaldocs/TEST_CONFLICT.md

git add globaldocs/TEST_CONFLICT.md
git commit -m "Test: Modify on Computer B (will conflict)

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"

# DON'T PUSH YET - wait for Computer A to create conflict
```

#### Back on Computer A (Create Conflict):

```bash
cd /path/to/Nori

# Modify Line 2 differently
echo "Line 1: Original
Line 2: Modified on Computer A
Line 3: Original" > globaldocs/TEST_CONFLICT.md

git add globaldocs/TEST_CONFLICT.md
git commit -m "Test: Modify on Computer A (will conflict)

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
git push origin master
```

#### Back on Computer B (Resolve Conflict):

```bash
cd /path/to/Nori

# Try to push (this will fail)
git push origin master
# Error: Updates were rejected (remote has changes)

# Pull (this will create a conflict)
git pull origin master
# CONFLICT in globaldocs/TEST_CONFLICT.md

# View the conflict
cat globaldocs/TEST_CONFLICT.md
# Should show:
# Line 1: Original
# <<<<<<< HEAD
# Line 2: Modified on Computer B
# =======
# Line 2: Modified on Computer A
# >>>>>>> [commit-id]
# Line 3: Original

# Resolve by editing the file
echo "Line 1: Original
Line 2: Merged from both computers
Line 3: Original" > globaldocs/TEST_CONFLICT.md

# Mark as resolved
git add globaldocs/TEST_CONFLICT.md

# Complete the merge
git commit -m "Test: Resolve conflict between Computer A and B

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"

# Push the resolution
git push origin master

# ✅ SUCCESS: Conflict resolved!
```

#### Cleanup (On Either Computer):

```bash
git rm globaldocs/TEST_CONFLICT.md
git commit -m "Test: Remove conflict test file

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
git push origin master
```

---

## Daily Workflow

### Starting Work on Any Computer

```bash
# 1. Navigate to NORI
cd /path/to/Nori

# 2. Check current status
git status
# Should show clean working tree

# 3. Pull latest changes from ALL computers
git pull origin master

# 4. Verify sync
git log -1 --oneline
# Review the latest commit to know what changed

# 5. Start your work
# Use Claude Code, edit files, run /project commands, etc.
```

### During Work

```bash
# Periodically check if you have uncommitted changes
git status

# Commit frequently (every major change)
git add .
git commit -m "Description of changes

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"

# Push frequently (especially if switching computers soon)
git push origin master
```

### Ending Work on Any Computer

**CRITICAL:** Follow [NORI_GIT_WORKFLOW.md](NORI_GIT_WORKFLOW.md) exactly:

```bash
# 1. Complete all work (logs, registry updates, etc.)

# 2. Update SESSION_STATE.md LAST (before commit)
# Edit globaldocs/SESSION_STATE.md with final session state

# 3. Stage ALL changes
git add .

# 4. Commit everything together
git commit -m "Session: [Brief description]

Changes:
- [List major changes]
- SESSION_STATE.md updated with session closure

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"

# 5. Push to GitHub (MANDATORY for multi-workspace)
git push origin master

# 6. Verify clean state
git status
# Should show: "nothing to commit, working tree clean"

# 7. Verify push succeeded
git log origin/master..HEAD
# Should show: nothing (no unpushed commits)
```

---

## Conflict Resolution

### Types of Conflicts

**1. Fast-Forward Conflicts (Most Common)**

Occurs when you forgot to pull before starting work.

**Symptoms:**
```bash
git push origin master
# Error: Updates were rejected because remote contains work
```

**Solution:**
```bash
# Pull with rebase (preserves linear history)
git pull --rebase origin master

# If no conflicts, push
git push origin master

# If conflicts occur, see "Merge Conflicts" below
```

---

**2. Merge Conflicts**

Occurs when the same file was edited on multiple computers.

**Symptoms:**
```bash
git pull origin master
# CONFLICT (content): Merge conflict in [file]
# Automatic merge failed; fix conflicts and commit
```

**Solution:**
```bash
# 1. View conflicted files
git status
# Files with conflicts are marked "both modified"

# 2. Open each conflicted file
# Look for conflict markers:
# <<<<<<< HEAD
# Your changes
# =======
# Changes from remote
# >>>>>>> commit-id

# 3. Edit the file to resolve
# Remove conflict markers
# Keep the correct version or merge both

# 4. Mark as resolved
git add [resolved-file]

# 5. Complete the merge
git commit -m "Merge: Resolve conflicts from [description]

Conflicts resolved in:
- [file1]
- [file2]

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"

# 6. Push the resolution
git push origin master
```

---

**3. SESSION_STATE.md Conflicts (Special Case)**

**Problem:** SESSION_STATE.md is frequently edited, high conflict risk.

**Prevention Strategy:**

Option A - **Append-Only Approach:**
```bash
# Instead of editing SESSION_STATE.md, append to it
echo "
## Session: $(date)
- Computer: [identifier]
- Changes: [description]
" >> globaldocs/SESSION_STATE.md
```

Option B - **Computer-Specific State Files:**
```bash
# Create separate state files per computer
# globaldocs/SESSION_STATE_ComputerA.md
# globaldocs/SESSION_STATE_ComputerB.md
# Keep globaldocs/SESSION_STATE.md as aggregate
```

Option C - **Always Pull Before Updating:**
```bash
# Before updating SESSION_STATE.md at end of session:
git pull origin master  # Get latest state
# Then edit SESSION_STATE.md
# Then commit and push
```

**Recommended:** Use Option C with the standard workflow.

---

**4. Registry Conflicts (PROJECT_INDEX.md, BIG_IDEAS.md)**

**Problem:** Multiple computers adding/archiving projects simultaneously.

**Prevention:**
- Use `/project` commands (handles registry atomically)
- Pull before creating new projects
- Push immediately after structural changes

**If Conflict Occurs:**
```bash
# 1. Pull to see the conflict
git pull origin master

# 2. Open the registry file
# Registries are structured markdown - conflicts are usually additive

# 3. Merge both changes manually
# Keep both new projects/ideas
# Ensure proper formatting

# 4. Resolve
git add globaldocs/registry/PROJECT_INDEX.md
git commit -m "Merge: Resolve registry conflict

Both changes preserved:
- [Change from Computer A]
- [Change from Computer B]

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
git push origin master
```

---

### Conflict Avoidance Best Practices

1. **Always pull before starting work**
   ```bash
   git pull origin master
   ```

2. **Push immediately after structural changes**
   - After creating a project: push
   - After archiving something: push
   - After major registry updates: push

3. **Communicate across computers**
   - Use SESSION_STATE.md to indicate what you're working on
   - Check SESSION_STATE.md before starting work
   - Don't work on the same project from multiple computers simultaneously

4. **Use atomic commits**
   - Complete one logical change
   - Commit
   - Push
   - Then start the next change

5. **Keep sessions short**
   - Shorter sessions = fewer conflicts
   - Push every 30-60 minutes if actively working

---

## Troubleshooting

### Problem 1: "diverged" Error

**Symptom:**
```bash
git status
# Your branch and 'origin/master' have diverged
```

**Cause:** Commits exist both locally and remotely that aren't shared.

**Solution:**
```bash
# See what's different
git log origin/master..HEAD     # Your commits not on remote
git log HEAD..origin/master     # Remote commits not local

# If you want to keep both (merge):
git pull origin master
# Resolve any conflicts
git push origin master

# If remote is correct (discard local):
git fetch origin
git reset --hard origin/master

# If local is correct (force push - DANGEROUS):
# Only if you're SURE remote is wrong
git push --force origin master
```

---

### Problem 2: Authentication Failures

**Symptom:**
```bash
git push origin master
# Error: Authentication failed
```

**Solutions:**

**For HTTPS:**
```bash
# Re-authenticate with GitHub
git credential-cache exit
git push origin master
# Enter credentials when prompted
```

**For SSH:**
```bash
# Test SSH connection
ssh -T git@github.com

# If fails, regenerate SSH key
ssh-keygen -t ed25519 -C "your.email@example.com"
# Add to GitHub: Settings > SSH Keys

# Update remote to use SSH
git remote set-url origin git@github.com:invictianimi/Nori.git
```

---

### Problem 3: Missing Files After Clone

**Symptom:**
Files exist on one computer but not another after cloning.

**Cause:** Files might be in `.gitignore` or are submodules.

**Solution:**
```bash
# Check .gitignore
cat .gitignore
# See if your files are listed

# Check for submodules
git submodule status
git submodule update --init --recursive

# Check if files exist in remote
git ls-tree -r master --name-only | grep [filename]
```

---

### Problem 4: Large Files Won't Push

**Symptom:**
```bash
git push origin master
# Error: file too large
```

**Cause:** Git has limits on file size. Build artifacts might not be ignored.

**Solution:**
```bash
# Remove large file from staging
git reset [large-file]

# Add to .gitignore
echo "[large-file-pattern]" >> .gitignore

# If already committed, remove from history (advanced)
git filter-branch --tree-filter 'rm -f [large-file]' HEAD
```

---

### Problem 5: Wrong Computer Identity in Commits

**Symptom:**
Commits show wrong author name or email.

**Solution:**
```bash
# Check current config
git config user.name
git config user.email

# Fix for this computer
git config --local user.name "Correct Name"
git config --local user.email "correct.email@example.com"

# Future commits will use correct identity
# Past commits can't be changed without rewriting history
```

---

### Problem 6: Accidental Force Push

**Symptom:**
You ran `git push --force` and lost remote commits.

**Solution:**
```bash
# GitHub keeps reflog for ~90 days
# View reflog
git reflog

# Find the commit before force push
git log --all --oneline

# Reset to that commit
git reset --hard [commit-id]

# Push to restore
git push origin master

# If you don't have the commit locally, contact GitHub support
```

---

## Best Practices

### 1. Establish a Primary Computer

**Recommendation:** Designate one computer as "primary" for certain tasks.

**Example:**
- **Primary (Desktop):** Major development, builds, testing
- **Secondary (Laptop):** Documentation, planning, light edits

**Why:** Reduces likelihood of complex conflicts.

---

### 2. Use Computer Identifiers in Commits

```bash
# Add computer identifier to commits
git commit -m "Session: Update project status [Laptop]

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
```

**Why:** Makes it clear which computer made which changes when reviewing history.

---

### 3. Session State as Communication Channel

**Use SESSION_STATE.md to communicate:**

```markdown
## Last Session
- Date: 2026-02-16
- Computer: Desktop
- Status: In progress - refactoring authentication
- **DO NOT EDIT:** auth files until desktop session completes
- Next Action: Finish auth refactor, then push
```

**Why:** Prevents conflicts by signaling what's in progress.

---

### 4. Pull More Than You Think

```bash
# Pull at start of day
git pull origin master

# Pull before each major task
git pull origin master

# Pull before ending session
git pull origin master

# Push immediately after pulling and committing
git push origin master
```

**Why:** Staying in sync prevents conflicts.

---

### 5. Commit Often, Push Often

**Anti-pattern:**
```bash
# Work all day
# Make 50 changes
# Commit once at end of day
# High conflict risk
```

**Best practice:**
```bash
# Make logical change
git add .
git commit -m "Description"
git push origin master

# Repeat for each logical change
```

**Why:** Smaller, frequent syncs reduce conflict complexity.

---

### 6. Use Branches for Experiments

```bash
# If you want to try something risky on one computer
git checkout -b experiment-feature
# Make changes
git commit -m "Experimental: [description]"
git push origin experiment-feature

# On other computer, you can choose to:
# - Ignore the branch (stay on master)
# - Pull and review: git checkout experiment-feature

# When ready, merge to master
git checkout master
git merge experiment-feature
git push origin master
```

**Why:** Keeps master stable across all computers.

---

### 7. Regular Integrity Checks

```bash
# Weekly or after major changes
cd /path/to/Nori

# Verify all computers have same commit
git log -1 --oneline
# Should match on ALL computers

# Run NORI validation
/project validate
# Should pass on ALL computers

# Check for uncommitted changes
git status
# Should be clean on ALL computers (when not actively working)
```

**Why:** Catches sync issues early.

---

### 8. Backup Strategy

Even with Git sync, maintain backups:

```bash
# Automated backup (cron/scheduled task)
# Create a tarball of entire NORI directory weekly
tar -czf ~/backups/nori-backup-$(date +%Y%m%d).tar.gz /path/to/Nori

# Or use GitHub as backup
# GitHub maintains repository history
# If local computers fail, clone fresh from GitHub
```

**Why:** Defense against git mistakes or data loss.

---

### 9. Network-Specific Configuration

```bash
# If on a slow network, reduce push frequency
# Commit often, push at end of session

# If on fast network, push after every commit
git commit -m "..." && git push origin master

# Use git config for network-specific settings
git config --local push.default simple  # Only push current branch
```

---

### 10. Document Your Workflow

Create a personal workflow file:

```bash
# In your NORI directory
cat > globaldocs/MY_WORKFLOW.md << 'EOF'
# My Personal NORI Workflow

## Computers
- Desktop (Primary): Heavy development, builds
- Laptop (Secondary): Documentation, planning

## Daily Routine
1. Morning: Pull on all computers
2. Choose computer based on task
3. Push after every logical change
4. Evening: Ensure all computers synced

## Conflict Strategy
- If conflict occurs, desktop version wins unless specified
- Always verify with git log before force actions

EOF

git add globaldocs/MY_WORKFLOW.md
git commit -m "Add personal workflow documentation"
git push origin master
```

---

## Quick Reference Card

### Daily Commands

```bash
# Start of work
cd /path/to/Nori && git pull origin master

# During work (repeat often)
git add . && git commit -m "Description" && git push origin master

# End of work
# (Update SESSION_STATE.md first)
git add . && git commit -m "Session: [description]" && git push origin master

# Check sync status
git status && git log -1 --oneline
```

---

### Emergency Commands

```bash
# Abandon local changes (reset to remote)
git fetch origin && git reset --hard origin/master

# Undo last commit (keep changes)
git reset --soft HEAD~1

# See what changed between computers
git diff origin/master

# Force pull (discard all local changes)
git fetch origin && git reset --hard origin/master
```

---

## Support and Resources

### NORI Documentation

- [NORI_GIT_WORKFLOW.md](NORI_GIT_WORKFLOW.md) - Git workflow standard
- [BOOTSTRAP.md](BOOTSTRAP.md) - Session start protocol with sync checks
- [NORI_Implementation_Runbook.md](NORI_Implementation_Runbook.md) - Complete NORI guide

### Git Resources

- [Git Documentation](https://git-scm.com/doc)
- [GitHub Guides](https://guides.github.com/)
- [Resolving Merge Conflicts](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts)

### Testing Checklist

After setup, verify:

- [ ] Can clone repository on new computer
- [ ] Can pull changes from other computers
- [ ] Can push changes to GitHub
- [ ] Can resolve basic merge conflicts
- [ ] SESSION_STATE.md syncs correctly
- [ ] Project registry syncs correctly
- [ ] All computers show same `git log -1 --oneline`
- [ ] No uncommitted changes after proper workflow

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | 2026-02-16 | Initial release |

---

**GOVERNANCE:** This document is part of NORI Project OS global documentation. Updates must maintain compatibility with [NORI_GIT_WORKFLOW.md](NORI_GIT_WORKFLOW.md) and [BOOTSTRAP.md](BOOTSTRAP.md).
