# Conflict: CLAUDE.md File Size

## The Conflict

Sources differ on how much to put in CLAUDE.md.

### Position A: Keep Under 500 Lines
**Source**: Sankalp - Claude Code 2.0 Experience
> "Maintain CLAUDE.md for persistent global instructions (keep under 500 lines)"

**Rationale**:
- Smaller files = less context consumption
- Forces prioritization of most important instructions
- Reduces "lost in the middle" effects

### Position B: Comprehensive but Concise
**Source**: Anthropic - Using CLAUDE.md Files
> "Avoid over-engineering... keep it concise"
> "File size matters—CLAUDE.md becomes part of Claude's system prompt, so context bloat reduces effectiveness"

No specific line count given, but emphasizes:
- Solving real problems over theoretical concerns
- Iterative improvement based on actual friction

### Position C: Reference External Files
**Source**: Anthropic - Using CLAUDE.md Files
> "Break large information into separate markdown files and reference them within CLAUDE.md to manage context efficiently"

**Rationale**:
- Keeps main file scannable
- Allows detailed docs without bloating system prompt
- Can load detailed context on-demand

## Analysis

All sources agree on the principle: **less is more for CLAUDE.md**. The disagreement is tactical:
- 500 lines is a specific heuristic
- "Concise" is subjective
- External references add complexity

## Proposed Resolution

**Tiered approach**:
1. **CLAUDE.md core** (target: 200-300 lines): Essential project info, standards, key commands
2. **External references**: Detailed workflows, architecture docs, extensive examples
3. **Skills**: Task-specific instructions loaded on-demand

**500-line maximum** as a hard limit, with goal of staying under 300.

## Testing Plan

1. Measure current CLAUDE.md effectiveness
2. Trim to ~200 lines, move detail to external files
3. Compare instruction adherence and context efficiency

## Status
**Tentatively resolved**: Adopt 500-line max with 300-line target; use external references

---

## Decision Log

| Date | Decision | Rationale |
|------|----------|-----------|
| 2025-01-03 | 500-line max, 300-line target | Conservative approach combining all sources |
