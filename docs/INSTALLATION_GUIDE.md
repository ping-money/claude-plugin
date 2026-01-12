# Installing Ping for Claude Code

Ping lets you earn money answering questions directly in Claude Code.

## Quick Install (One Command)

Copy and paste this into your terminal:

```bash
claude plugin marketplace add https://github.com/ping-money/claude-plugin && claude plugin install ping@ping-plugins
```

That's it! Now open Claude Code and say **"ping"** to start earning.

---

## Step-by-Step Installation

If you prefer to understand what's happening:

### Step 1: Add the Ping Marketplace

```bash
claude plugin marketplace add https://github.com/ping-money/claude-plugin
```

This tells Claude Code where to find Ping plugins.

### Step 2: Install the Plugin

```bash
claude plugin install ping@ping-plugins
```

This installs Ping with:
- MCP server connection (talks to Ping's API)
- Trigger keywords (Claude recognizes "ping login", "earn money", etc.)
- `/ping` slash command

### Step 3: Start Using Ping

Open Claude Code and try:
- **"ping"** - Start answering questions
- **"ping login"** - Authenticate with GitHub
- **"/ping"** - Same as above, using slash command

---

## Troubleshooting

### "Command not found: claude"

Make sure Claude Code CLI is installed:
```bash
npm install -g @anthropic/claude-code
```

### Plugin not working after install

1. Restart Claude Code (`/exit` then relaunch)
2. Check MCP status: type `/mcp` in Claude Code
3. Reinstall:
   ```bash
   claude plugin uninstall ping@ping-plugins
   claude plugin install ping@ping-plugins
   ```

### MCP server fails to connect

1. Make sure npm/npx are installed and in your PATH
2. Test manually: `npx ping-mcp-server`
3. If that fails, [report an issue](https://github.com/ping-money/claude-plugin/issues)

---

## Uninstalling

```bash
claude plugin uninstall ping@ping-plugins
claude plugin marketplace remove ping-plugins
```

---

## Alternative: Manual MCP Setup

If you prefer not to use the plugin system, you can add Ping as an MCP server directly:

```bash
claude mcp add --transport stdio ping -- npx -y ping-mcp-server
```

Note: This method works but Claude won't automatically recognize phrases like "ping login" - you'll need to explicitly ask Claude to use the ping tools.
