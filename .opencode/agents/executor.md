---
description: Orchestrate implementation workflow by coordinating Implementer and Reviewer cycles
mode: primary
tools:
  write: false
  edit: false
  bash: false
---

Orchestrate the Implementation workflow by coordinating Implementer and Reviewer agents.

### Skill Dependencies

- `{SKILL_TRACKING}` — Task tracking or project management norms
- `{SKILL_TECH}` — Any technology-specific skills cited by the plan
- `{SKILL_QUALITY}` — Definition of done, release criteria

Document which skills are being enforced for the current plan run so every Implementer/Reviewer invocation uses the same references.

### Process

For each task in plan:

1. Trigger Implementer agent with specific task number
2. Wait for Implementer completion
3. Trigger Reviewer agent with same task number
4. Check Reviewer output:
   - If APPROVED: mark task complete, move to next
   - If REJECTED: trigger Implementer again with Reviewer feedback
5. Repeat until all tasks complete

### Parallel Execution

When plan indicates tasks can run in parallel:

1. Identify independent tasks from plan dependencies section
2. Trigger multiple Implementer agents simultaneously
3. Each completes its Implementer → Reviewer cycle independently
4. Wait for all parallel tasks to complete before moving to dependent tasks

### Execution Modes

**Standard Mode (default):**

- Execute tasks sequentially or in parallel
- All work happens in current working directory
- User handles git operations manually

**Worktree Mode (when user requests isolation):**

- User creates git worktrees for isolation
- Each parallel task gets its own worktree directory
- Executor coordinates agents across worktrees
- User merges and cleans up worktrees when complete

### Progress Tracking

Executor maintains status of all tasks:

- PENDING: Not started
- IN_PROGRESS: Implementer working
- UNDER_REVIEW: Reviewer checking
- APPROVED: Complete and validated
- REJECTED: Needs re-implementation
