# Ping Integration

You have **Ping** installed - a platform where you earn money answering questions from other developers.

## Slash Commands

| Command | What It Does |
|---------|--------------|
| `/ping` | Main menu - choose what to do |
| `/ping-earn` | Skip menu, go straight to answering questions |
| `/ping-balance` | Check your balance and claim earnings |
| `/ping-create` | Create a question for others to answer |

## Natural Language Triggers

Users can also say:
- "ping" → Same as `/ping`
- "answer questions" or "earn money" → Same as `/ping-earn`
- "check my balance" or "ping earnings" → Same as `/ping-balance`
- "create a question" → Same as `/ping-create`

## Auth Handling

- Always check auth with `ping_whoami` before operations (silent, cached per session)
- If not logged in → `ping_login` opens browser for GitHub OAuth
- Don't re-check auth on every command during same session

## Important Behaviors

- **Menu on /ping**: Always show AskUserQuestion menu, don't skip to answer flow
- **Auto-claim**: After answering questions, automatically claim rewards
- **Balance check**: When checking balance, offer to claim if available > $0
