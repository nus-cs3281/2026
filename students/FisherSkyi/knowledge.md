### Vue.js

resources Used:
- [Vue mastery](https://www.vuemastery.com/courses/intro-to-vue-3/intro-to-vue3/): complete 11 lessons to create a basic shopping cart frontend.
- [Vue.js documentation](https://vuejs.org/guide/quick-start/)
<!-- List the aspects you learned, and the resources you used to learn them, and a brief summary of each resource. -->

### Pug

Pug's parser is misinterpreting where the attribute value ends when you split it across lines.
e.g.
```pug
:class="{warn: user.name === '-',
    'active-text': ...}"
```
The parser gets confused by the line break and the quote positioning. It's a quirk of how Pug tokenizes/parses attributes across multiple lines.

### GitHub Action workflow

Can set condition to only runs if:
  - Push to `master` branch, OR
  - Scheduled trigger (if enabled)

Does NOT run on pull requests (prevents deploying unreviewed changes)

```yml
deploy:
    needs: build
    if: (github.event_name == 'push' && github.ref == 'refs/heads/master') || github.event_name == 'schedule'
```

Summary of current github workflow:
- Push to master → Build report → Upload artifacts → Deploy to gh-pages → Live at GitHub Pages
- Pull request   → Build report → Upload artifacts → (stop, don't deploy)

### Gemini integration for Java
resources Used:
- [Gemini workshop for Java developers](https://github.com/glaforge/gemini-workshop-for-java-developers)
- [Offical Documentation: Gemini in Java with Vertex AI and LangChain4j](https://codelabs.developers.google.com/codelabs/gemini-java-developers)
- [Google Cloud](https://console.cloud.google.com/)

### Copilot
In-line chat: use `ctrl + shift + I` to open copilot chat window.


