# handoff (v0.1.0 — local testing build)

Generates a curated session summary in Claude Code (decisions, rejected
alternatives, open blockers) so you can bring context into a separate Claude
Desktop / Claude.ai chat without re-explaining your project.

## What's in this package
```
handoff-plugin/
├── .claude-plugin/
│   └── plugin.json
├── commands/
│   └── handoff.md
├── hooks/
│   └── hooks.json          (unverified — see comment inside)
└── skills/
    └── handoff-writing/
        └── SKILL.md
```

## Install for local testing (no marketplace needed)
1. Copy this whole `handoff-plugin/` folder somewhere on your machine — it
   does NOT need to be inside the project you're testing it on.
2. In your terminal:
   ```
   claude plugin marketplace add ./path/to/handoff-plugin --local
   ```
   (If your Claude Code version doesn't support `--local` folder installs,
   see the official plugin docs for the current local-dev install method —
   this has been known to change between versions.)
3. Restart Claude Code, or run `/reload-plugins` if that command is available
   in your version.
4. Run `/plugin` to confirm `handoff` shows up as installed.

## Test plan (do these in order)
1. Open a real project in Claude Code, have a short back-and-forth that
   includes at least one real decision (e.g. "let's use library X because Y").
2. Run `/handoff`. Confirm:
   - It prints a summary in chat
   - It creates `.ai-context/handoff.md` in your project root
   - The summary actually reflects the rubric (decision + reason captured,
     not just a generic recap)
3. Open that `.ai-context/handoff.md` file manually and check it's readable,
   sensible markdown.
4. Paste the printed chat summary into a separate Claude Desktop/Claude.ai
   chat. Confirm it reads naturally and Claude picks up the context.
5. Let a session end naturally (exit Claude Code). Check whether the
   `SessionEnd` hook message actually appears. If it doesn't fire at all,
   that's useful to know — note it and we'll adjust the hook config.
6. (Optional, only if you've set up a Filesystem connector in Claude Desktop
   pointed at this project folder) Ask Claude Desktop to read
   `.ai-context/handoff.md` directly and confirm it can.

## Known unverified pieces — flag these back
- Whether `SessionEnd` hooks can do more than print a message (e.g. actually
  prompt interactively) — untested assumption, built conservatively for now.
- Exact current syntax for local/unpublished plugin installs — verify against
  your installed Claude Code version's docs if step 2 above doesn't work as
  written.
