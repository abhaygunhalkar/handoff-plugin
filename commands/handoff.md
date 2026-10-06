---
description: Generate a curated handoff summary of this session and write it to .ai-context/handoff.md
---

Use the handoff-writing skill to produce a session handoff summary right now.

Steps:
1. Review the conversation so far in this session.
2. Apply the handoff-writing skill's rubric to decide what belongs in the summary (decisions + reasoning, rejected alternatives, open blockers/questions) and what to leave out (routine back-and-forth, resolved trivial issues).
3. If nothing in the session meets the rubric (no decisions, rejected alternatives, open blockers, or stated conventions), do NOT create or modify any file. Print exactly one line: "Nothing to hand off from this session — existing .ai-context/handoff.md (if any) left untouched." and stop.
4. Otherwise, create the directory `.ai-context/` in the project root if it doesn't already exist.
5. Write the summary to `.ai-context/handoff.md`, overwriting any previous version.
6. Also print the summary back to the user in the chat, so it can be copy-pasted immediately even if the file-based route isn't set up.
7. After writing, tell the user the file path, and remind them that pasting the printed summary into a Claude Desktop/Claude.ai chat is the reliable way to bring this context over, and that reading the file directly only works if they've configured a Filesystem connector pointed at this project.
