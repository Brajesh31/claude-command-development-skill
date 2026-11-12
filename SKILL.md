---
name: command-development
description: Design, implement, test, and maintain Claude Code slash commands. Use when working with command Markdown files, YAML frontmatter, dynamic arguments, file references, shell context, or command organization.
---

# Command Development for Claude Code

Slash commands are reusable Markdown instruction files that can be invoked by name during a Claude Code session. Build commands that are clear to the agent, predictable for the user, and safe to run.

## Command locations

- Project commands: `.claude/commands/`.
- User commands: `~/.claude/commands/`.
- Plugin commands: the plugin's `commands/` directory.

Use the location appropriate to the desired sharing scope and verify the conventions supported by the installed Claude Code version.

## File structure

A command is a Markdown file. YAML frontmatter is optional for simple commands and can configure supported metadata.

```markdown
---
description: Review the current change for correctness and security
argument-hint: [focus]
---

Review the requested change. Inspect the relevant diff, verify each finding,
and report actionable issues with file locations.
```

## Common frontmatter fields

Check current Claude Code documentation before relying on a field or feature. Common fields include:

| Field | Purpose |
| --- | --- |
| `description` | Explains the command in command discovery/help. |
| `argument-hint` | Shows expected argument syntax. |
| `allowed-tools` | Restricts tools available to the command. |
| `model` | Selects a supported model when configured. |
| `disable-model-invocation` | Restricts programmatic invocation when supported. |

## Arguments

- Use the full argument string when the command needs a free-form prompt.
- Use positional arguments when fields have distinct meanings.
- Mark required and optional arguments in the hint.
- Validate missing, malformed, or unexpected values.
- State defaults explicitly; never silently guess critical inputs.

Example:

```markdown
---
description: Explain a specific issue
argument-hint: <issue-number>
---

Investigate issue #$ARGUMENTS. Read the issue and relevant code first.
Do not close the issue or change code unless asked.
```

Confirm the exact argument expansion behavior against the user's installed version.

## File references and shell context

- Reference only files that exist and are relevant.
- Handle missing referenced files gracefully.
- Use shell context only when it materially improves the command.
- Quote variables and validate user-supplied values.
- Avoid commands with hidden side effects.

## Organization

Use descriptive kebab-case names. Keep a small command set flat. For larger sets, group related commands using supported command namespacing conventions and verify how they appear in command discovery.

## Safety and permissions

- Grant the minimum tool access needed.
- Separate inspection from mutation.
- Confirm before deleting data, changing permissions, publishing, deploying, or making irreversible changes.
- Never embed API keys, passwords, tokens, or personal data in command files.
- Make error handling and stopping conditions explicit.

## Development workflow

1. Define purpose, scope, inputs, outputs, and side effects.
2. Check current documentation and installed-version support.
3. Draft the command and frontmatter.
4. Validate file paths, arguments, and permissions.
5. Test in a safe project or fixture.
6. Review the command as an instruction set, not merely as prose.
7. Document invocation, requirements, and limitations.

## Bundled resources

- `examples/simple-commands.md`
- `examples/plugin-commands.md`
- `references/advanced-workflows.md`
- `references/documentation-patterns.md`
- `references/frontmatter-reference.md`
- `references/interactive-commands.md`
- `references/marketplace-considerations.md`
- `references/plugin-features-reference.md`
- `references/testing-strategies.md`

Consult the specific reference when implementing that feature. Treat version-sensitive examples as examples, not guaranteed current syntax.
