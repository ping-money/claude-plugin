---
description: Earn money answering questions with Ping - shows main menu
allowed-tools: mcp__ping__ping_login, mcp__ping__ping_whoami, mcp__ping__ping_answer_flow, mcp__ping__ping_check_earnings, mcp__ping__ping_claim_reward, mcp__ping__ping_create_question, mcp__ping__ping_my_questions
---

# Ping Main Menu

When the user runs /ping:

## Step 1: Check Auth (Silent, Cached)

Call `ping_whoami` to check login status. Cache this for the session - don't re-check on subsequent /ping calls unless user explicitly logs out.

## Step 2: Handle Auth

**If NOT logged in:**
- Tell user: "You need to login to use Ping."
- Call `ping_login` immediately (opens browser for GitHub OAuth)
- After login completes, continue to Step 3

**If logged in:**
- Continue to Step 3

## Step 3: Show Menu

Use AskUserQuestion:
- Header: "Ping"
- Question: "What would you like to do?"
- Options:
  1. "Answer questions" - Start earning by answering questions from other devs
  2. "Check balance" - See your earnings and claim to wallet
  3. "Create a question" - Pay others to answer your question
  4. "My questions" - View questions you've created

## Step 4: Execute Choice

Based on selection:
- "Answer questions" → Call `ping_answer_flow`, present questions via AskUserQuestion
- "Check balance" → Call `ping_check_earnings`, show balance, offer to claim if pending > $0
- "Create a question" → Ask for question text and reward amount, then call `ping_create_question`
- "My questions" → Call `ping_my_questions`, show list with response counts
