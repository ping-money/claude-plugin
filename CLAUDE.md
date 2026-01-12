# Ping Claude Plugin

This repository contains the official Ping plugin for Claude Code.

## Repository Structure

```
ping-claude-plugin/
├── .claude-plugin/
│   └── marketplace.json      # Marketplace manifest (required for installation)
├── ping/                     # The actual plugin
│   ├── .claude-plugin/
│   │   └── plugin.json       # Plugin config + MCP server definition
│   ├── skills/
│   │   └── ping.md           # Trigger keywords for discoverability
│   ├── commands/
│   │   └── ping.md           # /ping slash command
│   └── CLAUDE.md             # Context injected into Claude sessions
└── README.md                 # User-facing documentation
```

## How Installation Works

### For Users

Users install in two steps:

```bash
# 1. Add this repo as a marketplace
claude plugin marketplace add https://github.com/ping-money/claude-plugin

# 2. Install the plugin from the marketplace
claude plugin install ping@ping-plugins
```

### Why Two Steps?

Claude Code's plugin system uses **marketplaces** as registries:
- A marketplace is a repo with `.claude-plugin/marketplace.json`
- The marketplace lists available plugins and where to find them
- Users add marketplaces, then install plugins from them

This repo serves as BOTH:
1. A **marketplace** (via `marketplace.json` at root)
2. A **plugin** (via the `ping/` subdirectory)

### Key Files Explained

| File | Purpose |
|------|---------|
| `marketplace.json` | Lists this repo's plugins; points to `./ping` |
| `ping/plugin.json` | Defines MCP server: `npx -y ping-mcp-server` |
| `ping/skills/ping.md` | **Critical for discoverability** - lists trigger phrases |
| `ping/commands/ping.md` | Defines `/ping` slash command |
| `ping/CLAUDE.md` | Context loaded every session |

## Development Workflow

### Testing Changes Locally

1. Make changes to files in `ping/`
2. Changes hot-reload automatically in Claude Code
3. Test with "ping login" or `/ping`

### Validating

```bash
claude plugin validate ~/ping-claude-plugin/ping
```

### Common Issues

**Plugin not recognized after changes:**
- Restart Claude Code session
- Check `/mcp` for MCP server status

**MCP server fails:**
- Test manually: `npx ping-mcp-server`
- Check that npm/npx are in PATH

## Updating the Plugin

When updating, remember:

1. **Adding trigger phrases**: Edit `ping/skills/ping.md` - add keywords to the `description` frontmatter
2. **Changing MCP server**: Edit `ping/.claude-plugin/plugin.json`
3. **Adding context**: Edit `ping/CLAUDE.md`
4. **Version bump**: Update version in `ping/.claude-plugin/plugin.json`

## Related Repositories

- **ping-mcp-server**: The actual MCP server (npm package)
- **ping-money.com**: Marketing site with installation instructions
