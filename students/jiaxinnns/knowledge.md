### GitHub Copilot

GitHub Copilot is an AI-powered coding assistant built by GitHub and OpenAI that helps programmers write code faster and with less effort.

Learning points:
- Give examples of existing code with similar functionality, to avoid hallucination and ensure the code quality is consistent across the codebase
- Properly describe the expected usage of the product which is not always obvious when implementing libraries and dependencies. This can affect the implementation method chosen.
- Ask for many possible solutions (ie. planning) and evaluate them yourself before deciding on one and guiding the AI tool to implement it.

Resources:
- GitHub website
- Agentic AI prompting: https://www.ranthebuilder.cloud/post/agentic-ai-prompting-best-practices-for-smarter-vibe-coding


### Claude Code

Claude Code is an AI coding assistant by Anthropic that helps with code generation, refactoring, debugging, and repository-level understanding through natural language instructions.

Learning points:
- Give explicit constraints (tech stack, coding style, and file targets) so the tool can make precise edits with fewer iterations.
- Use task-specific command modes (for example `/review`) to get focused outputs for different goals such as code review, planning, or implementation.

Resources:
- Claude Code documentation: https://docs.anthropic.com/en/docs/claude-code


### Devin AI

Devin AI is an autonomous AI software engineer by Cognition that can browse the web, write code, and perform multi-step engineering tasks with minimal human intervention.

Learning points:
- Use Devin for code reviews by pointing it to a specific PR and asking targeted questions, as it can read diffs and provide contextual feedback. It is able to track logic across different files and flag bugs and inconsistencies which involve multiple files, which other AI review agents were unable to flag.

Resources:
- Devin documentation: https://docs.devin.ai