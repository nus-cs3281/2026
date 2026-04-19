# Knowledge

List the aspects you learned, and the resources you used to learn them, and a brief summary of each resource.

---

## ChatGPT Codex

**Resources:** [Introducing Codex](https://openai.com/index/introducing-codex/) · [Codex App](https://chatgpt.com/codex/) · [Codex Now GA](https://openai.com/index/codex-now-generally-available/)

Codex is OpenAI's agentic coding system (powered by GPT-5.3-Codex) that can receive a task description, write code, run it in a sandboxed cloud environment, debug errors, and open a pull request for review.

**Access & Interfaces:**

- Available via ChatGPT Plus ($30/month), CLI, IDE extension, and the web at [chatgpt.com/codex](https://chatgpt.com/codex)
- Each task runs in its own isolated cloud sandbox, pre-loaded with your repository

**Key Features:**

- **Remote Codex:** Delegate long-running tasks to cloud machines and open PRs from anywhere — including mobile. Unlike local AI assistants, tasks run asynchronously
- **Worktrees:** Run multiple agents in parallel on different features simultaneously, each in isolation
- **Skills:** Reusable, shareable instruction sets that align agents with team standards (code understanding, prototyping, documentation)
- **Automations (Background):** Codex works unprompted on scheduled workflows — issue triage, alert monitoring, CI/CD integration, and more
- **Mid-task steering:** Unlike one-shot prompts, you can guide and interact with Codex while it's working without losing context
- **Integrations:** GitHub today; issue trackers and CI systems coming soon

---

## Claude Code

**Resources:** [Claude Code Overview](https://code.claude.com/docs/en/overview) · [Claude Code Releases](https://github.com/anthropics/claude-code/releases)

Claude Code is Anthropic's agentic coding CLI that understands your entire codebase and can work across multiple files and tools to complete tasks end-to-end.

**Access & Interfaces:**

- Available via Claude Pro ($20/month) or API
- CLI (terminal), VS Code extension (inline diffs, @-mentions, plan review), JetBrains plugin, web app at [claude.ai/code](https://claude.ai/code)

**Key Features:**

- **Multi-agent collaboration:** Multiple agents can work together on a task, share context, and hand off work
- **Checkpoints:** Saves progress and allows instant rollback to a previous state — critical for long agentic tasks
- **MCP (Model Context Protocol):** Open standard for connecting Claude Code to external tools — Google Drive, Jira, Slack, or custom tooling. MCP servers can be self-hosted
- **Git integration:** Natively stages changes, writes commit messages, creates branches, and opens PRs
- **Hooks:** Shell commands that execute in response to events (tool calls, session start/stop) — enables automated workflows without leaving the harness
- **CLAUDE.md:** Project-level instruction files that scope Claude's behavior to your conventions
- **Compared to Codex:** Better performance on complex multi-file tasks due to its richer harness; local-first but supports remote agents

---

## Git Hooks

**Resources:** [githooks.com](https://githooks.com/) · [Lefthook GitHub](https://github.com/evilmartians/lefthook) · [pre-commit vs lefthook comparison](https://0xdc.me/blog/git-hooks-management-with-pre-commit-and-lefthook/) · [Using Lefthook across a team](https://www.d4b.dev/blog/2026-02-18-using-lefthook-to-manage-git-hooks-across-a-team)

Git hooks are scripts that run automatically at specific points in the Git workflow. They are stored in `.git/hooks/` but are not tracked by version control — hook managers solve this by committing the config to the repo.

**Hook Lifecycle:**
| Hook | When | Common Uses |
|---|---|---|
| `pre-commit` | Before commit is created | Lint, format, secret detection |
| `commit-msg` | After commit message is written | Enforce Conventional Commits |
| `pre-push` | Before push to remote | Run tests, check branch policy |
| `post-commit` | After commit | Notifications, doc generation |

**Tool Comparison — Lefthook vs pre-commit:**

|              | Lefthook             | pre-commit                |
| ------------ | -------------------- | ------------------------- |
| Language     | Go                   | Python                    |
| Execution    | Parallel (faster)    | Sequential                |
| Config       | `lefthook.yml`       | `.pre-commit-config.yaml` |
| Hook sources | Local scripts        | Community hook registry   |
| Best for     | Polyglot/any project | Python-heavy projects     |

**Lefthook** is preferred in the Git-Mastery project for its performance and language-agnosticism. Configuration example:

```yaml
# lefthook.yml
pre-commit:
  parallel: true
  commands:
    lint:
      glob: "*.py"
      run: ruff check {staged_files}
    format:
      glob: "*.py"
      run: ruff format {staged_files}
```

Install with `lefthook install` after placing `lefthook.yml` at the repo root.

**Git-Mastery implementation:** Lefthook was adopted across the exercises repository ([#265](https://github.com/git-mastery/exercises/pull/265)) and the app repository ([#76](https://github.com/git-mastery/app/pull/76)).

---

## Trunk-Based Development

**Resources:** [Atlassian Guide](https://www.atlassian.com/continuous-delivery/continuous-integration/trunk-based-development) · [DORA Capabilities](https://dora.dev/capabilities/trunk-based-development/) · [trunkbaseddevelopment.com](https://trunkbaseddevelopment.com/continuous-integration/) · [Harness Complete Guide](https://www.harness.io/blog/a-complete-guide-to-trunk-based-development)

A source control branching model where all developers integrate into a single branch (`main`/`trunk`), keeping it always releasable and avoiding long-lived branches and merge hell.

**Core Principles:**

- Short-lived feature branches only (ideally ≤1 day, ≤1k LoC) — never let branches diverge far from trunk
- Every commit on `main` must be in a deployable state — enforce this via CI gate
- Squash merges for clean history and atomic rollbacks
- Never merge unless CI passes; require minimum approvals via branch protection rules
- Feature toggles to ship incomplete features without long-lived branches

**Why it works:**

- Forces small, reviewable changes — reduces cognitive load on reviewers
- Conflict surface shrinks proportionally to integration frequency
- DORA research confirms TBD is a key predictor of elite software delivery performance (~85% of top-performing teams use CI/CD pipelines)

**Minimum Viable CI/CD pipeline:**

1. **Unit tests** — fast, per-function/module, run on every commit
2. **Integration tests** — API-level flows against a virtual environment
3. **E2E / Synthetic tests** — run on the actual environment (traditionally flaky; mitigation: retries, stable selectors, isolated state)
4. **Deployment gates** — post-deploy smoke tests; rollback automatically on failure

**Feature Flags (vs long-lived branches):**

- Incomplete code is merged but hidden behind a runtime toggle
- Code exists in production but is off — removes the need to maintain a parallel branch
- Tools: LaunchDarkly, Unleash (open-source), or simple environment variables

---

## CodeQL & Static Analysis

**Resources:** [GitHub CodeQL docs](https://docs.github.com/en/code-security/code-scanning/introduction-to-code-scanning/about-code-scanning-with-codeql)

CodeQL is GitHub's semantic code analysis engine. It treats code as data and runs queries to find security vulnerabilities automatically.

**How it works:**

- Creates a database from your codebase by extracting a relational representation of the code
- Runs queries (written in QL) against that database to find patterns matching known vulnerabilities
- Results surface as code scanning alerts on PRs and in the Security tab

**Key points:**

- Covers OWASP Top 10 out of the box for supported languages (Python, JS/TS, Go, Java, C/C++, etc.)
- Can be added as a GitHub Actions workflow (`github/codeql-action`)
- Free for public repos; included in GitHub Advanced Security for private repos
- Complements linters (which check style) — CodeQL checks for security and correctness

**Git-Mastery implementation:** CodeQL was set up alongside main branch hardening ([#116](https://github.com/git-mastery/app/issues/116)).
