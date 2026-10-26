# CLAUDE.md

Guidance for Claude Code when working in this repository.

## What this is

`cc-plus` is a Claude Code **plugin** (and marketplace) that bundles custom skills,
commands, subagents, mods, and reference config. It is distributed, not run: there is
no build or test suite for the repo as a whole — each surface is consumed directly by
Claude Code.

## Layout

- `.claude-plugin/` — `plugin.json` (the cc-plus plugin manifest) and `marketplace.json`
  (lists every plugin in this marketplace: `cc-plus` and `notify`).
- `agents/` — custom subagents (currently a placeholder kept via `.gitkeep`).
- `commands/` — slash commands as Markdown with YAML frontmatter
  (`description`, `argument-hint`, `allowed-tools`).
- `skills/` — skills, each a folder with a `SKILL.md` whose frontmatter needs `name` + `description`.
- `mods/` — function-hook mods; each subfolder is its **own plugin** in the marketplace.
- `resources/` — reference material (example CLAUDE.md files, slash-commands, guides). Vendored; don't treat as source of truth for this repo.
- `scripts/` — standalone PowerShell utilities.
- `themes/` — custom color themes (placeholder kept via `.gitkeep`).
- `examples/` — reference config for manual installs (`settings.json`, `statusline.json`).

## Conventions

- **Keep the manifests in sync.** Every plugin under `mods/` must have a matching entry
  in `.claude-plugin/marketplace.json`. The source paths there must point at real folders.
- **Mods are separate plugins.** A mod is `hooks/hooks.json` → `{ "modules": ["./register.ts"] }`
  plus its own `.claude-plugin/plugin.json`. Install/disable one without touching the others.
- **All JSON must stay valid.** After editing any `*.json`, parse it to confirm
  (e.g. `node -e "JSON.parse(require('fs').readFileSync('<file>','utf8'))"`).
- **Dependencies are recommendations, not hard deps.** cc-plus intentionally does **not**
  declare plugin `dependencies`; optional companions (humanizer, impeccable, notify) are
  listed under "Recommended Plugins" in the README. Don't re-add a `dependencies` array or
  `allowCrossMarketplaceDependenciesOn` without a reason.
- **Don't vendor proprietary skills.** The Anthropic document skills (`docx`, `pdf`,
  `pptx`, `xlsx`) are not redistributed here by license — keep it that way.

## Validating a mod

```bash
claude plugin validate ./mods/notify
claude plugin test ./mods/notify
```

## Commits

Conventional Commits with a scope, e.g. `feat(notify): ...`, `fix(docker): ...`,
`chore(plugin): ...`; append `!` for breaking changes. Keep the subject one line.

> Shell note: this repo is developed on Windows. For multi-line commit messages use the
> shell's own heredoc syntax — `@'...'@` is PowerShell-only and will corrupt the message
> if passed through bash.
