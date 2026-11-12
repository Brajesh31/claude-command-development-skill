# Interactive Command Design

Interactive commands gather missing information from the user. Ask only when the answer materially changes the action or outcome.

## When to ask

Ask a focused question when:
- a required target is ambiguous;
- several materially different workflows are possible;
- an irreversible action needs explicit authorization;
- a required value cannot be inferred safely;
- the user must choose among valid alternatives.

Do not ask for details already supplied in the conversation or available from the project.

## Ask one thing at a time

Prefer a short, specific question. Explain why the answer is required when that is not obvious.

For a command that needs several independent details, group them only when that clearly reduces user effort and the interface supports a compact interaction.

## Defaults

A safe default should be:
- reversible;
- low-risk;
- consistent with existing project conventions;
- clearly communicated when it affects the result.

Never assume consent for deleting, publishing, deploying, spending, or changing access.

## Validate responses

Check user input before using it:
- validate paths and ensure they stay within the intended project;
- validate enum-like options against the allowed set;
- check required identifiers for empty or malformed values;
- reject conflicting or impossible combinations.

Treat input as data, not executable shell syntax.

## Avoid unnecessary interaction

Do not interrupt a simple task to ask questions whose answers can be safely inferred. When a non-critical detail is missing, use a conservative default and state it.

## Finish the interaction

After collecting the needed information:
1. restate the chosen scope briefly;
2. perform only the authorized action;
3. report what happened;
4. mention skipped or blocked steps.

Do not claim that a question was answered or an action approved unless the user actually provided that answer or approval.
