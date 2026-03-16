# PROJECT.md — [Project Name]

## What is [Project Name]
<!-- FILL IN: 3-5 bullet points describing what the app does -->
<!-- What problem does it solve? Who uses it? What are the core workflows? -->

---

## Strict Rules
<!-- FILL IN: project-specific constraints that override everything else -->
- Never hardcode credentials or API keys — all secrets go in `.env` only
- `docs/[SPEC_FILE].md` is the source of truth from the client — it wins over any reference site
- Use `[REFERENCE_SITE]` as UX/flow reference
- Use `[DESIGN_REFERENCE]` for theme and color scheme
- Use `docs/DESIGN.md` for the design system
- After every feature or significant change, update `docs/PROGRESS_REPORT.md`

---

## Tech Stack

**Monorepo / Structure:** <!-- FILL IN: e.g. pnpm workspaces, nx, turborepo, single app -->

### Frontend
<!-- FILL IN: framework, language, styling, state management, routing, HTTP client, UI library -->

### Backend
<!-- FILL IN: runtime, framework, language, primary DB, cache, auth method, email, scheduling, validation -->

### Planned / Not Yet Integrated
<!-- FILL IN: list everything scoped but not built yet — keeps Claude from assuming it exists -->

---

## File Structure
```
[project-root]/
├── <!-- FILL IN: paste your actual folder tree here -->
```

> Keep this updated. Claude uses it to locate files without exploring the repo.

---

## Commands

### Root
```bash
# FILL IN: install, dev, build commands at monorepo root
```

### Frontend
```bash
# FILL IN: dev, build, lint, preview
```

### Backend
```bash
# FILL IN: dev, build, start
```

---

## Deployment

### Live URLs
<!-- FILL IN: frontend URL, backend URL, health check endpoint -->

### Deployment Targets
<!-- FILL IN: hosting platforms, auto-deploy triggers, config file locations -->

### Environment Variables
<!-- FILL IN: point to .env.example — never list actual values here -->
See `.env.example` for the full variable list. Secrets live in platform dashboards only.
```

---