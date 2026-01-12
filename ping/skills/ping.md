---
name: ping
description: Earn money answering questions in Claude Code. Use when someone says "ping", "/ping", "answer questions", "earn money", "check my earnings", "create a question", "login to ping", "ping login", "sign in to ping", "connect to ping", "start using ping", or wants to interact with the Ping Q&A platform.
---

# Ping - Earn Money Answering Questions

Ping is a Q&A platform where users earn money by answering questions from other developers.

## Getting Started

1. **First, check if logged in**: Use `ping_whoami` to see current auth status
2. **If not logged in**: Use `ping_login` to authenticate with GitHub (opens browser)
3. **Start earning**: Use `ping_answer_flow` to begin answering questions

## Available Tools

### Authentication
| Tool | Description |
|------|-------------|
| `ping_login` | Login with GitHub OAuth - opens browser for authentication |
| `ping_whoami` | Check current login status, wallet address, and balance |
| `ping_logout` | Sign out of Ping |

### Earning Money
| Tool | Description |
|------|-------------|
| `ping_answer_flow` | **Start here!** Interactive Q&A session to earn money |
| `ping_list_questions` | See available questions with rewards |
| `ping_submit_answer` | Submit an answer to a specific question |
| `ping_check_earnings` | Check pending balance and total claimed |
| `ping_claim_reward` | Claim pending earnings to your wallet |

### Creating Questions
| Tool | Description |
|------|-------------|
| `ping_create_question` | Create a question others can answer for rewards |
| `ping_my_questions` | View questions you've created |
| `ping_view_responses` | See answers to your questions |
| `ping_close_question` | Close a question and refund unused funds |
| `ping_deposit` | Add funds to create more questions |

## Common Workflows

### "I want to earn money"
1. `ping_login` (if not authenticated)
2. `ping_answer_flow` to start answering questions
3. `ping_claim_reward` to withdraw earnings

### "Check my balance"
1. `ping_check_earnings` shows pending and claimed amounts

### "I want to ask questions"
1. `ping_login` (if not authenticated)
2. `ping_deposit` to add funds
3. `ping_create_question` with reward amount
4. `ping_view_responses` to see answers
