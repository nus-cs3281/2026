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
* <b>Turn plain language into real coding tasks:</b> We can describe the task (debugging, fixing bugs, new implementation, etc) to Codex. Codex can give me a detailed implementation plan before it starting coding. We can exchange idea to better improve our approaches. Once we have reached an agreement, then started coding. Streamline the process, and speed up the development cycle.
* <b>Use project context for better output:</b> Codex gives much stronger suggestions when it can read the relevant files first, because it can follow the repo's structure, naming style, and existing patterns.
* <b>Reduce mistakes with quick verification:</b> A good habit is to ask Codex to explain assumptions, point to specific files, and run checks or tests so the final result is safer and more accurate.
* <b>Speed up debugging work:</b> It can help trace likely root causes, propose focused fixes, and produce small patches that are easier for teammates to review.
* <b>Write clearer docs faster:</b> Codex is also useful for drafting PR summaries, technical notes, and simple explanations for complex code changes.

<b>Resources:</b>
* [Best Practices when Using Codex](https://developers.openai.com/codex/learn/best-practices)

### GitHub Actions

GitHub Actions is a CI/CD automation platform built into GitHub that lets us run workflows directly from our repository. It helps automate repetitive engineering tasks like testing, linting, building, and deployment whenever events such as push, pull request, or manual dispatch happen.

<b>Learning Points:</b>
* <b>Automate development workflow:</b> We can define workflows in YAML files under `.github/workflows` to automatically run checks and scripts, which reduces manual work and human error.
* <b>Protect code quality in pull requests:</b> By running unit tests, lint checks, and security scans on every PR, GitHub Actions helps us catch issues early before merging.
* <b>Use event-driven pipelines:</b> Workflows can be triggered by repository events (e.g., `push`, `pull_request`, `release`) so automation happens at the right stage of the development cycle.
* <b>Reuse and scale with actions:</b> We can use community actions from GitHub Marketplace or create our own custom actions to keep workflows modular and maintainable.
* <b>Secure secrets and deployments:</b> GitHub Actions integrates with encrypted secrets and environment protection rules, allowing safer automation for deployment and external service integration.

<b>Common Usage:</b><br>
Create a workflow file at `.github/workflows/ci.yml` and define jobs for testing/building.

An `Action` is a packaged automation step we can use in a workflow. There are lots of prebuilt `Actions` made by Github or third parties. We can find these reusable `Actions` from [Marketplace](https://github.com/marketplace?type=actions)

```yaml
name: CI

on:
	pull_request:
	push:
		branches: [ main ]

jobs:
	test:
		runs-on: ubuntu-latest
		steps:
			- uses: actions/checkout@v4
			- name: Setup Node
				uses: actions/setup-node@v4
				with:
					node-version: 20
			- run: npm ci
			- run: npm test
```

Jobs run in parallel unless `needs` is added. Each job has its own steps, and is run in separated virtual environment. Steps inside one job run in order. 

{% raw %}
`${{}}` is Github Actions expression syntax. `${{ secrets.USERNAME }}` reads an encrypted secret at runtime, and their values are masked in logs. Secrets can be passed through `with:` or `env:`.

```yaml
jobs:
	test:
		runs-on: ${{ matrix.os }}
		strategy:
			matrix:
				os: [ubuntu-latest, macos-latest, windows-latest]
	steps:
		- uses: actions/setup-node@v4
			with: 
				username: ${{ secrets.USERNAME }}
				password: ${{ secrets.password }}
		- run: echo test
	
	deploy:
		needs: test
		runs-on: ubuntu-latest
		steps:
			- run: echo deploy
```
{% endraw %}

<b>Resources:</b>
* [GitHub Actions Documentation](https://docs.github.com/en/actions)
* [GitHub Actions Marketplace](https://github.com/marketplace?type=actions)

### Git Hooks and Lefthook

Git hooks are scripts that Git can run automatically at specific lifecycle events such as `pre-commit` and `pre-push`. They help teams enforce quality checks before code is committed or pushed. However, raw Git hooks are stored in `.git/hooks` (local-only), which makes them hard to version, share, and keep consistent across all contributors.

Lefthook is a fast Git hooks manager that solves this distribution and consistency problem. Instead of manually copying scripts per machine, teams define hooks once in a versioned `lefthook.yml`, and everyone runs the same checks. This is especially useful for AI-assisted development workflows.

<b>Learning Points:</b>
* <b>Why we need hooks:</b> Hooks automate repetitive quality tasks (linting, tests, formatting, commit message validation) so issues are caught before they reach CI or code review.
* <b>What problem raw Git hooks solve (and miss):</b> Native hooks can block bad commits locally, but they are not tracked by default in repository history, so onboarding and team-wide consistency are painful.
* <b>What Lefthook solves:</b> Lefthook provides a version-controlled, cross-platform, and team-friendly way to define and run hooks with strong performance and parallel execution.
* <b>Git hooks vs Lefthook:</b> Git hooks are the native trigger mechanism from Git itself; Lefthook is an orchestration layer that manages hook definitions, script execution, and sharing across the team.
* <b>Why Lefthook is often preferred:</b> It is simple to configure (`lefthook.yml`), fast on large projects, easy to install in CI/local environments, and reduces "works on my machine" differences in pre-commit behavior.

<b>Common Usage:</b><br>
1) Install Lefthook in the project using the package manager that matches your stack.

```bash
# Example for a Node.js project
npm install --save-dev lefthook

# Example for macOS via Homebrew
brew install lefthook
```

2) Create `lefthook.yml` in repo root (version-controlled):

```yaml
pre-commit:
  parallel: true
  commands:
    ruff-lint:
      glob: "*.py"
			run: uv run ruff check --fix {staged_files}
      stage_fixed: true

    ruff-format:
      glob: "*.py"
			run: uv run ruff format {staged_files}
      stage_fixed: true

    mypy:
      glob: "*.py"
      run: uv run mypy .
```

3) Run Lefthook install to initialize Git hooks from our Lefthook config.

```bash
lefthook install
```

**How it works:**
`lefthook install` writes hook launcher scripts into `.git/hooks` (for events like `pre-commit` and `pre-push`). Those launchers then read your versioned `lefthook.yml`. Each launcher is a small script that calls `lefthook run {hook-name}` when executed. Usually, we only rerun `lefthook install` when hook scripts in `.git/hooks` need regeneration (for example after reinstall, cleanup, or hook wiring changes). Simple command changes in `lefthook.yml` typically do not require reinstall.

4) Commit `lefthook.yml` so all teammates and CI environments share the same hook rules.

---

<b>Initialize Git Hook Using Git Only:</b><br>
If we choose not to use Lefthook, we can create native hooks manually.

1) Create a hook script directly in `.git/hooks` and make it executable.

```bash
cat > .git/hooks/pre-commit << 'EOF'
#!/bin/sh
echo "Running pre-commit checks..."
npm run lint || exit 1
EOF

chmod +x .git/hooks/pre-commit
```

This works, but the hook is local-only by default and not shared automatically through Git history unless you add extra tooling around it.

<b>Resources:</b>
* [Git Hooks Documentation](https://git-scm.com/docs/githooks)
* [Lefthook Documentation](https://lefthook.dev/)
* [Lefthook GitHub Repository](https://github.com/evilmartians/lefthook)

### UV

uv is an extremely fast Python package and project manager. It can replace tools like `pip`, `pip-tools`, `pipx`, `poetry`, `pyenv`, `virtualenv`, and `twine` in many workflows. It helps with dependency management, virtual environments, Python version management, running scripts, and installing command-line tools.

<b>Learning Points:</b>
* <b>What uv is used for:</b> uv manages Python projects, dependencies, lockfiles, virtual environments, scripts, and Python versions in one tool.
* <b>What problem it solves:</b> It reduces the need to combine multiple tools for everyday Python setup and makes project bootstrapping faster and more reproducible.
* <b>Why it is preferred:</b> uv is much faster than traditional Python packaging tools, uses a global cache, and provides a consistent workflow across macOS, Linux, and Windows.
* <b>How it improves consistency:</b> uv creates and syncs environments from a lockfile, which helps teams get the same dependencies without manual environment drift.
* <b>Why it fits modern Python projects:</b> It supports project workflows, scripts, and tools in a way that is simple enough for small projects but scalable for larger codebases.

<b>Common Usage:</b><br>
1) Install uv.

```bash
# macOS and Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows
winget install --id=astral-sh.uv  -e
```

2) Create a new project with uv, or use it in an existing project root.

```bash
# New project
uv init example

# Existing project
cd example
uv init
```

3) Add dependencies and run commands inside the managed environment.

```bash
uv add ruff
uv add --dev pytest
uv run ruff check
uv run python main.py
```

4) Keep the environment in sync.

```bash
uv lock
uv sync
```

5) Use uv to manage Python versions when needed.

```bash
uv python install 3.12
uv python pin 3.12
```

<b>Common Workflow:</b><br>
For a typical Python project, we usually install uv, run `uv init` for a new project, add packages with `uv add`, and use `uv run` to execute scripts or tools without manually activating a virtual environment.

<b>Resources:</b>
* [uv Documentation](https://docs.astral.sh/uv/)

### GitFlow and Trunk-Based Development

GitFlow and Trunk-Based Development are two popular Git branching strategies, but they optimize for different team needs.

GitFlow uses multiple long-lived branches (`main` and `develop`) plus supporting branches (`feature/*`, `release/*`, and `hotfix/*`). It gives clear release structure and strict separation between ongoing development and production-ready code.

Trunk-Based Development keeps one primary branch (often `main`) and encourages very short-lived branches or direct commits to trunk, with frequent integration and continuous delivery practices.

<b>Quick Comparison:</b><br>

| Aspect | GitFlow | Trunk-Based Development |
|---|---|---|
| Branch model | Multiple long-lived branches like `main`, `develop`, `release/*`, and `hotfix/*` | One main branch, usually `main`, with very short-lived branches |
| Release style | Scheduled, staged releases | Continuous delivery or very frequent releases |
| Change size | Larger batches of work | Small, incremental changes |
| Risk control | Release branches and stabilization phases | Strong CI, frequent merges, and feature flags |
| Merge overhead | Higher | Lower |
| Best fit | Enterprise teams, release-managed products, compliance-heavy workflows | SaaS teams, fast-moving product teams, mature CI/CD setups |
| Main trade-off | More process control but more complexity | Faster flow but requires discipline and automation |

<b>Common Usage:</b><br>
<b>GitFlow Workflow (release-oriented):</b>

1) A `develop` branch is created from `main`.
2) A `release` branch is created from `develop`.
3) `Feature` branches are created from `develop`.
4) When a feature is complete it is merged into the `develop` branch.
5) When the `release` branch is done it is merged into `develop` and `main`.
6) If an issue in `main` is detected, a `hotfix` branch is created from `main`.
7) Once the `hotfix` is complete it is merged to both `develop` and `main`.

---

<b>Trunk-Based Workflow (continuous integration):</b>

1) Keep one main integration branch (`main`).
2) Use tiny, short-lived branches (hours to 1-2 days max).
3) Merge to `main` frequently with passing CI.
4) Use feature flags to hide incomplete features.
5) Release continuously or in very small batches.

<b>When to Choose Which:</b><br>
* <b>Choose GitFlow when:</b> You need strict release governance, separate QA hardening phases, longer-lived support branches, or compliance-heavy release checkpoints.
* <b>Choose Trunk-Based Development when:</b> You want rapid delivery, high developer throughput, fast feedback loops, and your CI/CD plus test automation are mature.

<b>Resources:</b>
* [Atlassian: Gitflow Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)
* [CI/CD and Trunk-Based Development (AWS)](https://docs.aws.amazon.com/prescriptive-guidance/latest/choosing-git-branch-approach/advantages-and-disadvantages-of-the-trunk-strategy.html)

### Semantic Versioned Releases

Semantic versioned releases are a standard way to decide whether a new release should be a `major`, `minor`, or `patch` update. In practice, GitHub does not decide this by itself. A release tool or workflow looks at commits, pull request labels, or version changes, then decides whether a new release should be created.

The most common and practical setup is to use automation on `push` to `main`, then let a release tool infer the version bump from commit messages or PR labels.

<b>Learning Points:</b>
* <b>What this solves:</b> It gives the team a predictable release process instead of manually guessing when to publish a new version.
* <b>Why it is standard:</b> Semantic versioning makes it easier to communicate compatibility. `major` means breaking changes, `minor` means new backward-compatible features, and `patch` means backward-compatible bug fixes.
* <b>What GitHub actually does:</b> GitHub Actions can run the release workflow, but the version decision usually comes from tools like semantic-release or release-please.
* <b>Good practice:</b> Use either commit conventions or PR labels consistently so the automation can infer the right version bump.
* <b>When it is preferred:</b> This works best for teams that want repeatable releases, clear version history, and CI-driven publishing.

<b>Common Usage:</b><br>
1) Choose one version signal strategy and apply it consistently.

| Strategy | Signal | Common labels / messages |
|---|---|---|
| Commit-based | Conventional commits | `feat:`, `fix:`, `feat!:` |
| PR label-based | Pull request labels | `bump:major`, `bump:minor`, `bump:patch` |

2) If you use commit-based versioning, merge changes into `main` with consistent commit messages.

```bash
git commit -m "feat: add user search"
git commit -m "fix: handle empty response"
git commit -m "feat!: remove legacy endpoint"
```

3) If you use PR label-based versioning, add one bump label before merging.

```text
bump:major  # breaking change
bump:minor  # backward-compatible feature
bump:patch  # backward-compatible fix
```

4) Run a GitHub Actions workflow to create releases.

```yaml
name: Release

on:
	push:
		branches: [main]

jobs:
	release:
		runs-on: ubuntu-latest
		steps:
			- uses: actions/checkout@v4
			- run: npm ci
			- run: npm test
			- run: npm run build
			- run: npx semantic-release
```

5) Let the workflow decide the version bump and create the tag and release.

| Commit or label pattern | Result |
|---|---|
| `feat:`/`bump:minor` label | `minor` release |
| `fix:`/`bump:patch` label | `patch` release |
| `feat!:` or breaking change label/`bump:major` label | `major` release |

<b>When to Choose This:</b><br>
* <b>Choose this when:</b> You want release automation, consistent versioning, and a clear mapping between code changes and published versions.
* <b>Avoid this when:</b> Your team does not follow a consistent commit style or you need fully manual release approval for every version.
