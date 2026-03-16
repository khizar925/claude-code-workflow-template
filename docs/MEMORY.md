# MEMORY.md — [Project Name]

> Claude reads this before starting work on any existing area of the codebase.
> Do not edit manually — Claude updates this during sessions.
> If you do edit it, mark the change with `[manual]` so Claude knows.

---

## How Claude Uses This File

- Read at the start of every session touching existing code
- Update at the end of every session — add decisions, gotchas, patterns, warnings
- Never overwrite existing entries — only append
- Keep entries short and scannable — no paragraphs

---

## Decisions

> Why things were built a certain way.
> Prevents Claude from "improving" something that was intentionally designed.

<!-- Claude appends here during sessions -->
<!-- Format: [date] — decision made + reason -->
<!-- e.g. [2025-01-10] — using JWT over sessions: client needs stateless API for mobile -->

---

## Gotchas

> Things that caused bugs, wasted time, or behaved unexpectedly.
> Prevents Claude from hitting the same wall twice.

<!-- Claude appends here during sessions -->
<!-- Format: [date] — what the gotcha is + what triggered it + how it was resolved -->
<!-- e.g. [2025-01-12] — Mongoose doesn't return updated doc by default.
     Always pass { new: true } to findByIdAndUpdate or result will be stale -->

---

## Patterns

> Established conventions in this codebase.
> Claude must follow these — don't invent alternatives.

<!-- Claude appends here during sessions -->
<!-- Format: pattern name → rule -->
<!-- e.g. Error responses → always use { success: false, message, code } shape -->
<!-- e.g. Auth checks → always go through verifyToken middleware, never inline -->

---

## Warnings

> Hard stops. Things Claude must never do in this codebase.
> Usually learned the hard way.

<!-- Claude appends here during sessions -->
<!-- Format: NEVER [action] — [reason] -->
<!-- e.g. NEVER query without tenantId filter — breaks multi-tenant isolation -->
<!-- e.g. NEVER modify User.role directly from frontend input — always validate server-side -->

---

## External Services

> Quirks, limits, and gotchas specific to third-party integrations.
> Prevents Claude from making incorrect assumptions about external APIs.

<!-- Claude appends here during sessions -->
<!-- Format: [service] — [quirk or limit or behavior to know] -->
<!-- e.g. Resend — free tier limits to 100 emails/day. Don't batch-send in loops -->
<!-- e.g. MongoDB Atlas — free tier pauses after 60 days inactivity. Health check keeps it alive -->

---

## Performance Notes

> Slow queries, expensive operations, or scaling concerns already identified.

<!-- Claude appends here during sessions -->
<!-- Format: [area] — [what's slow or expensive] + [current mitigation if any] -->
<!-- e.g. GET /instances — returns all tasks per instance. Add pagination before scaling -->

---

## Session Log

> One line per session. What was worked on and what changed.
> Gives Claude a quick timeline without reading the whole file.

<!-- Claude appends here after every session -->
<!-- Format: [date] — [what was done] -->
<!-- e.g. [2025-01-15] — implemented reminder scheduler, wired Resend, added EmailReminder model -->
```

---
