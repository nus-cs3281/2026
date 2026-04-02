## Project Knowledge
[RepoSense](RepoSense.md)

### Vue.js

- Working with .vue single-file components using Pug templates, scoped SCSS, and Vue 3 composition patterns
- Built a reusable c-scroll-top-button component with a scroll-container-id prop, avoiding duplication across summary.vue, c-authorship.vue, and c-global-file-browser.vue
- Used composables as the Vue 3 idiomatic pattern for shared stateful logic

### Cypress

- Ran tests via ./gradlew testFrontend or npm run cypress:open/run
- Debugged cy.scrollTo() failures — the key lesson: Cypress won't scroll an element unless it's actually scrollable (scrollHeight > clientHeight), so tests need to ensure content is loaded first

## AI in Development

### Gemini integration for Java
resources Used:
- [Gemini workshop for Java developers](https://github.com/glaforge/gemini-workshop-for-java-developers)
- [Offical Documentation: Gemini in Java with Vertex AI and LangChain4j](https://codelabs.developers.google.com/codelabs/gemini-java-developers)
- [Google Cloud](https://console.cloud.google.com/)

### MCP Server Basics

- Built calculator MCP servers (calculator, plane ticket (with google api), weather reporter) from scratch
- Understood the architecture
- Connected local MCP servers to Claude Desktop via claude_desktop_config.json

### Setup claude github

- use claude and copilot to create, review PRs.
