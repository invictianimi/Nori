# Project Lifecycle

This document defines the standard lifecycle phases for all NORI-managed projects.

**Version:** v0.2.0
**Last Updated:** 2026-02-17
**Authority:** Vit

---

## Lifecycle Phases

### 1. Spark

**Purpose:** Capture initial idea energy before it fades.

**Duration:** Minutes to hours

**Required Outputs:**
- Idea entry in BIG_IDEAS.md
- "Why it matters" statement
- First tiny step (<30m)

**Exit Criteria:** Idea captured in registry OR idea archived

---

### 2. Discovery

**Purpose:** Understand the problem space and validate the idea before investing in planning.

**Duration:** Days to 1-2 weeks

**Required Outputs:**
- Problem statement
- Desired outcome (1 sentence)
- Rough success metrics
- Known constraints
- Decision on whether to proceed to Planning

**Exit Criteria:** Sufficient clarity to plan OR decision to pause/archive

---

### 3. Planning

**Purpose:** Design the solution and create an executable plan.

**Duration:** Days to 1 week

**Required Outputs:**
- Solution approach documented
- Key decisions recorded in DECISIONS.md
- Major milestones identified
- Risks identified in RISKS.md
- Task breakdown (high-level)

**Exit Criteria:** Clear path to execution OR discovery of blocker requiring pivot

---

### 4. Build

**Purpose:** Execute the plan and create the solution.

**Duration:** Weeks to months (depends on scope)

**Required Outputs:**
- Working implementation (prototype or production-ready)
- Core functionality complete
- Technical debt documented
- Build/deployment process defined

**Exit Criteria:** Solution built to "working" state OR pivot required

---

### 5. Test

**Purpose:** Validate that the solution works and meets success criteria.

**Duration:** Days to weeks

**Required Outputs:**
- Test results documented
- Defects identified and prioritized
- Success metrics measured
- Decision on readiness for deployment

**Exit Criteria:** Solution validated OR critical issues require rebuild

---

### 6. Deploy

**Purpose:** Release the solution to production/real-world use.

**Duration:** Hours to days

**Required Outputs:**
- Deployment completed
- Deployment log/record
- Rollback plan documented
- Initial real-world feedback captured

**Exit Criteria:** Solution live and operational OR rollback executed

---

### 7. Ops & Iteration

**Purpose:** Maintain, improve, and evolve the solution over time.

**Duration:** Ongoing (indefinite)

**Required Outputs:**
- Regular status updates
- Issue/enhancement tracking
- Performance monitoring (if applicable)
- Iterative improvements logged

**Exit Criteria:** Project archived OR returned to earlier phase for major changes

---

## Phase Navigation

### Linear vs. Non-Linear

- Most projects follow the sequence above
- **Loops are normal:** Build → Test → Build (iteration)
- **Backwards movement is acceptable:** Planning → Discovery (new info)
- **Phase skipping:** Allowed with justification (see below)

### Phase Skip Criteria

**Rule:** All phase skips must be logged in DECISIONS.md with rationale.

| From | To | Skip Allowed When |
|---|---|---|
| Spark | Discovery | Idea is immediately actionable and outcome is clear |
| Discovery | Planning | Problem is already well-understood (repeat domain, existing template) |
| Discovery | Build | Cognitive Load = S and desired outcome is unambiguous |
| Planning | Build | Architecture is trivially obvious; risk identification can happen inline |
| Build | Deploy | No test phase needed (documentation-only projects, config changes) |
| Test | Deploy | Tests are embedded in Build and continuously validated |

**Conservative default:** Only skip phases for Cognitive Load = S projects. Medium and Large projects must pass through all phases.

**Never skip:** Logging a phase transition in project logs. Even skipped phases must be recorded.

---

## Decision Gates

Gate checks are required before advancing to the next phase. Log gate passage in project logs.

### Discovery → Planning
- [ ] Problem stated in one sentence
- [ ] Desired outcome defined (what does done look like?)
- [ ] Rough success metrics identified
- [ ] Known constraints captured
- [ ] Decision made: proceed, pause, or archive

### Planning → Build
- [ ] Solution approach documented in PROJECT.md or DECISIONS.md
- [ ] Key risks logged in RISKS.md
- [ ] Task breakdown exists (Upcoming Milestones in STATUS.md)
- [ ] Next Action is concrete and <30 minutes
- [ ] No unresolved blockers

### Build → Test
- [ ] Core functionality builds without errors
- [ ] Intended behavior can be demonstrated or observed
- [ ] No critical defects blocking testing
- [ ] Test approach defined

### Test → Deploy
- [ ] Defined success metrics pass (from Discovery)
- [ ] Known defects are documented and prioritized
- [ ] Deployment approach defined or N/A for personal projects

### Deploy → Ops & Iteration
- [ ] Solution is live/in use
- [ ] Initial feedback captured
- [ ] Ongoing maintenance approach defined

---

## Governance Triggers

The following events require explicit governance action before work continues.

| Trigger | Required Action |
|---|---|
| Registry schema field added or removed | Update schema in PROJECT_INDEX.md, update templates, version bump in VERSIONING.md |
| Template field added or removed | Update template files, update PROJECT_SERVICE_PROMPT.md, version bump |
| New command added to project service | Update PROJECT_SERVICE_PROMPT.md, update NORI_Implementation_Runbook.md |
| Risk materializes (RISKS.md) | Move risk to Materialized, log in DECISIONS.md, update SESSION_STATE.md health |
| System health goes to Critical | Halt structural changes, run `/project validate`, resolve before continuing |
| Project phase transitions | Update STATUS.md + PROJECT_INDEX.md + log in project logs |
| Session with uncommitted changes | Commit + push before closing (mandatory per BOOTSTRAP.md) |
| Breaking change to any NORI schema | MAJOR version bump, review all projects for compliance |
| C# domain model diverges from markdown schema | Halt Build work, reconcile, log decision, run `/project validate` |

---

## Lifecycle State vs. Phase

**Phase** = where you are in the build process
**State** = operational status of the project

States:
- `active` = currently being worked on
- `paused` = temporarily halted (but will resume)
- `archived` = complete or discontinued

A project can be in any phase and any state.

Example: A project in "Build" phase can be "paused" if you take a break.

---

## Governance

- **Lifecycle changes:** Updates to phase definitions require version increment
- **Logging:** Phase transitions should be logged in project logs
- **Flexibility:** This lifecycle is a guide, not a prison. Adapt with rationale.
- **Authority:** Amendments require approval from Vit (current governance authority)

---

## Version History

| Version | Date | Changes | Author |
|---|---|---|---|
| v0.1.0 | 2026-02-13 | Initial lifecycle definition | NORI Bootstrap |
| v0.2.0 | 2026-02-17 | Filled in Phase Skip Criteria, Decision Gates, and Governance Triggers based on real project experience | Vit |
