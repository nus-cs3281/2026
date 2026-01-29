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

## Tools
### Github Copilot

* Copilot is able to automatically scan similar files and all scripts related to them before writing the json file I need.
* Non-agentic AI like ChatGPT on browsers can be more useful in catching mistakes in scripts and less prone to hallucinations compared to agentic AI that have to deal with a large context frame.

### VSCode

* To run the debugger on E2E tests (add –debug-jvm to the gradle command).
* To print statements when running tests using gradle (add –info to the gradle command).
* Possible to run “Convert Indentation to Spaces” in the command line in VSCode.
* Possible to run “Trim Trailing Whitespaces” in the command line in VSCode.




