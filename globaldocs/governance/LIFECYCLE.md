# Project Lifecycle

This document defines the standard lifecycle phases for all NORI-managed projects.

**Version:** v0.1.0
**Last Updated:** 2026-02-13
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

_(To be defined based on project experience)_

Placeholder for conditions under which phases can be safely skipped.

Examples:
- Tiny projects (cognitive load = S) might skip Planning
- Well-understood problems might compress Discovery
- Proof-of-concept work might skip formal Testing

**Rule:** All phase skips must be logged in DECISIONS.md with rationale.

---

## Decision Gates

_(To be defined based on governance maturity)_

Placeholder for formal go/no-go decision points between phases.

Examples:
- Discovery → Planning: Is the problem well-defined?
- Build → Test: Is the solution stable enough to test?
- Test → Deploy: Do success criteria pass?

---

## Governance Triggers

_(To be defined based on risk management needs)_

Placeholder for conditions that require explicit governance review.

Examples:
- Budget exceeds threshold
- Timeline extends beyond estimate by X%
- Critical risk materializes
- Scope changes significantly

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
