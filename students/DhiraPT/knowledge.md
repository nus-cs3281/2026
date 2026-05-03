### Tool/Technology 1: Asynchronous Processing & Job Scheduling Architectures in Java

- **Aspects Learned:**
    - Explored various background execution architectures to replace the legacy Google App Engine (GAE) Task Queue and Cron ecosystem.
    - Evaluated different paradigms for handling asynchronous workloads, specifically contrasting event-driven task queues with time-based job schedulers.
    - Deep-dived into Apache ActiveMQ Artemis—the modern, high-performance successor to classic ActiveMQ—learning how to implement its non-blocking, asynchronous messaging architecture for efficient task distribution.
- **Resources Used:**
    - **Apache ActiveMQ Artemis Documentation:** https://artemis.apache.org/components/artemis/documentation/latest/
    - **Quartz Scheduler Documentation:** https://www.quartz-scheduler.org/documentation/
    - **Google Cloud Tasks/PubSub Documentation:** https://docs.cloud.google.com/tasks/docs/comp-pub-sub

### Tool/Technology 2: AI-Assisted Development & Coding Agents

- **Aspects Learned:**
    - Extensively evaluated and integrated various AI coding assistants and autonomous agents into my daily development workflow to accelerate refactoring and test migration.
    - Explored the Architect-Builder pattern for AI agents, strategically pairing high-reasoning models for complex planning and system design (the Architect) with faster, cost-effective models for code generation and execution (the Builder).
    - **Tool Analysis:**
        - *Claude Code:* Found it highly capable for complex reasoning and generating large blocks of accurate code, though cost-prohibitive for continuous use.
        - *GitHub Copilot Workspace:* Evaluated its terminal-based execution model, but found it lacking in flexibility, especially after recent restrictions on premium models.
        - *Roo Code (VS Code Extension):* Identified this as the optimal tool due to its versatile custom modes (Architect, Code, Ask, Debug, Orchestrator) and the ability to seamlessly switch between different LLM backends (OpenAI, Anthropic, local models) depending on the task's complexity.
- **Resources Used:**
    - **Roo Code Documentation:** https://docs.roocode.com/tips-and-tricks
