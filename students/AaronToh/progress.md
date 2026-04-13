# Week 1

- Explored the code base and understood the rationale for migrating from datastore to SQL. 

# Week 2

- Performed migration of E2E test in [#13427](https://github.com/TEAMMATES/teammates/pull/13427/changes)
- Also fixed a flaky action test in [#13448](https://github.com/TEAMMATES/teammates/pull/13448)

# Week 3

- Replaced old datastore logic with sqllogic in UI component of TEAMMATES. Specfically, I removed any reference to the old feedbackDB in [#13483](https://github.com/TEAMMATES/teammates/pull/13483)
- In doing so, I had to better understand the design of the website as a whole. Specifically, I had to understand that the db interacted with the db through an intermediary logic layer and that any db migration required a refactoring of the logic layer as well. 

# Week 4

- Investigated for bugs in the V9 clean slate branch. Found a critical bug when deleting feedback responses and fixed the bug in [#13518](https://github.com/TEAMMATES/teammates/pull/13518)

# Week 5

- Investigated bugs in the V9 clean slate branch. Found a critical bug when filtering for participants comments and fixed the bug in [#13531](https://github.com/TEAMMATES/teammates/pull/13531)
- Continued work on migration - added unit tests for AccountRequestSearchDocument and AccountRequestSearchManager in [#13451](https://github.com/TEAMMATES/teammates/pull/13451/changes)

# Week 6

- Generated a list of user flows for UAT of V9-clean-slate-sql branch using claude opus 4.6. The list of user flows turned out to be comprehensive and fairly accurate. Divided the list among teammates devs
- Deployed an instance of V9-clean-slate-sql. Learnt to follow teammate-ops documentation and understood how GAE, CloudSQl, VPC, OAuth interact to deploy a fully functioning website [link](https://teammates-staging-489513.as.r.appspot.com/web/front/home)

# Week 7
- Tackled an issue raced by Florian [#13543](https://github.com/TEAMMATES/teammates/issues/13543). Followed suggestions by Samuel at fixed the bug at [#13543](https://github.com/TEAMMATES/teammates/pull/13598)

# Week 8
- Improved the workflow for admin users by allowing approval of account requests and fixed other bugs. Details may be found in the PR [#13629](https://github.com/TEAMMATES/teammates/pull/13629)

# Week 9
- Simplified task queueing logic [#13664](https://github.com/TEAMMATES/teammates/pull/13664)

# Week 10
- Removed intermediate results table on admin page. Some discussion with prof and other maintainers to determine what would be best for user experience [#130619](https://github.com/TEAMMATES/teammates/pull/13619)

# Week 11
- Upgraded encryption and hashing stack used [#13674](https://github.com/TEAMMATES/teammates/pull/13674)

# Week 12
- Improved on schema migration workflow [#13748](https://github.com/TEAMMATES/teammates/pull/13748)

# Week 13
- Completed and merged incomplete PRs.
