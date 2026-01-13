---
description: Earn money answering questions with Ping - shows main menu
allowed-tools: mcp__ping__ping_login, mcp__ping__ping_welcome, mcp__ping__ping_answer_flow, mcp__ping__ping_check_earnings, mcp__ping__ping_claim_reward, mcp__ping__ping_create_question, mcp__ping__ping_my_questions
---

# Ping Main Menu

When the user runs /ping:start:

## Step 1: Show Welcome Banner

Call `ping_welcome` - this returns the complete ASCII art banner with auth status and stats already included.

**If the banner shows "❌ Not logged in":**
- Call `ping_login` immediately (opens browser for GitHub OAuth)
- After login completes, call `ping_welcome` again to show updated banner

**If logged in:**
- Continue to Step 2

## Step 2: Show Menu

Use AskUserQuestion:
- Header: "Ping"
- Question: "What would you like to do?"
- Options:
  1. "Answer questions" - Start earning by answering questions from other devs
  2. "Check balance" - See your earnings and claim to wallet
  3. "Create a question" - Pay others to answer your question
  4. "My questions" - View questions you've created

## Step 5: Execute Choice (NO extra confirmations)

Based on selection, execute IMMEDIATELY without asking for confirmation:

- "Answer questions" → Call `ping_answer_flow` and IMMEDIATELY show the questions. Do NOT ask "are you ready?" - they already said they want to answer questions.
- "Check balance" → Call `ping_check_earnings`, show balance, offer to claim if pending > $0
- "Create a question" → Ask for question text and reward amount, then call `ping_create_question`
- "My questions" → Call `ping_my_questions`, show list with response counts

**IMPORTANT:** Never add extra confirmation steps. When the user makes a choice, execute it directly.
