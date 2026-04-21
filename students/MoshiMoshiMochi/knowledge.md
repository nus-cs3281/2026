### GitHub Copilot

GitHub Copilot is a code completion and programming AI-assistant that assist users in their IDE. It uses LLMs can assist with code generation, debugging or refactoring through either real-time suggestions or language prompts

**Key Learning Points:**
- Context is King! Providing all relevant files immediately leads to faster, more accurate fixes. The AI performs best when it "sees" the full scope of the bug.

- Don't stop at the first working fix. Specifically, we can try asking the AI to improve code quality and clarity after the initial generation helps eliminate "AI-style" clutter and technical debt.

- Initial AI suggestions often prioritize the simplest fix. It still requires manually prompts & investigation for edge cases to ensure the solution is robust.

- We should treat AI as a collaborator, and not an automated system. Reviewing proposed changes and selectively implementing only what fits the project context prevents the introduction of unnecessary or incorrect logic.

### Agent Skills

Agent Skills are folders of instructions, scripts, and resources that agents can discover and use to do things more accurately and efficiently. These skills are designed to be automatically founded and used by AI agents, providing them user-specific context they can load on demand hence extending their capabilities based on the task they’re working on.

**Key Learning Points:**
- Moving instructions from a giant system prompt into a SKILL.md file allows for "progressive disclosure," where the agent only loads the knowledge it needs for the specific task at hand.

- Provide a strict directory layout (Instructions in SKILL.md, automation in scripts/, and context in references/) to ensure the agent can reliably find and execute tools.

- Include specific trigger phrases & tags, as well as clear and well defined steps. This prevents the agent from guessing, thus ensuring it follows the exact logic required for the most effective application.

### CJS to ESM migration
One of the major milestone for Markbind this semester was typescript migration and the subsequent CJS to ESM migration. While I only contributed to parts of the process, the opportunity allowed me learn about the details of dependency resolution and the structural differences between module systems, and how the migration to ESM will uture-proof the codebase by enabling better tree-shaking, improved performance, and compatibility with the modern JavaScript ecosystem. 

**Key Learning Point:** Transitioning the CLI and Core packages to TypeScript highlighted the importance of robust type definitions. It transformed the migration from a find-and-replace task into a meaningful refactoring process which in turn helped significantly improve my knowledge of the flow across the codebase.

### Full Textual Search with Pagefind
My major contribution to Markbind this semester was contributing to the initial support for full textual search across the site with the use [Pagefind](https://pagefind.app/). 

Before the current Pagefind search, Markbind only supported full textual search across its site by using [Algolia's Doc Search plugin](https://markbind.org/userGuide/makingTheSiteSearchable.html#plugin-algolia) which requires an external API key. Otherwise, users would have to the built-in "Heading-Level" search. Hence this feature aims to (eventually) replace the existing built-in search, while providing a full textual search alternative to [Algolia's Doc Search plugin](https://markbind.org/userGuide/makingTheSiteSearchable.html#plugin-algolia) 

While still far from fully complete, significant progress was made on the feature, most notable of which includes

1. **Flexible filtering options**, allowing users to declare their additional specific elements which they would like to exclude from being searchable. This feature is especially helpful for users looking to migrate from Algolia's Doc Search as they can simply declare any existing CSS class used by Algolia. 

2. **Integrating page exclusion**: Pagefind's indexing now respects the searchable page option declared within `site.json`.As the goal is to integrate pagefind as the default search within Markbind (eventually replacing the built-in search), this feature will support a seamless onboarding/migration process for user's currently using the default built-in search.

3. **In-House vue component**: When initially worked on, Pagefind's supported UI was restrictive and hard to build upon. Hence a major work needed to be redone to overhaul this. Beyond just building a new custom vue component, this task also required custom utility files to help the processing of the pagefind results. While Pagefind has released a [new component library](https://github.com/Pagefind/pagefind/releases/tag/v1.5.0) improving upon their initial UI, having an In-House vue-component still provides us more customizability as relying on theirs would mean being suseptible to UI changes that we may be less receptive towards.

I thoroughly enjoyed working on the implementation of this feature as it allowed me to tackle the complexities of integrating a third-party indexing tool into a static site generator architecture, while navigating the various additional support to ensure a frictionless experience for users looking to make the switch from existing searches. All in all, it provided me the opportunity to dive deep into codebase of Markbind providing me a better understanding of how various components worked with one-another (especially on the process of site generation).

**Key learning point:**
Full textual search is essential for modern documentation and information retrieval because it bridges the gap between what a user remembers and how a site is structured. While heading-level search relies on the assumption that a page’s title or section headers perfectly encapsulate its entire content, it often excludes the nuanced details, specific code snippets, or technical explanations buried within paragraphs.

### Server Driven UI (SDUI)
Along my journey of finding a topic for my upcoming teachback, I stumbled upon a SDUI. As markbind is on web development (, all be it a static site generator), the concept of a SDUI approach towards web development certainly peaked my interest. SDUI is an architectural approach where the backend dictates the user interface's structure, layout, and behavior, rather than hardcoding it in the across different platforms (mobile, web etc).

**Key learning points:**
- The backend provides a "view model" (data and structure), while the client act as a renderer for a pre-defined library of native components. Instead of just sending data (like traditional REST APIs), the server sends a response describing how to display the UI (e.g., `{"type": "banner", "image": "..."}`). 
- As a result, this provides dynamic flexibility as changes to the app's layout, such as rearranging sections on a homepage, can be done immediately by updating the backend, bypassing the need for users to download app updates. Most famously, companies like [Airbnb](https://medium.com/airbnb-engineering/a-deep-dive-into-airbnbs-server-driven-ui-system-842244c5f5), [Lyft](https://eng.lyft.com/the-journey-to-server-driven-ui-at-lyft-bikes-and-scooters-c19264a0378e) and [Reddit](https://www.reddit.com/r/RedditEng/comments/158f8o3/evolving_reddits_feed_architecture/) have made the switch towards using a SDUI approach.


### Get Shit Done (GSD)
The topic I eventually decided on for my upcoming teachback was GSD! I chose to do so as  (, and putting poop emojis on my presentation was definitely a plus). Additionally, according to its Github repo, its "Trusted by engineers at Amazon, Google, Shopify, and Webflow.", but they don't provide any 

The GSD lifecycle can broken down into 3 stages. First begins the initialization stage where you discuss with the agent about what application you aim to build. This helps the agent's research process and its understanding of the various requirements needed by the product. After which it generates a roadmap which structures various phases of implementation. Next comes the iterative process of implementing each phase. In short the user further refining their requirements of the features being implemented for the phase, hence providing greater context for GSD to accurately build initial product discussed.

My experience working with GSD was a surprising positive one (given my friend's previous bad experience working with other AI SDD frameworks). It managed to capture most of what I wanted from the application, providing me with a satisfiable MVP. Having AI build the entire project thus far has certainly been an experience. However, looking back at the project developed, I've come to realise the joy and ownership it takes away from development out of the process.

**Key Learning Point:**
- GSD is focused on fast delivery, developing on what is required for each version specified.
- GSD follows an exploratory process towards development as it plans each of its "phases" one step at a time (instead of doing so right from the beginning like other AI SDD frameworks). 
- As later phases are not pre-planned in detail like BMAD’s, this allows for easier course correction during development as users aren’t locked in from the start.
- Hence, a major selling point for GSD is the greater flexibility it provides during the development process. This makes it great for any projects where requirements are likely to change in the future, or might require a lot of experimentation within each "phase"

Resources:
[GH repo](https://github.com/gsd-build/get-shit-done)

### Build More Architect Dreams (BMAD)
BMAD is a structured, multi-agent agile development framework and was often brought up during my research and implementation of GSD. BMAD is perhaps the most opinionated and methodology-heavy implementation of AI-driven development framework. 

It is an AI-driven SDLC framework that orchestrates a team of specialized agent personas—such as Product Managers, Architects, and Scrum Masters—through a rigorous, multi-phase pipeline. BMAD aims to enforces a strict sequence from requirements elicitation (PRDs) and technical architecture (ADRs) to implementation, ensuring that AI-generated code is grounded in high-level design rather than isolated prompts.

**Key Learning Point:**
- With BMAD, it follows a strict preloaded pipeline and this provides users with a tool that enforces "industrial-grade" software engineering standards automatically.
- However, a side of which results in all the specs created being heavily interlinked from the start. Hence when if a user is considering to use BMAD to build their software, they must be absolutely sure about what exactly they want to build & as many of its corresponding requirements from the get-go. This is because any changes made mid-way often requires “rewinding” the entire pipeline to re-shard each tasks, while any errors made during each stage can propagate through the entire pipeline.
- In theory, the BMAD framework provides a highly sophisticated workflow where it aims to minimize technical debt and architectural drift by treating the AI as a disciplined collaborator rather than just a code generator. However, this all comes at the cost of upfront rigidity.

Resources:
- [BMAD Documentation](https://docs.bmad-method.org/)
- [GH Repo](https://github.com/bmad-code-org/BMAD-METHOD)

### Superpowers
Another agentic skills development framework that was often brought up during my research on GSD was Superpowers. It was by far the most popular of the frameworks with over 150k github stars. Notably, it is the only framework in this category officially listed as a plugin on Anthropic’s Claude plugin marketplace which perhaps can be viewed as a form of credibility. 

So what is it? Superpowers is a development-centric agentic framework that prioritizes reliability through rigorous automation. It operates by **breaking down complex features into granular, testable units, leveraging a loop of automated testing and code refinement**.

**Key Learning Point:**
- Superpower follows a **TDD approach** towards implementation and development where it actively writes failing test before writing minimal code for it to pass and then commiting it. 
- Through following a TDD Superpowers aims to provide a high-integrity codebase where all features are verified from the start, significantly reducing the likelihood of regressions or "hallucinated" logic that doesn't actually function.
- But since the entire codebase is anchored by a specific suite of tests, changing a fundamental requirement mid-stream requires refactoring the tests themselves before the code can be updated. 
- All in all, this creates a high barrier for experimental or "exploratory" coding where the end goal is not yet clearly defined. Hence the frameworks comes at the cost of upfront rigidity making any pivots during the process or after implementation particularly costly. 

Resources:
- [Official Plugin](https://claude.com/plugins/superpowers)
- [GH Repo](https://github.com/obra/superpowers)

### Plan-Apply-Unify Loop (PAUL)
Perhaps the closest sibling to GSD I found whilst researching and implementing GSD. Indeed PAUL was developed on improving the GSD workflow, so much so that they provide documentation on what differentiates it from GSD.
> GSD pioneered the concept of treating plans as executable prompts. PAUL takes this further by recognizing that execution without reconciliation creates drift — and drift compounds across sessions.
>
> Where GSD focuses on getting work done, PAUL focuses on getting work done correctly, consistently, and with full traceability.

All in all, PAUL's claims are certainly impressive given my positive experience with GSD thus far. From the videos and forums I've read above PAUL it certainly seems like a promising and ever favourable alternative to GSD. That said, documentation explicitly covering the performance between the 2 are few are far between which somewhat affects its credibility. In comparsion, the current github repo has less than a thousand stars, while GSD has over 50k. I will certainly give it a try over the summer break and look forward to comparing it with GSD for myself.

**Key Learning Points:**
- Similar to GSD, PAUL focuses on an **iterative approach** towards development unlike other AI spec-driven frameworks like BMAD.
- **Interesting differntiator from GSD**: 
    - **Enforced "UNIFY" phase** after the execution step to create an audit trail that makes context resumption reliable.
    - **Token Economics**: Unlike GSD that focuses on the speed of delivery, PAUL focuses on the quality of delivery by reserving subagents use case for parallel research and discovery. This is because while Parallel execution subagents generate more output faster, it is often it's expensive and wasteful. Hence PAUL aims to optimize the value per-token during the execution stage.

Resources:
- [GH Repo](https://github.com/ChristopherKahler/paul)