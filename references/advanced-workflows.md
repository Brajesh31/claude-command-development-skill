# Advanced Command Workflows

Use an advanced workflow when a command has dependencies, conditional stages, or meaningful side effects. Keep each stage explicit and independently verifiable.

## Analyze, act, report

A reliable default sequence is:

1. **Preflight:** confirm the repository, scope, prerequisites, and working-tree state.
2. **Analyze:** collect the information needed to make the decision.
3. **Plan:** identify actions, files, risks, and validation.
4. **Act:** make only the changes within the authorized scope.
5. **Verify:** run the smallest checks that demonstrate the result.
6. **Report:** summarize changed files, checks, and remaining risks.

If the preflight stage fails, do not continue as though prerequisites were satisfied.

## Iterative fixing

Use a bounded loop for workflows such as fixing lint errors:

1. Run the selected check.
2. Parse the current failures.
3. Group failures by root cause.
4. Fix one coherent group.
5. Re-run the narrow check.
6. Stop when clean, blocked, or the retry limit is reached.

Define a reasonable stop condition. Do not loop indefinitely or broaden the scope to unrelated files.

## Agent delegation

Delegate only when the task benefits from independent expertise or parallel analysis.

A delegation request should include:
- the exact target and boundaries;
- relevant files and context;
- the question to answer;
- the required evidence format;
- whether the delegate may make changes.

Prefer independent read-only reviews in parallel. Avoid concurrent edits to the same files unless the work has been partitioned safely.

## Checkpoints and authorization

Add a checkpoint before actions that:
- delete or overwrite data;
- publish content or packages;
- deploy to an external environment;
- change permissions or credentials;
- create charges or irreversible external effects.

A user asking for a command to be written is not automatic permission to execute its future side effects.

## Idempotence and recovery

Where practical, commands should be safe to run more than once.

- Check whether a target already exists before creating it.
- Avoid appending duplicate configuration entries.
- Record which stage completed before retrying.
- Do not repeat external actions after an ambiguous response without checking their status.
- Preserve intermediate output needed for diagnosis.

## Failure reporting

Use clear states:
- completed;
- partially completed;
- blocked by a missing prerequisite;
- failed during execution;
- skipped because authorization was not given.

Include the failing stage and useful evidence. Never describe a partial run as a success.
