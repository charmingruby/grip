# Plan: {Topic}

Requirement: `memory/requirements/YYYY-MM-DD-{topic}-requirement.md`
Status: READY_TO_EXECUTE
Owner: Planner

> **How to use**: Author tasks so they remain stack-agnostic. Mark placeholders like `{FRAMEWORK_CMD}` or `{API_ENDPOINT}` where the project must inject specifics.

## Pre-flight Checklist

- Confirm requirement assumptions resolved?
- Repo/branch prepared? (`git status`, dependencies installed)
- Skills required: [ui-system, api, data, ...]
- Tooling commands verified or tagged as `{TODO:COMMAND}`

## Tasks

For each task include purpose, files, steps, and validation. Example structure:

### Task {N}: {Short name}

- **Goal**: [Outcome]
- **Files/Areas**: `{PATH_PLACEHOLDER}`
- **Implementation Notes**: [Steps, patterns to follow, TODO markers]
- **Verification**: `run {COMMAND}` or [manual QA]
- **Specialization Needed**: [What the user must fill later]

Repeat until the requirement is fully covered.

## Dependencies & Parallelism

- Sequential tasks: [Task → dependent task]
- Parallel groups: [Task A, Task B]
- External blockers: [e.g., "wait for API key"]

## Rollback / Contingency

- Describe how to revert code/config changes.
- Note feature flags, toggles, or migrations to undo if needed.
