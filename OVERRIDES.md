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

## Step 2 — Update workflow references

**Where:** `agents/*`

1. Review `Workflow` instructions that reference another files.
2. Point them to the **actual names used in the repository**.
3. Do not introduce stack-specific logic inside the agent.

---

## Step 3 — Normalize verification behavior

**Where:** `agents/*`, plans, and tasks

1. **Do not** hardcode commands like `npm run ...` inside agents.
2. Write common commands on `AGENTS.md`.

---

## Step 4 — Confirm output paths

**Where:** `agents/*`, templates

1. Ensure all `Deliverable` / `Output` paths point to:
   - `memory/requirements/...`
   - `memory/plans/...`

2. Create these folders in the destination repository if they do not exist.
3. These paths are **fixed** and must not be renamed.

---

## Step 5 — Final sanity check

Before using the workflow:

- [ ] Skills are declared, not assumed
- [ ] Commands are generic and reusable
- [ ] Agents contain no stack-specific execution logic
- [ ] Validation commands exists and runs successfully
- [ ] `memory/requirements` and `memory/plans` are present

---

### Design principle (do not change)

> **Agents execute contracts.
> Skills define how to think.
> Commands define how to run.**
