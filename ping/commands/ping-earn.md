---
description: Start answering questions and earning money immediately
allowed-tools: mcp__ping__ping_login, mcp__ping__ping_whoami, mcp__ping__ping_answer_flow, mcp__ping__ping_claim_reward
---

# Ping - Answer Questions

Skip the menu and go straight to earning.

1. Check auth with `ping_whoami` (silent)
2. If not logged in → call `ping_login` first
3. Call `ping_answer_flow` to get questions
4. Present questions via AskUserQuestion
5. Submit answers and auto-claim rewards
