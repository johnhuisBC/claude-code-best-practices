# Claude Code Best Practices

A synthesized guide from official Anthropic documentation and community experts.

> **Core Philosophy**: Claude Code is intentionally low-level and unopinionated. Nothing is universal; experiment to find what works for your specific use cases. Start simple and add complexity only when it demonstrably improves outcomes.

---

## Table of Contents

1. [Context Management](#context-management)
2. [CLAUDE.md Configuration](#claudemd-configuration)
3. [Workflows](#workflows)
4. [Dev Docs System](#dev-docs-system)
5. [Prompting Techniques](#prompting-techniques)
6. [Skills & Auto-Activation](#skills--auto-activation)
7. [Subagents](#subagents)
8. [Hooks](#hooks)
9. [Tool Usage](#tool-usage)
10. [Testing & Quality](#testing--quality)
11. [Multi-Claude Workflows](#multi-claude-workflows)
12. [Slash Commands](#slash-commands)
13. [Common Pitfalls](#common-pitfalls)

---

## Context Management

Context is your most precious resource. LLMs have finite attention capacity, and performance degrades as context grows (context rot).

### Key Practices

| Practice | Details | Sources |
|----------|---------|---------|
| **Monitor context** | Use `/context` command to track usage | [Sankalp], [Anthropic CC] |
| **Clear between tasks** | Use `/clear` when switching to unrelated work | [Anthropic CC], [CLAUDE.md Blog] |
| **Compact around 60-70%** | For continuous related work, don't let context fill | [Sankalp], [Context Engineering] |
| **Repeat objectives** | Inject reminders to combat "lost-in-the-middle" effects | [Sankalp], [Context Engineering] |
| **File-based context** | Store plans/todos in files, not just in-context | [tokenbender] |

### Just-In-Time Context Loading

Instead of pre-loading all information, maintain lightweight references and load dynamically:

- Let Claude discover context through exploration
- Use glob/grep for file discovery rather than dumping contents
- CLAUDE.md provides upfront context; tools provide just-in-time context

> **Principle**: Find "the smallest set of high-signal tokens that maximize the likelihood of your desired outcome." — [Context Engineering]

### When to Use Each Technique

| Situation | Technique |
|-----------|-----------|
| Switching to unrelated task | `/clear` |
| Long session on one task | Monitor and compact at 60-70% |
| Deep exploration needed | Use Explore subagent (fresh context) |
| Need to preserve decisions | Use markdown files that persist through compaction |
| Large feature work | Use Dev Docs system (see below) |
| Model ignoring feedback/looping | Jump to clean node, compact, start fresh |

**See also**: [Conflict: Context Threshold](conflicts/active/context-threshold.md)

---

## CLAUDE.md Configuration

CLAUDE.md provides persistent project context that loads automatically. It becomes part of the system prompt, so **size matters**.

### Size Guidelines

- **Target**: 200-300 lines
- **Maximum**: 500 lines
- **Strategy**: Reference external files for detailed documentation

**See also**: [Conflict: CLAUDE.md Size](conflicts/active/claude-md-size.md)

### Essential Sections

```markdown
# Project Name
Brief description (1-2 sentences)

## Directory Structure
Key locations only, not exhaustive

## Commands
- dev: `npm run dev`
- test: `npm test`
- lint: `npm run lint`

## Standards
- [Formatting rules]
- [Naming conventions]
- [Testing requirements]

## Workflows
Step-by-step for common tasks

## Notes
Project-specific quirks and warnings
```

### What to Include

- **Build/test commands** with examples
- **Code style** preferences (linters, formatters)
- **Naming conventions** for consistency
- **Architectural decisions** your team repeatedly explains
- **Testing requirements** and validation steps
- **Tool documentation** for custom utilities

### What NOT to Include

- API keys, credentials, secrets
- Security vulnerability details
- Overly comprehensive documentation
- Information that rarely applies

### Iteration

- Use `#` shortcut to add memories quickly
- Run `/init` for starter template, then refine
- Add instructions you find yourself repeating
- Effective files evolve with your codebase

---

## Workflows

### The Fundamental Pattern: Explore → Plan → Code → Commit

1. **Explore**: Ask Claude to read relevant files without writing code
2. **Plan**: Request a documented plan; use extended thinking for complex problems
3. **Code**: Implement with explicit verification steps
4. **Commit**: Generate commits with proper messages

> This prevents premature coding and improves results for complex problems.

### Extended Thinking

Use trigger words for deeper analysis:
- "think" → Standard reasoning
- "think hard" → More thorough
- "think harder" → Even more thorough
- "ultrathink" → Maximum reasoning depth

**Use for**: Hard tasks, self-review, rigorous explanation, complex planning

### Test-Driven Development

1. Request test cases based on input/output pairs
2. **Be explicit about avoiding mocks**
3. Confirm tests fail before implementation
4. Commit tests first
5. Implement iteratively until tests pass
6. Use independent subagent to verify no overfitting
7. Commit implementation

### Visual Iteration

1. Give Claude screenshot capability (Puppeteer MCP, manual screenshots)
2. Provide design mocks via screenshots or file paths
3. Implement → Screenshot → Iterate
4. Expect 2-3 iterations for polished results

### Course Correction

- **Plan first**: Ask for a plan before coding
- **Escape to interrupt**: Preserves context, stops current action
- **Double-Escape to rewind**: Jump back in history, try alternatives
- **Request undo**: Pivot approaches without losing progress

---

## Dev Docs System

For large features or multi-session tasks, create persistent documentation that survives context clearing and compaction.

> "Claude is like an extremely confident junior dev with extreme amnesia, losing track of what they're doing easily." — [Reddit 6 Months]

### The Three-File System

For every large task, create in `dev/active/[task-name]/`:

```
dev/active/user-authentication/
├── user-authentication-plan.md      # The accepted plan
├── user-authentication-context.md   # Key files, decisions, learnings
└── user-authentication-tasks.md     # Checklist of work
```

### Workflow

1. **Enter planning mode** for the task
2. **Review plan thoroughly** - catch mistakes here, not during implementation
3. **Hit ESC** before Claude starts implementing
4. **Create dev docs** with `/dev-docs` or manually
5. **Implement in sections**, reviewing between each
6. **Update docs regularly** - mark tasks complete, add context
7. **Before compacting**, run `/update-dev-docs` to capture state
8. **New session**: Just say "continue" - Claude reads the docs

### Why This Works

- Plans survive compaction
- Context persists across sessions
- Progress is tracked explicitly
- Claude can pick up exactly where it left off

### Slash Commands for Dev Docs

Create these in `.claude/commands/`:

- `/dev-docs` - Create the three files from an approved plan
- `/update-dev-docs` - Update context and tasks before compacting
- `/continue-task` - Read dev docs and continue from where we left off

---

## Prompting Techniques

### Be Specific

| Poor | Better |
|------|--------|
| "add tests for foo.py" | "write test case for foo.py covering the edge case where user is logged out; avoid mocks" |
| "fix the bug" | "fix the null pointer exception in getUserById when the user doesn't exist" |
| "make it faster" | "optimize the database query in getOrders to use an index on created_at" |

### Strike the Right Altitude

Avoid extremes:
- **Too rigid**: Hardcoded brittle logic that breaks with variations
- **Too vague**: High-level guidance without actionable direction

**Optimal**: Specific enough to guide behavior, flexible enough to handle variations.

### Use Examples Over Edge Cases

Rather than listing extensive edge cases, curate diverse, canonical examples.

> For LLMs, examples are "the 'pictures' worth a thousand words."

### Provide Visual Context

- Paste screenshots (`cmd+ctrl+shift+4` on macOS to clipboard)
- Drag-and-drop images directly
- Reference file paths for images

Critical for UI development and visual debugging.

### Don't Lead Questions

Claude tends to tell you what it thinks you want to hear. Ask neutral questions for honest feedback.

| Leading (Bad) | Neutral (Better) |
|---------------|------------------|
| "Is this approach good?" | "What are the tradeoffs of this approach?" |
| "This should work, right?" | "Walk me through how this would work" |
| "I think we need X" | "What options do we have here?" |

---

## Skills & Auto-Activation

Skills are reusable guidelines, but Claude often ignores them unless prompted. The solution: use hooks to force skill checking.

### The Problem

Skills exist but Claude doesn't use them automatically, even with matching keywords.

### The Solution: Hook-Based Auto-Activation

#### UserPromptSubmit Hook
Runs **before** Claude sees your message:
- Analyzes prompt for keywords and intent patterns
- Checks which skills are relevant
- Injects reminder into Claude's context

#### Stop Event Hook
Runs **after** Claude finishes:
- Analyzes which files were edited
- Checks for risky patterns (try-catch, database ops)
- Shows self-check reminder

### skill-rules.json Configuration

```json
{
  "backend-dev-guidelines": {
    "promptTriggers": {
      "keywords": ["backend", "controller", "service", "API"],
      "intentPatterns": ["(create|add).*?(route|endpoint)"]
    },
    "fileTriggers": {
      "pathPatterns": ["backend/src/**/*.ts"],
      "contentPatterns": ["router\\.", "export.*Controller"]
    }
  }
}
```

### Skill Organization (Per Anthropic Best Practices)

- **Main SKILL.md**: Under 500 lines
- **Resource files**: Detailed examples loaded on-demand
- **Result**: 40-60% token efficiency improvement

### Reference Implementation

See: https://github.com/diet103/claude-code-infrastructure-showcase

---

## Subagents

Subagents are specialized agents that can work in parallel or with fresh context.

### Built-in Types

| Type | Use Case | Context |
|------|----------|---------|
| **Explore** | Fast codebase search, file discovery | Fresh (read-only) |
| **Plan** | Design implementation strategies | Inherits full context |
| **general-purpose** | Complex multi-step tasks | Inherits full context |

### When to Use Subagents

**DO use subagents when**:
- Task requires deep codebase exploration
- You want to verify something without polluting main context
- Multiple independent tasks can run in parallel
- Current context is substantial and task is tangential

**DON'T use subagents when**:
- Task is simple (< 2-3 tool calls)
- Task requires current conversation context
- Just asking a clarifying question

### Best Practices

- Ask Claude which subagent type to use for a task
- Spawn multiple agents concurrently when possible
- Use `run_in_background` for long tasks
- Use independent subagents to verify implementations don't overfit to tests

### Multi-Agent Verification (Advanced)

For critical decisions, spawn multiple specialist subagents that work independently:

```
/multi-mind "find security vulnerabilities in our auth system"
```

**Benefits**:
- **Error decorrelation**: Agents make different mistakes; consensus filters errors
- **Specialist depth**: Focused expertise beats generalist responses
- **Independent verification**: Agents can't see each other's initial analysis

> "Single responses are hypotheses, not truth. Multiple independent verification or it didn't happen." — [tokenbender]

**See also**: [Conflict: Subagent Usage Frequency](conflicts/active/subagent-usage-frequency.md)

---

## Hooks

Hooks run at specific lifecycle points and can transform how Claude works.

### Essential Hooks

#### 1. Build Checker (Stop Hook)
Runs after Claude finishes responding:
- Tracks which repos were modified
- Runs build scripts on affected repos
- Shows errors to Claude for immediate fixing
- **Result**: Zero errors left behind

#### 2. Error Handling Reminder (Stop Hook)
After editing files:
- Detects risky patterns (try-catch, async, database ops)
- Shows gentle self-check reminder
- Non-blocking awareness

Example output:
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📋 ERROR HANDLING SELF-CHECK
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️  Backend Changes Detected
   ❓ Did you add error handling in catch blocks?
   ❓ Are database operations wrapped properly?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

#### 3. Skill Auto-Activation (UserPromptSubmit Hook)
See [Skills & Auto-Activation](#skills--auto-activation) above.

### Hook Warnings

**Avoid automatic formatting hooks** (Prettier, etc.):
- File modifications trigger `<system-reminder>` notifications
- Can consume 160k+ tokens in just a few rounds
- Better to format manually between sessions

### Hook Pipeline Example

```
Claude finishes responding
  ↓
Hook 1: Build checker → TypeScript errors caught
  ↓
Hook 2: Error reminder → Self-check awareness
  ↓
If errors found → Claude sees and fixes
  ↓
Result: Clean, error-free code
```

---

## Tool Usage

### Token Cost Awareness

- Tool definitions consume input tokens
- Tool results add to context
- Heavy tool usage fills context faster

### Tool Design Principles

- **Minimize overlap**: Clear distinction between when to use each tool
- **Self-containment**: Tools should be robust with clear intended use
- **Descriptive parameters**: Unambiguous input specifications

### MCP Servers

- Expose additional capabilities but add context overhead
- Configure at project, global, or shared (`.mcp.json`) levels
- Use `--mcp-debug` when troubleshooting

---

## Testing & Quality

### Pre-Implementation

- Write failing tests first
- Be explicit about avoiding mocks
- Specify edge cases to cover

### Post-Implementation

- Use independent subagent to verify (fresh perspective)
- Check for test overfitting
- Run full test suite, not just new tests

### Quality Gates (via Hooks)

- Pre-commit hooks for formatting/linting
- TDD guard hooks to enforce test-first
- Security scanning in CI/CD

---

## Multi-Claude Workflows

### Parallel Code Review

1. One Claude writes code
2. Second Claude reviews (fresh context advantage)
3. Third Claude synthesizes and makes final edits

### Git Worktrees

```bash
git worktree add ../project-feature-a feature-a
cd ../project-feature-a && claude
```

- Run multiple independent tasks without merge conflicts
- One terminal tab per worktree
- Clean up: `git worktree remove ../project-feature-a`

### Multiple Repository Checkouts

- Create 3-4 git checkouts in separate folders
- Run Claude in each terminal tab
- Cycle through to approve/deny permission requests

---

## Slash Commands

> "If you do something twice, make it a command." — [tokenbender]

### The Command Philosophy

Everything you feel like doing multiple times as a prompt should be a command. Rapid iteration: prototype a command, test it, refine it, share it.

### High-Value Commands to Create

| Category | Commands |
|----------|----------|
| **Context loading** | `/prime`, `/context-prime` |
| **Issue handling** | `/fix-issue`, `/analyze-issue` |
| **Testing** | `/tdd`, `/tdd-implement` |
| **Version control** | `/commit`, `/create-pr` |
| **Quality** | `/check`, `/lint` |
| **Dev docs** | `/dev-docs`, `/update-dev-docs` |
| **Session mgmt** | `/page` (save session state) |

### Creating Commands

Store markdown files in `.claude/commands/`:
- Project commands: `.claude/commands/` (shared via git)
- Personal commands: `~/.claude/commands/` (not shared)

Use `$ARGUMENTS` for parameterized commands.

### Meta-Commands

Create commands that create commands:
```
/crud-claude-commands create git-flow "automate git flow operations"
/crud-claude-commands list
```

See: https://github.com/tokenbender/agent-guides

---

## Common Pitfalls

### Context Issues

| Pitfall | Solution |
|---------|----------|
| Starting complex tasks mid-conversation | Start fresh or clear context first |
| Relying on Explore summaries alone | Have model read full relevant files |
| Letting context fill up | Monitor with `/context`, clear/compact proactively |

### Subagent Issues

| Pitfall | Solution |
|---------|----------|
| Spawning subagents for simple tasks | Only use when fresh context or parallelism helps |
| Not verifying implementations | Use independent subagent to check for overfitting |

### CLAUDE.md Issues

| Pitfall | Solution |
|---------|----------|
| Adding content without testing | Iterate based on actual instruction adherence |
| Bloated files | Keep under 500 lines; reference external files |
| Conflicting instructions | Fewer, non-conflicting instructions work better |

### Permission Issues

| Pitfall | Solution |
|---------|----------|
| Using `--dangerously-skip-permissions` unsafely | Only in offline, isolated containers |
| Repeated permission prompts | Use `/permissions` to whitelist |

---

## Quick Reference Card

```
/context          - Check context usage
/clear            - Reset context (keep CLAUDE.md)
/init             - Generate starter CLAUDE.md
/memory           - Edit memories directly
/permissions      - Manage tool permissions
Escape            - Interrupt current action
Escape+Escape     - Rewind to previous state
Ctrl+R            - Search prompt history
#                 - Quick add to memory
```

**Extended thinking triggers**: think, think hard, think harder, ultrathink

---

## Sources

All practices in this document are synthesized from:
- [Anthropic: Claude Code Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices)
- [Anthropic: Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents)
- [Anthropic: Context Engineering](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- [Anthropic: Using CLAUDE.md Files](https://claude.com/blog/using-claude-md-files)
- [Claude Code Official Documentation](https://code.claude.com/docs)
- [Reddit: Tips from 6 Months of Hardcore Use](https://www.reddit.com/r/ClaudeCode/comments/1oivs81/claude_code_is_a_beast_tips_from_6_months_of/)
- [Sankalp: Claude Code 2.0 Experience](https://sankalp.bearblog.dev/my-experience-with-claude-code-20-and-how-to-get-better-at-using-coding-agents)
- [Awesome Claude Code](https://github.com/hesreallyhim/awesome-claude-code)
- [tokenbender: How I Bring the Best Out of Claude Code (Parts 1 & 2)](https://tokenbender.com/post.html?id=how-i-bring-the-best-out-of-claude-code)

See [sources/index.md](sources/index.md) for full source catalog.

---

*Last updated: 2025-01-04*
