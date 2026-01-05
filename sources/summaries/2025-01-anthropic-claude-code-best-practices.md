# Anthropic: Claude Code Best Practices

**Source**: https://www.anthropic.com/engineering/claude-code-best-practices
**Date**: January 2025
**Authority**: Official Anthropic Engineering
**Status**: Active

---

## Key Takeaways

### Setup & Customization

#### CLAUDE.md Files
- Create configuration files that Claude automatically includes in context
- Store at: repository root, parent directories (monorepos), or home folder (`~/.claude/CLAUDE.md`)
- Document: bash commands, code style, testing instructions, repository etiquette, project quirks
- **Treat like frequently-used prompts**: iterate and refine for better instruction adherence

#### Permission Management
- Default: Claude requests approval for system-modifying actions
- Customize allowlists via:
  - "Always allow" buttons during sessions
  - `/permissions` command
  - `.claude/settings.json` or `~/.claude.json` files
  - `--allowedTools` CLI flag

#### Tool Access
- Install `gh` CLI for GitHub integration
- Document custom bash tools in CLAUDE.md (usage examples or `--help` output)

### Effective Workflows

#### Explore → Plan → Code → Commit
1. Ask Claude to read relevant files/images/URLs **without writing code**
2. Use "think," "think hard," "think harder," or "ultrathink" for extended thinking
3. Request a documented plan; save as GitHub issue for reference
4. Have Claude implement with explicit verification steps
5. Generate commits with PRs and documentation updates

#### Test-Driven Development
1. Request test cases based on input/output pairs; **be explicit about avoiding mocks**
2. Confirm tests fail before implementation
3. Commit tests first
4. Have Claude write implementation iteratively until tests pass
5. Use independent subagents to verify code isn't overfitting to tests
6. Commit final implementation

#### Visual Iteration
1. Give Claude browser screenshot capability (Puppeteer MCP, iOS simulator MCP, or manual screenshots)
2. Provide design mocks via screenshots, drag-and-drop, or file paths
3. Have Claude implement, screenshot, and iterate until matching mock
4. Expect 2-3 iterations for polished results

### Optimization Techniques

#### Be Specific
- **Poor**: "add tests for foo.py"
- **Better**: "write test case for foo.py covering the edge case where user is logged out; avoid mocks"

#### Provide Visual Context
- Paste screenshots (`cmd+ctrl+shift+4` on macOS)
- Drag-and-drop images directly
- Reference file paths for images

#### Course Correction Tools
1. Ask for a plan before coding
2. Press Escape to interrupt at any phase while preserving context
3. Double-tap Escape to jump back in history and edit previous prompts
4. Request undo of changes to pivot approaches

#### Context Management
- **Use `/clear` frequently** between tasks to reset context and maintain performance

### Multi-Claude Workflows

#### Parallel Code Review
- One Claude writes code
- Second Claude reviews or tests (fresh context advantage)
- Third Claude reads both and makes edits based on review

#### Git Worktrees
```bash
git worktree add ../project-feature-a feature-a
cd ../project-feature-a && claude
```
- Run multiple independent tasks without merge conflicts
- One terminal tab per worktree
- Clean up: `git worktree remove ../project-feature-a`

### Subagent Usage
- Use subagents to verify details or investigate specific questions early in conversations
- Preserve context availability without efficiency loss
- Validate implementations aren't overfitting to tests
- Handle parallel verification tasks

### Key Warnings

1. **Context Saturation**: Long sessions degrade performance. Use `/clear` frequently.
2. **Overfitting to Tests**: Explicitly ask for independent verification that solutions generalize.
3. **Permission Risks**: `--dangerously-skip-permissions` only in offline containers.
4. **CLAUDE.md Without Iteration**: Adding content without testing effectiveness wastes tokens.

### Core Philosophy

> Claude Code is intentionally low-level and unopinionated—close to raw model access without enforced workflows. This flexibility requires developing personal best practices. Nothing is universal; experiment to find what works for your specific use cases.

---

## Actionable Items for CLAUDE.md

```markdown
## Workflow
- Explore → Plan → Code → Commit pattern
- Use extended thinking ("think hard", "ultrathink") for complex problems
- Clear context between unrelated tasks with /clear

## Testing
- TDD: write failing tests first, then implement
- Be explicit about avoiding mocks when requesting tests
- Use independent verification to prevent test overfitting

## Course Correction
- Request plans before coding
- Use Escape to interrupt, double-Escape to rewind
```
