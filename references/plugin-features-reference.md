# Plugin Command Features Reference

This document describes common patterns for commands that are distributed as part of a Claude Code plugin. Verify exact syntax against the installed Claude Code version.

## Plugin root

Plugin commands can use `${CLAUDE_PLUGIN_ROOT}` to refer to the plugin's installation directory. Use it for stable plugin-local resources instead of assuming a fixed absolute path.

Example:

```markdown
---
description: Run the plugin's report generator
allowed-tools: Bash(node:*)
---

Run the report generator from the plugin directory. Inspect its output and summarize any validation failures.
```

When constructing an actual shell invocation, quote paths and arguments. Check that the target script exists before running it.

## Inline shell context

Some command formats support shell expansion that inserts command output into the prompt. Use it to gather limited context such as:
- current branch name;
- changed file names;
- package version;
- the result of a fast, read-only check.

Keep shell snippets deterministic and quick. Avoid printing environment variables that may contain secrets.

## Tool permissions

Declare only the permissions required by the workflow. Prefer a narrow allowlist or command prefix where supported. Avoid unrestricted shell access merely for convenience.

A command should state what it will do with tool output and how it handles a non-zero exit status.

## Referencing plugin resources

Commands may need templates, configuration, scripts, or documentation stored alongside the plugin. Use plugin-relative paths and ensure the referenced resources are packaged.

Check that:
- the file exists;
- its path is correct after installation;
- it contains no machine-specific assumptions;
- the command handles missing resources clearly.

## Coordinating components

A plugin command may coordinate with:
- **Agents:** request specialized analysis and require evidence in the result.
- **Skills:** use domain-specific instructions to shape the workflow.
- **Hooks:** account for automated checks that run around tool events.
- **Scripts:** perform deterministic operations that are better handled by code than natural-language instructions.

Do not assume a component is installed just because the command names it. Check availability or provide a clear fallback.

## Multi-stage example

A review workflow may:
1. run deterministic lint checks;
2. inspect changed files;
3. ask a specialized reviewer for an independent analysis;
4. verify high-confidence findings;
5. assemble a report from a template.

Separate deterministic check results from model-generated suggestions. Stop if a required stage cannot run.

## Safe shell handling

- Validate all dynamic inputs.
- Quote file paths and values.
- Avoid evaluating arbitrary user text as shell code.
- Use explicit working directories.
- Do not use destructive commands unless explicitly authorized.
- Keep secrets out of arguments and logs.
