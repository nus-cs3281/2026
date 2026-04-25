### ContextManager

A context manager in Python is a structured way to handle resources so setup and cleanup are done safely and automatically, usually through the with statement. Instead of manually opening and closing files or connections, a context manager guarantees that cleanup logic still runs even if an exception occurs inside the block, which reduces bugs and resource leaks. Under the hood, this works through the context manager protocol (`__enter__` and `__exit__`), where `__enter__` prepares the resource and `__exit__` handles teardown. This pattern makes code cleaner, easier to read, and more reliable because resource handling is localized to one clear block. Common examples include file I/O, database transactions, thread locks, and temporary state changes, and a good rule is to use with whenever something must always be released or restored.

**resources:**<ul><li>RFC: [Context Matters](https://docs.google.com/document/d/1JhHCS6hZ9iVoWQa4QZBpcGMuv4GB9z74bfhSgzD-WI0/edit?tab=t.0)</li></ul><ul><li>[Context Manager python documentation](https://book.pythontips.com/en/latest/context_managers.html)</ul></li>

### Utilising Codex for coding
OpenAI Codex is an AI coding agent, a large language model specialized for software tasks, combined with tools that let it work inside a real project. It can be very useful to read and understand files across a repository, run terminal commands,
propose and apply code edits, generate test cases etc.

#### AI Agent:
`Agent.md` is a project-specific instruction file that tells an AI coding assistant how to behave inside a codebase: what the project does, how the folders are organized, coding conventions, testing commands, and things to avoid. It improves AI performance by informing the LLM exactly how the project’s structure or style from scattered files look like, so it makes more accurate edits, follows the right conventions, avoids breaking assumptions, and produces code that fits the repository better.

Features of a good `Agent.md` includes:
<ul><li>State a clear role</li></ul>
<ul><li>Indicates the executable commands</li></ul>
<ul><li>Project knowledge</li></ul>
<ul><li>Real Examples</li></ul>

Ideally, `Agent.md` should be very specific on the task that this particular AI Agent should carry out, like writing test cases, debug, refactoring, instead of being very generic.

**resources**
- [How to write a great agents.md: Lessons from over 2,500 repositories](https://github.blog/ai-and-ml/github-copilot/how-to-write-a-great-agents-md-lessons-from-over-2500-repositories/)
- [Custom instructions with AGENTS.md](https://developers.openai.com/codex/guides/agents-md/)

#### Prompt Engineering:
Prompt engineering is the practice of designing clear, specific instructions so an AI can produce more accurate, useful, and consistent outputs.

A good prompt should:
<ul><li>give enough information about the task</li></ul>
<ul><li>provide desired response/output format</li></ul>
<ul><li>any constraints that is not clearly stated in the task information provided to the LLM</li></ul>

If the task is complicated, it is always recommended to break it into smaller tasks, and prompt the AI to complete a sequence of smaller tasks.



**resources:**
- [What Is Prompt Engineering? Definition and Examples](https://www.coursera.org/articles/what-is-prompt-engineering?utm_medium=sem&utm_source=gg&utm_campaign=b2c_apac_x_multi_ftcof_career-academy_cx_dr_bau_gg_pmax_gc_sg_all_m_hyb_25-04_desktop&campaignid=22449465350&adgroupid=&device=c&keyword=&matchtype=&network=x&devicemodel=&creativeid=&assetgroupid=6568546196&targetid=&extensionid=&placement=&gad_source=1&gad_campaignid=22442997015&gbraid=0AAAAADdKX6a5qC8HfJN4F-2bDlUpmsyuC&gclid=Cj0KCQiA2bTNBhDjARIsAK89wlHCKiGUC3EW_J0XliK1RhvXRh2FKKsCqMli93CJV-sINoChIimFdmYaAld0EALw_wcB)
- [Prompt Chaining Tutorial: What Is Prompt Chaining and How to Use It?](https://www.datacamp.com/tutorial/prompt-chaining-llm?utm_cid=19589720824&utm_aid=157098106775&utm_campaign=230119_1-ps-other~dsa-tofu~all_2-b2c_3-apac_4-prc_5-na_6-na_7-le_8-pdsh-go_9-nb-e_10-na_11-na&utm_loc=9062531-&utm_mtd=-c&utm_kw=&utm_source=google&utm_medium=paid_search&utm_content=ps-other~apac-en~dsa~tofu~tutorial~artificial-intelligence&gad_source=1&gad_campaignid=19589720824&gbraid=0AAAAADQ9WsFiJ5fau6lxdBuD9lgM46Iwl&gclid=Cj0KCQiA2bTNBhDjARIsAK89wlGLy8bdhIAsqSlxwlWNibpHzVqfuy-QFFN9iGE3kir4HC11yCDrbc0aAg8DEALw_wcB)

### GitHub Actions
GitHub Actions is a CI/CD automation tool built into GitHub that lets developers automate tasks directly from a repository. It is commonly used to run tests, build applications, check code quality, and deploy projects whenever certain events happen, such as pushing code or opening a pull request. By defining workflows in YAML files, teams can make their development process more consistent, repeatable, and easier to maintain. Some of the key points as follows:

**Workflow automation**

GitHub Actions works by defining workflows that are triggered by specific events. For example, a workflow can run whenever someone pushes code, opens a pull request, creates an issue, or on a scheduled time. This reduces the need for developers to manually run repeated commands, because checks and tasks can happen automatically when repository activity occurs. GitHub’s documentation states that workflows can be configured to run on GitHub events, scheduled times, or external events.

**CI/CD support**

One of the main uses of GitHub Actions is continuous integration and continuous delivery. In continuous integration, code changes are automatically tested before they are merged, helping teams catch bugs earlier. In continuous delivery or deployment, the project can be automatically built and released after the workflow passes. GitHub’s overview specifically mentions using workflows to build and test pull requests, or deploy merged pull requests to production.

**YAML-based configuration**

Workflows are written as YAML files and are usually stored inside the .github/workflows/ directory of a repository. This means the automation setup is kept together with the project code, making it easier for team members to view, review, and modify the workflow through normal Git version control. GitHub’s workflow syntax documentation explains that a workflow is a configurable automated process defined using a YAML file.

**resources:**
- [Understanding GitHub Actions](https://docs.github.com/en/actions/get-started/understand-github-actions?utm_source=chatgpt.com)

### AI Agent Orchestration

AI Agent Orchestration refers to the coordination of multiple specialized AI agents so that they can work together on complex, multi-step tasks. Instead of relying on one general-purpose AI agent to understand everything, plan everything, write all the code, and check all edge cases, orchestration separates responsibilities across different agents. For example, one agent may act as the orchestrator, another as the planner, another as the coder, and another as the designer. This makes the workflow more structured because each agent focuses on a clearer role while the orchestrator manages task delegation and communication.

**Why orchestration is useful**

A single AI agent can struggle when the task becomes large, especially in software projects involving backend logic, frontend design, architecture decisions, testing, and documentation. The agent may lose track of context, make inconsistent design choices, or overlook edge cases. By dividing the work among specialized agents, the system can handle complexity more systematically. AWS describes multi-agent orchestration as a way to route tasks or queries to specialized domains while maintaining context across interactions.

**Orchestrator agent**

The orchestrator is like the coordinator of the whole system. Its role is not necessarily to write code directly, but to understand the user’s high-level request, break it into smaller tasks, and assign those tasks to the correct specialist agents. For example, it may ask a planner to design the implementation approach, then ask a coder to implement the backend, and finally ask a designer to improve the frontend. In your notes, this is described as the orchestrator telling other agents what outcome is needed, rather than telling them exactly how to do their work.

**Specialized agents**

Different agents can be assigned different responsibilities. A planner agent may inspect the project structure, identify existing patterns, and produce an implementation plan without writing code. A coder agent may focus on writing backend logic, fixing bugs, and implementing functionality. A designer agent may focus on UI/UX, styling, accessibility, and visual consistency. Microsoft’s AutoGen documentation describes agents as self-contained units that can be developed, tested, reused, and combined into more complex systems, which supports this modular approach.

**Communication between agents**

A key part of orchestration is communication. Agents should not work in isolation, because the planner’s assumptions, the coder’s implementation choices, and the designer’s UI decisions need to stay aligned. Some orchestration patterns use a main agent that coordinates subagents, while others allow agents to hand off control to each other. LangChain’s multi-agent documentation describes both patterns: one where a main agent coordinates subagents as tools, and another where agents transfer control through handoffs.

**Planning and validation**

Agent orchestration is not only about generating code faster. It can also improve the development process by adding planning and validation stages. For example, the planner can identify edge cases before implementation, while the coder can check whether the implementation follows the plan. This reduces the risk of rushing directly into code without understanding the project structure. LangGraph’s documentation also distinguishes between workflows with predetermined steps and agents that dynamically decide their own process and tool usage, which is useful when designing more controlled agentic systems.

**Benefits and limitations**

The main advantage of AI orchestration is that it can produce more structured and potentially higher-quality outputs for complex tasks, especially when the agents are given clear roles. However, it also adds complexity. The orchestration setup needs careful prompting, clear agent responsibilities, and good communication rules. It may also increase total token usage because multiple agents are involved, even if each individual agent has a smaller context window. Your notes correctly frame these benefits as something to be further tested rather than as a guaranteed result.

**Use Cases:**

AI Orchestration should be considered for:
- Full-stack web application development
- Large codebase refactoring
- UI/UX improvement
- Feature planning and implementation

Should not be used when:
- You risk running out of tokens
- Simple or small tasks
- Project is too small
- Code explanability is important

**resources:**
- [What is AI agent orchestration?](https://www.ibm.com/think/topics/ai-agent-orchestration?utm_source=chatgpt.com)
- [AI agent orchestration patterns](https://learn.microsoft.com/en-us/azure/architecture/ai-ml/guide/ai-agent-design-patterns)
- [AI orchestration: A beginner’s guide for 2025](https://sendbird.com/blog/ai-orchestration)