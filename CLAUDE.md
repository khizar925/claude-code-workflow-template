# CLAUDE.md

> Universal agent instructions. Project-specific context is split across:
> - `docs/PROJECT.md` — app overview, tech stack, file structure, commands
> - `docs/ARCHITECTURE.md` — data models, auth strategy, access control, service boundaries, DB conventions
> - `docs/MEMORY.md` — decisions made, gotchas discovered, patterns established, warnings from past sessions
>
> **Read these only when relevant:**
> - Starting a new feature or unfamiliar area → read `PROJECT.md`
> - Writing any DB query, auth logic, or middleware → read `ARCHITECTURE.md`
> - Unsure about stack, commands, or file locations → read `PROJECT.md`
> - Touching routes, models, or access control → read `ARCHITECTURE.md`
> - Starting work on ANY existing area of the codebase → read `MEMORY.md` first

---

## Workflow Orchestration

### 1. Plan First
- Enter plan mode for ANY non-trivial task (3+ steps or architectural decisions)
- If something goes sideways, STOP and re-plan immediately — don't keep pushing
- Use plan mode for verification steps, not just building
- Write detailed specs upfront to reduce ambiguity

### 2. Subagent Strategy
- Use subagents liberally to keep main context window clean
- Offload research, exploration, and parallel analysis to subagents
- For complex problems, throw more compute at it via subagents
- One task per subagent for focused execution

### 3. Self-Improvement Loop
- After ANY correction from the user: update `tasks/lessons.md` with the pattern
- Write rules for yourself that prevent the same mistake
- Ruthlessly iterate on these lessons until mistake rate drops
- Review `tasks/lessons.md` at session start for the current project

### 4. Verify Before Done
- Never mark a task complete without proving it works
- Diff behavior between main and your changes when relevant
- Ask yourself: "Would a staff engineer approve this?"
- Run tests, check logs, demonstrate correctness

### 5. Demand Elegance
- For non-trivial changes: pause and ask "is there a more elegant way?"
- If a fix feels hacky: "Knowing everything I know now, implement the elegant solution"
- Skip this for simple, obvious fixes — don't over-engineer

### 6. Autonomous Bug Fixing
- When given a bug report: just fix it. Don't ask for hand-holding
- Point at logs, errors, failing tests — then resolve them
- Go fix failing CI without being told how

---

## Task Management

1. **Plan First** — write plan to `tasks/todo.md` with checkable items
2. **Verify Plan** — check in before starting implementation
3. **Track Progress** — mark items complete as you go
4. **Explain Changes** — high-level summary at each step
5. **Document Results** — add review section to `tasks/todo.md`
6. **Capture Lessons** — update `tasks/lessons.md` after every correction

> Before ending ANY session that touched existing code:
> append new entries to docs/MEMORY.md under the correct section.
> append new entries to docs/PROGRESS_REPORT.md under the correct section.
> Never leave a session without updating it.
---

## Communication Style

- **Plan mode**: be verbose — explain tradeoffs and reasoning
- **Execution mode**: be concise — one-liners for straightforward steps
- Surface risks and blockers upfront, not after the fact
- Never ask clarifying questions mid-task unless truly blocked

---

## Hard Rules

**Research**
- Search for latest docs when: integrating a new external library, using an unfamiliar API,
  or unsure about version-specific behavior
- Skip searching for: internal logic, refactors, and anything stack-stable
- Only implement when you are confident it will work — don't guess

**Decisions**
- If blocked on a decision: make the simpler choice, document reasoning in a `// NOTE:` comment,
  and flag it in your summary
- Never silently guess on anything architectural

**Architecture**
- Never put business logic inside route handlers — it belongs in services or controllers
- Never couple modules that should communicate over a defined interface (HTTP, events, queues)
- Never hardcode secrets, API keys, or environment-specific URLs — use environment variables

**Quality**
- Never leave debug statements in committed code — use proper logging
- Never write temporary fixes — find and resolve the root cause

---

## Core Principles

- **Simplicity First** — make every change as simple as possible; minimal code impact
- **No Laziness** — find root causes; senior developer standards throughout
- **Minimal Impact** — changes should only touch what's necessary; avoid introducing bugs