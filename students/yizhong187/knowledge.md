### Tool/Technology 1: GitHub Copilot

- Collaborative Context Management: Understand how to provide good context for Copilot Agent to work with, such as providing relevant files or documentation snippets (.github/copilot-instructions.md) to helps the agent generate more accurate suggestions.

- Verification and Human-in-the-Loop: Understand to treat Copilot’s output as a "first draft" that requires additional prompting and extensive testing regarding logic flow and existing architectural constraints.

- AI-Assisted Code Reviews: Use Copilot directly in GitHub to analyze PRs by asking it to explain complex logic, identify potential edge-case bugs, or ensure adherence to project standards. It can also be called directly to a review on its own.

Resources used:
- (Use custom instructions in VS Code)[https://code.visualstudio.com/docs/copilot/customization/custom-instructions]
- (Choosing the Right Model in GitHub Copilot: A Practical Guide for Developers)[https://techcommunity.microsoft.com/blog/azuredevcommunityblog/choosing-the-right-model-in-github-copilot-a-practical-guide-for-developers/4491623]

### Tool/Technology 2: Claude Code

- Agentic Workflows: Experimented with using autonomous subagents capable of executing multi-step tasks like major refactoring. (Breaking down into Planning + Model Making + Writing Tests + Executing with TDD)

- Efficient Branch Management (Worktrees): Leveraging Git worktrees with Claude Code to perform mutliple concurrent experimental changes in isolated environments, preventing interference with main development tasks.

Resources used: 
- (
learn git worktrees in under 5 minutes)[https://www.youtube.com/watch?v=8vsRb2mTBA8]
