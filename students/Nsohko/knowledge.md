### Cursor

Learned how to use Cursor as an AI-assisted development environment for code generation, refactoring, debugging, and understanding unfamiliar codebases.

**Resources used:**
- Cursor official documentation  
  Learned the main product features, including inline editing, AI chat, and codebase-aware assistance.
- Hands-on project experience  
  Applied Cursor in real coding tasks, which helped me understand how to use it effectively for implementation and debugging rather than just code generation.

### agents.md

Learned how to define project-specific agent instructions using `agents.md` to improve consistency, task delegation, and adherence to coding conventions.

**Resources used:**
- Online examples and community discussions  
  Learned how developers use agent instruction files to guide AI behaviour in coding workflows.
- Personal experimentation  
  Practised writing instructions tailored to software engineering tasks such as editing files, following project structure, and maintaining style consistency.

### OpenAI API

Learned how to integrate the OpenAI API into software applications to build LLM-powered features and automate language-based tasks, such as csv pasing for form submissions.

**Resources used:**
- OpenAI API documentation  
  Learned the fundamentals of API usage, request formatting, and response handling.
- Personal implementation work  
  Built familiarity with practical integration concerns such as prompt design, output parsing, and feature prototyping.

### Prompt Engineering for Software Engineering Tasks

Learned how to design effective prompts for technical tasks such as code generation, debugging, summarization, and implementation planning.

**Resources used:**
- Repeated use of Cursor and OpenAI API  
  Learned through experimentation how prompt specificity, constraints, and context improve output quality.
- Community-shared prompt patterns  
  Observed effective prompt structures used by other developers for engineering workflows.

### AI-Assisted Debugging and Refactoring

Learned how to use AI tools to analyse bugs, explain code behaviour, and support incremental refactoring in existing systems.

**Resources used:**
- Cursor in day-to-day development  
  Used AI support to trace bugs, understand unfamiliar code, and explore alternative implementations.
- Real project experience  
  Helped me understand the strengths and limitations of AI when working with non-trivial codebases.

### Rapid Prototyping of AI Features

Learned how to quickly prototype AI-enabled product ideas by combining LLM APIs with frontend or backend applications.

**Resources used:**
- Personal software projects  
  Gained experience turning simple ideas into working prototypes using AI components.
- OpenAI API documentation  
  Provided the technical basis for implementing these features correctly.

### RAG Pipeline Design

Learned the fundamentals of RAG pipeline design, especially how retrieval quality, chunking strategy, and context construction affect the usefulness of AI-assisted workflows built on top of existing systems.

**Resources used:**
- OpenAI API documentation and general LLM development references  
  Helped me understand how retrieval and generation work together in practical applications.
- Hands-on experimentation  
  Built intuition for how document structure and retrieved context affect output quality.

### OAuth / OIDC Integration

Learned more about OAuth and OIDC integration, including how authentication and identity claims should be modeled in a provider-agnostic way instead of tightly coupling application logic to one login provider.

**Resources used:**
- Real project work on account identity design  
  Helped me understand the limitations of provider-specific identifiers and the benefits of more flexible identity modeling.
- Official references and ecosystem documentation  
  Provided context on how provider subject identifiers are used in modern authentication flows.

### Schema Evolution and Data Migration

Learned how to approach schema evolution and data migration more safely, especially when refactoring entities, preserving compatibility, and rolling out changes incrementally across a large codebase.

**Resources used:**
- TEAMMATES migration-related tasks  
  Provided hands-on experience with entity changes, migration scripts, and compatibility concerns.
- Practical debugging and testing work  
  Reinforced the importance of validating migration behaviour carefully before rollout.

### Build and CI Tooling

Learned more about build and CI tooling by debugging Gradle and GitHub Actions issues, and by improving automation scripts so they are easier to maintain and extend over time.

**Resources used:**
- Hands-on work with Gradle and GitHub Actions  
  Helped me understand how build tooling changes can affect developer workflows and CI stability.
- Official tool documentation  
  Used to trace version compatibility issues and update workflow implementations correctly.

### Resilient Testing and Environment-Independent Design

Learned the importance of making tests and supporting infrastructure resilient, especially around transaction cleanup, time-sensitive fixtures, and reducing environment-specific assumptions that can cause flaky failures.

**Resources used:**
- Integration test debugging  
  Showed how small cleanup and fixture issues can cascade into larger test failures.
- Work on decoupling from GAE-specific behaviour  
  Reinforced the value of making systems more portable and predictable across environments.
