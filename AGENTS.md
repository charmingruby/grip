# AGENTS.md

## Mission

Provide concise guardrails so every contribution keeps the SvelteKit app stable, typed, and visually cohesive. Changes should feel native to the product, rely on existing primitives, and stay easy to verify.

## Core Principles

- Favor incremental fixes over sweeping rewrites; keep each change scoped to a single concern.
- Reuse established patterns (routing, state, styling) and align naming with nearby files before inventing new approaches.
- Keep UI state-driven; avoid manual DOM access unless a Svelte action truly needs it.
- Use the shadcn-first UI system already in place—extend primitives instead of creating redundant variants.
- When a needed component is missing, first look for an equivalent in the shadcn library and import it; only build a new primitive if shadcn does not cover the requirement.
- Document meaningful behavior changes within the codebase (types, schemas, UI descriptions) as part of the same change set.

## Development Commands

### Core Scripts

- `npm run dev` – start the Vite dev server
- `npm run build` – production build
- `npm run preview` – preview the production build locally
- `npm run check` – SvelteKit sync + svelte-check (required before completion)
- `npm run lint` – Prettier + ESLint verification
- `npm run check:watch` – live type-check feedback during large refactors
- `npm run format` – Prettier write mode (run only when formatting intentionally)

### Database Scripts

- `npm run db:generate` – produce Drizzle migrations from schema updates
- `npm run db:migrate` – apply migrations to the local database

## Project Conventions

### Source Layout & Imports

- UI components live in `src/components/`, grouped by feature (`team/`, `ui/`, etc.).
- Business logic, helpers, and shared utilities go under `src/lib/`.
- Use the `@/` alias everywhere inside `src/`; only `./$types` imports are allowed in route files.
- Name `.svelte` files in kebab-case even when the exported component stays PascalCase.
- Keep UI primitives self-contained; only split supporting files when there is a real reuse boundary.

#### Directory Responsibilities

- `src/routes/` – Feature entry points; keep files thin and delegate logic/UI to `@/components` and `@/lib`.
- `src/components/ui/` – Source of truth for shadcn primitives defined in `components.json`; extend via props/variants instead of recreating components elsewhere.
- `src/components/<feature>/` – Feature-scoped compositions that stitch primitives together; avoid business logic here.
- `src/lib/` – Shared domain logic, state helpers, schemas, and utilities usable across routes; never import UI from here.
- `src/lib/server/` – Server-only helpers (DB, integrations). Client bundles must not import from this tree.
- `src/lib/server/db/` – Drizzle schema + migrations helpers; any schema change must pair with `db:generate` and `db:migrate`.

### Svelte & Reactivity

- Use Svelte 5 runes (`$props`, `$state`, `$derived`, `$effect`, `$bindable`).
- Replace legacy `$:` blocks with `$derived` or `$effect` and prefer snippets/`{@render ...}` over slots when composing UI regions.
- Use modern event attributes (`onclick`, `onkeydown`, etc.); lean on bindings rather than DOM queries.
- Keep effects minimal; only reach for `onMount`/`onDestroy` when lifecycle semantics matter.
- Navigate with `$app/navigation` (`goto`) rather than `window.location`.

### Styling & UI System

- Treat shadcn-influenced primitives (`Button`, `Input`, `Sheet`, `Badge`, etc.) as the foundation. Extend them via props, Tailwind variants, or CSS variables instead of recreating from scratch.
- Tailwind usage should remain component-scoped; avoid expanding `app.css` unless defining shared tokens.
- Typography and color choices must feel intentional—lean on the existing font stacks and CSS variables (`--text-primary`, `--bg-secondary`, etc.).
- Prefer layered backgrounds (gradients, subtle textures) and meaningful transitions over flat, generic layouts.
- Keep responsive behavior in mind; test components at narrow and wide widths.

### TypeScript & Utilities

- The repo enforces strict TypeScript; keep interfaces/types close to their domains.
- Use `as const` for readonly structures and export reusable inferred types.
- Compose conditional classes with `cx` from `@/lib/cn` instead of inline string concatenation.

## Data & Server Guidance

- Drizzle ORM with SQLite/libsql backs all persistence; schema definitions live in `src/lib/server/db/schema.ts` and helper utilities in `src/lib/server/db/db.ts`.
- Schema changes always travel through migrations (`db:generate` + `db:migrate`).
- Server routes follow SvelteKit naming (`+page.server.ts`, `+server.ts`) and should validate inputs before hitting the database.
- Wrap asynchronous work that can fail in try/catch and surface errors through `throw error()` or a proper API response.

## Accessibility & Performance

- Prefer semantic HTML elements and ensure every interactive control is keyboard reachable.
- Provide `alt` text for informative media; mark decorative SVGs/images with `aria-hidden`.
- Announce dynamic updates when necessary and keep focus handling explicit for modals/sheets.
- Add `width`/`height` plus `decoding="async"` to images where possible; debounce expensive inputs and memoize derived state instead of recalculating in templates.

## Testing & Verification

- Always run `npm run check` and `npm run lint` before handing off work.
- Run `quality-gate` when available; if the command is missing or fails for unrelated reasons, record `NOT_RUN:quality-gate` (or the failing command) with a short explanation in the final hand-off.
- When no automated coverage exists, describe the manual checks performed (e.g., viewport sizes, keyboard navigation, DB flows).

## Quality Checklist

- [ ] `npm run check` passes
- [ ] `npm run lint` passes
- [ ] Code matches surrounding patterns (imports, naming, component structure)
- [ ] UI updates reuse shadcn-based primitives and remain responsive
- [ ] Types, schemas, and utilities stay strict and colocated
- [ ] Accessibility and performance considerations have been addressed
