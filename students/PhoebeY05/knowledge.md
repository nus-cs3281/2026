## GitHub Copilot

* Effective for understanding a large codebase using #codebase, helping me to identify relevant directories and files for E2E test migrations

* Useful for generating repetitive or boilerplate files (e.g. SQL-specific E2E test JSON) when similar examples already exist

* Less effective at identifying logical errors, often fixing symptoms (modifying test data) instead of root causes (updating test logic)

* Struggles with browser-based E2E tests due to lack of awareness of actual UI state and rendered content

* May ignore constraints in prompts and go off-tangent, requiring careful supervision and iteration

* Different modes can serve different purposes: Ask/Plan for exploration, Edit/Agent for code generation

* Undo functionality is useful for restarting cleanly.

* Output quality can be inconsistent even with similar prompts, requiring manual verification (especially for strict JSON formats).

## Data Migration

* Data migration can be approached either top-down (front to back) or bottom-up (back to front), depending on the situation.
    * Example dependency chain: DeleteInstructorActionTest → InstructorLogic → Logic → InstructorsDb.

    * Top-down approach (front to back): Starts from endpoints of dependency
        * Changes are usually non-breaking initially.
        * Risk of missing dependent components if the call chain is not fully traced.

    * Bottom-up approach (back to front): Starts from database or low-level components.

        * Changes are often breaking during migration and require iterative fixes.
        * Immediately reveals all affected files and dependencies.

    * The choice of approach should be made based on the scope, risk, and complexity of the migration task.

## GCP in GitHub Actions

### Deployment Credentials
* Treating CI/CD auth as an afterthought is a real risk as deployment credentials
  have broad cloud access, never expire by default, and are hard to rotate

* Short-lived tokens (via Workload Identity Federation) eliminate an entire class
  of risk. If a token leaks, it's expired within the hour


### Authentication
* Workload Identity Federation: 
Rather than storing a credential, the pipeline proves its identity 
    * GitHub issues a signed token containing the repo, branch, and run context, which GCP
  validates against a trust policy configured once
* IAM makes least privilege concrete: grant a specific role, to a specific
  identity, on a specific resource. A compromised deploy pipeline should only be able
  to deploy

* Scoping trust by repo and branch goes further because even a fork of the same
  codebase can't trigger a deploy.

## Full-Text Search
### Search Infrastructure
* Relying on external search engines like Solr increases operational complexity, introduces additional points of failure, and can slow down deployments due to extra configuration and maintenance.

* Migrating search to PostgreSQL leverages existing infrastructure, reduces maintenance overhead, and streamlines deployment—no more managing a standalone Solr cluster.

### Query and Performance
* PostgreSQL full-text search uses functions like to_tsvector and @@ to match and rank results, enabling fast, relevant search directly within the database layer.

* Adding proper indexes (such as GIN) is essential as this significantly improves performance and ensures user experience doesn’t regress after migration.

* Direct SQL-based search lets you fine-tune result ranking and relevance with native SQL expressions, making future tweaks easier for developers.

### Security and Configuration
* With search consolidated in the database, access control and audit trails are centralized, reducing risk compared to cross-system integrations.

* Old configuration variables, secrets, and maintenance scripts for Solr can be removed for a safer, leaner environment (shrinks the project’s attack surface area).