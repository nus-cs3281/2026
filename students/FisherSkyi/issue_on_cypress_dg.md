```bash
./gradlew serveTestReportDefault
```

The test report has been generated successfully. The task completed with "BUILD SUCCESSFUL" and you can see:

"The report is generated at /Users/sky/CS3281/RepoSense/build/serveTestReport/./default/reposense-report"
The Vite dev server started automatically at the end
Now the server should be running on http://localhost:9000 with the actual RepoSense report (not the upload page).

The report now has:

The #summary element
The .mui-select.grouping dropdown with "Author" option
All the test data needed for Cypress tests
You should now be able to:

Keep this server running (it's already running from the gradle task)
Go to IntelliJ and click the green triangle next to the chartView_author_blurbs.cy.js test
The Cypress test should now find the #summary .mui-select.grouping select element and pass successfully.

Try running the Cypress test now!

in testcase `subzoom panel range should work correctly when timeline is optimised` in `chartView_optimiseTimeline.cy.js` (and other cypress test cases) there are hard coded 

```js
cy.get('body').type(zoomKey, { release: false })
  .get('#summary-charts .summary-chart__ramp .ramp')
  .first()
  .click(110, 20)
  .click(120, 20);
```
Will browser window size and screen resolution influence where should we click? 

Using Gradle (from project root)
# Headless (CI mode)
`./gradlew testFrontend`

# Interactive GUI (debug mode)
`./gradlew cypress`

Using npm directly (from frontend/cypress/)
cd frontend/cypress
```
npm ci                # install dependencies first
npm run tests         # headless with Chrome
npm run debug         # interactive GUI
```

Note: The tests expect two local servers running — a default report on port 9000 and a portfolio report on port 9001. The Gradle task handles starting those automatically. If running via npm directly, you'd need to start them yourself first:

# From frontend/
```
npm run serveTestDefault     # port 9000
npm run serveTestPortfolio   # port 9001
```