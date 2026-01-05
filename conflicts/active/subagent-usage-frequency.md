# Conflict: When to Use Subagents

## The Conflict

Sources differ on how liberally to use subagents.

### Position A: Use Subagents Liberally
**Source**: Anthropic - Claude Code Best Practices
> "Use subagents to verify details or investigate specific questions early in conversations"
> "Preserve context availability without efficiency loss"

**Source**: Sankalp
> "Spawn multiple agents concurrently where possible"
> "Ask Claude directly which sub-agent type to use"

**Rationale**:
- Subagents start with fresh context (no degradation)
- Parallel work increases throughput
- Keeps main context clean

### Position B: Avoid Unnecessary Subagents
**Source**: Sankalp (same article)
> "Don't spawn unnecessary sub-agents for simple tasks (token waste)"

**Source**: Anthropic - Building Effective Agents
> "Start simple and increase complexity only when it demonstrably improves outcomes"

**Rationale**:
- Subagents have overhead (spawning, context setup)
- Simple tasks don't need the complexity
- Token cost adds up

## Analysis

The apparent conflict is actually about **task complexity**:
- Complex, parallel, or deep-dive tasks → Use subagents
- Simple, quick tasks → Don't use subagents

The threshold is: **Does this task benefit from a fresh context or parallel execution?**

## Proposed Resolution

**Use subagents when**:
- Task requires deep codebase exploration (use Explore agent)
- You want to verify something without polluting main context
- Multiple independent tasks can run in parallel
- Current context is already substantial and task is tangential

**Don't use subagents when**:
- Task is simple and quick (< 2-3 tool calls)
- Task requires the current conversation context
- You're just asking a clarifying question

## Testing Plan

1. For a medium-complexity task, try with and without Explore subagent
2. Measure: time to completion, quality of result, main context cleanliness
3. Document the threshold where subagents become beneficial

## Status
**Leaning toward Position A (liberal usage)**: Use subagents freely unless the task is super minor.

## Testing Plan

To validate:
1. For a medium-complexity task, try with and without Explore subagent
2. Measure: time to completion, quality of result, main context cleanliness
3. Document the threshold where subagents become beneficial

Current hypothesis: The overhead of subagents is worth it for anything beyond trivial tasks.

---

## Decision Log

| Date | Decision | Rationale |
|------|----------|-----------|
| 2025-01-03 | Documented conflict | Initial setup - logical resolution proposed |
| 2025-01-04 | Leaning toward liberal usage | User input: use freely unless super minor; needs testing to confirm |
| 2026-01-05 | Strong evidence for liberal usage | Boris Cherny (Claude Code creator) uses custom subagents regularly; thinks of them as "automating the most common workflows that I do for most PRs" |
