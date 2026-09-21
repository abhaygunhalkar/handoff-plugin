# handoff

Carry your Claude Code project context into a separate Claude Desktop or
Claude.ai chat — without re-explaining your architecture, decisions, and
open issues from scratch every time you switch windows.

## The problem this solves

Claude Code's project memory and Claude.ai's conversation memory are
separate systems — they don't share context with each other. If you've been
working through a problem in Claude Code and then switch to a Claude
Desktop chat to keep thinking it through, ask a side question, or plan next
steps, that chat starts with no idea what you just did.

`handoff` closes that gap with a two-second copy-paste instead of a
five-minute re-explanation.

## What it does

- **`/handoff`** — generates a curated summary of your current Claude Code
  session: decisions made (with the reasoning behind them), alternatives
  that were considered and rejected, open blockers, and any conventions you
  stated along the way. Prints it in the chat, ready to copy, and also
  writes it to `.ai-context/handoff.md` in your project.
- **Automatic session-end reminder** — a hook nudges you to run `/handoff`
  when a session ends, so it doesn't rely on remembering to do it.
- **A consistent format, every time** — instead of a generic "summarize
  this conversation" (which varies in what it captures run to run), the
  summary always follows the same rubric: decisions + reasoning, rejected
  alternatives, open blockers, stated conventions. Nothing else.

## Installation

```
/plugin marketplace add YOUR_GITHUB_USERNAME/handoff-plugin
/plugin install handoff@handoff-marketplace
```

Choose **user scope** when prompted, so it's available across all your
projects, not just one repo.

## Usage

1. Work in Claude Code as normal.
2. At any point — mid-session or right before you're about to switch to
   another Claude window — run:
   ```
   /handoff
   ```
3. Copy the printed summary.
4. Paste it into your Claude Desktop or Claude.ai chat. That conversation
   now has the context it needs to reason about your project correctly,
   without you re-explaining anything.

You don't need to do anything special to trigger the automatic reminder —
it fires on its own when a Claude Code session ends.

## Example

```
/handoff

## invoice-parser — session handoff

**Decisions:**
- Using SQLite instead of Postgres — small local tool, no need for a server

**Rejected alternatives:**
- Considered Postgres — overkill for single-user local use

**Open / blocked:**
- Not yet decided how to handle partial-failure retries on OCR calls

**Conventions noted:**
- All market data flows through the backend, never fetched directly from
  the frontend
```

Paste that into Claude Desktop, and it now knows exactly where things stand
— including *why* SQLite was chosen, not just that it was.

## Requirements

- Claude Code (any recent version — built and tested against version
  2.1.x-era CLI syntax; if `/plugin` commands behave differently for you,
  check your installed version against the current
  [Claude Code plugin docs](https://code.claude.com/docs/en/plugins))

## What this doesn't do

- It does not automatically sync context — you still paste it yourself.
  There's no live connection between Claude Code and Claude Desktop/Claude.ai.
- It does not read your files for you on the Claude Desktop/Claude.ai side.
  If you've set up a Filesystem connector pointed at your project, Claude
  Desktop can read `.ai-context/handoff.md` directly instead of you pasting
  — but that requires that connector to already be configured; it's not
  part of what this plugin sets up for you.

## License

MIT — see [LICENSE](LICENSE) for details.
