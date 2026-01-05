# Reddit: Claude Code Tips from 6 Months of Hardcore Use

**Source**: https://www.reddit.com/r/ClaudeCode/comments/1oivs81/claude_code_is_a_beast_tips_from_6_months_of/
**Author**: u/JokeGold5455
**Date**: ~November 2024 (2 months ago from Jan 2025)
**Authority**: Community Power User (300k LOC rewrite, 6 months daily use)
**Status**: Active
**Repository**: https://github.com/diet103/claude-code-infrastructure-showcase

---

## Key Takeaways

### Core Philosophy

> "If you want the best out of CC, then you should be working together with it: planning, reviewing, iterating, exploring different approaches."

> "Claude is like an extremely confident junior dev with extreme amnesia, losing track of what they're doing easily."

### Skills Auto-Activation System (Major Innovation)

**The Problem**: Skills exist but Claude doesn't use them automatically. Even with exact keywords, Claude ignores skills.

**The Solution**: Use hooks to force skill checking.

#### Hook 1: UserPromptSubmit (Before Claude sees your message)
- Analyzes prompt for keywords and intent patterns
- Checks which skills might be relevant
- Injects reminder into Claude's context
- Example: When you ask about layout, Claude sees "🎯 SKILL ACTIVATION CHECK - Use project-catalog-developer skill"

#### Hook 2: Stop Event (After Claude finishes)
- Analyzes which files were edited
- Checks for risky patterns (try-catch, database ops, async)
- Displays self-check reminder
- Non-blocking awareness

#### skill-rules.json Configuration
```json
{
  "backend-dev-guidelines": {
    "type": "domain",
    "enforcement": "suggest",
    "priority": "high",
    "promptTriggers": {
      "keywords": ["backend", "controller", "service", "API", "endpoint"],
      "intentPatterns": [
        "(create|add).*?(route|endpoint|controller)",
        "(how to|best practice).*?(backend|API)"
      ]
    },
    "fileTriggers": {
      "pathPatterns": ["backend/src/**/*.ts"],
      "contentPatterns": ["router\\.", "export.*Controller"]
    }
  }
}
```

### Skill Organization (Anthropic Best Practices)

**Keep main SKILL.md under 500 lines** with progressive disclosure:
- Main file: 300-400 lines of core patterns
- Resource files: Detailed examples loaded on-demand
- Result: 40-60% token efficiency improvement

**Example structure**:
```
frontend-dev-guidelines: 398-line main file + 10 resource files
backend-dev-guidelines: 304-line main file + 11 resource files
```

### Dev Docs System (Prevents "Lost the Plot")

**The Problem**: Claude loses track of what it's doing, goes off on tangents, forgets the plan.

**The Solution**: Three-file system for every task:

```
~/git/project/dev/active/[task-name]/
├── [task-name]-plan.md      # The accepted plan
├── [task-name]-context.md   # Key files, decisions
└── [task-name]-tasks.md     # Checklist of work
```

#### Workflow:
1. Use planning mode (or strategic-plan-architect agent)
2. Review plan thoroughly - catch mistakes early
3. Hit ESC before Claude starts implementing
4. Run `/dev-docs` to create the three files
5. During implementation, remind Claude to update tasks/context
6. Before compacting, run `/update-dev-docs`
7. New session: just say "continue"

**Key insight**: Even through auto-compaction, Claude can continue seamlessly with these files.

### CLAUDE.md Evolution

**Old approach**: Everything in CLAUDE.md + massive BEST_PRACTICES.md (1,400+ lines)

**New approach**:
- **Skills**: All "how to write code" guidelines
- **CLAUDE.md**: Only "how this specific project works" (~200 lines)

**Structure**:
```
Root CLAUDE.md (100 lines)
├── Critical universal rules
├── Points to repo-specific claude.md files
└── References skills for detailed guidelines

Each Repo's claude.md (50-100 lines)
├── Quick Start pointing to:
│   ├── PROJECT_KNOWLEDGE.md - Architecture
│   ├── TROUBLESHOOTING.md - Common issues
│   └── Auto-generated API docs
└── Repo-specific quirks
```

### PM2 Process Management (Backend Debugging)

**The Problem**: Can't ask Claude to debug backend when it can't see logs.

**The Solution**: PM2 manages all services with accessible logs.

```javascript
// ecosystem.config.js
module.exports = {
  apps: [
    {
      name: 'form-service',
      script: 'npm',
      args: 'start',
      cwd: './form',
      error_file: './form/logs/error.log',
      out_file: './form/logs/out.log',
    },
    // ... more services
  ]
};
```

**Result**: Claude can run `pm2 logs email --lines 200`, diagnose issues, and `pm2 restart email` autonomously.

### Hooks System (#NoMessLeftBehind)

#### Hook 1: File Edit Tracker
- Logs which files were edited and which repo
- Timestamps for tracking

#### Hook 2: Build Checker (Stop hook)
- Reads edit logs to find modified repos
- Runs build scripts on affected repos
- If < 5 errors: Shows to Claude for fixing
- If ≥ 5 errors: Recommends auto-error-resolver agent
- **Result**: Zero instances of Claude leaving errors behind

#### Hook 3: Error Handling Reminder
- Detects risky patterns in edited files
- Shows gentle self-check reminder
- Non-blocking awareness

**⚠️ Warning about Prettier hook**: Author initially recommended auto-formatting hook but later removed it. File modifications trigger `<system-reminder>` notifications that can consume 160k+ tokens in just 3 rounds.

### Planning is King

> "If you aren't at a minimum using planning mode before asking Claude to implement something, you're gonna have a bad time."

**Process**:
1. Enter planning mode
2. Let Claude research codebase and build plan
3. **Review thoroughly** - catch mistakes here, not later
4. Context often at 15% after planning - that's okay
5. Create dev docs before starting fresh session
6. Implement in sections, review between each
7. Have a subagent review code during implementation

### Specialized Agents

**Quality Control**:
- code-architecture-reviewer
- build-error-resolver
- refactor-planner

**Testing & Debugging**:
- auth-route-tester
- auth-route-debugger
- frontend-error-fixer

**Planning & Strategy**:
- strategic-plan-architect
- plan-reviewer
- documentation-architect

**Key**: Give agents specific roles and clear instructions on what to return.

### Prompting Tips

1. **Be specific** about desired results
2. **Don't lead questions** - Claude tells you what it thinks you want to hear
3. **Re-prompt often** - Double-ESC to branch from previous prompts
4. **Research first** if you don't know specifics
5. **Self-reflect** when quality seems low - often it's the prompting

> "Ask not what Claude can do for you, ask what context you can give to Claude"

### Know When to Step In

> "If you've spent 30 minutes watching Claude struggle with something that you could fix in 2 minutes, just fix it yourself."

AI excels at many things but struggles with:
- Logic puzzles requiring real-world intuition
- Problems where human "just gets it" faster

### Scripts Attached to Skills

Attach utility scripts to skills so Claude has ready-to-use tools:
```markdown
### Testing Authenticated Routes
Use the provided test-auth-route.js script:
`node scripts/test-auth-route.js http://localhost:3002/api/endpoint`
```

### Productivity Tools

- **SuperWhisper**: Voice-to-text for prompting
- **BetterTouchTool**: Double-tap hotkeys, custom gestures
- **Memory MCP**: Tracking architectural decisions (less needed with skills)

---

## Notable Unique Insights

1. **Skills auto-activation via hooks** - Novel solution to skills being ignored
2. **Three-file dev docs system** - Prevents context loss across sessions
3. **PM2 for Claude-accessible logging** - Enables autonomous debugging
4. **Build checker hook** - Zero errors left behind
5. **Review during implementation** - Have subagent review as you go
6. **Avoid Prettier hook** - Token cost from system-reminders

## Conflicts with Other Sources

### Context Management
This author uses dev docs files to persist through compaction rather than the 60% threshold approach. These are complementary strategies.

### Skill File Size
Aligns with other sources: Keep main skill under 500 lines, use resource files for detail.

---

## Actionable Items for CLAUDE.md

```markdown
## Dev Docs Workflow
For large tasks, create in dev/active/[task-name]/:
- [task-name]-plan.md - The accepted plan
- [task-name]-context.md - Key files, decisions
- [task-name]-tasks.md - Checklist

Update before compacting with /update-dev-docs
New session: just say "continue"

## Quality Hooks
- Build checker: Run builds on edited repos after each response
- Error reminder: Self-check for error handling patterns
- No Prettier hook (token cost too high)

## Planning
- Always use planning mode for non-trivial work
- Review plan thoroughly before implementing
- Implement in sections, review between each
- Have subagent review during implementation
```
