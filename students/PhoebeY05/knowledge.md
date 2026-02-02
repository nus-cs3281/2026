### GitHub Copilot

* Effective for understanding a large codebase using #codebase, helping me to identify relevant directories and files for E2E test migrations

* Useful for generating repetitive or boilerplate files (e.g. SQL-specific E2E test JSON) when similar examples already exist

* Less effective at identifying logical errors, often fixing symptoms (modifying test data) instead of root causes (updating test logic)

* Struggles with browser-based E2E tests due to lack of awareness of actual UI state and rendered content

* May ignore constraints in prompts and go off-tangent, requiring careful supervision and iteration

* Different modes can serve different purposes: Ask/Plan for exploration, Edit/Agent for code generation

* Undo functionality is useful for restarting cleanly.

* Output quality can be inconsistent even with similar prompts, requiring manual verification (especially for strict JSON formats).

### Data Migration

* Data migration can be approached either top-down (front to back) or bottom-up (back to front), depending on the situation.
    * Example dependency chain: DeleteInstructorActionTest → InstructorLogic → Logic → InstructorsDb.

    * Top-down approach (front to back): Starts from endpoints of dependency
        * Changes are usually non-breaking initially.
        * Risk of missing dependent components if the call chain is not fully traced.

    * Bottom-up approach (back to front): Starts from database or low-level components.

        * Changes are often breaking during migration and require iterative fixes.
        * Immediately reveals all affected files and dependencies.

    * The choice of approach should be made based on the scope, risk, and complexity of the migration task.