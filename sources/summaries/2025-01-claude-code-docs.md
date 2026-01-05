# Claude Code Official Documentation

**Source**: https://code.claude.com/docs
**Date**: January 2025 (continuously updated)
**Authority**: Official Anthropic Documentation
**Status**: Active

---

## Key Areas Covered

This is the official documentation hub. Key sections include:

### Getting Started
- Overview and quickstart guides
- Common workflows
- Claude Code on the web

### Build with Claude Code
- **Sub-agents**: Specialized agents for different tasks
- **Plugins**: Extending Claude Code functionality
- **Skills**: Reusable agent capabilities
- **Output Styles**: Customizing Claude's output format
- **Hooks**: Lifecycle event handling
- **Headless Mode**: Non-interactive/CI usage
- **GitHub Actions**: CI/CD integration
- **MCP**: Model Context Protocol servers

### Deployment
- Third-party integrations
- Amazon Bedrock setup
- Google Vertex AI setup
- Network configuration
- LLM Gateway configuration
- Devcontainer support
- Sandboxing

### Administration
- Setup and installation
- IAM and security
- Data usage policies
- Monitoring and analytics
- Cost management

### Configuration
- Settings files
- VS Code extension
- JetBrains integration
- Terminal configuration
- Model configuration
- **Memory (CLAUDE.md)**

### Reference
- CLI reference
- Interactive mode shortcuts
- Slash commands
- Checkpointing
- Hooks reference
- Plugins reference

---

## Key Documentation Highlights

### Subagents
- Built-in types: Explore, Plan, general-purpose
- Configuration via `.claude/agents.json`
- Model selection per subagent
- Tool access control

### Skills
- Create with `SKILL.md` files
- Personal, project, or plugin scope
- Restrict tool access with `allowed-tools`

### Hooks
Key events:
- `PreToolUse` / `PostToolUse`
- `PermissionRequest`
- `UserPromptSubmit`
- `Stop` / `SubagentStop`
- `SessionStart` / `SessionEnd`
- `PreCompact`

### Headless Mode
- `-p` flag for non-interactive use
- `--output-format stream-json` for streaming
- Useful for CI/CD, automation, scripting

### Memory (CLAUDE.md)
- Hierarchy: project > user > enterprise
- Use `#` shortcut to add memories quickly
- `/memory` to edit directly
- Import external files into CLAUDE.md

---

## Actionable Items

The documentation is the authoritative source. Key things to reference:

1. **Subagent configuration**: When to use which type
2. **Hooks**: For automation and quality gates
3. **Headless mode**: For CI/CD integration
4. **Settings precedence**: Understanding how configs layer

## Link for Quick Reference

https://code.claude.com/docs/llms.txt - Machine-readable documentation index
