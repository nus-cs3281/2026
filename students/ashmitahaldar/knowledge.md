<!-- List the aspects you learned, and the resources you used to learn them, and a brief summary of each resource. -->

### AI Coding Tools

This module exposed me to multiple AI coding tools that are popular in the market, such as GitHub Copilot, Codex by OpenAI, and Claude Code.

#### Claude Code

My first major use of Claude Code for RepoSense PRs was to implement a YAML configuration wizard, which revealed both the promise and the limits of AI-assisted development.

- Plan mode proved genuinely useful for scoping out the work ahead.
- However, I quickly learned that leaving Claude entirely to its own devices was not a viable approach. I had to continuously review the code it produced, prompt it to re-examine its own output for potential issues, and actively probe for bugs — catching problems like a null branch issue that might otherwise have slipped through.
- Beyond debugging, the collaborative process required real engagement: discussing potential features, weighing multiple implementation approaches, and asking targeted questions. For instance, exploring two different ways to handle git usernames and evaluating the tradeoffs of each.
- Crucially, I also had to bring my own knowledge of the codebase to the table. When the generated plan referenced CSS files, I was the one who recognised that the main frontend used SCSS and flagged the inconsistency for the sake of consistency, something Claude did not realize until it was told. This is why I kept "manually accept edits" enabled throughout.

The broader takeaway is that working with AI on an existing codebase still demands that the developer be deeply familiar with it. Claude is a powerful collaborator, but it cannot be expected to independently scour a codebase and always arrive at the most contextually appropriate solution. That judgment still has to come from you.

### Terminal UIs

While working on my YAML config wizard, I spent some time researching about terminal UIs, when deciding wheher to implement a TUI or GUI for the wizard.

- A TUI, or Text-based User Interface, is an interactive interface that runs entirely inside a terminal emulator. It is like a GUI but rendered with characters, box-drawing symbols, and ANSI color codes instead of pixels and windows.
- They have been around since the early days of computing (ncurses-style apps like vim, htop, and midnight commander are classic examples) and have seen a real renaissance with modern frameworks that make them much easier to build.
- Modern libraries like Bubble Tea (Go's Elm-inspired TUI framework), Rich and Textual for Python, and Ink for React-based terminal rendering can build TUIs.
- I was weighing whether to go this route, something that lives entirely in the terminal using keyboard navigation, text-based forms, and styled layouts, or go with a more traditional GUI.
- A TUI felt natural for a config wizard since developers are already in the terminal, it would avoid any frontend dependency overhead, and keeping more of RepoSense CLI-native felt elegant.
- But ultimately I decided against it. GUIs just offered more flexibility for the kind of user experience I wanted to build, especially for something as structured and potentially complex as YAML configuration, where visual hierarchy, validation feedback, and form layouts benefit from a proper windowed interface.

So after the research detour, I went with a GUI.

### .yaml files

A YAML file is a human readable, plain-text file used mainly for configuration. DevOps, and data serialization. It uses indentation-based, hierarchical structures rather than curly braces or bracckets for data storage. Such a key-value pair structure makes it more readable and human friendly compared to JSON or XML.
Key aspects:

- Uses whitespace indentation to define structure, with colons `:` separating keys and values.
- It supports multiple data types (such as strings, integers, booleans etc.), sequences such as lists/arrays, and maps.
- Highly sensitive to indentation (spaces, not tabs). Comments are created with the `#` symbol.

Worked with YAML files when exploring the development of a GUI `.yaml` config filee generation wizard.

### GitHub Actions

GitHub Actions is GitHub's built-in CI/CD platform that automates workflows in response to repository events like pushes and pull requests.

- Workflows are defined as YAML files in `.github/workflows/` and consist of jobs that run on GitHub-hosted virtual machines (runners).
- Each job contains a sequence of steps that can run shell commands or use pre-built community actions (e.g., `actions/checkout`, `actions/setup-java`).
- Jobs can run in parallel across a strategy matrix of different OS and tool versions, and workflows support caching, artifact uploads, and conditional execution via if expressions.

Across my contributions to RepoSense, I gained significant practical experience with how GitHub Actions CI interacts with the development workflow.

- RepoSense's integration.yml runs a build matrix across six OS variants (Ubuntu, macOS, Windows) and includes separate jobs for backend tests (Gradle checkstyleAll, test, systemTest) and Cypress frontend tests.
- One of my earliest lessons came from the temp repo directory PR (#2537), where I refactored repository cloning to use temporary directories. The change worked locally but broke system tests on CI because the test environment assumed cloned repos persisted across test runs for snapshot reuse. I had to add a `SystemUtil.isTestEnvironment()` guard to skip cleanup in tests, teaching me that CI runners have different lifecycle assumptions than local development.
  - Similarly, the build.gradle `deleteReposAddressDirectory()` cleanup function had to be updated to match the new naming convention, showing me how Gradle build scripts and CI are tightly coupled.
- The title.md to intro.md rename PR (#2516) and its follow-up removal of backward compatibility (#2566) taught me about the CI pipeline's
  breadth. Changes that touched `build.gradle`, Vue frontend components, Cypress test support files, and documentation all had to pass linting, checkstyle, unit tests, system tests, and frontend tests across the full OS matrix.

- The config wizard work gave me the deepest CI experience.
  - I learned that RepoSense's Cypress tests run via Gradle's `testFrontend` task, which uses the `ExecFork` plugin to start Vite dev servers as background processes before running tests. When I added wizard-specific Cypress tests, they initially failed in CI because the global `support.js` `beforeEach` hook visits `localhost:9000` before every spec — interfering with wizard tests on port 9002.
  - I went through a cycle of writing tests, removing them when CI failed, debugging the port isolation issue, fixing it by adding a conditional guard in `support.js` and using `Cypress.env('configWizardBaseUrl')` with absolute URLs in intercepts, adding the `serveConfigWizard` Gradle task with proper `dependsOn/mustRunAfter` ordering, and then rewriting the tests from scratch.
- I also encountered multiple rounds of linter failures in CI — Pug lint errors and Java checkstyle violations. That passed locally but were caught by the CI pipeline's stricter enforcement, reinforcing the importance
  of running the full lint suite locally before pushing.

### Calling LLMs in Programs

This activity showed me how to move from using an LLM interactively to embedding it inside a real Python workflow.

- I learned how to use AI to call an OpenAI model from code using the SDK, pass structured prompts and dataset rows into the model, and capture the output in a machine-usable form for downstream processing. Here, that meant using an LLM to validate keyword labels in a CSV instead of relying only on manual checking.

- I also learned that calling LLMs in programs requires more than just sending prompts. In practice, we had to handle environment setup, API keys, Python package installation, and compatibility issues between models and SDK parameters.

- The activity also surfaced operational concerns that matter in scripts: rate limits, batching requests, retries, progress logging, and writing outputs to files like `validation_report.csv`. I learnt that when LLMs are used programmatically, the surrounding engineering is just as important as the prompt itself.

- A major takeaway was that LLMs work well in scripts as one component in a larger pipeline. I used deterministic rules for initial labeling, then layered LLM validation on top as a semantic checker. We can combine traditional code for consistency and speed with LLMs for judgment and language understanding.

### GitHub Worktrees

Worktrees are a Git feature that allow you to have multiple branches checked out simultaneously on your system, through multiple working directories all associated with a single local repository. This allows users to work on multiple features/branches without constantly switching between them and stashing changes.

- All worktrees share the same underlying Git history, saving disk space compared to multiple full clones.
- They eliminate the need for `git stash` when switching tasks, as each has their own dedicated workspace.
  Operations like `git fetch` or creating a new branch are immediately reflected in all linked worktrees.

Commands

- `git worktree list`
- `git worktree add <path> [<branch>]`
- `git worktree remove <path>`
- `git worktree prune`

Resources used:

- https://www.youtube.com/watch?v=S8_AsOuAwLo
- https://www.youtube.com/watch?v=oI631eCAQnQ
- https://git-scm.com/docs/git-worktree

### Java Packages

#### Files, JVM, and Shutdown Hooks

- Working with the Files package in Java introduced me to how the JVM manages file system interactions at a higher level of abstraction than the older `java.io` API.
- Through the `java.nio.file` package, I explored how to perform common file operations: reading, writing, copying, and deleting, in a more expressive and reliable way.
- This led naturally into understanding the JVM itself more deeply: how it manages the lifecycle of a running Java program and what happens as it prepares to shut down.
- From there, I learned about shutdown hooks, which are threads registered with the JVM's runtime that execute automatically when the program is about to terminate, whether through a normal exit or an interruption.
- This was particularly relevant in the context of file handling when resolving a critical user-reported bug in RepoSense (PR #), as shutdown hooks provide a mechanism to ensure resources are cleanly released and any pending file operations are properly completed before the process exits, guarding against data loss or corruption.

### Google Stitch

I presented a teachback on Google Stitch, a Google Labs tool that generates high-fidelity UI designs from plain text prompts, and found it impressive for early-stage prototyping.

- It runs on an AI-native infinite canvas where you can bring in images, text, or even code as context, and a design agent tracks your progress across the whole project. Under the hood it uses Gemini and Nano Banana.
- What really sold me on it was the MCP integration with Claude Code — Stitch produces a `DESIGN.md` file that captures your color tokens, typography scales, and layout rules in a format Claude Code understands natively, so instead of copying and pasting design specs between apps, your agent connects directly and reads them in real time.
- To wire it up, you need a Google Cloud project with the Stitch API enabled, and then you can either use a Stitch API key (simpler) or OAuth via gcloud (more stable for heavy use)
- I went with the API key approach first. The Claude Code command is: `claude mcp add stitch --transport http https://stitch.googleapis.com/mcp --header "X-Goog-Api-Key: YOUR-API-KEY" -s user`, and once that's in you can verify it's live by running `/mcp` inside Claude Code and checking the server list.
- The tools Claude Code can then call include `create_project`, `generate_screen_from_text`, `get_screen_code`, and `build_site`, which means you can describe a screen in natural language, have Stitch generate it, and have Claude Code pull the HTML/CSS and scaffold it into React components, all without ever leaving the terminal.
- The typical flow for simple apps: five minutes designing in Stitch, a couple minutes for the MCP export, then Claude Code handling the backend and deploying.

### Vue.js and Pug

Through building the RepoSense Configuration Wizard, I gained hands-on experience with Vue.js and the Pug templating language.

Vue.js is a progressive JavaScript framework for building user interfaces. It uses a component-based architecture where each `.vue` file encapsulates a template, script, and style block.

Pug is an indentation-based HTML templating language that eliminates closing tags and angle brackets, producing cleaner and more concise markup. Vue supports Pug natively via `<template lang="pug">`, allowing developers to write Pug syntax while still using Vue directives like `v-model`, `v-for`, and `@click`.

- I learned how to structure a Vue project with reusable components, and how to manage cross-component communication through props, events, and a centralized store.
- Midway through development, I migrated all templates from standard HTML to Pug, which reduced template verbosity significantly.
- This taught me Pug's indentation-based syntax for expressing HTML hierarchy, how to bind Vue directives in Pug (e.g., `v-model`, `v-for`, `@click`, `:class`), and the importance of running a Pug linter (`puglint`) to catch formatting issues.
- I also learned that Pug's conciseness comes with trade-offs: the indentation sensitivity can make diffs harder to read and requires careful attention to nesting depth, especially in components with complex conditional rendering.

### Writing Cypress tests for Vue.js

I wrote a comprehensive Cypress end-to-end test suite for the config wizard.

Cypress is a JavaScript end-to-end testing framework for modern web applications. Unlike Selenium-based tools that run outside the browser, Cypress executes directly in the browser alongside the application, giving it native access to the DOM, network requests, and browser APIs. It provides a chainable command API (e.g., `cy.get().type().blur()`) for interacting with elements, `cy.intercept()` for stubbing and spying on network requests, and `cy.wait()` for synchronizing on asynchronous operations.

- A key technique I learned was using `cy.intercept()` to stub backend API calls, which allowed the frontend tests to run independently of the Java backend server.
- I created reusable `setupIntercepts()` helper functions that accept overrides, making it easy to test both success and error scenarios. For example, passing `{ validate: { valid: false, error: 'Repository not found' } }` to simulate an invalid repo URL.
- I also learned how to test multi-step wizard flows by writing navigation helper functions that programmatically advance through earlier steps before testing the target step.
- Other Cypress patterns I picked up include stubbing `window:alert` with `cy.stub().as('alert')` to assert on alert messages, using `cy.wait('@alias')` to synchronize on intercepted network requests, and configuring a custom `baseUrl` via `Cypress.env('configWizardBaseUrl')` so the wizard tests can target a different dev server than the main RepoSense app.
