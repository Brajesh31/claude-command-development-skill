# Command Testing Strategies

Test commands as executable workflows, not just as Markdown documents.

## 1. Static checks

Verify:
- frontmatter delimiters and YAML validity;
- required fields and supported values;
- Markdown code fences;
- argument placeholders;
- referenced file paths;
- shell snippets for obvious syntax errors;
- consistency between the description and the body.

Static validity does not prove runtime behavior.

## 2. Invocation checks

Test a normal invocation with:
- no arguments when arguments are optional;
- valid arguments;
- missing required arguments;
- malformed or unexpected values;
- paths that contain spaces.

Confirm that defaults and error messages are clear.

## 3. Behavioral checks

Use a disposable repository or fixture. Verify:
- the command reads the intended files;
- modifications stay within scope;
- read-only commands do not change state;
- tools and scripts are invoked only when expected;
- output follows the documented format;
- failure states stop the workflow.

## 4. Side-effect checks

For commands that stage, commit, deploy, publish, delete, or change settings:
- verify the target before action;
- require authorization at the appropriate point;
- test failure and retry behavior;
- ensure an ambiguous result does not cause duplicate external actions.

Use mock services or dry-run modes where possible.

## 5. Regression checks

Whenever the command changes:
- rerun its focused test cases;
- check all referenced files;
- update examples and documentation;
- inspect the final diff;
- verify compatibility claims.

## 6. Test report

Record:
- environment and Claude Code version;
- command and arguments tested;
- fixture or repository state;
- checks performed;
- observed output;
- failures and untested cases.

Never report a command as tested when it was only inspected.
