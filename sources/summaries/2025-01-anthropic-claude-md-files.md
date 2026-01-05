# Anthropic: Using CLAUDE.md Files

**Source**: https://claude.com/blog/using-claude-md-files
**Date**: January 2025
**Authority**: Official Anthropic
**Status**: Active

---

## Key Takeaways

### What CLAUDE.md Is
A configuration file providing Claude with persistent project context across conversations. Can be placed in:
- Repository root
- Parent directories (monorepos)
- Home folder for universal application

### Key Purposes
- Provides architectural context without repetition
- Establishes coding standards and workflows
- Connects Claude to development tools and custom utilities
- Prevents rework through consistent process guidance

### Essential Sections

1. **Project Summary** - Brief overview of what the project does
2. **Directory Map** - Tree structure showing key locations (helps Claude navigate)
3. **Standards** - Type hints, code style, line length, formatting rules
4. **Common Commands** - Development, testing, and deployment commands with examples
5. **Dependencies & Frameworks** - Key libraries and architectural patterns
6. **Workflows** - Step-by-step processes for different task types
7. **Testing Requirements** - How to validate changes
8. **Notes** - Project-specific warnings or context

### What to Include

**Workflow Documentation**
- Define standard processes before implementation
- Example: "Before modifying X: consider effects on A, B, C; construct implementation plan; develop test plan"

**Tool Integration**
- Document custom tools with usage examples and help flags
- Include MCP server configurations with usage guidelines

**Code Patterns**
- Domain-specific patterns
- Non-standard organizational choices
- Architectural decisions your team repeatedly explains

**Testing Protocols**
- Test framework locations
- Fixture paths
- Validation requirements

### What to Avoid

**Never Include**:
- API keys, credentials, or connection strings
- Sensitive security vulnerability details
- Information unsuitable for version control
- **Overly comprehensive documentation** (keep it concise)

**Key Warning**: File size matters—CLAUDE.md becomes part of Claude's system prompt, so context bloat reduces effectiveness.

### Getting Started: The `/init` Command

Running `/init` automatically:
- Analyzes codebase structure
- Reads package files and configuration
- Generates starter CLAUDE.md with detected patterns

**Important**: Treat generated output as starting point, not finished product.

### Best Practices

**Keep It Fresh**
- Use `/clear` between distinct tasks to reset context while preserving CLAUDE.md

**Reference External Files**
- Break large information into separate markdown files
- Reference them within CLAUDE.md to manage context

**Version Control**
- Commit CLAUDE.md to repositories for team benefit

**Iterative Improvement**
- Add instructions you find yourself repeating using the `#` key
- Effective files evolve with your codebase

### Advanced Techniques

**Subagents for Distinct Phases**
- Use separate subagents for isolated analysis
- Prevents earlier context from coloring fresh perspectives

**Custom Commands**
- Store repetitive prompts as markdown in `.claude/commands/`
- Become slash commands supporting arguments via `$ARGUMENTS`

---

## Key Principle

> Effective CLAUDE.md files solve real problems rather than theoretical concerns. Document workflows matching how your team actually develops, not idealized practices.

---

## Template Structure

```markdown
# Project Name

Brief description of what this project does.

## Directory Structure
```
src/
├── components/    # React components
├── services/      # API and business logic
└── utils/         # Shared utilities
```

## Development Commands
- `npm run dev` - Start development server
- `npm test` - Run tests
- `npm run lint` - Run linter

## Code Standards
- TypeScript strict mode
- Prettier for formatting
- ESLint for linting

## Workflows

### Adding a New Feature
1. Create feature branch from main
2. Write failing tests first
3. Implement feature
4. Ensure all tests pass
5. Create PR with description

## Project-Specific Notes
- [Any quirks or important context]
```
