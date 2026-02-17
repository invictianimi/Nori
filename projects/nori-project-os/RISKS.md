# Risks: [Project Name]

This log identifies and tracks risks throughout the project lifecycle.

**Purpose:** Proactive risk awareness and mitigation planning.

---

## Active Risks

<!-- Template for new risks:

### [Risk Title]

- **Risk:** [Description of the risk]
- **Likelihood:** [L (Low) / M (Medium) / H (High)]
- **Impact:** [L (Low) / M (Medium) / H (High)]
- **Priority:** [Calculated: likelihood × impact → L/M/H]
- **Mitigation:** [What can be done to reduce likelihood or impact]
- **Trigger:** [What event or condition would indicate this risk is materializing]
- **Owner:** [Who is responsible for monitoring/mitigating this risk]
- **Status:** [Monitoring / Mitigating / Materialized / Resolved]
- **Last Reviewed:** [YYYY-MM-DD]

---

-->

### Over-Engineering the C# Layer

- **Risk:** Building a complex framework in NORI.Core when the markdown + AI model is sufficient for current needs. Temptation to abstract too early before real usage patterns are known.
- **Likelihood:** M
- **Impact:** H
- **Priority:** H
- **Mitigation:** Start with the minimum viable implementation — read-only registry access first. No abstractions without two concrete use cases. Review scope at each milestone.
- **Trigger:** Any NORI.Core class exceeds ~100 lines or has more than 2 layers of abstraction before first CLI command ships.
- **Owner:** Vit
- **Status:** Monitoring
- **Last Reviewed:** 2026-02-17

---

### Documentation Drift (C# ↔ Markdown Schema)

- **Risk:** NORI.Core domain model diverges from the markdown schema defined in governance docs. C# types may add/change fields that aren't reflected in PROJECT_INDEX.md schema or template files.
- **Likelihood:** M
- **Impact:** H
- **Priority:** H
- **Mitigation:** Every C# domain type change must be cross-checked against the markdown schema. Include schema alignment as a checklist item in any Build session. Run /project validate after structural changes.
- **Trigger:** A C# property exists that has no corresponding field in the markdown registry or vice versa.
- **Owner:** Vit
- **Status:** Monitoring
- **Last Reviewed:** 2026-02-17

---

### Scope Creep into NORI.CLI Too Early

- **Risk:** Starting CLI development before NORI.Core is stable. CLI work introduces UI/UX concerns that distract from core library correctness.
- **Likelihood:** M
- **Impact:** M
- **Priority:** M
- **Mitigation:** Enforce milestone gate — NORI.CLI work does not start until ProjectRegistry reader and ValidationEngine have passing unit tests.
- **Trigger:** Any NORI.CLI code is written before first NORI.Core tests pass.
- **Owner:** Vit
- **Status:** Monitoring
- **Last Reviewed:** 2026-02-17

---

### Windows Path Coupling

- **Risk:** NORI.Core hardcodes or assumes Windows-style paths (backslash, drive letters), making it brittle if ever used on another platform or if root path changes.
- **Likelihood:** L
- **Impact:** M
- **Priority:** L
- **Mitigation:** Use `Path.Combine()` and `Path.GetFullPath()` throughout. Accept root path as a constructor/config parameter — never hardcode `E:\MyProjects\Nori`.
- **Trigger:** Any hardcoded path string in NORI.Core source code.
- **Owner:** Vit
- **Status:** Monitoring
- **Last Reviewed:** 2026-02-17

---

---

## Materialized Risks

[Risks that have actually occurred and their outcomes]

_None_

---

## Resolved Risks

[Risks that have been fully mitigated or are no longer relevant]

_None_

---

## Risk Matrix

| Risk | Likelihood | Impact | Priority | Status |
|---|---|---|---|---|
| Over-Engineering the C# Layer | M | H | H | Monitoring |
| Documentation Drift (C# ↔ Markdown Schema) | M | H | H | Monitoring |
| Scope Creep into NORI.CLI Too Early | M | M | M | Monitoring |
| Windows Path Coupling | L | M | L | Monitoring |

---

## Risk Categories

Common risk types:

- **Technical:** Technology limitations, complexity, technical debt
- **Resource:** Time, budget, people availability
- **Dependency:** External dependencies, third-party services
- **Scope:** Scope creep, unclear requirements
- **Quality:** Quality issues, testing gaps
- **Knowledge:** Skill gaps, learning curve
- **External:** Market changes, regulatory changes, competitive threats

---

## Risk Review Process

Risks should be reviewed:
- At phase transitions
- When new information emerges
- Monthly for long-running projects
- When a trigger event occurs

**Review Process:**
1. Re-assess likelihood and impact
2. Update mitigation status
3. Move to appropriate section (Active/Materialized/Resolved)
4. Log review in project logs

---

## Risk Escalation

**High Priority Risks (H/H or H/M):**
- Must have active mitigation plan
- Reviewed weekly
- Escalated to decision log if requiring strategic changes

**Medium Priority Risks (M/M or H/L or L/H):**
- Monitored regularly
- Mitigation plan recommended

**Low Priority Risks (L/L or L/M or M/L):**
- Logged for awareness
- Revisited at phase transitions

---

## Governance

- **Risk Logging:** All identified risks should be logged
- **Regular Review:** Risks must be reviewed at phase transitions
- **Mitigation Tracking:** Track mitigation actions in STATUS.md or DECISIONS.md
- **Learning:** When risks materialize, capture lessons in DECISIONS.md
- **No Risk Deletion:** Move risks between sections; don't delete them

---

## Notes

Risk management is about awareness, not prediction.

It's OK to have risks. It's not OK to be unaware of them.
