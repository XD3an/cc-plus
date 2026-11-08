# CLAUDE.md

Working guidance for Claude Code. Not tied to one repo — these defaults apply anywhere.

## Principles

Four principles, adapted from
[andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills) (MIT).
Every cc-plus agent follows them.

1. **Think before you act.** State your assumptions. If the task can be read more than
   one way, or a simpler approach would do, say so and ask before starting. Don't ask
   about choices you can reasonably make yourself.
2. **Simplicity first.** Do what was asked and nothing more: no features, abstractions,
   or configuration nobody requested. If 200 lines could be 50, write 50.
3. **Surgical changes.** Touch only what the task needs and match the existing style.
   Prefer existing libraries and utilities over new dependencies. Clean up only what your
   own change made unused; mention unrelated problems instead of fixing them. Every
   changed line should trace to the request.
4. **Goal-driven, verified.** Turn the task into checkable criteria, then loop until
   they pass. For a bug, reproduce it first. Report the real output, say plainly what
   failed or was skipped, and never claim done without evidence.

For trivial tasks, use judgment: not every one-line fix needs the full process.

## Safety

- Never commit secrets. Keep credentials in env/config, not in source.
- Confirm before hard-to-reverse or outward-facing actions (deletes, pushes, publishing).
- Don't delete or overwrite something you didn't create without looking at it first.

## Commits

- Conventional Commits with a scope: `feat(x): ...`, `fix(x): ...`, `chore(x): ...`;
  append `!` for breaking changes. One-line subject, imperative mood.
- Commit or push only when asked.

## Keep this file lean

Add a project-specific section only when a convention isn't obvious from the code
itself. If the code already shows it, don't document it here.
