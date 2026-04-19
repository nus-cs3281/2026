### Tool/Technology 1: GitHub Copilot

- Collaborative Context Management: Understand how to provide good context for Copilot Agent to work with, such as providing relevant files or documentation snippets (.github/copilot-instructions.md) to helps the agent generate more accurate suggestions.

- Verification and Human-in-the-Loop: Understand to treat Copilot’s output as a "first draft" that requires additional prompting and extensive testing regarding logic flow and existing architectural constraints.

- AI-Assisted Code Reviews: Use Copilot directly in GitHub to analyze PRs by asking it to explain complex logic, identify potential edge-case bugs, or ensure adherence to project standards. It can also be called directly to a review on its own.

Resources used:
- [Use custom instructions in VS Code](https://code.visualstudio.com/docs/copilot/customization/custom-instructions)
- [Choosing the Right Model in GitHub Copilot: A Practical Guide for Developers](https://techcommunity.microsoft.com/blog/azuredevcommunityblog/choosing-the-right-model-in-github-copilot-a-practical-guide-for-developers/4491623)

### Tool/Technology 2: Claude Code

- Agentic Workflows: Experimented with using autonomous subagents capable of executing multi-step tasks like major refactoring. (Breaking down into Planning + Model Making + Writing Tests + Executing with TDD)

- Efficient Branch Management (Worktrees): Leveraging Git worktrees with Claude Code to perform mutliple concurrent experimental changes in isolated environments, preventing interference with main development tasks.

Resources used: 
- [Learn git worktrees in under 5 minutes](https://www.youtube.com/watch?v=8vsRb2mTBA8)

### Tool/Technology 3: `renovate` Bot

- Automated Dependency Updates: `renovate` is a bot that automatically creates pull requests to update project dependencies. It scans dependencies on a configurable schedule, detects available updates, and creates PRs with version bumps—reducing manual effort and keeping projects up-to-date.

- Group-Based Dependency Configuration: Configured `renovate` with grouping strategies to batch related dependency updates into single PRs rather than creating one PR per package. This approach reduces notification noise and allows teams to test grouped updates together, improving safety and reducing merge overhead for projects with many dependencies.

Resources used:
- [Renovate Documentation](https://docs.renovatebot.com/configuration-options/)

### Tool/Technology 4: Model Context Protocol (MCP)

- Understand what is MCP, which is a protocol enabling AI agents to securely access custom tools and resources by acting as an API between AI models and external services.

- Setting Up Custom MCP Servers: Define tools with schemas, add instructions for AI guidance, implement handlers, and connect via HTTP. Tailor tools and instructions for your specific use cases.

Resources used:
- Letian's Teachback 👍👍👍
- [Model Context Protocol Documentation](https://modelcontextprotocol.io/)
