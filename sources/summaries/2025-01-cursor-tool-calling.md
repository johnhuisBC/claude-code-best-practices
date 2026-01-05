# Cursor: Tool Calling in AI Coding Assistants

**Source**: https://cursor.com/learn/tool-calling
**Date**: January 2025
**Authority**: Cursor (AI Coding Tool)
**Status**: Active

---

## Key Takeaways

### Core Concepts

**What Tool Calling Is**:
Tool calling enables AI models to "call other APIs themselves" rather than being limited to text generation.

**Process**:
1. Model recognizes needed capability
2. Returns JSON-formatted response specifying tool and parameters
3. Application executes the tool
4. Result incorporated into context

**Why It Matters**:
Without tools, models rely solely on explicitly provided context. Tool calling allows models to actively explore codebases and interact with environments dynamically.

### Essential Tool Components

Every tool requires three fundamental elements:

| Element | Purpose |
|---------|---------|
| **Name** | Identifies the tool (e.g., `read_file`) |
| **Description** | Clarifies when and how to use it |
| **Parameters** | Specifies required inputs with purposes |

### Practical Capabilities

Tools empower AI models to:
- Read and write codebase files
- Search code for relevant functions or patterns
- Execute shell commands for testing/installation
- Access current documentation or web information
- Run linters and tests for error detection

### Token Cost Considerations

Tool usage affects pricing in two ways:
- **Tool definitions** consume input tokens (typically hundreds per tool)
- **Tool results** add output tokens based on returned data

> "Conversations with lots of tool usage will fill up the context window faster and cost more."

However, the tradeoff often justifies itself through improved AI assistance quality.

### Best Practice: Use MCP

The Model Context Protocol (MCP) provides a universal standard for tool integration, allowing developers to build tools once for use across multiple AI applications.

---

## Relevance to Claude Code

While this source is from Cursor, the principles apply to Claude Code:

1. **Understand tool cost**: Heavy tool usage fills context faster
2. **Tool design matters**: Clear names, descriptions, and parameters improve model selection
3. **MCP compatibility**: Tools built for MCP work across AI assistants

## Actionable Items for CLAUDE.md

```markdown
## Tool Usage Awareness
- Heavy tool usage fills context faster
- Consider cost vs. benefit of each tool invocation
- Prefer built-in tools with clear definitions over custom tools with ambiguous purposes
```
