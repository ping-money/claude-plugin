---
description: Check your Ping balance and claim earnings
allowed-tools: mcp__ping__ping_login, mcp__ping__ping_whoami, mcp__ping__ping_check_earnings, mcp__ping__ping_claim_reward
---

# Ping - Check Balance

Show the user their current balance.

1. Check auth with `ping_whoami` (silent)
2. If not logged in → call `ping_login` first
3. Call `ping_check_earnings`
4. Display:
   - Available balance (ready to claim)
   - Pending balance (being processed)
   - Total claimed (lifetime)
5. If available > $0, ask: "Would you like to claim your earnings now?"
6. If yes → call `ping_claim_reward`
