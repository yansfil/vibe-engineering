---
name: implement
description: |
  Use when the user asks Claude Code to execute an approved PRD or scoped task.
  Read the requirements, create a live checklist, implement the smallest safe
  changes, and keep acceptance criteria and verification evidence tracked.
allowed-tools:
  - Bash
  - Read
  - Grep
  - Glob
  - Write
  - Edit
  - Task
  - TodoWrite
  - AskUserQuestion
---

# implement

Use this skill to implement an approved PRD or a clearly scoped task end to end.

This is the execution counterpart to `prd`.

`implement` includes the verification promised by the PRD. A separate `verify`
skill can still be used after this skill finishes when the user wants an
independent completion check, extra QA, or a second pass over runtime behavior.

## Readiness Check

Before editing code:

1. Read the PRD, task description, or linked spec.
2. Identify scope, non-goals, requirements, acceptance criteria, and
   verification.
3. Check `git status --short`.
4. Read the actual files likely to be touched.
5. Stop and ask if required pre-work, credentials, product decisions, destructive
   data changes, or structural approval are missing.

## Live Checklist

Create a working checklist from the source document.

Track:

- requirements
- acceptance criteria
- implementation tasks
- verification commands
- browser or runtime QA scenarios
- human checks

Do not mark a task complete until its acceptance criteria have evidence or a
concrete blocker.

## Implementation Loop

For each task:

1. Re-read the relevant files.
2. Make the smallest change that satisfies the mapped requirement.
3. Avoid unrelated refactors.
4. Preserve user-owned worktree changes.
5. Run the smallest useful check after meaningful edits.
6. Record evidence as you go.

If a new task is needed, add it only when it maps to an approved requirement or
is pure verification/release hygiene. Ask before adding new product scope or
materially changing the approved structure.

## Verification Loop

Run the verification promised by the PRD or task.

This verification is part of implementation, not a separate review phase. Use it
to decide whether each acceptance criterion has enough evidence to be marked
complete.

Use three levels when relevant:

- Level 1: lint, typecheck, build, unit tests, content validation, or static
  checks.
- Level 2: automated behavior tests for requirements.
- Level 3: real runtime QA with browser, API, DB, logs, screenshots, DOM, or
  network evidence.

Use `chromux` for browser QA when available and appropriate.

Do not claim completion when verification failed, was skipped, or used a weaker
target than requested. Report the concrete gap.

## Final Report

```md
## Status

Done | Partially Done | Blocked

## Changed

- ...

## Acceptance Criteria

- AC1: Met | Not Met | Blocked - evidence

## Verification

- Command or scenario:
- Result:

## Human Check

- ...

## Risks

- ...
```
