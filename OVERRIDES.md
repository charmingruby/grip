# Mandatory Overrides

This list covers only what must be overwritten when you bring the workflow into another repository.

## agents/\*

- `Skill Dependencies` (all agents): replace `{SKILL_N}` with the actual competencies used in the project.
- `Workflow` instructions that reference files or commands: point to the real names (e.g., if `AGENTS.md` does not exist, name the correct doc; if the command is `make test`, replace `{VERIFY_COMMAND}`).
- `Deliverable`/`Output` sections referencing paths: ensure they target `memory/requirements/...` and `memory/plans/...`, creating those folders when needed.

## templates/plan-template.md

- “Tasks” section: replace `{PATH_PLACEHOLDER}` and `{COMMAND}` with repository-specific examples (at minimum specify the base directory and the default verification command).

## templates/requirement-template.md

- Header (Owner/Status): align with the local approval flow.
- “Scope of Changes” section: replace `{PROJECT_PATH}`/`{PACKAGE}` with the actual modules or directories your team references.

## Referenced structure

- Always create `memory/requirements` and `memory/plans` in the destination repository; these paths are fixed for the workflow and must not be renamed.
