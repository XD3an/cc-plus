# cc-plus

- [claude-code docs](https://code.claude.com/docs/en/overview)

- [awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code)：Claude Code workflows, slash-commands, and templates

- [claude-code-skills](https://github.com/anthropics/skills/tree/main/skills)

- [claude-code-plugin](https://github.com/anthropics/claude-code/tree/main/plugins)

- community plugins, skills, and commands:

  - [everything-claude-code](https://github.com/affaan-m/everything-claude-code): Battle-tested configs from an Anthropic hackathon winner.

  - [superpowers-claude-code](https://github.com/obra/superpowers-claude-code): Superpowers for Claude Code.

  - [compound-engineering-plugin](https://github.com/EveryInc/compound-engineering-plugin): Compound Engineering Plugin for Claude Code.

## Structure

```
cc-plus/
├── .claude-plugin/             # Plugin metadata
├── agents/                     # Custom agents
├── commands/                   # Custom commands
├── contexts/                   # Context definitions
├── examples/                   # Example files
├── hooks/                      # Custom hooks
├── resources/                  # Documentation and resources
├── rules/                      # Coding rules and guidelines
├── skills/                     # Custom skills
├── .dockerignore
├── .env.example
├── .gitignore
├── .mcp.json
├── docker-compose.yml
├── Dockerfile
├── LICENCE
├── README.docker.md
├── README.md
└── settings.json
```

## Usage

```bash
claude --plugin-dir "path/to/cc-plus"
```

### Run with Docker

- reference [README.docker.md](./README.docker.md)
