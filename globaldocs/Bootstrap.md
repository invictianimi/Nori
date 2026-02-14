# NORI Claude Code Bootstrap Protocol

This file defines how Claude Code must behave when working on NORI.

## Session Start Ritual (Mandatory)

Before executing any NORI-related command:

1. Read:
   - globaldocs/NORI_Implementation_Runbook.md
   - globaldocs/templates/prompts/PROJECT_SERVICE_PROMPT.md
   - globaldocs/registry/PROJECT_INDEX.md

2. Summarize:
   - Current registry state
   - Any structural inconsistencies
   - Current active projects

3. Confirm readiness before modifying files.

4. Read:
   - globaldocs/SESSION_STATE.md

5. Summarize:
   - Last session date
   - Active project
   - Pending next action
   - System health status

6. Ask the user:
   - Resume previous session?
   - Review last log?
   - Start new session?

7. If System Health is Warning or Critical:
   - Run /Projects validate before any structural change.
   - Require correction before proceeding.

---

## Execution Discipline

- Never delete files. Archive instead.
- Ask before overwriting existing files.
- Make minimal diffs.
- Log all actions.
- Pause after each major section.
- Do not batch unrelated structural changes.

---

## Integrity Enforcement

If structural inconsistency is detected:
- Report it.
- Do not auto-correct without approval.
- Log discrepancy if correction is approved.
- If uncertainty exists, ask for clarification before proceeding.

---

## End-of-Session Protocol (Mandatory)

Before concluding any NORI session:

1. Ensure all structural changes are logged.
2. Confirm registry consistency.
3. Update:
   - globaldocs/SESSION_STATE.md

4. SESSION_STATE.md must reflect:
   - Last Session Date
   - Active Project (if any)
   - Last Command Executed
   - Pending Next Action
   - System Health
   - Path to last log file

5. Confirm with user that session state is accurate.


