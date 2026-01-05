# tokenbender: How I Bring the Best Out of Claude Code - Part 2

**Source**: https://tokenbender.com/post.html?id=how-i-bring-the-best-out-of-claude-code-part-2
**Author**: tokenbender
**Date**: June 19, 2025
**Authority**: Community Power User
**Status**: Active
**Repository**: https://github.com/tokenbender/agent-guides

---

## Key Takeaways

### Philosophy

> "Everything I feel like doing multiple times as a prompt should be a command."

> "Stop repeating yourself. If you do something twice, make it a command."

### 1. Multi-Mind: Solving Hallucinations with Multiple Agents

**Problem**: Models confidently tell you wrong things, may be sycophantic, lack opposing viewpoints.

**Solution**: Spawn 4-6 specialist subagents that work independently:

```
/multi-mind "find security vulnerabilities in our auth system"
```

Specialists:
- Security Analyst
- Edge Case Hunter
- Performance Auditor
- API Contract Validator

**How it works**:
- Each works independently (can't see each other's initial analysis)
- After finishing, they review each other's findings
- **Independent verification kills hallucinations**

> "Caught a timing attack that single-agent analysis completely missed."

### 2. Conversation Search: Your Second Brain

**Problem**: Solving problems at 3am, then forgetting the solution.

**Solution**: Search through conversation history:

```
/search-all "redis optimization"
```

Searches through:
- SQLite conversation history
- Exported JSON sessions
- Current context

**Use cases**:
- Run analytics on your conversations
- Discover your preferences
- Have preferences reflected in future commands

> "Your past conversations are a goldmine. Most people just let them rot."

### 3. Session Paging: Infinite Context Hack

**Problem**: Claude's context fills up, work gets lost.

**Solution**: Page out sessions like OS memory:

```
/page "ml pipeline progress checkpoint 1"
```

Saves:
- Complete state
- Generated summaries
- Preserved citations
- Lets you pick up exactly where you left off

Resume with:
```
claude --resume checkpoint-1
```

> "Treat context like OS memory. Page out, page in, never lose work."

### 4. Deep Code Analysis

**Problem**: Simple explanations derived from docstrings aren't enough.

**Solution**: Deep reasoning about code:

```
/analyze-function "def batch_process(items, workers=4):"
```

Analysis includes:
- Line-by-line performance implications
- Hidden complexity (found O(n²) in "linear" code)
- Edge cases missed
- Mathematical foundations
- Optimization opportunities

### 5. CRUD Commands: Build Your Own Commands

**Problem**: Typing the same prompts repeatedly.

**Solution**: Meta-command system to create/manage commands:

```
/crud-claude-commands create git-flow "automate git flow operations"
/crud-claude-commands read git-flow
/crud-claude-commands update git-flow "enhanced workflow..."
/crud-claude-commands delete git-flow
/crud-claude-commands list
```

**Power**: Rapid iteration - prototype, test, refine, share.

### 6. Workflow Examples

**Architecture reviews**:
```
/multi-mind "review our microservices for bottlenecks"
→ 5 specialists work in parallel
→ cross-pollination finds blind spots
→ /page "architecture-review-final"
```

**Debugging**:
```
/search-all "null pointer kubernetes"
→ find similar past issues
→ /analyze-function on suspect code
→ multi-mind verification of fix
```

**Long projects**:
```
issue #142 → docs/plan_142.md
→ work until context fills
→ /page "issue-142-session-1"
→ resume seamlessly next day
```

### 7. Protocols Being Enforced

1. **Single responses are hypotheses, not truth** - Always verify through multiple agents or past evidence
2. **Every conversation builds lasting value** - Searchable, reusable, compounding knowledge
3. **Small tools compose into powerful workflows** - Unix philosophy for AI assistance
4. **Context is precious, manage it** - Page out before you lose work
5. **Knowledge reuse is key** - Every conversation builds lasting value

### 8. Multi-Agent Design Benefits

- **Error decorrelation**: Agents make different mistakes; consensus filters out individual errors
- **Specialist depth**: Focused expertise beats generalist responses
- **Progressive refinement**: Cross-pollination rounds systematically improve quality

> "No more 'Claude said so' disasters. Multiple independent verification or it didn't happen."

### 9. Setup

```bash
git clone https://github.com/tokenbender/agent-guides
cd agent-guides

# Install commands in your project
mkdir -p /path/to/your/project/.claude/commands
cp -r claude-commands/* /path/to/your/project/.claude/commands/

# Copy supporting scripts
cp -r scripts /path/to/your/project/.claude/scripts/
```

Available commands:
```
claude-commands/
├── multi-mind.md           # parallel specialist analysis
├── search-prompts.md       # conversation archaeology
├── page.md                 # session state management
├── analyze-function.md     # deep code reasoning
└── crud-claude-commands.md # dynamic command creation
```

---

## Key Unique Insights

1. **Multi-agent verification** solves hallucination/sycophancy problems
2. **Conversation history as searchable knowledge base** - don't let it rot
3. **Session paging** like OS memory management
4. **Meta-commands** to create commands on the fly
5. **Unix philosophy** for AI tools - small, composable

---

## Actionable Items for CLAUDE.md

```markdown
## Verification
- Use multi-agent verification for important decisions
- Single responses are hypotheses, not truth
- Multiple independent verification or it didn't happen

## Knowledge Management
- Search past conversations before solving problems
- Page out sessions before context fills
- Every conversation should create lasting value

## Commands
- If you do something twice, make it a command
- Build a library of reusable commands
- Prototype, test, refine, share
```
