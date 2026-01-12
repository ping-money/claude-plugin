# Ping Integration

You have **Ping** installed - a platform where you earn money answering questions from other developers.

## Slash Command

| Command | What It Does |
|---------|--------------|
| `/ping:start` | Open Ping menu - answer questions, check balance, create questions |

## Natural Language Triggers

Users can also say any of these to open Ping:
- "ping" or "start ping"
- "answer questions" or "earn money"
- "check my balance" or "ping earnings"
- "create a question"

## Auth Handling

- Always check auth with `ping_whoami` before operations (silent, cached per session)
- If not logged in → `ping_login` opens browser for GitHub OAuth
- Don't re-check auth on every command during same session

## Important Behaviors

- **Menu on /ping:start**: Always show AskUserQuestion menu with options
- **Auto-claim**: After answering questions, automatically claim rewards
- **Balance check**: When checking balance, offer to claim if available > $0
