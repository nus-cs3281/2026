### Tool/Technology 1

### Developer tools 
## Agentic programming
* Explored the use of Agentic programming through applications such as Claude Code CLI, Antigravity, and Cursor.
  * Such applications help to orchastrate multiple AI agents in implementing and executing a prompt.
  * Agentic workflows is much better for complex tasks
  * PLAN phase helps to ensure that the AI is following exactly what you learnt
* Understand and effectively use sub-agents in programming  
* Explored how to structure prompts in a way to be clear about requirements and implementation methods
* Understood the use of different AI models: not a one-size-fits-all approach
  * Claude Opus for difficult tasks, Gemini/Sonnet/Codex for simple, Haiku/Gemini(Low) for basic tasks
## AI Design
* Explored and used AI design tools such as Google Stitch to generate and re-design initial designs in Figma
  * Don't just ask the AI to create a design based off words. Way better to find similar designs that you like, or even make a mockup on Figma first.
  * This saves processing time as the AI has a reference image that they can tweak

## Vibe Coding
* Explored how vibe coding can generate useable prototypes
* Explored how to prompt AI to make changes to its own designs and iterate
* Takeaways:
  1. It is possible to create an MVP through vibe coding
  2. However, the code produced is not good and would be almost as much work to refactor it as it is to rewrite from scratch
  3. Asking AI to refactor the codebase takes too long. 
  > Maybe it would have been better to be strict on code quality with the AI, perhaps in a CLAUDE.md file.


### Electron
* Chromium browser
  * Electron ships a Chromium browser, so effectively any web technology can be used
  * Better for quick development, as existing web developers will feel at home and any UI library can be used (such as React)
  * However, Chromium is not lightweight and is often critisied as unnecessary bloat, and many seasoned developers prefer to build native code
  * Ultimately, the choice between Electron and native comes down to that of project requirements: for CS3282, probably better to use Electron as there are likely to be more people knowing HTML/CSS/JS than native code
    * Especially for multi-platform development
* `main` process
  * The main process is actually just a NodeJS process
  * All NodeJS functions are available (e.g. fs).
  * Communication is done via Inter-process-communication (IPC)
* IPC
  * IPC allows communication between the Chromium browser and the NodeJS backend
  * Using `exposeInContextBridge` in a special script called `preload`, we can have a few options:
    * ipcSend: fire-and-forget 
    > used to trigger something in the backend without expecting a response
    * ipcInvoke
    > request-response: expect a response from the backend
  * `ipcInvoke('gitmastery-start-task', { command })` is used to start a task and get a single response.
  * Continuous updates are streamed by listening on `ipcOn('gitmastery-task-data', ...)`, with a cleanup function to unsubscribe.
* WebView
  * Embedding an external website is possible in one of two ways:
  1. iframe, 2. WebContentsView
  * iframe 
    * \+ Is a HTML element
    * \+ Simple
    * \- Cannot run custom JS code (needed for GitMastery JS injection)
  * WebContentsView
    * \+ Can inject custom JS code
    * \- Requires custom code to listen to window size and adjust
      * Since WCV is handled by the backend but yet the viewport is in the frontend, a IPC handler has to be set up
    * \- Is NOT actually a HTML element, rather it's drawn by the system, so it has higher display priority and will block any elements rendered by the frontend behind this
      * especially annoying for showing modal popups as the WCV will be visible 
      * solved by making a custom modal handler that hides the WCV whenever a modal is to be shown
