# Claude Code Best Practices

A living knowledge base for Claude Code best practices, curated from authoritative sources and validated through testing.

## Purpose

This repository documents best practices for using Claude Code effectively, distilled from:
- Official Anthropic documentation and engineering blog posts
- Community experts and power users
- Personal experimentation and validated findings

## Structure

```
claude-code-best-practices/
├── BEST_PRACTICES.md              # Master document, organized by topic
├── CLAUDE_MD/
│   ├── general.md                 # Universal rules for any project
│   └── templates/
│       ├── python.md              # Python-specific additions
│       ├── typescript.md          # TS/JS-specific additions
│       └── ...
├── sources/
│   ├── index.md                   # Source catalog with status/dates
│   └── summaries/
│       └── [dated-source-name].md
├── conflicts/
│   ├── active/                    # Conflicts needing resolution
│   └── resolved/                  # Documented experiments & decisions
└── videos/
    └── [video-notes].md           # Notes or transcripts from video content
```

## How to Use

### Quick Reference
Start with [BEST_PRACTICES.md](BEST_PRACTICES.md) for organized, actionable guidance.

### For Your CLAUDE.md
Copy relevant sections from [CLAUDE_MD/general.md](CLAUDE_MD/general.md) and any language-specific templates.

### Deep Dive
Browse [sources/summaries/](sources/summaries/) to see the original takeaways from each source.

### Conflicts
Check [conflicts/](conflicts/) to see how we resolved contradictory advice.

## Adding New Sources

1. Add the source link to [sources/index.md](sources/index.md)
2. Create a summary in `sources/summaries/`
3. Cross-reference against existing practices for conflicts
4. Update BEST_PRACTICES.md with new/refined practices
5. Periodically distill into CLAUDE_MD templates

## Staleness Policy

Sources older than 6 months should be reviewed for continued relevance, as Claude Code evolves rapidly. Each practice includes provenance for easy auditing.

---

Last updated: 2025-01-03
