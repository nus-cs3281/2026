### AI-Assisted Coding Tools

So far, I've experimented with many AI coding tools, incorporating them into my workflow and trying them out.

I've tried [opencode](https://opencode.ai/), [Mistral Vibe](https://mistral.ai/products/vibe), [Proxy AI](https://docs.tryproxy.io/), Github Copilot, [Cline](https://cline.bot/). 

They can be divided into roughly two categories; AI tools that live in the CLI and those that integrate directly into IDEs. While their usage may be similar (many of them can inject context using slash/@ commands, in addition to other common features), their value can be quite different.

I've found that tools that integrated directly into IDEs felt superior for engineering, provided that one does not enable settings such as "YOLO" mode (editing without permission). This way, you may review the AI's work file-by-file, and guiding it if its approach needs changing.

While I've found human-in-the-loop workflows to feel better as a developer (more supervision over work), less hands-on approaches also can be useful for iterating quickly. However, I've also found that the success of these methods are highly contingent on model quality.

On top of that, leveraging [plan/act modes](https://docs.cline.bot/features/plan-and-act), [skills](https://docs.cline.bot/features/skills), and keeping context focused can improve model performance.

Resources:
[Cline documentation](https://docs.cline.bot/introduction/welcome)

### Spec-Driven Development (SDD) Tools
I also explored SDD tools to create a medium-small vibe-coded application. These tools work in a very similar way - they inject skills or workflows (in the form of markdown files) to provide a structured step-by-step approach in conceptualizing and building a whole application based on **specification**, not code. My experimentations led me to testing out 3 different frameworks: spec-kit, spec-kitty, and BMAD. There is a *lot* more.

Their target audiences are somewhat different, but the overarching goal is the same: through solely prompting frontier-level models with specification info, create a whole well-coded application. My expectations which would perform better were completely subverted; spec-kit, despite maintained by an industry giant (Microsoft), was not much better than prompting *without* frameworks. BMAD, highly regarded from my searching and at about 45k stars at time of writing, was by far the most inefficient and poorly-performing. And spec-kitty, an underdog by all rights (1k stars at time of writing), turned out to fit my needs the best and created the best application in a reasonable amount of time.

I don't think these tools are at a level to replace developers wholesale in greenfield projects (they're not really intended for brownfield). But the industry seems to be moving frighteningly fast, and who knows what happens even 1 year from now. But they are indeed useful for creating proof-of-concepts, and can actually be better over framework-less prompting alone. 

Overall, here's my **learning points**:
* AI Tooling can be deceptive 
    * bigger or more popular != better
    * Things that *feel* like they help LLMs may not *actually* help them - keeping context windows cleaner may just be better sometimes.
* Use the right tool
    * A quarter way through my use of BMAD I realized that it was certainly not for small vibe-coded applications. It's intent is a lot more on actual prod-level applications, with a high emphasis on compliance. %%*(This does not change the fact that BMAD still burned a LOT of tokens and failed to produce a working app)*%%

### TypeScript (and the JavaScript/Node ecosystem)

So far, I've been working on much of the CLI components of MarkBind. I've done much research on it due to working on PRs such as [TypeScript migration](https://github.com/MarkBind/markbind/pull/2830) and [Migrating TypeScript output from CJS to ESM](typescript). I would say currently I'm more well-versed in it than an average developer due to my deep involvement in these migration works where I've had to update tooling, workflows, and developer experience regarding TypeScript.

Key Learning Points
* **CJS vs ESM**: CommonJS (CJS) and EcmaScript Modules (ESM) are different module systems for the JavaScript environment. Their key difference is in how they resolve imports/other modules - CJS was primarily designed for server-side, and modules are loaded synchronously. This is compared to ESM which allows for both synchronous and asynchronous module loading. As the ecosystem is currently moving towards ESM, MarkBind has migrated to ESM.
* **Node Versions**: Even-versioned releases in Node are LTS. Using newer version of Node allow you to use newer features that are sometimes nicer for Dev Experience.
* **Dependency Management**: MarkBind, along with much of the current JS/TS ecosystem, uses npm to manage packages. npm uses certain files such as `package.json` and `package-lock.json` to keep dependency trees updated and consistent across deployment environments (or just developer PCs). I performed a short presentation on why these exists, how they can get broken, and how to recover when it happens.

Resources:
[CJS vs ESM (Better Stack)](https://betterstack.com/community/guides/scaling-nodejs/commonjs-vs-esm/)

### Intimate Knowledge of the MarkBind codebase
Throughout the semester, I worked across most sections of the MarkBind codebase. I mostly worked on Core and CLI, though in the latter end of the semester I looked at and did some development on the pagefind component in vue-components.

I've learnt how to debug MarkBind when things go wrong, which was useful on February 25th when a change in a transitive dependency (minimatch) silently caused a knock-on effect on MarkBind, resulting in pages not being able to be built and served. Through tedious but well-intentioned tracing, I was able to identify the problematic dependency and temporarily fix it on my end by pinning the dependency's version.

I've also touched on the `markbind-action` repository, when needing to upgrade node.

Lastly, I learned how to make a new release for MarkBind!

### Langchain

I learnt and used [Langchain](https://docs.langchain.com/) to create an AI workflow for the CSV classifier task.

Resources:
[Langchain documentation](https://docs.langchain.com/)
