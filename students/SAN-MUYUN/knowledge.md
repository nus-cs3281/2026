### ContextManager

A context manager in Python is a structured way to handle resources so setup and cleanup are done safely and automatically, usually through the with statement. Instead of manually opening and closing files or connections, a context manager guarantees that cleanup logic still runs even if an exception occurs inside the block, which reduces bugs and resource leaks. Under the hood, this works through the context manager protocol (`__enter__` and `__exit__`), where `__enter__` prepares the resource and `__exit__` handles teardown. This pattern makes code cleaner, easier to read, and more reliable because resource handling is localized to one clear block. Common examples include file I/O, database transactions, thread locks, and temporary state changes, and a good rule is to use with whenever something must always be released or restored.

**resources:**<ul><li>RFC: [Context Matters](https://docs.google.com/document/d/1JhHCS6hZ9iVoWQa4QZBpcGMuv4GB9z74bfhSgzD-WI0/edit?tab=t.0)</li></ul><ul><li>[Context Manager python documentation](https://book.pythontips.com/en/latest/context_managers.html)</ul></li>

### Utilising Codex for coding
OpenAI Codex is an AI coding agent, a large language model specialized for software tasks, combined with tools that let it work inside a real project. It can be very useful to read and understand files across a repository, run terminal commands,
propose and apply code edits, generate test cases etc.

#### AI Agent:
`Agent.md` is a project-specific instruction file that tells an AI coding assistant how to behave inside a codebase: what the project does, how the folders are organized, coding conventions, testing commands, and things to avoid. It improves AI performance by informing the LLM exactly how the project’s structure or style from scattered files look like, so it makes more accurate edits, follows the right conventions, avoids breaking assumptions, and produces code that fits the repository better.

Features of a good `Agent.md` includes:
<ul><li>State a clear role</li></ul>
<ul><li>Indicates the executable commands</li></ul>
<ul><li>Project knowledge</li></ul>
<ul><li>Real Examples</li></ul>

Ideally, `Agent.md` should be very specific on the task that this particular AI Agent should carry out, like writing test cases, debug, refactoring, instead of being very generic.

**resources**
- [How to write a great agents.md: Lessons from over 2,500 repositories](https://github.blog/ai-and-ml/github-copilot/how-to-write-a-great-agents-md-lessons-from-over-2500-repositories/)
- [Custom instructions with AGENTS.md](https://developers.openai.com/codex/guides/agents-md/)

#### Prompt Engineering:
Prompt engineering is the practice of designing clear, specific instructions so an AI can produce more accurate, useful, and consistent outputs.

A good prompt should:
<ul><li>give enough information about the task</li></ul>
<ul><li>provide desired response/output format</li></ul>
<ul><li>any constraints that is not clearly stated in the task information provided to the LLM</li></ul>

If the task is complicated, it is always recommended to break it into smaller tasks, and prompt the AI to complete a sequence of smaller tasks.



**resources:**
- [What Is Prompt Engineering? Definition and Examples](https://www.coursera.org/articles/what-is-prompt-engineering?utm_medium=sem&utm_source=gg&utm_campaign=b2c_apac_x_multi_ftcof_career-academy_cx_dr_bau_gg_pmax_gc_sg_all_m_hyb_25-04_desktop&campaignid=22449465350&adgroupid=&device=c&keyword=&matchtype=&network=x&devicemodel=&creativeid=&assetgroupid=6568546196&targetid=&extensionid=&placement=&gad_source=1&gad_campaignid=22442997015&gbraid=0AAAAADdKX6a5qC8HfJN4F-2bDlUpmsyuC&gclid=Cj0KCQiA2bTNBhDjARIsAK89wlHCKiGUC3EW_J0XliK1RhvXRh2FKKsCqMli93CJV-sINoChIimFdmYaAld0EALw_wcB)
- [Prompt Chaining Tutorial: What Is Prompt Chaining and How to Use It?](https://www.datacamp.com/tutorial/prompt-chaining-llm?utm_cid=19589720824&utm_aid=157098106775&utm_campaign=230119_1-ps-other~dsa-tofu~all_2-b2c_3-apac_4-prc_5-na_6-na_7-le_8-pdsh-go_9-nb-e_10-na_11-na&utm_loc=9062531-&utm_mtd=-c&utm_kw=&utm_source=google&utm_medium=paid_search&utm_content=ps-other~apac-en~dsa~tofu~tutorial~artificial-intelligence&gad_source=1&gad_campaignid=19589720824&gbraid=0AAAAADQ9WsFiJ5fau6lxdBuD9lgM46Iwl&gclid=Cj0KCQiA2bTNBhDjARIsAK89wlGLy8bdhIAsqSlxwlWNibpHzVqfuy-QFFN9iGE3kir4HC11yCDrbc0aAg8DEALw_wcB)

