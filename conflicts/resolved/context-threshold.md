# Resolved: Context Threshold for Compaction

## The Original Conflict

Different sources suggested different thresholds for when to compact or clear context.

### Positions
- **Position A (Sankalp)**: Compact at 60% capacity
- **Position B (Anthropic CC)**: Clear between tasks (activity-based)
- **Position C (Context Engineering)**: Let auto-compaction handle it

## Resolution

**All positions are true and complementary.** They address different scenarios in a hierarchy:

### The Rule (Priority Order)

1. **Always clear between unrelated tasks** (`/clear`)
   - This is non-negotiable - fresh context for fresh work
   - Prevents cross-contamination between unrelated work

2. **Compact starting at 60% capacity** for continuous related work
   - Monitor with `/context`
   - Proactive compaction preserves quality
   - Don't wait until context is nearly full

3. **Auto-compaction as last resort**
   - Useful safety net, but don't rely on it as primary strategy
   - By the time auto-compaction triggers, you may have already lost quality

### Decision Matrix

| Situation | Action |
|-----------|--------|
| Switching to unrelated task | `/clear` immediately |
| Continuous related work, < 60% | Keep working |
| Continuous related work, 60-70% | Compact proactively |
| Continuous related work, > 80% | Compact urgently |
| Forgot to monitor, context full | Let auto-compact handle, but avoid this |

## Rationale

The positions weren't conflicting - they were addressing different scenarios. The hierarchy makes all of them valid:
- Task boundaries trump everything
- Percentage thresholds guide continuous work
- Auto-compaction is the safety net

---

## Decision Log

| Date | Decision | Rationale |
|------|----------|-----------|
| 2025-01-03 | Documented conflict | Initial setup |
| 2025-01-04 | Resolved: All positions complementary | User insight: hierarchy of rules, not competing options |
