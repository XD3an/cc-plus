# cc-plus

my custom set of skills, commands, hooks, and plugin config for Claude Code.

## Getting Started

New to Claude Code? Install it with the official native installer ([docs](https://code.claude.com/docs/en/setup)):

```bash
# macOS, Linux, WSL
curl -fsSL https://claude.ai/install.sh | bash
```

```powershell
# Windows PowerShell
irm https://claude.ai/install.ps1 | iex
```

Then start a session from your project folder:

```bash
cd your-project
claude          # start an interactive session
```

Just talk to it — describe what you want ("add a login form", "find why the build is slow"), and Claude reads, edits, and runs code for you. Type `/help` any time to see available commands.

## Installation

### Option 1: Install as Plugin

The easiest way to use this collection - install as a Claude Code plugin:

```bash
# Add this repo as a marketplace
/plugin marketplace add XD3an/cc-plus

# Install the plugin
/plugin install cc-plus@cc-plus
```

Or add directly to your `~/.claude/settings.json`:

```json
{
  "enabledPlugins": {
    "cc-plus@cc-plus": true
  }
}
```

### Option 2: Manual Installation

If you prefer manual control over what's installed:

```bash
# Clone the repo
git clone https://github.com/<your-username>/cc-plus.git

# Copy commands
cp cc-plus/commands/**/*.md ~/.claude/commands/

# Copy skills
cp -r cc-plus/skills/* ~/.claude/skills/
```

#### Add Notifications

Desktop notifications come from the [`notify`](./mods/notify) mod: install it with `/plugin install notify@cc-plus`, or load it with `claude --plugin-dir path/to/cc-plus/mods/notify`.

#### Configure MCPs

Copy desired MCP servers from `.mcp.json` to your `~/.claude.json`.

**Important:** Some servers need credentials of their own — the `github` server reads a `GITHUB_PERSONAL_ACCESS_TOKEN`, and `notion` requires an OAuth authorization on first use. Supply these in your own config; `.mcp.json` ships without any secrets.

### Option 3: Use as Plugin Directory

```bash
claude --plugin-dir "path/to/cc-plus"
```

### Run with Docker

For a containerized deployment (isolated Linux environment with Claude Code pre-installed), see [README.docker.md](./README.docker.md) for detailed instructions.

## Usage

### What cc-plus adds

With the plugin installed ([see Installation](#installation)), four kinds of capability become available in every session:

| Surface | How you use it |
| --- | --- |
| **Skills** | Load automatically when relevant — e.g. ask for a chart, a `.docx`, or MCP-server help and the matching skill kicks in. You can also name one, e.g. "use the planning-with-files skill". |
| **Commands** | Type a slash command, e.g. `/do ...` or `/cc:create-command`. Type `/` to browse them. |
| **Subagents** | Delegate work to a named helper (see [Agents](#agents)), or let Claude pick one. |
| **Mods** | Background behaviors like desktop notifications (see [Mods](#mods)). |

If you're unsure what's available, just ask Claude in the session ("what skills/commands do I have?").

### Agents

`agents/` holds a delegation hierarchy modeled as a small company: a coordinator routes a goal to department agents, each department does its scoped work and reports back, and results are verified before they're accepted. **No agent performs outward actions** — anything bound for email, publishing, or an external system is produced as a draft for a human to send.

**Company (cross-function)** — use `/do` when a goal spans more than one department; it hands off to the coordinator:

```bash
/do research our top 3 competitors and draft a one-page summary
```

| Agent | Role |
| --- | --- |
| [`coordinator`](./agents/coordinator.md) | Routes a goal to departments, verifies and aggregates their results, and stops at a human approval gate before any outward action. Doesn't do the work itself. |
| [`researcher`](./agents/researcher.md) | Gathers and verifies information (web + repo), returns a sourced report. Read-only. |
| [`writer`](./agents/writer.md) | Drafts documents, content, and outbound messages — **drafts only**, never sends. |
| [`analyst`](./agents/analyst.md) | Analyzes data and reports findings. |

**Engineering squad** — the engineering department the coordinator delegates coding work to:

| Agent | Role |
| --- | --- |
| [`orchestrator`](./agents/orchestrator.md) | Decomposes an engineering goal into subtasks, delegates each to a worker, verifies results, and bounces failures back. Doesn't write code itself. |
| [`implementer`](./agents/implementer.md) | Implements one scoped coding subtask. |
| [`tester`](./agents/tester.md) | Writes and runs tests, reports objective evidence. |
| [`reviewer`](./agents/reviewer.md) | Read-only quality gate; returns a PASS/FAIL verdict. |

`/do` hands off to the coordinator, which fans the work out to the departments (in parallel where it can), verifies each result, and holds anything outbound as a draft for you to send.

### Mods

`mods/` holds Claude Code mods: plugins written as TypeScript function hooks (`hooks/hooks.json` → `{ "modules": ["./register.ts"] }`). Each mod is a separate plugin in this marketplace, so you can install, disable, or break one without touching the others.

| Mod | What it does |
| --- | --- |
| [`notify`](./mods/notify) | Notifications when a session starts, a long turn finishes, a tool fails, or Claude asks for permission. On Windows, an animated popup with a little Claude buddy (built-in WPF); on macOS `osascript`, on Linux `notify-send`. Nothing extra to install. |

```bash
/plugin install notify@cc-plus
```

While developing a mod, load it straight from disk so every save hot-reloads it:

```bash
claude --plugin-dir ./mods/notify
claude plugin validate ./mods/notify
claude plugin test ./mods/notify
```

> Mods are an early-access Claude Code surface and the API may change between releases.

## Structure

```
cc-plus/
├── .claude-plugin/             # Plugin metadata (plugin.json, marketplace.json)
├── agents/                     # Custom subagents
├── commands/                   # Custom commands
├── examples/                   # Reference files (e.g. settings.json for manual installs)
├── mods/                       # Function-hook mods, each its own plugin in the marketplace
├── resources/                  # Reference material: example CLAUDE.md files, slash-commands, workflow guides
├── scripts/                    # Standalone utility scripts (model switching, litellm proxy)
├── skills/                     # Custom skills
├── themes/                     # Custom color themes
├── .dockerignore
├── .env.example
├── .gitignore
├── .mcp.json
├── docker-compose.yml
├── Dockerfile
├── LICENCE
├── README.docker.md
└── README.md
```

## Configuration

Copy `.env.example` to `.env` and configure your settings:

```bash
cp .env.example .env
```

For manual installs, start from [`examples/settings.json`](./examples/settings.json) and adjust `enabledPlugins`/`hooks` to taste.

## Resources

### Official Documentation

- [Claude Code Docs](https://code.claude.com/docs/en/overview) - Official documentation
- [Claude Code Skills](https://github.com/anthropics/skills/tree/main/skills) - Official skills repository
- [Claude Code Plugins](https://github.com/anthropics/claude-code/tree/main/plugins) - Official plugins

> The document skills (`docx`, `pdf`, `pptx`, `xlsx`) are not redistributed here: they are under Anthropic's proprietary license. Get them from the official [anthropics/skills](https://github.com/anthropics/skills) repo or the `document-skills` plugin.

### Community Resources

- [awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code) - Claude Code workflows, slash-commands, and templates
- [superpowers-claude-code](https://github.com/obra/superpowers-claude-code) - Superpowers for Claude Code
- [compound-engineering-plugin](https://github.com/EveryInc/compound-engineering-plugin) - Compound Engineering Plugin for Claude Code

### Recommended Plugins

cc-plus pairs well with these plugins. They're not required and aren't installed for you — add them if you want the extra capabilities:

- [humanizer](https://github.com/blader/humanizer) - removes AI-writing tells from text
- [impeccable](https://github.com/pbakaus/impeccable) - frontend design fluency: `/impeccable polish`, `audit`, `critique`, ...
- [notify](./mods/notify) - desktop notifications, from this marketplace (`/plugin install notify@cc-plus`)

To install the external ones, add their marketplaces first, then install:

```bash
/plugin marketplace add blader/humanizer
/plugin marketplace add pbakaus/impeccable
/plugin install humanizer@humanizer
/plugin install impeccable@impeccable
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

See [LICENCE](./LICENCE) for details.
