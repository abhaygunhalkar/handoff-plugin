---
name: handoff-writing
description: Use when generating a session handoff summary (triggered by the /handoff command or the SessionEnd hook) to bring Claude Code project context into a separate Claude Desktop or Claude.ai chat. Defines exactly what to capture and what to leave out so summaries stay consistent across sessions.
---

# Handoff Summary Writing

## Purpose
Produce a short, consistently-structured summary of a Claude Code session that a
human can paste into a different Claude conversation (or that Claude can read
directly via a Filesystem connector) so project context doesn't have to be
re-explained from scratch.

## What to include (in this order)

1. **Project / feature name** — one line, plain text, no formatting flourishes.
2. **Decisions made, with the reason** — not just "used Zod" but "used Zod over
   Yup — better TypeScript inference." The reasoning is the part worth
   preserving; the bare fact alone is often re-derivable, the reasoning isn't.
3. **Alternatives explicitly rejected, and why** — if the user or Claude
   considered and dismissed an approach, capture it. This prevents the same
   dead end from being re-explored in the next session.
4. **Current blockers or open questions** — anything unresolved at session end.
   Be specific: name the actual error, API, or decision pending, not just
   "there's an issue with the API."
5. **Conventions/preferences the user stated** — naming conventions, style
   preferences, anything said explicitly that should persist going forward.

## What to leave out
- Routine back-and-forth that led nowhere (a typo fixed, a file path corrected)
- Anything already captured in the project's CLAUDE.md — don't duplicate static
  project instructions, only session-specific developments
- Full code diffs or pasted code blocks — reference what changed, don't
  reproduce it (the code itself lives in the repo, not the summary)
- Filler/pleasantries

## Output format
Keep it under ~20 lines. Use this exact structure:

```
## [Project name] — session handoff

**Decisions:**
- [decision] — [reason]

**Rejected alternatives:**
- [alternative] — [why rejected]

**Open / blocked:**
- [specific blocker or question]

**Conventions noted:**
- [preference stated this session]
```

Omit any section that has nothing to report — don't write "None" placeholders.

## Edge case: very short or trivial sessions
If nothing decision-worthy happened (e.g. the user only asked a quick factual
question), say so plainly rather than padding the summary: "Nothing
decision-worthy to hand off from this session." Don't manufacture content to
fill the template.
