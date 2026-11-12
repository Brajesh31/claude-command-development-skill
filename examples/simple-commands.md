# Simple Slash Command Examples

These examples demonstrate focused commands with a single responsibility. Confirm the supported frontmatter syntax in the installed Claude Code version.

## 1. Review a file

File: `.claude/commands/review-file.md`

```markdown
---
description: Review a source file for defects
argument-hint: [file-path]
---

Review @$1 for correctness, security, maintainability, and test coverage.

1. Confirm the file exists and belongs to the current project.
2. Read relevant surrounding code and tests.
3. Report only actionable findings with line references.
4. Separate confirmed defects from questions and suggestions.
5. Do not edit the file.
```

Example invocation: `/review-file src/auth/session.ts`

## 2. Summarize the current diff

File: `.claude/commands/summarize-diff.md`

```markdown
---
description: Summarize current working tree changes
allowed-tools: Read, Bash(git:*)
---

Inspect the working tree using git status and the available diff.

Summarize:
- files changed;
- behavior added, changed, or removed;
- tests added or modified;
- possible risks or missing verification.

Do not stage, commit, discard, or edit changes. Preserve untracked files and report when a diff cannot be inspected.
```

Example invocation: `/summarize-diff`

## 3. Add a regression test

File: `.claude/commands/add-regression-test.md`

```markdown
---
description: Add a focused regression test
argument-hint: [bug-description]
---

Investigate the reported bug: $ARGUMENTS

1. Find the affected implementation and nearby test conventions.
2. Identify the expected behavior and a reproducible failing case.
3. Add the smallest focused regression test.
4. Run that test and report the result.
5. Do not change production behavior unless explicitly asked to fix the bug.

Preserve unrelated modifications and explain any assumptions.
```

Example invocation: `/add-regression-test "empty email should be rejected"`

## 4. Validate configuration

File: `.claude/commands/check-config.md`

```markdown
---
description: Check project configuration for consistency
argument-hint: [config-path]
---

Inspect @$1 and the project files that define its schema or usage.

Check syntax, required fields, types, referenced paths, and consistency with the project. Do not print secret values. Do not modify the configuration.

Return a concise list of passed checks, failures, and recommended corrections.
```

Example invocation: `/check-config config/app.yml`

## Design notes

- Each example has a single job and a clear boundary.
- Arguments are named in the hint and used explicitly.
- Read-only examples state that they must not edit files.
- Commands that change project files describe their limited scope and verification.
- No command claims that a test or external action succeeded without executing it.
