# Overview

## PRs Created

| ID     | TITLE                                              | STATE |
|--- |--- |--- |
| #2893  | Add commands to pull AI Skills                     | MERGED |
| #2891  | Add Command to pull user-facing skills            | MERGED |
| #2889  | User facing AI Skills                             | CLOSED |
| #2856  | Add Dark Mode Support                             | MERGED |
| #2853  | Migrate Core Patches to TypeScript                | MERGED |
| #2852  | Update markbind deploy success log message        | MERGED |
| #2834  | Migrate packages/vue-components Utils files to TS  | MERGED |
| #2828  | Add Card Counts to Tag                             | MERGED |
| #2824  | Add setup to pretest script                        | OPEN |
| #2809  | Implement custom cardstack tag colors and order    | MERGED |
| #2805  | Migrate vue-components package to TS               | CLOSED |
| #2804  | Add agent skills for AI coding                     | MERGED |
| #2794  | feat_specify cardstack tags order and colour       | CLOSED |
| #2788  | Update architecture diagram to use mermaid       | MERGED |

## PR Details

### #2893  Add commands to pull AI Skills

- Added new command family `markbind skills` that manages AI skills created in
the new [skills](https://github.com/markbind/skills) repository.
- Implemented version control for skills using `.markbind-skills.json` to track skill versions.
- Added new package `@inquirer/prompts` for interactive prompts, laying the
foundation for future interactive repo setup commands.

### #2889  User facing AI Skills

- Preview of user-facing AI skills for MarkBind users.
- Allow users to use AI coding tools to manage their MarkBind sites more
efficiently.
- Skills meant to live on a separate repository.

### #2856  Add Dark Mode Support

- Upgraded Bootstrap to 5.3 for dark theme support.
- Added dark mode flag in `site.json` that respects system preference by default.
- Added toggle button in navbar to switch between light and dark mode.
- Added runtime page theme switching.
- Refactored hardcoded color values to use bootstrap CSS variables

### #2853  Migrate Core Patches to TypeScript

- Migrated `nunjucks`, `htmlparser2` and `markdown-it` patches to TypeScript and ESM.
- Used module augmentation to add types for patched packages.
- A lot of monkey patching

### #2852  Update markbind deploy success log message

- Initially, deploy command always showed a success message regardless of the
actual deployment result.
- Updated deploy log message to instead include both GitHub Actions URL deploying the site and the deployed site URL.

### #2834  Migrate packages/vue-components Utils files to TS

- Migrated `packages/vue-components/src/utils` files to TypeScript.
- Uses babel to compile the TypeScript files, with `tsc` for type checking.
- No additional dependencies added, added `babel/preset-typescript` to handle the compiling.

### #2828  Add Card Counts to Tag

- Modified the `cardstack` and `card` components to include a count of the number of cards with each tag.
- Used Vue 3's reactivity system to dynamically update the tag counts as we search the cards.

### #2824  Add setup to pretest script

- Adds a pre-test cleanup step to delete stale artifacts before running tests.
- Addresses issue where tests pass locally but fail in CI due to stale built files.
- Currently still open, pending review.

### #2809  Implement custom cardstack tag colors and order

- Implemented the feature to specify custom tag colors and order in the `cardstack` component.
- The tag colors and order are specified as props.
- Supports bootstrap color classes and custom hex codes for colors.

### #2805  Migrate vue-components package to TS

- Migrated the `packages/vue-components` JavaScript files to TypeScript.
- Part of the effort to migrate the entire codebase to TypeScript and ES6.
- Done primarily using OpenCode with Claude Sonnet 4.5 to experiment with AI coding.

### #2804  Add agent skills for AI coding

- Added agent skills for AI coding tools (OpenCode/ClaudeCode).
- Used the open source SKILL.md standard which is provider agnostic.
- Created skills by reading the devGuide and generating relevant skill files.

### #2788  Update architecture diagram to use mermaid

- Replaced `architecture.pptx` and `architecture.png` with mermaid diagram in `architecture.md`.
- Diagram rendered correctly when serving the markbind site.
