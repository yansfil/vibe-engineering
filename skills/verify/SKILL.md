---
name: verify
description: |
  Use before declaring a task complete, after code/content/config changes, or
  when the user asks to verify, QA, smoke test, validate, or inspect whether
  something really works. Inspect the changed scope, run the right checks,
  verify runtime behavior when needed, and report evidence without inventing
  results.
allowed-tools:
  - Bash
  - Read
  - Grep
  - Glob
  - Edit
  - AskUserQuestion
---

# verify

Use this skill when the work looks done but needs proof.

The job is not to celebrate completion. The job is to decide whether the change
can be accepted, based on evidence.

Use this as a separate pass after `implement` when the implementation agent
already ran its planned checks but the user wants additional confidence,
runtime QA, or an independent completion audit.

## What This Skill Does

`verify` answers four questions:

1. What changed?
2. What could have broken?
3. What did we actually check?
4. What risk remains?

Do not make broad product or implementation changes while using this skill. If
verification finds a small obvious bug, fix it only when the user asked you to
verify and finish the task end to end. If the fix changes scope, ask first.

## Verification Levels

Use the smallest level that covers the real risk. Move wider only when needed.

### Level 1. Static Checks

Use when the change could break syntax, types, lint rules, content parsing, or
the build.

Examples:

- `npm run lint`
- `npm run typecheck`
- `npm test`
- `npm run build`
- project-specific validators such as `verify:content`

### Level 2. Behavior Checks

Use when the change has expected behavior that can be tested or inspected
without relying only on human taste.

Examples:

- unit tests for pure logic
- integration tests for data loading or API behavior
- smoke scripts
- migration or seed verification
- checking generated output files

### Level 3. Runtime QA

Use when the result depends on the real app, browser, API, database, logs, or
external service configuration.

Examples:

- open the local or deployed route
- click the changed flow
- check visible text and state
- inspect console or network errors
- call the API endpoint
- verify database rows or counts
- capture screenshot, DOM, log, or command evidence

Use `chromux` for browser QA when it is available and appropriate.

## Workflow

1. Run `git status --short` and identify the changed files.
2. Read the relevant diff or files. Do not rely on memory.
3. State the intended behavior in one or two sentences.
4. List the main risks introduced by the change.
5. Choose Level 1, 2, and/or 3 checks that cover those risks.
6. Run the checks. Prefer focused checks first.
7. If a check fails, decide whether it is caused by this change, pre-existing,
   or unrelated.
8. If UI/runtime changed, inspect the real route or runtime target.
9. Report only evidence you actually collected.
10. Say what remains unchecked.

## Evidence Rules

- A command is evidence only if it actually ran.
- A browser check is evidence only if the route, state, and observed result are
  named.
- A database check is evidence only if the target environment and query/result
  are named.
- A screenshot is evidence only if the path or captured view is named.
- "Looks good" is not evidence by itself.
- Do not hide skipped checks. Explain why they were not run.

## Failure Handling

When a check fails:

- quote or summarize the important error line
- say whether it appears related to the current change
- if unrelated, name the file/command that proves it is outside scope
- if related and fixable in scope, fix and rerun the focused check
- if blocked, stop and report the blocker clearly

Do not keep rerunning broad checks when a narrower failure already explains the
problem.

## Output Format

```md
## Verdict

Pass | Partial | Fail | Blocked

## Checked

- ...

## Evidence

- Command:
- Result:
- Runtime:
- Result:

## Failed Or Blocked

- ...

## Not Checked

- ...

## Remaining Risk

- ...
```
