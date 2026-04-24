## AI Coding Tools

### Skills

Worked with the team to explore adding repo-specific AI coding skills for common harnesses such as Claude, OpenCode and GitHub Copilot.

### Subagents

Created subagents to handle specific tasks such as writing unit tests, generating documentation, and refactoring code.

## Vue

### Reactivity (Vue 3)

Learned about Vue 3's reactivity system, including `ref`, `reactive`, and `computed` properties.

Used `reactive` and `computed` to implement dynamic data tag count in CardStack Component.

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
I decided to leverage on that and use a headless browser to render the site and print it to pdf.

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
<script> section to read system's theme preference and add a
data-bs-theme="dark" attribute to the <html> element where applicable.

### CSS scoping with global selectors

When adding dark mode styles inside `<style scoped>` Vue components, CSS scoping
transforms selectors and breaks global attribute selectors like `[data-bs-theme="dark"]`.
Solutions:
- Use `:global([data-bs-theme="dark"])` or `::deep()` for global ancestor selectors
- Or move global rules to an unscoped `<style>` block
- Bootstrap 5.3 uses `data-bs-theme="dark"` on `<html>` for theming

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

### Widening parameter types

Prefer `Iterable<T>` over `T[]` for function parameters when the function only iterates,
to accept Sets, generators, and other iterables without forcing array conversions downstream.

## GitHub API / Deployment

### Parsing Git remote URLs

When parsing GitHub remote URLs to construct deployment URLs:
- Strip trailing `.git` only when present: `repoSegment.endsWith('.git') ? repoSegment.slice(0, -4) : repoSegment`
- Using `substring(0, lastIndexOf('.'))` fails for URLs without `.git` (empty repo name) or repos with dots in names
