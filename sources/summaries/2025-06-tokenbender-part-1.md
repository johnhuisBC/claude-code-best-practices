# tokenbender: How I Bring the Best Out of Claude Code - Part 1

**Source**: https://tokenbender.com/post.html?id=how-i-bring-the-best-out-of-claude-code
**Author**: tokenbender
**Date**: June 14, 2025
**Authority**: Community Power User
**Status**: Active

---

## Key Takeaways

### 1. Setup Requirements

Store requirements as files (e.g., `issues/<issue_no>.md`):
- Your requirements list is crucial - treat it like a wish list
- **The more vague you are, the higher the chance you won't get what you wanted**
- Ideally, instructions should be as unambiguous as a program
- Be aware of what is already known by the model

### 2. Context Management (Most Important)

**Common pattern** (not ideal):
```
[claude code] --> [todo list]
               (fresh context)
```

**Better approach**:
```
well-formalized --> issues/<issue_no>.md (issue requirement)
                --> docs/plan_<issue_no>.md (plan)
```

- The `plan_<issue_no>.md` serves as Claude's context
- The todo list is nice but hard to keep up as context grows
- Store todo in a file (`todo.md`) so it persists

### 3. Parallel Claude Code Usage

When using multiple Claude Code windows:
- Assign each one an issue with its corresponding docs, todos, and requirements
- Everything gets tracked automatically

**Current limitations** (author avoids parallel usage because Claude tends to):
- Create new files for everything
- Edit existing files in unexpected ways
- Update code based on outdated understanding
- Run commands unknowingly, filling context with needless output

**Solutions**:
- Ask Claude to detail its plan for "smell checks"
- Question intentions: "You were aiming to do xyz. Then why modify abc?"
- Run commands manually yourself, provide error snippets for debugging

### 4. Execution Strategy

- Go through each item step by step
- Enforce quality standards
- Decide how frequently to execute
- Ensure there are no blindspots
- **Avoid diving into thousands of LOC you haven't written or understood**

### 5. Iteration and Updating Context

As you implement:
1. Iterate with errors and debug
2. Go back and update crucial observations in planning docs
3. This allows the model to build better understanding

### 6. Working Compactly

**Ideal**: Work on one issue end-to-end in one session

**Reality**: Context fills out faster and faster
- Use "compact" more often
- If context runs out, Claude auto-compacts or asks to go back

**When model ignores feedback and loops**:
1. Jump to a clean node where you were satisfied
2. Compact
3. Generate a summary
4. Start fresh

### 7. Integrating Claude Code into Tooling

With Claude Code SDK:
- Add Claude to shell scripts and proto files
- Protocols reflect opinionated views of methodologies
- Build a local multi-agent system

**Author's ecosystem**:
- `issues/` folder
- `todo.md` files
- Shell scripts to invoke tasks
- Claude instances interacting with other Claude instances

---

## Key Insights

1. **File-based context management** beats in-memory todo lists
2. **Plans should be stored as files** that persist through sessions
3. **Question Claude's intentions** before accepting changes
4. **Run commands manually** to control what fills context
5. **Jump back to clean nodes** when Claude gets stuck in loops

---

## Actionable Items for CLAUDE.md

```markdown
## Context Management
- Store requirements in issues/<issue_no>.md
- Store plans in docs/plan_<issue_no>.md
- Keep todo in file (todo.md) not just in-context list
- Update planning docs with observations during implementation

## Execution
- Review Claude's plan before implementation ("smell check")
- Question unexpected modifications
- Run commands manually, share error snippets
- Avoid diving into large codebases you don't understand
```
