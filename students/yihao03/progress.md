# Overview

## PRs Created

| ID     | TITLE                                              | BRANCH |
|--- |--- |--- |
| #2834  | Migrate packages/vue-components Utils files to TS  | yihao03:feat/migrate-vue-utils-to-ts |
| #2828  | Add Card Counts to Tag                             | yihao03:feat/add-tag-count |
| #2824  | Add setup to pretest script                        | yihao03:chore/update-test-script |
| #2809  | Implement custom cardstack tag colors and order    | yihao03:feat/cardstack-tag-order-colors-implementation   |
| #2805  | Migrate vue-components package to TS               | yihao03:feat/migrate-vue-components-to-ts |
| #2804  | Add agent skills for AI coding                     | yihao03:feat/experiment-with-skills |
| #2794  | feat/specify cardstack tags order and colour       | yihao03:feat/specify-cardstack-tags-order-and-colour |
| #2788  | Update architecture diagram to use mermaid         | yihao03:chore/user-mermaid |

## PR Details

### #2834  Migrate packages/vue-components Utils files to TS

- Migrated `packages/vue-components/src/utils` files to TypeScript.
- Uses babel to compile the TypeScript files, with `tsc` for type checking.
- No additional dependencies added, added `babel/preset-typescript` to handle the compiling.

### #2828  Add Card Counts to Tag

- Modified the `cardstack` and `card` components to include a count of the number of cards with each tag.
- Used Vue 3's reactivity system to dynamically update the tag counts as we search the cards.

### #2824  Add setup to pretest script

I noticed that sometimes when tests rely on built files, after pulling from remote, the built files might be outdated and cause test failures. To solve this, I added a setup step to the pretest script to ensure that the necessary build steps are executed before running the tests.

However, it increases the time to run the tests, so I'm not sure if its the best solution. It has not been merged yet.

### #2809  Implement custom cardstack tag colors and order

- Implemented the feature to specify custom tag colors and order in the `cardstack` component.
- The tag colors and order are specified as props.
- Supports bootstrap color classes and custom hex codes for colors.
