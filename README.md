# claude-code-template-workflow

A universal Claude Code starter template. Drop it into any project and get a structured, AI-ready workspace in minutes — with planning, reporting, and self-improvement built in.

---

## What's Included

```
claude-starter/
├── CLAUDE.md                        # Universal agent behavior rules (keep as-is)
├── docs/
│   ├── PROJECT.md                   # App overview, stack, file structure, commands
│   ├── ARCHITECTURE.md              # Data models, auth, access control, DB conventions
│   ├── MEMORY.md                    # Decisions, gotchas, patterns, warnings
│   └── PROGRESS_REPORT.md           # Session-by-session progress log
├── tasks/
│   ├── todo.md                      # Task planning per session
│   └── lessons.md                   # Self-improvement log
└── .claude/
    ├── skills/
    │   └── plan.md                  # /plan — implementation planner (no code changes)
    └── commands/
        ├── lesson.md                # /lesson — log a correction as a lesson
        ├── report.md                # /report — generate daily standup report
        └── sprint.md                # /sprint — generate sprint summary report
```

---

## Setup

### 1. Add to an existing project

Run this from the **root of your existing repo** — it copies all template files in without touching your git history:

```bash
npx degit your-username/claude-starter
```

> **First time?** `npx` runs `degit` without a global install. It overwrites files with the same name, so check for conflicts with any existing `CLAUDE.md` or `docs/` folder first.

### 2. Fill in project context

Open Claude Code in your project root and run the prompts below — one file at a time.

---

#### Fill in `docs/PROJECT.md`

```
Read docs/PROJECT.md and the actual codebase (package.json, config files, folder structure).
Fill in every <!-- FILL IN --> section with what you can verify from real files.
Do not guess — leave any section blank if evidence is missing and flag it in your summary.
Cover: what the app does, tech stack (frontend + backend), file structure, dev commands, deployment info.
```

---

#### Fill in `docs/ARCHITECTURE.md`

```
Read docs/ARCHITECTURE.md and explore the codebase — models, middleware, auth logic, route files, DB config.
Fill in every <!-- FILL IN --> section based only on what exists in the code.
Cover: data models (fields, types, relationships), auth flow end-to-end, access control table,
service boundaries, all API routes, DB conventions, environment variables.
Flag anything you cannot verify.
```

---

#### Fill in `docs/MEMORY.md`

```
Read docs/MEMORY.md. This file is the project knowledge base — Claude reads it before touching any existing code.
Based on a review of the codebase, pre-populate the following sections with anything already known:
- Decisions: why certain patterns or libraries were chosen
- Gotchas: anything that could cause bugs or confusion
- Patterns: established conventions (naming, error shape, auth checks, etc.)
- Warnings: things that must never be done in this codebase
- External Services: known quirks of any third-party integrations
Leave any section with its comment placeholder if nothing is known yet. Do not invent entries.
```

---

#### Verify `tasks/lessons.md` and `tasks/todo.md`

These start empty — Claude populates them automatically during sessions. No action needed.

---

## What to Keep vs Fill In

| File | Action |
|---|---|
| `CLAUDE.md` | Keep as-is — universal agent rules |
| `docs/PROJECT.md` | Fill in per project (use prompt above) |
| `docs/ARCHITECTURE.md` | Fill in per project (use prompt above) |
| `docs/MEMORY.md` | Pre-populate if possible, then Claude appends during sessions |
| `docs/PROGRESS_REPORT.md` | Starts empty — Claude appends after sessions |
| `tasks/todo.md` | Starts empty — Claude writes plans here per session |
| `tasks/lessons.md` | Starts empty — Claude appends after every correction |
| `.claude/skills/plan.md` | Keep as-is, or customize planning output format |
| `.claude/commands/report.md` | Customize report format to match your team's standup style |
| `.claude/commands/sprint.md` | Keep as-is, or adjust date format and output structure |
| `.claude/commands/lesson.md` | Keep as-is |

---

## Available Commands

| Command | What it does |
|---|---|
| `/plan [feature]` | Creates a detailed implementation plan with file-by-file breakdown — no code changes |
| `/report [context]` | Generates a daily standup report from Asana tickets and previous reports |
| `/sprint [date range]` | Generates a sprint summary from all daily reports in `REPORTS.md` |
| `/lesson [what went wrong]` | Logs a correction to `tasks/lessons.md` so Claude doesn't repeat the mistake |

---

## How It Works

**`CLAUDE.md`** tells Claude how to behave — planning first, verification, bug fixing, communication style, and hard rules. It applies to every session automatically.

**`docs/`** gives Claude project-specific knowledge so it doesn't explore the codebase blind at the start of every session.

**`tasks/`** keeps Claude accountable within a session — what's planned, what's done, and what was learned from corrections.

**`.claude/`** gives you slash command shortcuts for repetitive workflows like standup reports, sprint summaries, and lesson logging.

---

## Workflow Summary

```
1. Start session → Claude reads docs/MEMORY.md + tasks/lessons.md
2. Plan task     → /plan [feature] or Claude writes to tasks/todo.md
3. Build         → Claude tracks progress in tasks/todo.md
4. Correction    → /lesson [what went wrong] → appended to tasks/lessons.md
5. End session   → Claude appends to docs/MEMORY.md + docs/PROGRESS_REPORT.md
6. Standup       → /report [context]
7. Sprint end    → /sprint [date range]
```
