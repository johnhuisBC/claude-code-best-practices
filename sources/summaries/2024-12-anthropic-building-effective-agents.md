# Anthropic: Building Effective Agents

**Source**: https://www.anthropic.com/engineering/building-effective-agents
**Date**: December 2024
**Authority**: Official Anthropic Engineering
**Status**: Active

---

## Key Takeaways

### Core Principle

> Success isn't about sophistication—it's about building the *right* system for your needs. Start simple and increase complexity only when it demonstrably improves outcomes.

### When NOT to Use Agents
- For simple tasks optimizable through single LLM calls with retrieval and in-context examples
- When latency and cost are critical concerns (agents trade both for better performance)
- When predefined workflows suffice for well-defined tasks

### Architectural Distinction

| Type | Description |
|------|-------------|
| **Workflows** | LLMs and tools orchestrated through predefined code paths |
| **Agents** | LLMs dynamically directing their own processes and tool usage |

### Key Workflow Patterns

1. **Prompt Chaining**: Decompose tasks into sequential steps with programmatic gates
   - Use for: Fixed subtasks (e.g., writing then translating content)

2. **Routing**: Classify inputs and direct to specialized handlers
   - Use for: Distinct task categories or model-selection optimization

3. **Parallelization**: Run subtasks simultaneously or multiple attempts
   - Sectioning: Independent parallel subtasks
   - Voting: Multiple attempts for higher confidence

4. **Orchestrator-Workers**: Central LLM dynamically breaks tasks and delegates
   - Use for: Unpredictable subtasks (e.g., multi-file code changes)

5. **Evaluator-Optimizer**: Iterative refinement with feedback loops
   - Use for: Tasks with clear evaluation criteria (e.g., literary translation)

### When Agents Work Best
- Tasks are open-ended with unpredictable steps
- You can't hardcode fixed paths
- Clear success criteria exist
- Environmental feedback guides iteration
- You have trust in model decision-making

**Critical requirement**: Extensive testing in sandboxed environments with appropriate guardrails.

### Three Core Principles for Implementation

1. **Simplicity**: Keep agent design straightforward
2. **Transparency**: Explicitly show planning steps
3. **Tool Design**: Invest as much effort in agent-computer interfaces as you would in user-facing interfaces

### Framework Guidance

Frameworks (Claude Agent SDK, etc.) simplify setup but add abstraction layers that obscure prompts and responses.

**Recommendation**: Start with LLM APIs directly; use frameworks only if you understand underlying mechanics.

### Tool Development Best Practices

- Give models sufficient tokens to "think" before writing
- Keep formats close to naturally occurring internet text
- Eliminate formatting overhead (line counting, string escaping)
- Include example usage, edge cases, and input format requirements
- Test extensively to identify mistakes and iterate
- Use "poka-yoke" principles to make errors harder

**Key insight**: Tool optimization often deserves more attention than overall prompt engineering.

### Critical Warnings

- Autonomous agents mean higher costs and potential for compounding errors
- Incorrect framework assumptions are common error sources
- Human review remains crucial despite automated verification
- Frameworks can tempt unnecessary complexity addition

---

## Relevance to Claude Code

This informs **when** to use Claude Code's agentic features:
- Use simple prompts for straightforward tasks
- Use subagents for parallel or specialized work
- Use workflows (custom commands) for predictable, repeatable tasks
- Reserve full agentic behavior for open-ended exploration

## Actionable Items for CLAUDE.md

```markdown
## Agent Usage Philosophy
- Start simple; add complexity only when demonstrably needed
- Use predefined workflows (slash commands) for repeatable tasks
- Reserve agentic exploration for open-ended problems
- Always maintain human review for critical changes
```
