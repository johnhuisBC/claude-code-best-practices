# Subagent Usage Tracking Experiment

## Purpose

Automatically track subagent usage decisions to gather data on when they're helpful vs. wasteful.

## CLAUDE.md Addition

Add this to your CLAUDE.md or user memory:

```markdown
## Subagent Tracking (Experiment)

When you use OR deliberately skip a subagent, briefly log it:

**Location**: Append to `experiments/subagent-log.md` (create if doesn't exist)

**Format**:
| Date | Task Summary | Used Subagent? | Type | Outcome | Notes |
|------|--------------|----------------|------|---------|-------|

**Log when**:
- You spawn any subagent (Explore, Plan, general-purpose)
- You consider but skip a subagent for a non-trivial task
- A subagent notably helps or wastes time

**Don't log**: Trivial questions where subagent was never considered
```

## Example Log Entries

```markdown
| Date | Task Summary | Used Subagent? | Type | Outcome | Notes |
|------|--------------|----------------|------|---------|-------|
| 2025-01-04 | Find all uses of deprecated API | Yes | Explore | Helpful | Found 15 files, kept main context clean |
| 2025-01-04 | What does this function return? | No | - | Fine | Simple question, no need |
| 2025-01-04 | Review auth implementation | Yes | general-purpose | Wasteful | Task needed current context, had to repeat info |
| 2025-01-05 | Search for error handling patterns | Yes | Explore | Helpful | Deep search, would have polluted context |
| 2025-01-05 | Add a single log statement | No | - | Fine | Trivial change |
```

## Analysis

After ~20 entries, review the log to identify:
1. What task types consistently benefit from subagents?
2. What types are wasteful?
3. Where's the complexity threshold?

## Notes

- This is opt-in tracking - Claude will only log if this is in your CLAUDE.md
- Logging itself consumes minimal tokens
- Can be removed once the conflict is resolved
