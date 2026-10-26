# CLAUDE.md

Working guidance for Claude Code. Not tied to one repo — these defaults apply anywhere.

## Principles

- **Match the surrounding code.** Follow the existing style, naming, and patterns
  before introducing your own. Prefer existing libraries/utilities over new dependencies.
- **Smallest change that works.** Solve the task that was asked; don't expand scope or
  refactor unrelated code without being asked.
- **Verify before you claim done.** Run the thing — tests, build, or the actual flow —
  and report the real output. If something fails or was skipped, say so plainly.
- **Be honest about gaps.** Surface what doesn't work or what you're unsure of rather
  than papering over it.
- **Act on sensible defaults; ask only when truly blocked.** Don't ask about choices you
  can make reasonably yourself; do ask when the answer changes the outcome.

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
