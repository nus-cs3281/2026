### AI-Assisted Coding Tools

So far, I've experimented with many AI coding tools, incorporating them into my workflow and trying them out.

I've tried [opencode](https://opencode.ai/), [Mistral Vibe](https://mistral.ai/products/vibe), [Proxy AI](https://docs.tryproxy.io/), Github Copilot, [Cline](https://cline.bot/). 

They can be divided into roughly two categories; AI tools that live in the CLI and those that integrate directly into IDEs. While their usage may be similar (many of them can inject context using slash/@ commands, in addition to other common features), their value can be quite different.

I've found that tools that integrated directly into IDEs felt superior for engineering, provided that one does not enable settings such as "YOLO" mode (editing without permission). This way, you may review the AI's work file-by-file, and guiding it if its approach needs changing.

While I've found human-in-the-loop workflows to feel better as a developer (more supervision over work), less hands-on approaches also can be useful for iterating quickly. However, I've also found that the success of these methods are highly contingent on model quality.

On top of that, leveraging [plan/act modes](https://docs.cline.bot/features/plan-and-act), [skills](https://docs.cline.bot/features/skills), and keeping context focused can improve model performance.

Resources:
[Cline documentation](https://docs.cline.bot/introduction/welcome)

### TypeScript (and the JavaScript/Node ecosystem)

So far, I've been working on much of the CLI components of MarkBind. I've done much research on it due to working on PRs such as [TypeScript migration](https://github.com/MarkBind/markbind/pull/2830) and [Migrating TypeScript output from CJS to ESM](typescript). I would say currently I'm more well-versed in it than an average developer due to my deep involvement in these migration works where I've had to update tooling, workflows, and developer experience regarding TypeScript.

Key Learning Points
* **CJS vs ESM**: CommonJS (CJS) and EcmaScript Modules (ESM) are different module systems for the JavaScript environment. Their key difference is in how they resolve imports/other modules - CJS was primarily designed for server-side, and modules are loaded synchronously. This is compared to ESM which allows for both synchronous and asynchronous module loading. As the ecosystem is currently moving towards ESM, MarkBind has migrated to ESM.
* **Node Versions**: Even-versioned releases in Node are LTS. Using newer version of Node allow you to use newer features that are sometimes nicer for Dev Experience.

Resources:
[CJS vs ESM (Better Stack)](https://betterstack.com/community/guides/scaling-nodejs/commonjs-vs-esm/)

### Langchain

I learnt and used [Langchain](https://docs.langchain.com/) to create an AI workflow for the CSV classifier task.

Resources:
[Langchain documentation](https://docs.langchain.com/)
