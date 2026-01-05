# Anthropic: Effective Context Engineering for AI Agents

**Source**: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
**Date**: January 2025
**Authority**: Official Anthropic Engineering
**Status**: Active

---

## Key Takeaways

### Core Definition

> Context engineering is "the set of strategies for curating and maintaining the optimal set of tokens (information) during LLM inference."

**Guiding Principle**: Find "the smallest set of high-signal tokens that maximize the likelihood of your desired outcome."

### Critical Constraints

#### Attention Budget Limitations
- LLMs have finite attention capacity similar to human working memory
- Performance degrades as context grows (**context rot**)
- The transformer architecture creates n² pairwise token relationships
- Models have less training experience with longer sequences

### System Prompt Best Practices

**Strike the Right Altitude**: Avoid two extremes:
- Neither hardcoded brittle logic nor vague high-level guidance
- Optimal prompts are "specific enough to guide behavior effectively, yet flexible enough to provide the model with strong heuristics"

**Structural Organization**:
- Use distinct sections with XML tags or Markdown headers
- Include: background information, instructions, tool guidance, output descriptions
- Start minimal and test with best available models before adding complexity

### Tool Design Principles

- **Minimize overlap**: If humans can't definitively choose between tools, agents will struggle more
- **Self-containment**: Tools should be robust and extremely clear about intended use
- **Token efficiency**: Return information that reduces context consumption
- **Descriptive parameters**: Input parameters should be unambiguous
- Avoid bloated toolsets covering excessive functionality

### Few-Shot Prompting

Rather than listing extensive edge cases, curate "a set of diverse, canonical examples that effectively portray the expected behavior."

> For LLMs, examples are "the 'pictures' worth a thousand words."

### Runtime Context Retrieval: "Just-In-Time" Strategy

Instead of pre-loading all data, maintain lightweight identifiers (file paths, URLs) and dynamically load information as needed.

**Benefits**:
- Agents discover relevant context progressively through exploration
- File hierarchies, naming conventions provide behavioral signals
- Reduces irrelevant information drowning working memory

**Trade-offs**: Runtime exploration is slower; requires engineering to prevent dead ends.

**Hybrid Approach**: Retrieve some data upfront for speed while allowing autonomous exploration. Claude Code exemplifies this—CLAUDE.md files load initially while glob/grep enable just-in-time file retrieval.

### Long-Horizon Task Techniques

#### Compaction
Summarize conversation history when approaching context limits, then reinitiate with compressed summary.

**Implementation focus**: Maximize recall initially to capture all relevant details, then iterate to improve precision. Tool result clearing is the safest, lightweight form.

#### Structured Note-Taking (Agentic Memory)
Agents regularly write persistent notes outside the context window, retrieving them later.

This enables tracking progress across complex tasks without keeping everything in active memory.

#### Sub-Agent Architectures
Delegate focused tasks to specialized sub-agents with clean context windows.
- Main agent coordinates high-level planning
- Sub-agents perform deep work but return condensed summaries (1,000-2,000 tokens)

**Advantage**: Clear separation of concerns—detailed exploration stays isolated.

### Choosing the Right Approach

| Technique | Best For |
|-----------|----------|
| Compaction | Conversational tasks with extensive back-and-forth |
| Note-taking | Iterative development with clear milestones |
| Multi-agent | Complex research with parallel exploration |

### Key Warnings

- **Context pollution**: Even larger context windows face relevance concerns
- **Overly aggressive compaction**: Risks losing subtle but critical context
- **Tool misuse**: Without proper guidance, agents waste context on wrong tools

### Future Outlook

> "Smarter models require less prescriptive engineering, allowing agents to operate with more autonomy."

**Practical advice**: "Do the simplest thing that works."

---

## Actionable Items for CLAUDE.md

```markdown
## Context Management
- Monitor context with /context; compact or start fresh around 60% capacity
- Use /clear between distinct tasks
- Prefer just-in-time file loading over pre-loading everything
- Use subagents for deep exploration to keep main context clean

## Prompting
- Keep instructions specific yet flexible (right altitude)
- Use examples over extensive edge case lists
- Organize with clear sections (XML tags or Markdown headers)
```
