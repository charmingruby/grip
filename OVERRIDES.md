# Mandatory Overrides

**Step-by-step adaptation guide**

Follow the steps below when bringing this workflow into another repository.
Only the items listed here must be changed.

---

## Step 1 — Review agent skills

**Where:** `agents/*`

1. Locate the `Skills` (or `Skill Dependencies`) section in agents that **execute or review code**.
2. Replace `{SKILL_N}` with the actual competencies used in the project.

Examples:

```md
- Applicable skills:
  - `ui-system`
  - `sveltekit-conventions`
```

**Rules:**

- Do **not** hardcode skills as always-on.
- Skills must remain **declarative**.
- Plans and tasks decide **when** a skill applies.

---

## Step 2 — Define reusable commands

**Where:** `.opencode/commands/*`

1. Create reusable command definitions for the repository (e.g. `quality-gate`).
2. Each command must describe **how to run** validation without exposing details to agents.

Example:

```md
.opencode/commands/quality-gate.md
```

3. In agents, replace `{COMMAND_N}` with these reusable command names.

---

## Step 3 — Update workflow references

**Where:** `agents/*`

1. Review `Workflow` instructions that reference another files.
2. Point them to the **actual names used in the repository**.
3. Do not introduce stack-specific logic inside the agent.

---

## Step 4 — Normalize verification behavior

**Where:** `agents/*`, plans, and tasks

1. **Do not** hardcode commands like `npm run ...` inside agents.
2. Use generic references instead:

```md
- Applicable commands:
  - command: quality-gate
```

3. Commands must be resolved via:

```
.opencode/commands/{NAME}.md
```

4. If no verification is explicitly specified:
   - Default to `command: quality-gate` when available.

---

## Step 5 — Confirm output paths

**Where:** `agents/*`, templates

1. Ensure all `Deliverable` / `Output` paths point to:
   - `memory/requirements/...`
   - `memory/plans/...`

2. Create these folders in the destination repository if they do not exist.
3. These paths are **fixed** and must not be renamed.

---

## Step 6 — Final sanity check

Before using the workflow:

- [ ] Skills are declared, not assumed
- [ ] Commands are generic and reusable
- [ ] Agents contain no stack-specific execution logic
- [ ] `quality-gate` exists and runs successfully
- [ ] `memory/requirements` and `memory/plans` are present

---

### Design principle (do not change)

> **Agents execute contracts.
> Skills define how to think.
> Commands define how to run.**
