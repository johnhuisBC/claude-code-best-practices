## Claude Code Best Practices

### Model Choice
- Default to Opus 4.5 with thinking (less steering = faster overall)

### Context Management
- Monitor with `/context`; compact around 60% capacity
- Use `/clear` between unrelated tasks
- Let auto-compaction be last resort, not primary strategy

### Workflow
- Start sessions in Plan mode (`shift+tab` twice) for non-trivial tasks
- Get plan right first, then switch to auto-accept edits
- Read code before modifying it
- Use TodoWrite to plan multi-step tasks
- "If you do it twice, make it a slash command"

### Subagents
- Use liberally for exploration and parallel work
- Skip for trivial tasks (< 2-3 tool calls)
- Prefer Explore agent for codebase searches

### Verification (Critical - 2-3x quality improvement)
- Always give Claude a way to verify its work
- Web apps: Use browser/Chrome extension to test UI
- CLI tools: Run bash commands to test functionality
- Libraries: Run test suite
- APIs: curl/httpie to test endpoints
- For long tasks: Use background agent or Stop hook to verify when done

### CLAUDE.md Files
- Keep under 500 lines (target 200-300)
- Use external references for detailed docs
- Include: project overview, key commands, coding standards, common workflows
- Add mistakes to CLAUDE.md so they don't repeat (compounding effect)

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
