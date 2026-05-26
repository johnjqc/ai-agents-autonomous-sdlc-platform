---
name: "sdlc-orchestrator"
description: "Perform a orchestration of an automated SDLC pipeline invoking each sub-agent in sequence."
argument-hint: "Pipeline orchestration"
user-invocable: true
disable-model-invocation: false
---

# Pipeline Orchestrator Skill

## Purpose
Teaches an orchestrator agent how to execute a multi-step pipeline by invoking
sub-agents sequentially, validating each step before proceeding.

## When to use this skill
Read this skill whenever you are asked to run, start, or trigger a pipeline.

---

## Core orchestration rules

### Execution model
- Steps run **strictly in order**. Never skip, reorder, or parallelize them.
- Each sub-agent is invoked **exactly once** per pipeline run.
- Every run is always **fresh** — never assume a step completed based on prior
  conversation history.

### Invoking a sub-agent
When the pipeline definition specifies a sub-agent, invoke it using:

    @<agent-file> <input defined in the pipeline>

Pass **only** what the pipeline definition specifies in the "Invoke with" column.
Do not add instructions, expected formats, or extra context to the invocation prompt.

### Step validation
After each sub-agent responds:
- Any response = success. Do not evaluate the content of the response.
- No response or an explicit error = failure → report failure with the agent name
  and stop the pipeline immediately.

### Execution mode
- Run from start to finish **without pausing**.
- Never ask the user for confirmation between steps.
- Never ask "would you like to proceed?".
- Never prompt the user mid-pipeline.

### What you must never do
- Read tickets, generate documents, write code, create branches, or open PRs yourself.
- Invoke skills directly — skills are reserved for sub-agents only.
- Add, invent, or improvise steps not defined in the pipeline.
- Proceed if the current step has not been confirmed as successful.

---

## How to read a pipeline definition

A pipeline is defined as a table with these columns:

| Step | Agent file | Invoke with | Success condition |
|------|-----------|-------------|-------------------|

- **Step**: execution order (1, 2, 3…)
- **Agent file**: the sub-agent to invoke (e.g. `@jira-reader.md`)
- **Invoke with**: exactly what to pass as input to that agent
- **Success condition**: when to consider the step done

---

## Execution checklist (run mentally before each step)

1. Am I invoking the correct agent for this step number?
2. Am I passing only what "Invoke with" specifies — nothing more?
3. Did the previous step succeed before I moved forward?
4. Am I about to pause or ask the user anything? → Do not.

---

## Reporting

On pipeline completion:

    Pipeline complete.
    ✓ Step 1 — @jira-reader.md — success
    ✓ Step 2 — @sdd-runner.md — success
    ✓ Step 3 — @cicd-runner.md — success

On failure:

    Pipeline stopped at step <N>.
    ✗ Step <N> — @<agent>.md — failed: <reason>
    Steps not executed: <remaining steps>