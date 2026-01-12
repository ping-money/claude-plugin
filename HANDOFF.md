# Ping Plugin Handoff Document

**Created:** 2026-01-12
**Purpose:** Context preservation before auto-compact

---

## What We Built

A **Claude Code plugin** for Ping that makes onboarding easier. Located at:
```
~/ping-claude-plugin/
```

### Plugin Structure
```
ping-claude-plugin/
├── .claude-plugin/
│   └── marketplace.json      # Marketplace manifest
├── ping/                     # The actual plugin
│   ├── .claude-plugin/
│   │   └── plugin.json       # MCP server config
│   ├── commands/             # Slash commands
│   │   ├── ping.md           # /ping - main menu
│   │   ├── ping-earn.md      # /ping-earn
│   │   ├── ping-balance.md   # /ping-balance
│   │   └── ping-create.md    # /ping-create
│   ├── skills/
│   │   └── ping.md           # Natural language triggers
│   └── CLAUDE.md             # Session context
├── docs/
│   ├── INSTALLATION_GUIDE.md
│   └── FAQ.md
├── CLAUDE.md                 # Dev docs for this repo
└── README.md
```

### Installation (for users)
```bash
claude plugin marketplace add https://github.com/ping-money/claude-plugin && claude plugin install ping@ping-plugins
```

---

## The Problem We Found

### Root Cause of MCP Failures

In `/Users/brianflynn/projects/ping/packages/mcp-server/package.json`:

```json
"bin": {
  "ping-mcp-server": "./dist/init.js",   // ← WRONG! Runs wizard
  "ping-mcp": "./dist/index.js",          // ← This is the actual server
  "ping-init": "./dist/init.js"
}
```

When Claude Code runs `npx ping-mcp-server`, it gets the **setup wizard** (init.js) which:
1. Shows a banner
2. Asks "Add Ping MCP server to Claude Code? (y/n)"
3. Waits for user input

Claude Code can't answer interactive prompts, so it hangs forever and fails.

### The Fix (Not Yet Applied)

Change package.json to:
```json
"bin": {
  "ping-mcp-server": "./dist/index.js",  // ← Server (what users expect)
  "ping-init": "./dist/init.js"           // ← Wizard (only when needed)
}
```

**File to edit:** `/Users/brianflynn/projects/ping/packages/mcp-server/package.json`

---

## What's Done

- [x] Created plugin directory structure
- [x] Created marketplace.json
- [x] Created plugin.json with MCP server config
- [x] Created slash commands (/ping, /ping-earn, /ping-balance, /ping-create)
- [x] Created skill with trigger keywords
- [x] Created CLAUDE.md context files
- [x] Created documentation (README, FAQ, Installation Guide)
- [x] Plugin installs successfully locally
- [x] Identified root cause of MCP server failures

---

## What's Left To Do

1. **Fix MCP server binary naming** (in ping repo)
   - Edit: `/Users/brianflynn/projects/ping/packages/mcp-server/package.json`
   - Change `ping-mcp-server` to point to `./dist/index.js` (not init.js)
   - Rebuild and publish new version to npm

2. **Push plugin to GitHub**
   - Create repo: `ping-money/claude-plugin`
   - Push `~/ping-claude-plugin/` contents

3. **Update ping-money.com**
   - Replace MCP install instructions with plugin install command

4. **Test end-to-end**
   - Fresh Claude Code session
   - Install plugin from GitHub
   - Verify `/ping` shows menu
   - Verify MCP tools work

---

## Key Files Reference

| File | Purpose |
|------|---------|
| `~/ping-claude-plugin/` | The plugin we're building |
| `/Users/brianflynn/projects/ping/packages/mcp-server/` | The MCP server source code |
| `/Users/brianflynn/projects/ping/packages/mcp-server/package.json` | **NEEDS EDIT** - fix bin mapping |
| `/Users/brianflynn/projects/ping/packages/mcp-server/src/index.ts` | Actual MCP server |
| `/Users/brianflynn/projects/ping/packages/mcp-server/src/init.ts` | Setup wizard (problematic) |

---

## Commands to Resume

After compact, run these to continue:

```bash
# 1. Fix the MCP server (edit package.json as described above)

# 2. Rebuild MCP server
cd /Users/brianflynn/projects/ping/packages/mcp-server
pnpm build

# 3. Publish to npm (if you have access)
npm publish

# 4. Push plugin to GitHub
cd ~/ping-claude-plugin
git init
git add .
git commit -m "Initial ping plugin for Claude Code"
# Then create repo on GitHub and push
```

---

## User Context

- Brian is non-technical - explain things simply
- "Learning Mode" is enabled in his ~/.claude/CLAUDE.md
- He wants Claude to challenge decisions and explain the "why"
