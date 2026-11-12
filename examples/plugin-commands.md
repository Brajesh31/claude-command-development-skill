# Plugin Command Examples

These examples show how commands can use plugin-local resources. Adapt frontmatter fields and tool permissions to the Claude Code version installed in the target environment.

## 1. Run a plugin script

File: `commands/check-config.md`

```markdown
---
description: Validate the plugin configuration
allowed-tools: Read, Bash(node:*)
---

Inspect the plugin configuration.

1. Locate the configuration file under ${CLAUDE_PLUGIN_ROOT}.
2. Run the plugin's validation script with the supplied configuration path.
3. Read the validation output.
4. Report errors with file and field references.
5. Do not modify configuration unless the user asks for a fix.
```

Keep the executable invocation narrow. Validate user-supplied paths before passing them to a shell command.

## 2. Load a plugin template

File: `commands/create-release-notes.md`

```markdown
---
description: Draft release notes from verified changes
argument-hint: [version]
---

Read the release-note template from the plugin's templates directory.

Inspect the repository changes for the requested release. Draft release notes for version $1 using verified changes only. Do not publish or tag a release.

Return the draft and list any uncertain items separately.
```

A template is useful when several commands must produce the same output structure. Keep the template focused on format rather than duplicating the workflow.

## 3. Coordinate with a specialist agent

File: `commands/security-review.md`

```markdown
---
description: Review a target for security weaknesses
argument-hint: [path]
---

Review @$1 for security issues.

First inspect the target and its callers. Delegate a focused review to the available security specialist when that agent exists in the active environment. Ask for evidence, affected code paths, severity, and a remediation recommendation.

Verify every reported finding before presenting it. Do not modify files, create commits, or claim that a scan was run unless it actually ran.
```

Mention only agents that are installed and available. Do not assume a named agent exists merely because a plugin command refers to it.

## 4. Combine static checks and human-readable reporting

A multi-stage plugin command may:
1. Validate required files and executables.
2. Run a deterministic checker.
3. Read its output.
4. Explain failed checks in context.
5. Suggest a correction without silently applying it.

Make each stage observable. Stop when a failed prerequisite makes later results unreliable.

## Portability checklist

- Use the plugin root variable rather than hard-coded installation paths.
- Confirm referenced scripts and templates exist.
- Declare only the tool permissions the command needs.
- Quote shell arguments and validate paths.
- Keep user data and credentials out of logs.
- Separate drafting from publishing, deployment, and other external actions.
