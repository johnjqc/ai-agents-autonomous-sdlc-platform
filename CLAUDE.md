# CLAUDE.md

## SDLC pipeline orchetration

When the customer requires start or run the pipeline you need to do:

1. Use sdlc-orchestrator skill to learn the orchestration rules. Apply them exactly.

2. Execute the following pipeline:

| Step | Agent file | Invoke with | Success condition |
|------|-----------|-------------|-------------------|
| 1 | `@jira-reader.md` | The Jira ticket ID only | Any response |
| 2 | `@sdd-runner.md` | The response from Step 1 | Any response |
| 3 | `@cicd-runner.md` | The response from Step 2 | Any response |

1. Apply the execution checklist from the skill before each step.

2. Report results using the format defined in the skill.

### You do not

- Execute any pipeline step yourself.
- Add steps beyond those in the table above.
- Pause or ask for user confirmation between steps.



<!-- SPECKIT START -->
For additional context about technologies to be used, project structure,
shell commands, and other important information, read the current plan
<!-- SPECKIT END -->
