### AI Coding

#### OpenCode
OpenCode is a CLI program for agentic coding. It allow users to use the same application with different LLM models, supporting many different providers.

* Planning: Creating a plan for the agent to follow in order to complete a task allows ensuring implementation will be as specified.
* Context management: Provide only strictly required information to the agent when prompting and writing project rules to manage the context window effectively. Agent's exploration of the codebase can provide most of the low level details.
* Skills: Progressive disclosure of skills to the agent allows sterring the agent's behavior only when needed, preventing pollution of context

#### Gemini code assist
Gemini Code Assist for GitHub is able to review PRs. It was able to find multiple issues in the PRs which i use it in.

* Security: It found potential atack vectors like decompressing zip files into arbitrary locations
* Bugs: It found potential bugs like brittle code that could break if string format changes or missing variables when creating hash for cache keys that is supposed to invalidate the cache when changed.

#### Resources
* Youtube: Many content creators create videos about agentic coding that can be transferred across different harnesses.
* [Aihero](https://www.aihero.dev/): A website with articles and resources for agentic coding.

### QML

A declarative language for designing user interfaces, which can be used through PySide to create GUI applications in python.

#### Aspects learned
* Syntax: Using QML classes to create layouts, signals to handle interations, models and views to display data.
* Resources: Including external resources like images and custom modules to use custom classes written in QML and python.

#### Resources
* [PySide documentation](https://doc.qt.io/qtforpython-6/): Official documentation for PySide, for information on using QML with PySide.
* [Qt documentation](https://doc.qt.io/qt-6/): Official documentation for Qt, for information on QML classes.

### Electron

A framework for developing desktop applications using web technologies.

#### Aspects learned
* Frontend: Using component library (Maintine) to create user interfaces with react.
* Architecture: Setting up electron process and allowing the renderer process to communicate with the main process using IPC.
* Development: Running the electron backend and react frontend without buiding them to watch for code changes and reloading when there are.
* Packaging: Building both the frontend and backend packaging both into an application for distribution.
