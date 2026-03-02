## General Knowledge
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

### Design Patterns

* [Builder Design Pattern](https://www.geeksforgeeks.org/system-design/builder-design-pattern/) to allow separation of construction logic from the final product and enables flexibility in building variations of the same product.


## Tips

* You can right click and inspect a web UI element to check its ID for debugging.
* You can terminate the E2E test early to keep a browser open, so when an E2E test fails, I can reload the previous browser to check the latest state of the failed E2E.
* Splitting a big PR into multiple smaller ones may cause the codebase to be in an non-ideal state (such as removing tests first will introduce a codebase with un-tested features), but fine if done in one go during the same iteration or migration. Other choices include defining the clear boundary of each small PR using commits within the same PR, or push the PRs into a separate branch before merging that branch into master.
* It’s possible to create a PR to fork’s master branch to run the CI privately.
* You can change the base branch that a PR merges into if you have write access.


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
