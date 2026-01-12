---
description: Create a question for others to answer (you pay the rewards)
allowed-tools: mcp__ping__ping_login, mcp__ping__ping_whoami, mcp__ping__ping_create_question, mcp__ping__ping_deposit
---

# Ping - Create Question

Help the user create a question others can answer for rewards.

1. Check auth with `ping_whoami` (silent)
2. If not logged in → call `ping_login` first
3. Ask for the question text (use AskUserQuestion with text input via "Other")
4. Ask for reward amount per answer (suggest $0.10, $0.25, $0.50, $1.00)
5. Ask for max responses (suggest 5, 10, 25)
6. Show cost breakdown: (reward × max responses) + 25% platform fee
7. Confirm before creating
8. Call `ping_create_question` with the details
