---
description: Earn money answering questions with Ping - shows main menu
allowed-tools: mcp__ping__ping_login, mcp__ping__ping_whoami, mcp__ping__ping_stats, mcp__ping__ping_answer_flow, mcp__ping__ping_check_earnings, mcp__ping__ping_claim_reward, mcp__ping__ping_create_question, mcp__ping__ping_my_questions
---

# Ping Main Menu

When the user runs /ping:start:

## Step 1: Check Auth & Get Stats (Parallel)

Call these two tools IN PARALLEL:
- `ping_whoami` - Check login status
- `ping_stats` - Get platform stats for the banner

## Step 2: Handle Auth

**If NOT logged in:**
- Tell user: "You need to login to use Ping."
- Call `ping_login` immediately (opens browser for GitHub OAuth)
- After login completes, call `ping_stats` and continue to Step 3

**If logged in:**
- Continue to Step 3

## Step 3: Show Welcome Banner

Display this ASCII art banner with the stats from `ping_stats`:

```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃                                                      ┃
┃   ██████╗ ██╗███╗   ██╗ ██████╗                      ┃
┃   ██╔══██╗██║████╗  ██║██╔════╝                      ┃
┃   ██████╔╝██║██╔██╗ ██║██║  ███╗                     ┃
┃   ██╔═══╝ ██║██║╚██╗██║██║   ██║                     ┃
┃   ██║     ██║██║ ╚████║╚██████╔╝                     ┃
┃   ╚═╝     ╚═╝╚═╝  ╚═══╝ ╚═════╝                      ┃
┃                                                      ┃
┃         💰 Get paid to share your knowledge          ┃
┃                                                      ┃
┣━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┫
┃                                                      ┃
┃   📊 Today on Ping                                   ┃
┃   ─────────────────                                  ┃
┃   🏆 {answersToday} answers submitted                ┃
┃   💵 {claimedToday} in rewards claimed               ┃
┃                                                      ┃
┃   📬 {questionsAvailable} questions waiting for you  ┃
┃                                                      ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

Replace the placeholders with actual stats:
- `{answersToday}` → stats.answersToday
- `{claimedToday}` → stats.rewardsClaimedToday
- `{questionsAvailable}` → stats.questionsAvailable

If stats show 0 for everything, use encouraging defaults like "Be the first today!"

## Step 4: Show Menu

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
