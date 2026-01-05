# Resolved: CLAUDE.md File Size

## The Original Conflict

Sources differed on how much to put in CLAUDE.md.

### Positions
- **Position A (Sankalp)**: Keep under 500 lines
- **Position B (Anthropic)**: "Concise" (no specific number)
- **Position C (Anthropic)**: Reference external files

## Resolution

**Tiered approach adopted:**

1. **CLAUDE.md core**: Target 200-300 lines
   - Essential project info
   - Key standards and commands
   - High-level workflows

2. **External references**: For detailed content
   - Architecture documentation
   - Extensive examples
   - Detailed workflow steps

3. **Skills**: Task-specific instructions
   - Loaded on-demand
   - Keep main SKILL.md under 500 lines
   - Use resource files for detail

### Hard Limits

- **CLAUDE.md maximum**: 500 lines (hard limit)
- **CLAUDE.md target**: 200-300 lines (goal)
- **SKILL.md maximum**: 500 lines per skill

### Rationale

All sources agreed on the principle: **less is more**. The specific numbers provide actionable guidance while the external reference strategy allows for comprehensive documentation without bloating the system prompt.

---

## Decision Log

| Date | Decision | Rationale |
|------|----------|-----------|
| 2025-01-03 | 500-line max, 300-line target | Conservative approach combining all sources |
| 2025-01-04 | Confirmed resolution | User agreed with proposed approach |
