# Boris Cherny's Claude Code Setup (Twitter Thread)

**Source**: https://x.com/bcherny/status/2007179832300581177
**Author**: Boris Cherny (@bcherny) - Claude Code creator
**Date**: January 2, 2026
**Type**: Official (from Claude Code team member)

## Context

Boris Cherny, who created Claude Code, shared his personal setup and workflow. He notes that "there is no one correct way to use Claude Code" and that each person on the Claude Code team uses it "very differently." His setup is "surprisingly vanilla" - Claude Code works great out of the box.

## Key Practices

### 1. Parallel Sessions
- Runs 5 Claudes in parallel in terminal (tabs numbered 1-5)
- Uses system notifications to know when Claude needs input (iTerm2 config)
- Also runs 5-10 Claudes on claude.ai/code in parallel with local sessions
- Hands off local sessions to web (using &) or vice versa
- Starts sessions from phone (Claude iOS app) morning and throughout day

**Reference**: [Terminal notifications config](https://code.claude.com/docs/en/terminal-config#iterm-2-system-notifications)

### 2. Model Choice
- Uses **Opus 4.5 with thinking for everything**
- Rationale: "It's the best coding model I've ever used"
- Even though bigger & slower than Sonnet, requires less steering
- Better at tool use, so "almost always faster than using a smaller model in the end"

### 3. Shared CLAUDE.md
- Team shares a single CLAUDE.md for the Claude Code repo
- Checked into git, whole team contributes multiple times a week
- **Key practice**: "Anytime we see Claude do something incorrectly we add it to the CLAUDE.md, so Claude knows not to do it next time"
- Other teams maintain their own CLAUDE.md files - each team's job to keep theirs up to date

### 4. GitHub Action for CLAUDE.md Updates
- Tags @claude on coworkers' PRs to add something to CLAUDE.md as part of PR
- Uses Claude Code GitHub action (`/install-github-action`)
- Calls this their version of "Compounding Engineering" (referencing @danshipper)

### 5. Plan Mode First
- Most sessions start in Plan mode (shift+tab twice)
- Goes back and forth with Claude until plan looks good
- Then switches to auto-accept edits mode
- "Claude can usually 1-shot it. A good plan is really [important]"

### 6. Slash Commands for Inner Loops
- Creates slash commands for every "inner loop" workflow done many times a day
- Example: `/commit-push-pr` - uses inline bash to pre-compute git status
- Commands checked into git and live in `.claude/commands/`
- Philosophy: saves from repeated prompting, makes workflows usable by Claude too

**Reference**: [Slash commands with bash](https://code.claude.com/docs/en/slash-commands#bash-command-execution)

### 7. Custom Subagents
- Uses subagents regularly for common workflows
- Examples from his `.claude/agents/` folder:
  - `build-validator.md`
  - `code-architect.md`
  - `code-simplifier.md` - simplifies code after Claude is done
  - `oncall-guide.md`
  - `verify-app.md` - detailed instructions for testing Claude Code end to end
- Thinks of subagents as "automating the most common workflows that I do for most PRs"

**Reference**: [Sub-agents documentation](https://code.claude.com/docs/en/sub-agents)

### 8. PostToolUse Hook for Formatting
- Uses PostToolUse hook to format Claude's code
- Claude generates well-formatted code ~90% of the time
- Hook handles the last 10% to avoid formatting errors in CI

```json
{
  "PostToolUse": [
    {
      "matcher": "Write|Edit",
      "hooks": [
        {
          "type": "command",
          "command": "bun run format || true"
        }
      ]
    }
  ]
}
```

### 9. Permissions Over Dangerously-Skip
- Does NOT use `--dangerously-skip-permissions`
- Instead uses `/permissions` to pre-allow common safe bash commands
- Most permissions checked into `.claude/settings.json` and shared with team
- Avoids unnecessary permission prompts while maintaining safety

### 10. MCP for External Tools
- Claude Code uses all his tools via MCP
- Examples: Slack (searches and posts), BigQuery queries, Sentry error logs
- Slack MCP configuration checked into `.mcp.json` and shared with team

```json
{
  "mcpServers": {
    "slack": {
      "type": "http",
      "url": "https://slack.mcp.anthropic.com/mcp"
    }
  }
}
```

### 11. Long-Running Task Verification
- For very long tasks, uses one of:
  - (a) Prompt Claude to verify with a background agent when done
  - (b) Use an agent Stop hook for deterministic verification
  - (c) Use the ralph-wiggum plugin (by @GeoffreyHuntley)
- Uses `--permission-mode=dontAsk` or `--dangerously-skip-permissions` in sandbox to avoid being blocked

### 12. Verification is Critical (Final Tip)
- "Probably the most important thing to get great results out of Claude Code -- give Claude a way to verify its work"
- "If Claude has that feedback loop, it will 2-3x the quality of the final result"
- Claude tests every single change on claude.ai/code using Chrome extension
- Opens browser, tests UI, iterates until code works and UX feels good
- Verification looks different per domain: bash command, test suite, browser/phone simulator

**Reference**: [Chrome extension](https://code.claude.com/docs/en/chrome)

## Summary of Key Themes

1. **Parallelization** - Run many Claudes simultaneously across terminal and web
2. **Plan first** - Start in Plan mode, get plan right, then auto-accept
3. **Automate repetition** - Slash commands and custom subagents for common workflows
4. **Compound learnings** - Add mistakes to CLAUDE.md so they don't repeat
5. **Verification** - Always give Claude a way to verify its work (2-3x quality improvement)
6. **Team sharing** - Check CLAUDE.md, permissions, MCP configs into git for team use
7. **Safe permissions** - Use `/permissions` allow-list instead of skipping all permissions
