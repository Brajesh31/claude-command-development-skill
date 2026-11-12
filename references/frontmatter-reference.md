# Slash Command Frontmatter Reference

Claude Code command frontmatter is YAML placed between the opening and closing `---` lines at the beginning of a command file. Check the current Claude Code documentation for version-specific behavior before relying on a field.

## Common fields

| Field | Purpose | Guidance |
|---|---|---|
| `description` | Short command description, commonly shown in command discovery | Use a clear action and outcome. |
| `allowed-tools` | Restricts or declares tools available to the command | Grant only the tools needed. Confirm accepted names and syntax for the installed version. |
| `model` | Selects a model for command execution where supported | Omit to inherit the conversation model unless a specific reason exists. |
| `argument-hint` | Shows the expected argument shape | Use readable placeholders such as `[file-path]`. |
| `disable-model-invocation` | Controls whether a command can be invoked programmatically by the model | Use only when manual invocation is a requirement and the installed version supports it. |

## Example

```yaml
---
description: Review a pull request for correctness
argument-hint: [pr-number]
allowed-tools: Read, Grep, Bash(gh:*)
---
```

This is an illustrative pattern. Verify the allowed-tools grammar and field support for the target Claude Code release.

## YAML safety

- Quote values containing characters that may be interpreted as YAML syntax.
- Use spaces, not tabs, for indentation.
- Avoid duplicate keys.
- Keep descriptions short and useful.
- Do not put credentials or secret values in frontmatter.
- Do not invent fields or copy fields from a different command system.

## Validation checklist

1. The file begins with a valid frontmatter delimiter.
2. The YAML parses.
3. Every field is supported by the installed version.
4. Tool declarations are narrow and intentional.
5. The argument hint agrees with the command's actual argument usage.
6. The body instructions agree with the metadata.
7. The command still works when optional values are omitted.
