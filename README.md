# Ping Plugin for Claude Code

Earn money answering questions directly in Claude Code.

## Installation

### Option 1: From GitHub (Recommended)

```bash
# Add the Ping marketplace
claude plugin marketplace add https://github.com/ping-money/claude-plugin

# Install the plugin
claude plugin install ping@ping-plugins
```

### Option 2: From Local Directory

```bash
# Clone the repo
git clone https://github.com/ping-money/claude-plugin ~/ping-claude-plugin

# Add as local marketplace
claude plugin marketplace add ~/ping-claude-plugin

# Install the plugin
claude plugin install ping@ping-plugins
```

## Usage

Once installed:

- **`/ping:start`** - Open the Ping menu (slash command)
- Or just say **"ping"**, **"answer questions"**, **"earn money"** - Claude understands natural language too

The plugin teaches Claude to recognize Ping-related phrases and automatically use the right tools.

## What is Ping?

Ping is a Q&A platform where developers earn money by answering questions. Questions are created by other users who pay for quality answers.

### How it works:

1. **Login** with your GitHub account
2. **Answer questions** from the queue
3. **Earn rewards** for quality answers (AI-reviewed)
4. **Claim earnings** to your crypto wallet (USDC on Base)

## Plugin Contents

```
ping-claude-plugin/
├── .claude-plugin/
│   └── marketplace.json      # Marketplace manifest
├── ping/
│   ├── .claude-plugin/
│   │   └── plugin.json       # Plugin manifest + MCP server config
│   ├── skills/
│   │   └── ping.md           # Trigger keywords for discoverability
│   ├── commands/
│   │   └── start.md          # /ping:start slash command
│   └── CLAUDE.md             # Context injection
└── README.md
```

### What Each File Does:

| File | Purpose |
|------|---------|
| `marketplace.json` | Lets users add this repo as a plugin source |
| `plugin.json` | Configures the MCP server (`npx ping-mcp-server`) |
| `skills/ping.md` | Teaches Claude when to use Ping (trigger keywords) |
| `commands/start.md` | Defines `/ping:start` slash command |
| `CLAUDE.md` | Reminds Claude about Ping features every session |

## Troubleshooting

### "ping" command not recognized

1. Make sure the plugin is installed: `claude plugin install ping@ping-plugins`
2. Restart Claude Code to load the plugin
3. Try `/ping:start` (slash command) instead of "ping"

### MCP server fails to connect

1. Run `/mcp` to check server status
2. Make sure `npx` is available in your PATH
3. Try manually: `npx ping-mcp-server` to test

### Still having issues?

- Check MCP status: `/mcp`
- Reinstall: `claude plugin uninstall ping@ping-plugins && claude plugin install ping@ping-plugins`
- [Report an issue](https://github.com/ping-money/claude-plugin/issues)

## Development

To test changes locally:

```bash
# Make changes to files in ping/
# Changes hot-reload automatically in Claude Code
```

To validate the plugin:

```bash
claude plugin validate ~/ping-claude-plugin/ping
```

## Links

- [Ping Website](https://ping-money.com)
- [MCP Server on npm](https://www.npmjs.com/package/ping-mcp-server)
- [Report Issues](https://github.com/ping-money/claude-plugin/issues)

## License

MIT
