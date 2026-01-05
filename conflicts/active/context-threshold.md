# Conflict: Context Threshold for Compaction

## The Conflict

Different sources suggest different thresholds for when to compact or clear context.

### Position A: 60% threshold (Conservative)
**Source**: Sankalp - Claude Code 2.0 Experience
> "Monitor context usage with `/context` command; compact or start fresh around 60% capacity"

**Rationale**:
- Effective context windows are likely 50-60% of stated length due to attention degradation
- Conservative approach prevents quality degradation

### Position B: Use `/clear` frequently (Activity-based)
**Source**: Anthropic - Claude Code Best Practices
> "Use `/clear` frequently between tasks to reset context and maintain performance"

**Rationale**:
- Task boundaries are better triggers than percentage thresholds
- Fresh context for each distinct task prevents cross-contamination

### Position C: Compaction when approaching limits
**Source**: Anthropic - Context Engineering
> "Summarize conversation history when approaching context limits"

**Rationale**:
- Let the system manage via compaction rather than manual clearing
- Preserves important context through summarization

## Analysis

These positions aren't necessarily contradictory—they address different scenarios:

1. **60% threshold**: Good heuristic for long, continuous work sessions
2. **Clear between tasks**: Best for distinct, unrelated tasks
3. **Auto-compaction**: Useful when continuity matters

## Proposed Resolution

**Hybrid approach**:
- Clear context (`/clear`) between **distinct, unrelated tasks**
- Monitor context (`/context`) during long sessions; compact around **60-70%** for related work
- Let auto-compaction handle edge cases, but don't rely on it as primary strategy

## Testing Plan

1. Work a session using 60% as hard threshold
2. Work a session using task-boundary clearing only
3. Work a session using 80% threshold
4. Compare: quality of outputs, perceived model confusion, token usage

## Status
**Needs testing**: Will resolve after empirical comparison

---

## Decision Log

| Date | Decision | Rationale |
|------|----------|-----------|
| 2025-01-03 | Documented conflict | Initial setup |
