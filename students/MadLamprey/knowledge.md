### Langchain4j

The standard JVM library for adding LLM features to Java applications. Provides a unified API across multiple model providers, plus chat memory, RAG primitives, and tool/function-calling.

- An effective tool for building **agentic** Java applications. The tool-calling abstraction lets you expose existing Java methods as "tools" the LLM can invoke, which is the foundation for any agent-mode feature in a Java app.
- Reliability of tool-calling tracks model size: capable models follow the JSON schema cleanly; smaller ones hallucinate parameters or skip the tool call entirely and respond in prose.
- Closest equivalent to LangChain in the Python ecosystem, with similar abstractions but a tighter, less sprawling API surface.

### Local LLM Inference (JLama, llama.cpp, Ollama)

Three approaches to running LLM inference locally instead of through a hosted API.

- **JLama**: pure-Java inference, no JNI or Python, model runs inside the same JVM as the app. Narrow model coverage; quality drops off fast on non-trivial prompts.
- **llama.cpp**: C++ inference engine. Better quality than JLama at the same parameter count, but Java integration needs JNI bindings, and you have to ship the model and runtime alongside the app.
- **Ollama**: a daemon that wraps llama.cpp and manages models for you. Best developer experience for local use, but still ends up being "ship a daemon alongside your app" if you want it embedded.
- Tradeoff that holds across all three: local inference makes sense when latency or offline operation dominates. Anywhere else, a hosted API is simpler and cheaper to operate.

### GitHub Actions for CI-Driven AI Tooling

GitHub's CI/CD platform, used here as the runtime for AI-powered tooling that activates on repo events.

- The workflow YAML that runs for an event is whichever version exists at the relevant ref: the tagged commit for tag pushes, the default branch for issue comments. Mixing the two without thinking about it is a source of confusing bugs.
- Force-pushing a tag fires both a delete and a create event, so tooling that posts artefacts has to be idempotent. Keying by `(tag, head SHA)` and updating the existing artefact is one way to do that safely.
- Repository **variables** are visible in workflow logs; **secrets** are masked. Provider name and model belong in variables; API keys belong in secrets.

### OpenAI Codex

I picked it as the assistant to evaluate for Prof's assignment on which AI tool best helps a developer learn an unfamiliar codebase fast.

- Functions more as a **codebase explainer** than a repo summariser. Stronger than I expected at tracing code paths and identifying which files are relevant to a given concern.
- What it does well: describing how different parts of a codebase interact (it generated a reasonable UML diagram), answering questions about dependencies and entry points, and narrowing the search space to the right files when given a specific fix to make.
- What it does less well: it doesn't reliably point to exact lines or snippets in the first few turns, and it tends to give localised answers rather than complete end-to-end task workflows.
- Net read: a very good *navigation* tool for students who need to understand an unfamiliar codebase, but not on the same level as Claude Code or Copilot as a general coding assistant.

### Agentic Design

A design lens for systems where an LLM is given some authority to take actions, not just produce text.

- The central question is *which decisions the model makes* and *which the surrounding code reserves for itself*. Agency is a dial, not a binary.
- High-autonomy designs (LLM picks an action, executes it, evaluates the result, loops) are flexible but hard to constrain. In pedagogical contexts they actively harm the learning the system is supposed to support.
- Low-autonomy designs (LLM produces a structured plan; the surrounding system executes and evaluates) are bounded but still benefit from the model's creativity at the generation step.
- Rule of thumb: the LLM should be generative where its creativity is the value (inventing test inputs, phrasing observations, drafting plans) and absent where determinism matters (executing tests, posting to GitHub, deciding pass/fail).

### Prompt Engineering

The discipline of writing the system + user prompts that make an LLM produce the output you actually want.

- For structured output: OpenAI-compatible JSON mode (`response_format={"type": "json_object"}`) is the most reliable way to keep smaller models on format. The prompt has to ask for an object, since bare arrays aren't allowed.
- For pedagogical output: instruction-tuned models default to being helpful, which in code-review contexts means giving the answer. Forcing question-shaped output needs multiple stacked constraints (no code, no specific line numbers unless they appear in the input, every observation framed as a question).
- Always evaluate prompts against the *worst* model you might run them on, not the best. Small models surface the prompt's fragility in ways large ones don't.

### Building an AI Code Reviewer

- The product is what the reviewer *won't* do. Generic LLM review is what every chat tab already provides; the value of a custom reviewer comes from the constraints it imposes (Socratic posture, refusal to write code, narrow scope per mode).
- Grounding is the cheap wedge. Embedding the cohort's actual rubric and coding standard in the prompt is what differentiates the output from generic chat-tab review.
- Output format matters as much as content. `file:line` citations make findings verifiable; multiple bullets about the same problem make it look bigger than it is.

### Pedagogical Design as an Engineering Constraint

A way of treating "will students actually use this" as a hard engineering input.

- A tool that competes with a general-purpose chat tab on UX will lose. The chat tab will always be lower-friction for open-ended interactions.
- The way out is to constrain every feature to something a chat tab fundamentally cannot do: execute the user's code, read their full repo at once, run on a trigger the user didn't have to invoke.
- Cutting features is often higher-leverage than adding them. The most flexible mode of any tool tends to be the most useless one, because it overlaps the most with what a chat tab already covers.
