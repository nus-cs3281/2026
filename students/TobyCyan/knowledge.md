## General Knowledge

### OAuth (Open Authorization)
* OAuth (Open Authorization) is an authorization protocol for third-party apps to have limited access to a user’s protected resources. Usually a request is to be sent to a resource server to obtain the user’s credentials such as email. This works because the resource server already holds my credentials and knows that I am authentic, the third-party app doesn’t need to know my secrets other than the fact that I’m proven to be who I am by the resource server.
  * Step 1 (Pre-callback): Request for an authorization code from the authorization server within a defined scope (e.g. I want the user’s email), the resource server will only be able to serve resources within the scope.
  * Step 2 (Callback): Obtain access token by creating a token request to the authorization server using the authorization code.
  * Step 3: Execute a HTTP request to the resource server API using the access token.
  * Step 4: Extract the resource from the HTTP response and set the login cookie.
* In simple words, from the client app POV, it only knows the user’s email, but it trusts the user to be authentic because the Google resource server says so (i.e. the user has already logged into Google with their gmail). Hence, the app will allow the user to log in as if they have entered their complete login credentials.
* [OAuth2 for Google API](https://developers.google.com/identity/protocols/oauth2), [OAuth2 for Microsoft Entra ID](https://learn.microsoft.com/en-us/entra/identity-platform/v2-protocols).

### MS Entra ID
* When building a Microsoft client to query the authorization server, we can query the endpoint based on whether we want our app to be single-tenant or multi-tenant.
  * Single-tenant: `https://login.microsoft.com/{tenant-id}`
  * Multi-tenant: `https://login.microsoft.com/common`
* MS Entra recommends using certificates for authentication rather than client secrets. [Source](https://learn.microsoft.com/en-us/entra/identity-platform/how-to-add-credentials?tabs=certificate)

### Google Cloud
* Google Cloud also can be used to monitor the logs in the [logs explorer](https://console.cloud.google.com/logs/query;cursorTimestamp=2026-03-22T02:53:56.868370Z;duration=P7D?project=teammates-staging-487205).
* Go to API & Services -> Click on client ID -> Authorized Redirect URIs to set the redirect URI.

### Branding Guidelines
* Each authentication provider has their own branding guidelines when creating sign in buttons.
  * [Google](https://developers.google.com/identity/branding-guidelines), [Microsoft](https://learn.microsoft.com/en-us/entra/identity-platform/howto-add-branding-in-apps), [Firebase](https://firebase.google.com/brand-guidelines).

### Web Servlets
* Web servlets are mapped to their URL patterns in web.xml, same thing goes to filters such as OriginCheckFilter which is called for every visit to the mapped URL patterns to prevent CSRF attacks.
* [Resource for Jakarta Servlets](https://javadoc.io/doc/jakarta.servlet/jakarta.servlet-api/latest/jakarta.servlet/jakarta/servlet/http/package-summary.html).

### Testing

* Additional logic in test case may introduce issues:
  - More logic to maintain & might diverge.
  - Depending on the frontend may cause tests to pass if the frontend code is buggy (false-positive).
  - Depending on the local test case external logic may mismatch with what the front-end expects.
* Be very particular about test cases (we want them to fail to spot bugs).
* Hard-coded test inputs allow full control of the desired outcome.
* UUID has a different format than long.
* The server depends on the docker status, so I need to run docker first.
* Back door APIs for testing aims to improve testing performance by providing a more direct way to perform API calls without going through the UI, for databases it allows direct manipulation to set up the exact db state the test requires. However, it may introduce security risks like allowing unauthenticated users to make API calls and false positives in test outcomes if front door API calling isn’t tested properly.
* TestNG: `@BeforeTest` and `@BeforeMethod` differences: `@BeforeTest` runs before the entire test class, `@BeforeMethod` runs before every `@Test` in the same class, same applies to `@AfterTest` and `@AfterMethod`. [Source](https://www.baeldung.com/java-testng-beforetest-vs-beforemethod)
* UAT: The destructive path of error handling would be trying out cases that would make the system accept a faulty input.

### Identity Broker vs. Identity Provider
* Identity broker is like a gateway that sits between the app and identity providers such as Microsoft Entra ID, Google etc.
* The broker serves the client a list of supported providers and lets the client choose which provider they would like to authenticate with.
* Once the client chooses, the broker will pass on the authentication request to the respective provider.

### Regex
* `/[]` defines a set of characters to match within the `[]`.
* `/g` is a global flag to match every instance instead of the first one only.
* Using an escape (denoted using a backslash `\`), the regex treats the symbol that comes after it literally.
* E.g. `\*` would be literally the `*` character instead of `*` that represents ‘all’. 
* Same reason to represent a backslash `\` literally, it must be written as a double `\\`.

### Word Boundary
* In regex, a word boundary `\b` is to match a position between a word character and non-word character.
* E.g. `\\bcat\\b` matches cat exactly and not scatter or catholic.
* This means the character before and after cat must be non-word such as space, punctuations, and asterisks.

### Design Patterns

* [Builder Design Pattern](https://www.geeksforgeeks.org/system-design/builder-design-pattern/) to allow separation of construction logic from the final product and enables flexibility in building variations of the same product.

### Network Throttling
* Network throttling is a way for developers to emulate different network speeds by intentionally slowing it down. This feature can be found in the browser developer tools under the network tab.

### 3NF (Third Normal Form)
* 3NF (Third Normal Form) is a normalization level in databases to ensure that a non-key attribute doesn’t depend on another non-key attribute.
* The solution is to encapsulate related attributes into their own table and link the primary key back to the original table as a foreign key.


## Tips

* You can right click and inspect a web UI element to check its ID for debugging.
* You can terminate the E2E test early to keep a browser open, so when an E2E test fails, I can reload the previous browser to check the latest state of the failed E2E.
* Splitting a big PR into multiple smaller ones may cause the codebase to be in an non-ideal state (such as removing tests first will introduce a codebase with un-tested features), but fine if done in one go during the same iteration or migration. Other choices include defining the clear boundary of each small PR using commits within the same PR, or push the PRs into a separate branch before merging that branch into master.
* It’s possible to create a PR to fork’s master branch to run the CI privately.
* You can change the base branch that a PR merges into if you have write access.
* We should prioritize reading the DB using more efficient queries.
  * Should avoid making DB queries in a loop.
  * E.g. Fetching all students for a course in one query is better than querying the student for each deadline extension. (1 vs N queries)
* You can add a `--fail-fast` flag when running gradlew jobs to force stop it when something fails.
* TEAMMATES uses HTTP for local development, but authentication requires HTTPS TLS hand shake which causes protocol error during callback.

## Tools
### Github Copilot

* Copilot is able to automatically scan similar files and all scripts related to them before writing the json file I need.
* Non-agentic AI like ChatGPT on browsers can be more useful in catching mistakes in scripts and less prone to hallucinations compared to agentic AI that have to deal with a large context frame.
* You can ask Copilot to access the git commit history on the current branch to check for potential bugs due to changes made.

### VSCode

* To run the debugger on E2E tests (add –debug-jvm to the gradle command).
* To print statements when running tests using gradle (add –info to the gradle command).
* Possible to run “Convert Indentation to Spaces” in the command line in VSCode.
* Possible to run “Trim Trailing Whitespaces” in the command line in VSCode.

### Git

* Can use keywords like `Closes #<issue-number>` or `Fixes #<issue-number>` to automatically close an issue when a PR is merged, but this doesn’t work in issues (an issue cannot close another issue).
* `git switch -c <branch-name>` to create and switch to the new branch, which was introduced solely for checking out branches, while ‘git checkout’ can be used for branches, commits, and files.
* You can create a new branch and make it track an upstream branch using `git switch -c <branch-name> <upstream-name>/<upstream-branch-name>`. 
  * Example: To fetch a branch called `chore/new-branch` from the upstream repo and work on it locally, simply create a new branch of any name (preferably similar to better distinguish) and make it track that upstream repo branch.
  * Command line: `git switch -c chore/new-branch upstream/chore/new-branch`.
* Rebasing with -i (interactive) `git rebase -i <target-branch>`.
  * Rebasing to move the current commits on top of the HEAD of the target branch (i.e. doesn’t do anything if current branch is already on top).
  * Using interactive tag -i, we are able to edit/refactor the commits on the current branch and rebase will perform the operations.

### TestNG
* Sometimes snapshots can be detected to be obsolete, especially if it doesn’t match the rendering anymore, run `ng test --u` to update snapshots.

### Gradle
* Gradle runs tests parallelly which is much faster to run everything then a single suite which runs sequentially (Extremely slow).
* Github CI uses extensive powerful cores that scales dynamically and has fine-tuned resource control, which is why it runs so much faster than locally.

### Hibernate

* Hibernate ignores inserted `@UpdateTimestamp` annotated attributes.
* `@CreationTimestamp` and `@UpdateTimestamp` are initialized automatically with the same initial value, then `@UpdateTimestamp` will update itself when the entry is updated. [Source](https://www.baeldung.com/hibernate-creationtimestamp-updatetimestamp)

### Postman

* To test an API request, I can use API testing tools like Postman.
* Making API calls from another origin may require a CSRF (Cross-Site Request Forgery) token, this and the authentication token can be found in any of the HTTP request headers under the network tab.
* Configure the tokens under Headers tab in Postman.

### Apache JMeter
* Apache JMeter is a tool to simulate user traffic to a website/API endpoint. It can also be used to test HTTP requests using assertions.
* To configure cookies, go to HTTP Cookie Manager and insert CSRF-TOKEN, AUTH-TOKEN, JSESSIONID as separate entries where applicable.
* After configuring the managers, you can create a HTTP Request to an endpoint and use assertions to test the response (e.g. Response Code is 200).
* Running the load testing in CLI is more efficient because it doesn’t have the overhead of rendering the process and results in the GUI, consuming memory and CPU resources. [Source for CLI](https://jmeter.apache.org/usermanual/get-started.html#non_gui)
* JMeter CLI can generate detailed visualised reports covering response times, throughput, request statistics, request errors etc.
  * Flags for report generation (-e to generate report, -o <empty folder path> to indicate report output folder).

### Snyk
* Snyk is a tool used to monitor/detect security vulnerabilities in package dependencies. Synk CLI can be installed globally (`-g`) and used to test the project locally.
* To test for current directory: `snyk test`
* Test for all directories: `snyk test --all-projects`
* Test for specific file: `snyk test --file={file_name}`
