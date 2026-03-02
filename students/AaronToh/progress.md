# Week 1

- Explored the code base and understood the rationale for migrating from datastore to SQL. 

# Week 2

- Performed migration of E2E test in [#13427](https://github.com/TEAMMATES/teammates/pull/13427/changes)
- Also fixed a flaky action test in [#13448](https://github.com/TEAMMATES/teammates/pull/13448)

# Week 3

- Replaced old datastore logic with sqllogic in UI component of TEAMMATES. Specfically, I removed any reference to the old feedbackDB in [#13483](https://github.com/TEAMMATES/teammates/pull/13483)

# Week 4

- Investigated for bugs in the V9 clean slate branch. Found a critical bug when deleting feedback responses and fixed the bug in [#13518](https://github.com/TEAMMATES/teammates/pull/13518)

# Week 5

- Investigated bugs in the V9 clean slate branch. Found a critical bug when filtering for participants comments and fixed the bug in [#13531](https://github.com/TEAMMATES/teammates/pull/13531)