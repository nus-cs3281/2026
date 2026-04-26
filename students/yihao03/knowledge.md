## AI Coding Tools

### Skills

Worked with the team to explore adding repo-specific AI coding skills for common harnesses such as Claude, OpenCode and GitHub Copilot.

#### Developing AI Skills

Learned about good practices for developing AI skills. Generally, the follow the
guidelines provided by [claude](https://code.claude.com/docs/en/skills) and
study this [skill](https://skills.sh/anthropics/skills/skill-creator) meant to teach AI agents to create skills.

Some notable points include:

- Do not teach AI general knowledges or concepts that it should already know. It
  wastes context and may cause confusion, degrading the performance and
  increasing token usage.
- Include project/user specific guard rails that the AI agents should follow,
  i.e.:
  - what **NOT** to do (e.g. modify files outside of the project directory, work
  on untracked files, perform database oeprations, etc.)
  - what **TO** do (e.g. write unit tests, add comments to code, avoid writing
  trivial comment to code, etc.)
  - **HOW** to do things (e.g. common make/npm commands to run, lints etc.)
- Keep the top level `SKILL.md` concise. Treat it like an index/table of
  contents, and refer to the other markdown files for detailed instructions and examples.

Most importantly: test the skill if they work, and pick up quirks/issues
introduced by the skills and tweak your files to improve them. Make sure you run
your AI coding tool's debug mode to see if the skills are being picked up.

#### Version controlling AI skills

Why AI skills are useful, they should be treated like code, i.e. it has to be
maintained. Otherwise, as project evolves, the code architecture or feature set
may change, and the skills would simply confuse the AI agents and make them do
wrong things, wasting token and time.

There are a few ways to mitigate this:

1. Use AI to maintain AI  
   - Create a subagent that periodically reviews the skill files and updates them based on the current state of the codebase and project requirements.
   - This could be done before PRs are merged, before each releases, or on a
   regular schedule
   - could be automated using GitHub Actions
   - This way, the skills can evolve with the project without requiring manual updates.
2. Enforce skill updates in PRs  
   - Make it a requirement for developers to review and update the AI skills whenever they make significant changes to the codebase.
   - This can be enforced through code review checklists or automated checks that flag outdated skills based on code changes.

#### Distributing AI skills

when the skills are not part of your own repo, i.e. meant to be shared with
developers outside of your team, you can publish them to a public registry such
as a github repository. There are a few ways for user to do this, the most
common one being

```sh
npx agent install <organization>/<repo>
```

provided by `vercel-lab/skills`

However, for MarkBind, since the skills should be tied to the version of
MarkBind, we have developed an in house command `markbind skills pull` that
enforces version control by fetching the skills release according to the version
specified in `markbind-cli`'s `package.json`.'

### Subagents

Created subagents to handle specific tasks such as writing unit tests, generating documentation, and refactoring code.

Useful tips:  

- customizing the subagents to use specific models to balance the cost, speed
and intelligence.
- use the subagents to manage the context window of the main agent.

### List of tools experimented with

1. OpenCode: My current favourite. Open source and supports multiple provider,
   has strong ecosystem and plugin support. works well with Neovim with
   [opencode.nvim](https://github.com/NickvanDyke/opencode.nvim) (the dev is super
   cool too)
2. Claude Code: also works well, especially with claude's own model. However,
   the UI is worse than OpenCode and UX is really bad.
3. GitHub Copilot: works well and has great VSCode integration. However,
   rate-limiting became really bad.

## Vue

### Reactivity (Vue 3)

Learned about Vue 3's reactivity system, including `ref`, `reactive`, and `computed` properties.

Used `reactive` and `computed` to implement dynamic data tag count in CardStack Component.

### Templates and slots

Learned about Vue's template syntax and slot system for component composition.
Useful for creating reusable components with flexible content, especially in the context of MarkBind's custom components.

### Other frameworks/meta-frameworks

- Svelte: explored Svelte's reactivity and component model, which uses a compiler to optimize updates.
- Astro: learned about Astro's island architecture for building static sites with partial hydration.
- Next.js: explored Next.js's server-side rendering and API routes for building full-stack React applications.

## TypeScript migration

### `tsc`

Learned to use the TypeScript compiler (`tsc`) to check for type errors and compile TypeScript code to JavaScript.

Several useful configs/flags learned:

- outDir: specifies the output directory for compiled JavaScript files.

## PDF generation for MarkBind sites

When making my own course notes with MarkBind, I realised a need to export the entire site to pdf file so that
it could be printed and brought to exams, and distribute easily in general. That's why I started exploring the idea
of creating a `@/packages/core-pdf` module that achieves this goal.

### Applications

- Export MarkBind sites to be distributed as pdf files
  - example use case: generate pdf for CS2103T ip/tp to be submitted for use in CS2101
- Export MarkBind sites to be printed for offline use
  - example use case: generate pdf for personal notes to be printed and brought to exams

### Experimentation

Considering MarkBind already creates a static site with proper formatting, with appropriate CSS for media print,
I decided to leverage on that and use a headless browser (Puppeteer) to render the site and print it to pdf.

### Challenges

#### Solved (i think)

##### Page order when merging

- In the built `_site` directory, the pages are individual `.html` files, with no particular order in the directory.
  - This makes it difficult to determine the correct page order when merging them into a single pdf.
- Implemented solution:
  - Parse the `.html` pages to extract the `<site-nav>` structure, which contains the correct page order.
  - Use the extracted page order to merge the individual pdfs in the correct sequence.

##### Hidden elementes

- Some elements (e.g. panels) can be collapsed by default and thus hidden when rendered, which may lead to missing content in the generated pdf.
- Implemented solution:
  - Inject javascript into the rendered page to expand all collapsible elements before printing to pdf, ensuring all content is included in the final output.

#### Outstanding issues

##### Big dependency/bundle size

- The headless browser library (Puppeteer) is quite large, which may not be ideal for a MarkBind plugin.
- Possible solution: Make Puppeteer an optional dependency, try to use the system's browser if available,
  only fallback to Puppeteer if no suitable browser is found.

##### iframes rendering

- Some pages with iframes (e.g. pdf and youtube videos) may not be able to show the rendered content but just
  the placeholder instead
- Attempted solution: use Puppeteer to take a screenshot of the iframe and inject that into the page. I can't get it to work though

## Adding dark mode support to MarkBind sites

I just found out that there's a `<mark>` component in HTML

### Old school HTML/CSS/JS

In implementing dark mode, I had to inject a script into page.njk which serves
as the template for every page rendered in markbind. To do that, I added a
`<script>` section to read system's theme preference and add a
data-bs-theme="dark" attribute to the <html> element where applicable.

### CSS scoping with global selectors

When adding dark mode styles inside `<style scoped>` Vue components, CSS scoping
transforms selectors and breaks global attribute selectors like `[data-bs-theme="dark"]`.
Solutions:

- Use `:global([data-bs-theme="dark"])` or `::deep()` for global ancestor selectors
- Or move global rules to an unscoped `<style>` block
- Bootstrap 5.3 uses `data-bs-theme="dark"` on `<html>` for theming

### CSS variables for theming

To implement dark mode, I replaced hardcoded color values with bootstrap CSS
variables (e.g., `var(--bs-body-bg)`) that automatically adapt to the theme,
ensuring consistent theming across components and maintenability. However, to
preserve some custom styles, I had to override some variables in the dark mode context (e.g.,
`[data-bs-theme="dark"]`) to ensure the colors look good in dark mode.

### Template value injection into JS (security)

Nunjucks template variables embedded directly into JS strings (e.g., `const theme = '{{ codeTheme }}'`)
can break the script or introduce injection if the value contains quotes or `</script>`.
Must serialize/escape as JSON before injecting template values into JS.

## CLI Development

### Interactive prompts

`@inquirer/prompts` provides interactive command-line prompts for CLI tools, useful for
setup flows and user identification of harnesses.

### Version control for AI skills

Skills pulled from external repos (e.g., `MarkBind/skills`) can be version-tracked via a
`.markbind-skills.json` file in `.agents/skills`, similar to `package-lock.json`.
The version is compared against `package.json`'s `aiSkillsVersion` to prompt users to update.

## TypeScript Patterns

### Module augmentation for patched packages

When patching third-party packages (nunjucks, htmlparser2, markdown-it), use `declare module`
to add types for augmented modules. For packages with internal sub-modules not exposed in
their types, create ambient declarations (e.g., `nunjucks-submodules.d.ts`).

### `import type` for pure type imports

Use `import type { X } from 'y'` for types-only imports to improve compile performance and
clarify intent.

### CJS require hack in ESM

ESM imports are read-only namespaces, so prototype monkey-patching on imported modules won't work.
The workaround is using `require('module/path')` from `node:module` to get a mutable CommonJS
object while using `import type` for development-time type safety. This creates technical debt
and may break if the package shifts to pure ESM output.

when `require` is not natively available in ESM, we can use `createRequire` to create a CommonJS `require` function:

```ts
import { createRequire } from 'node:module';
const require = createRequire(import.meta.url);
const nunjucks = require('nunjucks');
```

### Widening parameter types

Prefer `Iterable<T>` over `T[]` for function parameters when the function only iterates,
to accept Sets, generators, and other iterables without forcing array conversions downstream.
