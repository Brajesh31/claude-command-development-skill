# Command Documentation Patterns

Command documentation should make the command understandable, discoverable, and safe to invoke.

## Document the contract

For each command, describe:
- purpose and trigger;
- arguments, accepted values, and defaults;
- required tools and external dependencies;
- files or systems read;
- files or systems modified;
- side effects and required authorization;
- expected output;
- validation and failure behavior.

Do not document behavior the command does not implement.

## Keep the main command concise

Put essential instructions in the command file. Move long, stable reference material into a nearby document when it is reused or would otherwise obscure the workflow.

Good candidates for a reference:
- detailed formatting standards;
- extensive API or schema notes;
- large sets of examples;
- troubleshooting procedures;
- policy checklists shared by several commands.

Do not create a separate file for a single sentence or repeat the entire command in a reference.

## Reference files clearly

Use explicit relative paths that match the repository's command layout. Check every referenced file into the repository and test that the path resolves from the expected location.

A reference should explain when it is useful, not merely exist as an attachment.

## Use examples deliberately

Examples should show:
- the command file path;
- the relevant frontmatter;
- a realistic invocation;
- expected behavior;
- important safety boundaries.

Use placeholders for secrets and environment-specific values. Label pseudocode and illustrative examples clearly.

## Keep documentation current

When command behavior changes:
1. Update the command contract.
2. Update affected reference sections.
3. Review examples that use the changed arguments or fields.
4. Check that paths remain valid.
5. Remove obsolete instructions rather than leaving conflicting guidance.

## Write for the executing agent

Use direct imperatives and explicit ordering. Avoid vague language such as "handle this appropriately." State what to inspect, how to make decisions, when to stop, and what to report.
