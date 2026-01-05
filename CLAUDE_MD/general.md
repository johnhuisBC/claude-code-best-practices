# General CLAUDE.md Rules

These rules apply to any project. Copy relevant sections to your project's CLAUDE.md or your global `~/.claude/CLAUDE.md`.

---

## Context Management

- Monitor context with `/context`; clear or compact around 60% capacity
- Use `/clear` between distinct, unrelated tasks
- For long sessions on one task, compact before context fills
- Repeat key objectives in prompts to combat attention degradation

## Workflow

- Follow Explore → Plan → Code → Commit pattern for non-trivial changes
- Use extended thinking ("think hard", "ultrathink") for complex problems
- Ask for a plan before coding; verify it looks correct
- Use Escape to interrupt, double-Escape to rewind and try alternatives

## Prompting

- Be specific: include edge cases, constraints, and expected behavior
- Provide visual context for UI work (screenshots, mocks)
- Use examples over exhaustive edge case lists
- Ask clarifying questions before implementing

## Testing

- Write failing tests first (TDD), then implement
- Be explicit about avoiding mocks when requesting tests
- Use independent verification to prevent test overfitting
- Run full test suite, not just new tests

## Subagents

- Use Explore agent for codebase search and discovery
- Use subagents for parallel or deep-dive tasks
- Avoid subagents for simple tasks (< 2-3 tool calls)
- Use independent subagents to verify implementations

## Code Quality

- Only make changes directly requested or clearly necessary
- Don't add features, refactoring, or "improvements" beyond scope
- Keep solutions simple and focused
- Avoid over-engineering and premature abstractions

## Course Correction

- Request plans before coding
- Interrupt with Escape when going off track
- Request undo to pivot approaches
- Use checkpoints to try alternatives

---

## Usage

Copy the sections above to your CLAUDE.md. Keep total file under 500 lines (ideally under 300).

For project-specific additions, see:
- [templates/python.md](templates/python.md)
- [templates/typescript.md](templates/typescript.md)
