# Sankalp: Claude Code 2.0 Experience

**Source**: https://sankalp.bearblog.dev/my-experience-with-claude-code-20-and-how-to-get-better-at-using-coding-agents
**Date**: January 2025
**Authority**: Community Expert / Power User
**Status**: Active

---

## Key Takeaways

### Context Management is Critical

- Monitor context usage with `/context` command
- **Compact or start fresh around 60% capacity**
- Tool calls and results consume tokens—everything stays in context window
- Effective context windows are likely 50-60% of stated length due to attention degradation
- **"Recite" objectives repeatedly** (via todo lists, plans) to keep goals in recent attention span

### Exploration Before Execution

- Ask clarifying questions and understand requirements deeply before implementation
- Use **Explore sub-agents for fast codebase searches**
- Let Opus 4.5 read full relevant files itself
- Cross-reference ingested context for better reasoning

### Leverage the Right Tool

- Use Claude Code (Opus 4.5) for execution and collaboration
- Use Codex for code review and bug detection (excels at severity classification)
- **Keep review separate** from implementation
- Use checkpointing (`Esc+Esc` or `/rewind`) to backtrack without losing history

### Sub-agents & Task Delegation

- **Explore agent**: Read-only codebase search specialist; starts with fresh context
- **general-purpose & Plan agents**: Inherit full context for complex multi-step work
- Spawn multiple agents concurrently where possible
- Run long tasks in background with `run_in_background`
- Ask Claude directly which sub-agent type to use

### Custom Commands

- Create repetitive prompts as slash commands in `.claude/commands/`
- Example: `/handoff` to summarize session before compacting
- Commands are context-appended prompts for static, reusable instructions

### Context Engineering Techniques

- Skills load on-demand (avoid bloating system prompt)
- Hooks observe lifecycle stages (e.g., play notification on Stop)
- System reminders inject objectives mid-context
- MCP servers expose tools but bloat context; consider code execution MCP pattern

### Advanced Features

- **Ultrathink mode**: Use for hard tasks, self-review, or rigorous explanation
- **Prompt history search**: `Ctrl+R` to find previous prompts across projects
- **Syntax highlighting** (v2.0.71+): Review diffs without opening IDE

### Execution Patterns

#### "Throw-Away First Draft" Approach
1. Create branch, let Claude write feature end-to-end while observing
2. Compare output against mental model; identify divergences
3. Run second iteration with refined prompts informed by first-pass learnings
4. Reveals model's decision biases and context limitations

#### Micro-Management Strategy
- Enable fast feedback loops
- Closely monitor changes
- Ask for second opinion on difficult decisions
- Use Plan sub-agent only when requirements are fuzzy

### Scratchpad & CLAUDE.md

- Maintain CLAUDE.md for persistent global instructions (**keep under 500 lines**)
- Use scratchpad extensively for session-specific context
- Divide instructions into skill files to reduce bloat

### Model-Specific Insights (Opus 4.5)

**Strengths**:
- Superior intent detection and communication
- Acts as better pair-programmer
- Excellent writer and explainer
- Good at ASCII diagrams and clarification
- 200K context window with proven effectiveness

### Common Pitfalls to Avoid

- Don't start complex tasks mid-conversation (context degradation compounds)
- Don't rely solely on Explore summaries—model must read full relevant files
- Don't spawn unnecessary sub-agents for simple tasks (token waste)
- Avoid bloated tool definitions; use code execution patterns instead

### Context Engineering Best Practices

- Plug relevant context; reduce irrelevant bloat
- Keep instructions few and non-conflicting
- **Inject reminders repeatedly** to combat "lost-in-the-middle" effects
- Use markdown files (plans, todos, specs) that persist through compaction
- Load skills/MCP resources on-demand rather than upfront

### Augmentation Mindset

- Focus on "augmentation" not just "keeping up" with tools
- Build domain expertise vertically (depth) and horizontally (adjacent areas)
- **Let implementation speed free time for taste refinement**
- Run more experiments since iteration cycles are fast
- Develop strong judgement

---

## Notable Insights

This source provides several unique perspectives:

1. **60% context threshold**: More conservative than some other sources
2. **"Throw-away first draft"**: Novel technique for learning model biases
3. **Cross-tool strategy**: Using different AI tools for different purposes
4. **500-line CLAUDE.md limit**: Specific guidance on file size

## Actionable Items for CLAUDE.md

```markdown
## Context Hygiene
- Monitor with /context; compact around 60% capacity
- Keep CLAUDE.md under 500 lines
- Use skills and on-demand loading vs upfront bloat
- Repeat objectives in prompts to combat attention degradation

## Exploration Strategy
- Use Explore subagent for codebase search
- Read full relevant files, don't rely on summaries alone
- Ask clarifying questions before implementing
```
