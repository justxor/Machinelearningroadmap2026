# Claude Code course

A practical course on using **Claude Code** — Anthropic's terminal AI agent — for development, refactoring, debugging, and automating work with code.

The course targets engineers who do not just want to "write prompts" but want to embed the agent into a real workflow: reading large codebases, building features, code review, migrations, working with tests, CI/CD, MCP servers, and their own tools.

## What Claude Code is

Claude Code is a CLI tool that runs the Claude model in your terminal with direct access to files, shell commands, git, tests, the browser (via MCP), and any external systems. Unlike a chat, the agent reads the repository itself, plans changes, edits files, runs commands, and iteratively verifies the result.

Key differences from copilots:
- Works at the repository level, not at the level of a single file
- A full agent loop: plan → action → observation → correction
- Extensible via MCP servers and custom commands
- Headless mode for CI and automation

## Course structure

### Block 1. Foundations
- [01. Installation and first run](01-setup.md)
- [02. CLAUDE.md and project context](02-claude-md.md)
- [03. Basic commands and modes](03-commands-modes.md)
- [04. Permissions and safety](04-permissions.md)

### Block 2. Workflow
- [05. Reading and navigating the codebase](05-codebase-navigation.md)
- [06. Implementing features end-to-end](06-feature-development.md)
- [07. Debugging and bug hunting](07-debugging.md)
- [08. Tests and TDD with the agent](08-testing-tdd.md)
- [09. Refactoring and migrations](09-refactoring.md)
- [10. Git, branches, PRs](10-git-workflow.md)

### Block 3. Extensions
- [11. MCP: Model Context Protocol](11-mcp-basics.md)
- [12. Connecting MCP servers](12-mcp-servers.md)
- [13. Custom slash commands](13-custom-commands.md)
- [14. Subagents and parallelism](14-subagents.md)
- [15. Hooks and automation](15-hooks.md)

### Block 4. Production
- [16. Headless mode and CI/CD](16-headless-ci.md)
- [17. Cost, tokens, context](17-cost-context.md)
- [18. Anti-patterns and common mistakes](18-antipatterns.md)

## Practice

- [Cheatsheet: commands, flags, patterns](cheatsheet.md)
- [Capstones: 3 real projects](capstones/README.md)

## What you will be able to do after the course

- Run Claude Code in any project and tune CLAUDE.md for your team
- Hand off features, bugs, and refactors to the agent without micromanaging every step
- Write custom slash commands and connect MCP servers (Postgres, Playwright, Sentry, your own)
- Embed the agent in CI: auto-generated PRs, reviews, test fixing
- Control cost, context, and risks (permissions, sandbox, git hygiene)

## Requirements

- A terminal (macOS/Linux/WSL), Node.js 18+
- An Anthropic account with API access or a Claude Pro/Max subscription
- Basic git and shell

---

Next: [01. Installation and first run →](01-setup.md)
