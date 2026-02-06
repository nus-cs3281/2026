### Github Copilot

GitHub Copilot is a sophisticated AI-powered developer tool that functions as an intelligent pair programmer, helping developers write code with greater efficiency and less manual effort. Unlike traditional autocomplete, it uses advanced large language models to understand the deep context of the project to suggest everything from single lines of code to entire functional blocks. By automating routine tasks and providing real-time technical guidance, it allows developers to focus more on high-level problem solving and architectural design.

<b>Learning Points:</b>
* <b>Ensure Full Repo Understanding:</b> Before implementation, provide Copilot with comprehensive context by indexing the repository and opening relevant files to ensure it understands the project structure and architectural decisions.
* <b>Verify Understanding via Q&A:</b> Use a Q&A section in Copilot Chat to clarify its internal logic and ensure it isn't making false assumptions about the codebase. Explicitly asking AI not to assume but to verify against actual files (like package.json or custom logic) prevents confident but incorrect "hallucinations".
* <b>Provide Existing Code Examples:</b> Feed Copilot snippets of the existing project patterns to ensure consistency across the codebase.
* <b>Demand a Full Implementation Plan:</b> Instruct Copilot to generate a step-by-step reasoning plan before it writes a single line of code. Breaking down complex tasks into atomic, verifiable steps allows developers to identify logical flaws in the AI's approach early on.
* <b>Evaluate Multiple Solutions:</b> Prompt Copilot to offer several distinct solutions so developers can evaluate the trade-offs in robustness and platform compatibility themselves. Moreover, developers can also provide some possible solution to Github Copilot for evaluation.

<b>Resources:</b>
* [Github Copilot Documentation](https://docs.github.com/en/copilot)
* [Voiceflow: How to Prevent LLM Hallucinations](https://www.voiceflow.com/blog/prevent-llm-hallucinations)


### CodeRabbit
CodeRabbit is an AI-powered code review tool that integrates directly into developers' GitHub Pull Requests (PRs). For team project, it acts as an automated "gatekeeper" that catches common mistakes before a human mentor reviews the code.

<b>Learning Points:</b>
* <b>Learn automated context-aware reviews:</b> CodeRabbit analyzes the entire repository to understand how a change in one file might break another, providing instant, comprehensive feedback on every pull request.
* <b>Identify edge cases in PRs:</b> It identifies potential issues, such as bugs that static analyzers miss, security oversights, and logic errors that only surface under specific conditions.
* <b>Summarize complex changes:</b> It automatically generates a summary and walkthrough of code changes, which is particularly handy for large PRs where context helps teammates understand the scope of the work.

<b>Resources:</b>
* [CodeRabbit Documentation](https://docs.coderabbit.ai/)
* [CodeRabbit: 10 Best Practices for GitHub Copilot](https://www.coderabbit.ai/blog/github-copilot-best-practices-10-tips-and-tricks-that-actually-help)

### Claude Agent Skills
Claude Agent Skills is a specialized feature within the Claude ecosystem that allows developers to define and package complex, reusable behaviors as "skills" that the AI can invoke when needed.

<b>Learning Points:</b>
* <b>Encapsulate Domain Logic:</b> Developers can create specific skills that encapsulate the complex logic of their project, such as a "Scope-Parser-Skill" that handles the different scenario, ensuring the AI uses the most robust method every time.
* <b>Modularize Intelligence:</b> Instead of overwhelming the AI with a massive list of instructions, developers can break them into modular skills that the agent only activates when the context of the task requires them.
* <b>Continuous Skill Refinement:.</b> Developers can iteratively improve these skills by feeding the agent feedback from failed runs.

<b>Resources:</b>
* [Claude Agent Skills Overview](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview)