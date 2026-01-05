## Claude Code Best Practices

### Context Management
- Monitor with `/context`; compact around 60% capacity
- Use `/clear` between unrelated tasks
- Let auto-compaction be last resort, not primary strategy

### Subagents
- Use liberally for exploration and parallel work
- Skip for trivial tasks (< 2-3 tool calls)
- Prefer Explore agent for codebase searches

### CLAUDE.md Files
- Keep under 500 lines (target 200-300)
- Use external references for detailed docs
- Include: project overview, key commands, coding standards, common workflows

### Workflow
- Read code before modifying it
- Use TodoWrite to plan multi-step tasks
- Verify critical operations with multi-agent checks
- "If you do it twice, make it a slash command"

### Prompting
- Be specific and direct
- Provide examples of desired output
- Show don't tell (paste code, errors, context)

## Subagent Tracking (Experiment)

When you use OR deliberately skip a subagent, briefly log it:

**Location**: Append to `experiments/subagent-log.md` in claude-code-best-practices repo

**Format**:
| Date | Task Summary | Used Subagent? | Type | Outcome | Notes |

**Log when**: Spawning subagents, skipping for non-trivial tasks, or notable help/waste
**Don't log**: Trivial questions where subagent was never considered
