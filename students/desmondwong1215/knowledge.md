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
* <b>Continuous Skill Refinement:</b> Developers can iteratively improve these skills by feeding the agent feedback from failed runs.

<b>Common Usage:</b><br>
We will create `AGENTS.md` file. It will contain high-level overview of the repository. Moreover, `.claude` folder will also be created, it will contains different `skill.md` files, which contain a more detailed information about the specific component of the repository.<br>
Ideally, when we give a task to AI Agent, it will read through `AGENTS.md` file to identify the `skills` needed to perform the task. Thus, it only need to read the relevant `skill.md`.

<b>Resources:</b>
* [Claude Agent Skills Overview](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview)

### Git Worktree
Git Worktree is a native Git feature that allows developers to manage multiple working directories (worktrees) attached to a single repository.

<b>Learning Points:</b>
* <b>Eliminate Context Switching Friction:</b> Instead of using git stash and git checkout to move between branches, developers simply change directories. This preserves their uncommitted changes, terminal history, and IDE state in each branch exactly where developers left them.
* <b>Optimized Resource Usage:</b> Worktrees share the central `.git` directory and object database, making them much faster and lighter than a full `git clone`.
* <b>Isolated "Agent" Workspaces:</b> In a AI-driven workflow, developers can assign a dedicated AI agent (like Claude Code) to its own worktree. This provides the agent with a bounded context where it can research, build, and test a specific task without interfering with their primary work or other ongoing AI tasks.

<b>Common Usage:</b><br>
Suppose we are working on a repo named `worktree`. We can create a new worktree using
```bash
git worktree add ../worktree-testing
```
which create a directory named `worktree-testing` at the same level as `worktree`. A new branch `worktree-testing`, which is the same as directory name, will be created. If we want to specify the branch name, we can use
```bash
git worktree add ../worktree-testing -b hotfix
```
Note that no two worktrees can work on the same branch. Now, we can open `worktree-testing` separately and make changes accordingly.

---

If we want to see the full list of worktrees, we can use
```bash
git worktree list
```

---

Once we are comfortable with the changes, we can just merge or rebase the branch, which is similar to our usual workflow.
```bash
git merge hotfix
git rebase hotfix
```

---

To delete the worktree, we can remove the `worktree-testing` directory, and it will be marked as prunable. Then, we can run
```bash
git worktree prune
```
Besides, we can remove clean worktrees (no untracked files and no modification in tracked files) by running
```bash
git worktree remove ../worktree-testing 
```

<b>Resources:</b>
* [Git Worktree Documentation](https://git-scm.com/docs/git-worktree)

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

### ChatGPT Codex App

ChatGPT Codex App is an AI coding assistant that helps developers go from idea to working code faster. Instead of only suggesting the next line, it can help with planning, implementation, debugging, and documentation, so it feels more like a practical coding partner in day-to-day work.

<b>Learning Points:</b>
* <b>Turn plain language into real coding tasks:</b> We can describe the task (debugging, fixing bugs, new implementation, etc) to Codex. Codex can give me a detailed implementation plan before it starting coding. We can exchange idea to better improve our approaches. Once we have reached an agreement, then started coding. Streamline the process, and speed up the development cycle
* <b>Use project context for better output:</b> Codex gives much stronger suggestions when it can read the relevant files first, because it can follow the repo's structure, naming style, and existing patterns.
* <b>Reduce mistakes with quick verification:</b> A good habit is to ask Codex to explain assumptions, point to specific files, and run checks or tests so the final result is safer and more accurate.
* <b>Speed up debugging work:</b> It can help trace likely root causes, propose focused fixes, and produce small patches that are easier for teammates to review.
* <b>Write clearer docs faster:</b> Codex is also useful for drafting PR summaries, technical notes, and simple explanations for complex code changes.

<b>Resources:</b>
* [Best Practices when Using Codex](https://developers.openai.com/codex/learn/best-practices)
