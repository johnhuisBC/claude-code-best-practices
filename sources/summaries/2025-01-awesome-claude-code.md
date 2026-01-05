# Awesome Claude Code

**Source**: https://github.com/hesreallyhim/awesome-claude-code
**Date**: January 2025
**Authority**: Community Curated Resource
**Status**: Active

---

## Key Takeaways

### Essential Tools & Utilities

#### Session Management
- **cchistory**: View all Bash commands executed in Claude Code sessions
- **recall**: Full-text search across sessions; resume work easily
- **cc-sessions**: Opinionated approach to productive Claude Code development

#### Usage & Cost Tracking
- **ccflare / better-ccflare**: Web dashboard with token metrics and usage analytics
- **CC Usage**: CLI tool analyzing local logs with cost information

#### Quality & Hooks
- **cc-tools**: Go-based hooks with smart linting and testing
- **cchooks**: Python SDK simplifying hook creation
- **TDD Guard**: Hooks blocking changes violating TDD principles

### Critical Workflow Patterns

#### Planning & Context
- Load project structure first via `/prime` or `/context-prime` commands
- Use CLAUDE.md files for coding standards, naming conventions, architecture
- Leverage "Agentic Workflow Patterns" for subagent orchestration

#### Version Control Integration
- Create commits via `/commit` using conventional format
- Implement `/create-pr` to automate branch creation, formatting, submission
- Use `/fix-issue` and `/fix-pr` for systematic GitHub issue resolution

#### Code Quality
- Enforce TDD with `/tdd` commands following Red-Green-Refactor
- Run `/check` for comprehensive static analysis and security scanning
- Implement pre-commit hooks using Husky for quality gates

### High-Value Slash Commands to Create

| Category | Commands |
|----------|----------|
| Context loading | `/prime`, `/initref`, `/context-prime` |
| Issue handling | `/analyze-issue`, `/fix-github-issue`, `/do-issue` |
| Testing | `/tdd`, `/tdd-implement`, `/repro-issue` |
| Documentation | `/create-docs`, `/update-docs`, `/add-to-changelog` |
| Release | `/release` |

### CLAUDE.md Best Practices

1. **Document project structure** with clear directory organization
2. **Define build/test commands** explicitly
3. **Establish code style** via linters and formatters
4. **Specify naming conventions** for files, functions, components
5. **Include testing requirements** and coverage expectations
6. **Outline deployment procedures** and CI/CD workflows

### MCP & Skills Strategy

- **Claude Codex Settings**: Pre-built skills for GitHub, Azure, MongoDB, Tavily, Playwright
- **Context Engineering Kit**: Advanced patterns with minimal token footprint
- **Basic Memory**: AI-human collaboration framework using MCP

### Orchestration & Multi-Agent Setups

- **Claude Squad**: Manages multiple Claude Code instances in separate workspaces
- **Claude Code Flow**: Code-first orchestration enabling recursive agent cycles
- **Happy Coder**: Spawn/control multiple instances with notifications

### Advanced Techniques

- **Infrastructure Showcases**: Use hooks to intelligently activate skills based on context
- **Session Continuity**: Implement cross-session memory banks
- **Container Workflows**: Run agents safely in Docker with isolation
- **Worktrees Strategy**: Use `/create-worktrees` for managing multiple PR branches

### Monitoring & Analytics

- **Vibe-Log**: Analyzes prompts locally with HTML reports
- **Claudex**: Web-based conversation history browser with full-text search

---

## Key Insight

> The most effective Claude Code workflows combine clear project documentation (CLAUDE.md), well-designed slash commands for recurring tasks, strategic hook placement for quality gates, and thoughtful context priming before major work sessions.

---

## Actionable Items for CLAUDE.md

```markdown
## Slash Commands to Create
- /prime or /context-prime - Load project structure before major work
- /commit - Create conventional commits
- /tdd - Enforce test-driven development workflow
- /check - Run linting, tests, and security scans

## Quality Gates
- Pre-commit hooks for automated formatting/linting
- TDD guard hooks to enforce test-first development
- Security scanning as part of /check workflow
```
