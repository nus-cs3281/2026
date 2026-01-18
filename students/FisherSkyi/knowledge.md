### Vue.js

resources Used:
- [Vue mastery](https://www.vuemastery.com/courses/intro-to-vue-3/intro-to-vue3/): complete 11 lessons to create a basic shopping cart frontend.
- [Vue.js documentation](https://vuejs.org/guide/quick-start/)
<!-- List the aspects you learned, and the resources you used to learn them, and a brief summary of each resource. -->

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

