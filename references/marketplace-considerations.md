# Sharing and Distribution Considerations

Commands may be local to a project, personal to a user, or packaged with a plugin. Choose the distribution model based on who needs the workflow and which dependencies it requires.

## Project-local commands

Use project-local commands when:
- the workflow depends on repository conventions;
- teammates should share the same command;
- referenced files live in the repository;
- the command is part of the project's development process.

Keep paths relative and commit the command with the relevant supporting documents.

## Personal commands

Use a personal command when it is useful across unrelated repositories and does not depend on project-specific files. Avoid hard-coding machine-specific paths.

## Plugin-packaged commands

A plugin is appropriate when commands need to be distributed with agents, skills, hooks, scripts, configuration, or templates. Define a clear plugin boundary and keep the command's dependencies inside that boundary where possible.

## Compatibility

Before sharing:
- state the minimum supported Claude Code version when known;
- avoid undocumented frontmatter fields;
- verify command discovery and argument behavior;
- check referenced tools and plugin components;
- test on a clean installation or isolated fixture.

Do not claim compatibility with a release that has not been tested.

## Security and privacy

- Do not embed credentials or tokens in command files.
- Do not require broad tool permissions by default.
- Explain any network access and external side effects.
- Do not collect sensitive information unless essential.
- Review scripts and templates before distribution.

## Maintenance

Assign ownership for updates, keep examples synchronized with behavior, and remove obsolete commands. A command that silently depends on an unavailable plugin or an expired path is not production-ready.
