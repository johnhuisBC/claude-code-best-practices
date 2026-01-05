# Conflict: Model Choice (Opus vs Sonnet)

## The Conflict

Should you use Opus 4.5 (bigger, slower, more expensive) or Sonnet (faster, cheaper) for Claude Code?

### Position A: Use Opus 4.5 for Everything
**Source**: Boris Cherny (Claude Code creator)
> "I use Opus 4.5 with thinking for everything. It's the best coding model I've ever used, and even though it's bigger & slower than Sonnet, since you have to steer it less and it's better at tool use, it is almost always faster than using a smaller model in the end."

**Rationale**:
- Less steering required = fewer iterations
- Better tool use = more efficient execution
- Net time savings despite slower per-token speed
- Higher first-attempt success rate

### Position B: Use Sonnet by Default
**Source**: General community practice, cost-conscious users

**Rationale**:
- Significantly cheaper per token
- Faster response times
- "Good enough" for most tasks
- Save Opus for complex tasks only

## Analysis

Boris's argument is compelling: **total time to completion** matters more than **per-token speed**. If Opus gets it right on the first try while Sonnet takes 3 attempts, Opus wins.

However, this may depend on:
- Task complexity
- User's ability to course-correct (experienced users may steer Sonnet effectively)
- Cost sensitivity
- Whether you're running parallel sessions (Opus costs add up)

## Proposed Resolution

**Default to Opus 4.5 with thinking** for:
- Non-trivial coding tasks
- Complex multi-file changes
- Tasks where getting it right matters more than speed

**Consider Sonnet** for:
- Simple, well-defined tasks
- Cost-sensitive situations
- Tasks where you can easily course-correct

## Resolution

**Use Opus 4.5 with thinking as the default.**

Boris Cherny created Claude Code and uses it daily. His recommendation carries significant weight - less steering and better tool use means faster total time despite slower per-token speed.

---

## Decision Log

| Date | Decision | Rationale |
|------|----------|-----------|
| 2026-01-05 | Documented conflict | Boris Cherny strongly advocates Opus; community varies |
| 2026-01-05 | **Resolved: Opus default** | Creator's recommendation + "less steering = faster overall" logic is compelling |
