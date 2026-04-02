<!-- List the aspects you learned, and the resources you used to learn them, and a brief summary of each resource. -->

### AI Coding Tools
This module exposed me to multiple AI coding tools that are popular in the market, such as GitHub Copilot, Codex by OpenAI, and Cluade Code.
(Elaborate on learnings from each)

### Terminal UIs
Implementing TUIs, potential libraries, TUI vs GUI

### .yaml files
A YAML file is a human readable, plain-text file used mainly for configuration. DevOps, and data serialization. It uses indentation-based, hierarchical structures rather than curly braces or bracckets for data storage. Such a key-value pair structure makes it more readable and human friendly compared to JSON or XML.
Key aspects:
- Uses whitespace indentation to define structure, with colons `:` separating keys and values.
- It supports multiple data types (such as strings, integers, booleans etc.), sequences such as lists/arrays, and maps.
- Highly sensitive to indentation (spaces, not tabs). Comments are created with the `#` symbol.

Worked with YAML files when exploring the development of a GUI `.yaml` config filee generation wizard.

(Add more about learnings w.r.t its use in RepoSense)

### GitHub Actions

### Calling LLMs in Programs
for the CSV activity

### GitHub Worktrees
Worktrees are a Git feature that allow you to have multiple branches checked out simultaneously on your system, through multiple working directories all associated with a single local repository. This allows users to work on multiple features/branches without constantly switching between them and stashing changes.
- All worktrees share the same underlyinh Git history, saving disk space compared to multiple full clones.
- They eliminate the need for `git stash` when switching tasks, as each has their own dedicated workspace.
Operations like `git fetch` or creating a new branch are immediately reflected in all linked worktrees.

Commands
- `git worktree list`
- `git worktree add <path> [<branch>]`
- `git worktree remove <path>`
- `git worktree prune`

Resources used:
- https://www.youtube.com/watch?v=S8_AsOuAwLo
- https://www.youtube.com/watch?v=oI631eCAQnQ
- https://git-scm.com/docs/git-worktree

### Java Packages
#### Files
Files package, JVM, shutdown hooks