## Lessons I Picked Up

### E2E Testing with Selenium & Page Object Model

End-to-end (E2E) testing validates the full user journey through a real browser, and the Page Object Model (POM) is the standard design pattern for keeping such tests maintainable and readable.

Learning points:

* **Page Object Pattern:** Encapsulated UI interactions (e.g., `waitForElementPresence`, button clicks, form fills) into dedicated Page Object classes, decoupling test logic from raw Selenium API calls and making tests easier to maintain.
* **Test Data Management:** Structured test data as JSON bundles that map to SQL entities, learning how to convert legacy Datastore fixtures to SQL-compatible formats for use across test suites.
* **Async Synchronization:** Handled timing-sensitive interactions such as datepicker widgets and dynamically loaded elements by using explicit waits rather than fixed sleeps, improving test reliability.
* **TestNG Configuration:** Registered E2E test suites via `testng-e2e-sql.xml` configuration files and integrated them into the Gradle build pipeline for consistent CI execution.
* **Bug Identification Through Testing:** Discovered and fixed real production bugs (e.g., inverted boolean logic in `UpdateFeedbackSessionAction`, an overwrite bug in `setLogsFromDateTime`) as a direct result of writing and running E2E tests.

Resources:

* Selenium WebDriver Documentation: [https://www.selenium.dev/documentation/](https://www.selenium.dev/documentation/)
* Page Object Model Guide: [https://martinfowler.com/bliki/PageObject.html](https://martinfowler.com/bliki/PageObject.html)

### Database Migration (Datastore to SQL)

Large-scale database migrations involve transitioning data models, persistence logic, and test infrastructure from a legacy system to a relational SQL backend without disrupting existing functionality.

Learning points:

* **Liquibase Schema Migrations:** Defined and applied incremental database schema changes (e.g., creating the `email_templates` table) using Liquibase migration scripts, ensuring version-controlled and repeatable schema evolution.
* **JPA Entity Mapping:** Adapted legacy `Attributes`-based Datastore entities to JPA-annotated SQL entities, understanding how annotations like `@Entity`, `@Id`, and `@Column` map Java classes to relational tables.
* **DAO Pattern:** Implemented Data Access Objects (e.g., `EmailTemplatesDb`) to abstract CRUD operations from business logic, keeping the persistence layer cleanly separated and testable.
* **Surrogate Keys & UUIDs:** Migrated from natural string-based keys (courseId, session name) to database-generated surrogate keys (UUIDs), and learned how to additively plumb new key parameters through the system during transition.
* **Dual-System Testing:** Ran tests against both legacy and SQL backends simultaneously during the migration period, verifying behavioural equivalence and catching divergence early before full cutover.

Resources:

* Liquibase Documentation: [https://docs.liquibase.com/](https://docs.liquibase.com/)
* Jakarta Persistence (JPA) Guide: [https://jakarta.ee/specifications/persistence/](https://jakarta.ee/specifications/persistence/)

### Gradle Build System

Gradle is a flexible build automation tool used in Java projects for compiling, testing, and packaging code, with support for custom task definitions to extend the build pipeline.

Learning points:

* **Custom Task Definition:** Created new Gradle tasks (e.g., `axeSqlTests`) to run specific test suites, learning how to configure source sets, dependencies, and task lifecycle hooks within `build.gradle`.
* **TestNG Suite Integration:** Wired TestNG XML suite files (e.g., `testng-axe-sql.xml`) into Gradle tasks, enabling targeted execution of accessibility, E2E, and unit test groups independently from the main test run.
* **Build Verification:** Used `./gradlew compileTestJava` as a fast pre-push check to catch compilation errors early without running the full test suite, improving iteration speed during development.

Resources:

* Gradle User Manual: [https://docs.gradle.org/current/userguide/userguide.html](https://docs.gradle.org/current/userguide/userguide.html)
* TestNG Documentation: [https://testng.org/doc/documentation-main.html](https://testng.org/doc/documentation-main.html)

## Tools I Picked Up

### Gemini Code Assist

Gemini Code Assist is an AI-powered collaborator integrated directly into the IDE to help developers write, understand, and troubleshoot code.

Learning points:

* **Codebase Navigation:** Used the assistant to track execution flow and trace logic across multiple files, which is invaluable for understanding how legacy systems and new implementations interact in a large codebase.
* **Linting and Formatting:** Leveraged the tool to pre-check code against strict project style guides, quickly catching and resolving checkstyle and linting errors before pushing commits.
* **Context-Aware Debugging:** Learned to feed specific error logs and file context into the prompt to rapidly diagnose complex issues, such as database connection failures or syntax errors.

Resources:

* Gemini for Google Cloud Documentation: [https://cloud.google.com/gemini/docs](https://cloud.google.com/gemini/docs)
* Prompt Engineering guidelines for AI coding assistants

### Multi-Agent AI Collaboration

Throughout this module, I expanded my workflow to include multiple AI coding assistants, utilizing each agent's specific strengths to optimize the development and review process.

Learning points:

* **Agent Specialization:** Discovered how to effectively route tasks based on AI capabilities. I used **Gemini LLM** primarily for high-level architectural planning, logic structuring, and generating concise summaries of complex tasks, while relying on **Claude Code** for tasks requiring "deep thinking," intensive coding, and complex refactoring.
* **Meaningful Code Reviews:** Learned to leverage **GitHub Copilot** to conduct insightful and useful code reviews. By feeding the assistant specific pull request context, I could systematically identify edge cases, spot potential logic gaps, and suggest meaningful improvements to peer contributions.

Resources:

* GitHub Copilot Documentation: [https://docs.github.com/en/copilot](https://docs.github.com/en/copilot)
* Claude Code Documentation: [https://docs.anthropic.com/en/docs/agents-and-tools/claude-code](https://www.google.com/search?q=https://docs.anthropic.com/en/docs/agents-and-tools/claude-code)
