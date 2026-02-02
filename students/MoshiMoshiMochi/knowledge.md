### GitHub Copilot

GitHub Copilot is a code completion and programming AI-assistant that assist users in their IDE. It uses LLMs can assist with code generation, debugging or refactoring through either real-time suggestions or language prompts

Key Learning Points:
- Context is King! Providing all relevant files immediately leads to faster, more accurate fixes. The AI performs best when it "sees" the full scope of the bug.

- Don't stop at the first working fix. Specifically, we can try asking the AI to improve code quality and clarity after the initial generation helps eliminate "AI-style" clutter and technical debt.

- Initial AI suggestions often prioritize the simplest fix. It still requires manually prompts & investigation for edge cases to ensure the solution is robust.

- We should treat AI as a collaborator, and not an automated system. Reviewing proposed changes and selectively implementing only what fits the project context prevents the introduction of unnecessary or incorrect logic.

### Agent Skills

Agent Skills are folders of instructions, scripts, and resources that agents can discover and use to do things more accurately and efficiently. These skills are designed to be automatically founded and used by AI agents, providing them user-specific context they can load on demand hence extending their capabilities based on the task they’re working on.

Key Learning Points:
- Moving instructions from a giant system prompt into a SKILL.md file allows for "progressive disclosure," where the agent only loads the knowledge it needs for the specific task at hand.

- Provide a strict directory layout (Instructions in SKILL.md, automation in scripts/, and context in references/) to ensure the agent can reliably find and execute tools.

- Include specific trigger phrases & tags, as well as clear and well defined steps. This prevents the agent from guessing, thus ensuring it follows the exact logic required for the most effective application.