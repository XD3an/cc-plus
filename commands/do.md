---
description: Run a goal end to end. Small changes are done directly; larger goals go to the coordinator, which routes them to department agents and verifies the results.
argument-hint: "[goal]"
---

# Do

**Goal:** $ARGUMENTS

1. Read only the code you need, then write 1-3 checkable completion criteria. If the
   goal can be read more than one way, ask before starting. If a simpler approach
   would do, say so.
2. If the work touches a core area, stop and ask before changing anything, however
   small the change. Core areas are payments, billing, auth, permissions, secrets,
   database migrations, deployment, and anything the project's `CLAUDE.md` lists.
3. If it is a small, clear code change in a few files, do it yourself here without
   subagents. For a bug, reproduce it first with a failing test or command. Change only
   what the goal needs and match the existing style; mention unrelated problems instead
   of fixing them. Then run the relevant tests.
4. Otherwise, hand the goal and the criteria to the `coordinator` subagent.
5. Report in the user's language: each criterion with its evidence, what changed, and what was not tested. If
   nothing could be run, say the work is unverified. Never call it done without evidence.
