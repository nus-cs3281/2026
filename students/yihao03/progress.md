# Overview

## Weekly Progress (MarkBind)

<box type="info" header="## Scope">

`MarkBind/markbind` and `MarkBind/skills` via GitHub contributions.

</box>

---

### Week 1

<panel type="secondary" header="Week 1 Summary" expanded style="margin-bottom: 1.5rem; margin-top: 1rem;">

- **Review:** [#2775 Structurally refactor Site class into Facade and separate Managers](https://github.com/MarkBind/markbind/pull/2775) (2026-01-16)
  - Related issue(s): [#1756](https://github.com/MarkBind/markbind/issues/1756), [#2774](https://github.com/MarkBind/markbind/issues/2774)
- **Review:** [#2777 Add example of content processing flow in developer documentation](https://github.com/MarkBind/markbind/pull/2777) (2026-01-16)
  - Related issue(s): [#2229](https://github.com/MarkBind/markbind/issues/2229)

</panel>

### Week 2

<panel type="secondary" header="Week 2 Summary" expanded style="margin-bottom: 1.5rem; margin-top: 1rem;">

- **PR:** [#2788 Update architecture diagram to use mermaid](https://github.com/MarkBind/markbind/pull/2788) (MERGED, 2026-01-19)
  - Replaced `architecture.pptx` and `architecture.png` with a mermaid diagram in `architecture.md`.
  - Diagram rendered correctly when serving the MarkBind site.
- **Review:** [#2801 Use ts-graphviz/setup-graphviz](https://github.com/MarkBind/markbind/pull/2801) (2026-01-25)
  - Related issue(s): [#2798](https://github.com/MarkBind/markbind/issues/2798)
- **Review:** [#2803 Remove bluebird dependency from async functions](https://github.com/MarkBind/markbind/pull/2803) (2026-01-25)
  - Related issue(s): [#2776](https://github.com/MarkBind/markbind/issues/2776)

</panel>

### Week 3

<panel type="secondary" header="Week 3 Summary" expanded style="margin-bottom: 1.5rem; margin-top: 1rem;">

- **PR:** [#2804 Add agent skills for AI coding](https://github.com/MarkBind/markbind/pull/2804) (MERGED, 2026-01-26)
  - Added agent skills for AI coding tools (OpenCode/ClaudeCode).
  - Used the open-source `SKILL.md` standard, which is provider agnostic.
  - Created skills by reading the dev guide and generating relevant skill files.
- **PR:** [#2805 Migrate vue-components package to TS](https://github.com/MarkBind/markbind/pull/2805) (CLOSED, 2026-01-26)
  - Migrated `packages/vue-components` JavaScript files to TypeScript.
  - Part of the effort to migrate the codebase to TypeScript and ES6.
  - Done primarily using OpenCode with Claude Sonnet 4.5 to experiment with AI coding.
- **PR:** [#2809 Implement custom cardstack tag colors and order](https://github.com/MarkBind/markbind/pull/2809) (MERGED, 2026-01-29)
  - Implemented feature to specify custom tag colors and order in the `cardstack` component.
  - Tag colors and order are specified as props.
  - Supports bootstrap color classes and custom hex codes.
- **Issue:** [#2818 Full Screen Diagrams](https://github.com/MarkBind/markbind/issues/2818) (OPEN, 2026-02-01)

</panel>

### Week 4

<panel type="secondary" header="Week 4 Summary" expanded style="margin-bottom: 1.5rem; margin-top: 1rem;">

- **Review:** [#2814 Add `AGENTS.md` files to provide guidelines for project and packages](https://github.com/MarkBind/markbind/pull/2814) (2026-02-02)
- **Review:** [#2813 Add update-docs skill](https://github.com/MarkBind/markbind/pull/2813) (2026-02-02)
- **Issue:** [#2822 Add AI Subagents](https://github.com/MarkBind/markbind/issues/2822) (CLOSED, 2026-02-02)
- **PR:** [#2824 Add setup to pretest script](https://github.com/MarkBind/markbind/pull/2824) (OPEN, 2026-02-02)
  - Added a pre-test cleanup step to delete stale artifacts before running tests.
  - Addresses issue where tests pass locally but fail in CI due to stale built files.
  - Currently still open, pending review.
- **Review:** [#2823 Add skills setup info to docs](https://github.com/MarkBind/markbind/pull/2823) (2026-02-04)
- **PR:** [#2828 Add Card Counts to Tag](https://github.com/MarkBind/markbind/pull/2828) (MERGED, 2026-02-05)
  - Modified the `cardstack` and `card` components to include card counts for each tag.
  - Used Vue 3 reactivity to dynamically update tag counts during search.
  - Related issue(s): [#2808](https://github.com/MarkBind/markbind/issues/2808)

</panel>

### Week 5

<panel type="secondary" header="Week 5 Summary" expanded style="margin-bottom: 1.5rem; margin-top: 1rem;">

- **PR:** [#2834 Migrate packages/vue-components Utils files to TS](https://github.com/MarkBind/markbind/pull/2834) (MERGED, 2026-02-11)
  - Migrated `packages/vue-components/src/utils` files to TypeScript.
  - Uses babel to compile TypeScript and `tsc` for type checking.
  - No additional dependencies added; used `babel/preset-typescript` for compile support.
- **Review:** [#2807 Add create-pull-request skill for GitHub PR automation](https://github.com/MarkBind/markbind/pull/2807) (2026-02-13)

</panel>

### Week 6

<panel type="secondary" header="Week 6 Summary" expanded style="margin-bottom: 1.5rem; margin-top: 1rem;">

- **Issue:** [#2849 Misleading deploy command success despite failure output](https://github.com/MarkBind/markbind/issues/2849) (OPEN, 2026-02-28)

</panel>

### Week 7

<panel type="secondary" header="Week 7 Summary" expanded style="margin-bottom: 1.5rem; margin-top: 1rem;">

- **PR:** [#2852 Update markbind deploy success log message](https://github.com/MarkBind/markbind/pull/2852) (MERGED, 2026-03-02)
  - Deploy command previously showed success regardless of actual deployment result.
  - Updated deploy output to include both the GitHub Actions URL and deployed site URL.
- **PR:** [#2853 Migrate Core Patches to TypeScript](https://github.com/MarkBind/markbind/pull/2853) (MERGED, 2026-03-04)
  - Migrated `nunjucks`, `htmlparser2`, and `markdown-it` patches to TypeScript and ESM.
  - Used module augmentation to add types for patched packages.
  - Included significant monkey patching updates.
- **Issue:** [#2854 Add open page command for `markbind serve`](https://github.com/MarkBind/markbind/issues/2854) (OPEN, 2026-03-06)

</panel>

### Week 8

<panel type="secondary" header="Week 8 Summary" expanded style="margin-bottom: 1.5rem; margin-top: 1rem;">

- **PR:** [#2856 Add Dark Mode Support](https://github.com/MarkBind/markbind/pull/2856) (MERGED, 2026-03-11)
  - Upgraded Bootstrap to 5.3 for dark theme support.
  - Added a dark mode flag in `site.json` that respects system preference by default.
  - Added a navbar toggle to switch between light and dark mode.
  - Added runtime page theme switching.
  - Refactored hardcoded color values to use bootstrap CSS variables.

</panel>

### Week 9

<panel type="secondary" header="Week 9 Summary" expanded style="margin-bottom: 1.5rem; margin-top: 1rem;">

- **Review:** [#2860 Add verbose logging (`-v` option) functionality](https://github.com/MarkBind/markbind/pull/2860) (2026-03-18)
- **Review:** [#2863 Migrate Core output from CJS to ESM](https://github.com/MarkBind/markbind/pull/2863) (2026-03-21)

</panel>

### Week 10

<panel type="secondary" header="Week 10 Summary" expanded style="margin-bottom: 1.5rem; margin-top: 1rem;">

- **Review:** [#2868 Fix `markbind serve -d`](https://github.com/MarkBind/markbind/pull/2868) (2026-03-27)
- **Review:** [#2862 Enhance deployment output logs](https://github.com/MarkBind/markbind/pull/2862) (2026-03-27)
- **Review:** [#2877 Fix updatetest script](https://github.com/MarkBind/markbind/pull/2877) (2026-03-28)

</panel>

### Week 12

<panel type="secondary" header="Week 12 Summary" expanded style="margin-bottom: 1.5rem; margin-top: 1rem;">

- **Review:** [#2887 Update about page on markbind](https://github.com/MarkBind/markbind/pull/2887) (2026-04-08)
  - Related issue(s): [#2881](https://github.com/MarkBind/markbind/issues/2881)
- **Issue:** [#2888 Interactive setup for MarkBind sites](https://github.com/MarkBind/markbind/issues/2888) (OPEN, 2026-04-09)

</panel>

### Week 13

<panel type="secondary" header="Week 13 Summary" expanded style="margin-bottom: 1.5rem; margin-top: 1rem;">

- **PR:** [#2889 User facing AI Skills](https://github.com/MarkBind/markbind/pull/2889) (CLOSED, 2026-04-13)
  - Built a preview of user-facing AI skills for MarkBind users.
  - Enables users to use AI coding tools to manage MarkBind sites more efficiently.
  - Skills were intended to live in a separate repository.
  - Created a new repo [MarkBind/skills](https://github.com/markbind/skills) to
    host the user-facing AI skills.
- **Review:** [#2885 Replace error logging with silent skip when page DNE](https://github.com/MarkBind/markbind/pull/2885) (2026-04-13)
- **Review:** [#2890 Add Pagefind incremental indexing](https://github.com/MarkBind/markbind/pull/2890) (2026-04-16)
  - Related issue(s): [#2873](https://github.com/MarkBind/markbind/issues/2873)
- **PR:** [#2893 Add commands to pull AI Skills](https://github.com/MarkBind/markbind/pull/2893) (MERGED, 2026-04-16)
  - Added new `markbind skills` command family to manage AI skills from `MarkBind/skills`.
  - Implemented version control for skills using `.markbind-skills.json`.
  - Added `@inquirer/prompts` for interactive prompts and future repo setup flows.
- **Issue:** [#2894 Update deployment workflow](https://github.com/MarkBind/markbind/issues/2894) (OPEN, 2026-04-17)
- **Issue:** [#2895 Replace .md by .html when building sites for interlinks](https://github.com/MarkBind/markbind/issues/2895) (OPEN, 2026-04-17)

<box type="success" header="## Milestone">

Published `markbind-cli@7.1.0` on npm with new workflow!

</box>

</panel>
