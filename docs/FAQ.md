# Ping FAQ

## Getting Started

### How do I install Ping?

One command:
```bash
claude plugin marketplace add https://github.com/ping-money/claude-plugin && claude plugin install ping@ping-plugins
```

### What can I say to use Ping?

Any of these work:
- "ping" or "/ping" - Start earning
- "ping login" or "login to ping" - Authenticate
- "answer questions" or "earn money" - Start Q&A flow
- "ping earnings" or "check my balance" - See earnings
- "ping claim" or "withdraw" - Claim to wallet

### Why does Claude need a plugin? Can't I just use the MCP server?

You can! Run `claude mcp add --transport stdio ping -- npx -y ping-mcp-server`

But the plugin is better because:
1. **Discoverability**: Claude recognizes "ping login" without you explaining what Ping is
2. **Slash command**: `/ping` provides an obvious entry point
3. **Context**: Claude remembers Ping features across sessions

---

## Troubleshooting

### Claude says "pong login" or doesn't understand "ping"

This happens when the plugin isn't installed. Install it:
```bash
claude plugin marketplace add https://github.com/ping-money/claude-plugin && claude plugin install ping@ping-plugins
```

Then restart Claude Code.

### I see "ping · x failed" in /mcp

The MCP server isn't connecting. Try:

1. **Restart Claude Code** - Exit and relaunch
2. **Test manually**: `npx ping-mcp-server` - does it start?
3. **Check npm**: Make sure `npx` is in your PATH
4. **Reinstall plugin**:
   ```bash
   claude plugin uninstall ping@ping-plugins
   claude plugin install ping@ping-plugins
   ```

### I installed via MCP (not plugin) and Claude doesn't recognize "ping login"

The MCP server provides the *tools*, but Claude doesn't know when to use them. The plugin adds a "skill" that teaches Claude to recognize trigger phrases.

**Solution**: Switch to the plugin method:
```bash
claude mcp remove ping  # Remove old MCP config
claude plugin marketplace add https://github.com/ping-money/claude-plugin
claude plugin install ping@ping-plugins
```

### How do I check if Ping is working?

In Claude Code, type `/mcp` to see MCP server status. You should see:
```
ping · ✓ connected
```

---

## Earnings & Payments

### How do I get paid?

1. Answer questions with `ping` or `/ping`
2. Check balance with "ping earnings"
3. Claim with "ping claim" - sends USDC to your wallet on Base

### What wallet do I need?

When you run `ping_login`, a wallet is automatically created for you. Your earnings go there and you can claim to any Ethereum-compatible wallet.

### How much can I earn?

Rewards vary by question - typically $0.10 to $1.00 per answer. Quality answers (reviewed by AI) are approved automatically.

---

## Technical

### What's the difference between marketplace and plugin?

- **Marketplace**: A directory/registry that lists available plugins (like an app store)
- **Plugin**: An actual extension that adds features to Claude Code

You add the marketplace once, then install plugins from it.

### Why do I need to add a marketplace first?

Claude Code's plugin system is designed for organizations to control what plugins their teams can use. Marketplaces are trusted sources.

For Ping, we bundle both in one repo - so adding the marketplace and installing the plugin is a one-liner.

### Can I contribute to Ping's Claude plugin?

Yes! The plugin is open source:
https://github.com/ping-money/claude-plugin

PRs welcome for:
- Better trigger phrases
- Improved documentation
- Bug fixes
