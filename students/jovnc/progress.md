# Git-Mastery

## Overview

- **App Infrastructure & CI/CD**: Built and optimized the E2E testing infrastructure for the app ([#54](https://github.com/git-mastery/app/pull/54), [#57](https://github.com/git-mastery/app/pull/57), [#58](https://github.com/git-mastery/app/pull/58)); split and improved CI workflows ([#59](https://github.com/git-mastery/app/pull/59)); migrated app and exercises to `uv` package manager ([#83](https://github.com/git-mastery/app/pull/83), [#279](https://github.com/git-mastery/exercises/pull/279))
- **Windows Distribution**: Authored RFC and implemented winget publishing support for Windows users ([#61](https://github.com/git-mastery/app/pull/61), [#80](https://github.com/git-mastery/app/pull/80))
- **Pre-commit Tooling**: Proposed and implemented Git hooks via LeftHook across the exercises and app repositories ([#265](https://github.com/git-mastery/exercises/pull/265), [#76](https://github.com/git-mastery/app/pull/76))
- **Exercise Development**: Implemented and improved verify logic for multiple exercises (mix-messy-graph, mix-messy-docs, remote-branch-rename, branch-forward)
- **Developer Documentation**: Restructured developer documentation ([#6](https://github.com/git-mastery/developers/pull/6)), wrote onboarding docs, and added `AGENTS.md`
- **Bug Fixes**: Fixed critical bugs including progress sync failures, help command truncation, Arch Linux release URL, and OneDrive FileNotFound incident
- And more! See the weekly log below for a comprehensive list of contributions.

---

## Weekly Log

### Week 0

- Implemented PRs:
  - Fix exercise undo-init ([#27](https://github.com/git-mastery/app/pull/27))
  - Add FAQ section ([#12](https://github.com/git-mastery/progress-dashboard/pull/12))
  - Fix contribution message workflow permission issue on PR from fork ([#224](https://github.com/git-mastery/exercises/pull/224))
  - [mix-messy-graph] Add checkout and validate file content in verify logic ([#202](https://github.com/git-mastery/exercises/pull/202))
  - Implement tweak dashboard top ([#11](https://github.com/git-mastery/progress-dashboard/pull/11))
  - Skip repo_smith when exercise doesn't require git init ([#31](https://github.com/git-mastery/app/pull/31))
  - Fix inconsistent commit ordering for git log ([#213](https://github.com/git-mastery/exercises/pull/213))
  - [tooling] Use PYTHONPATH in test download script ([#223](https://github.com/git-mastery/exercises/pull/223))
  - Fix arch publish release AMD64 URL ([#36](https://github.com/git-mastery/app/pull/36))
  - Fix help command output incomplete ([#35](https://github.com/git-mastery/app/pull/35))
  - [branch-forward] Fix verify does not consider initial commit ([#218](https://github.com/git-mastery/exercises/pull/218))
  - Support go to dashboard when enter key pressed ([#10](https://github.com/git-mastery/progress-dashboard/pull/10))
  - Update base URL ([#13](https://github.com/git-mastery/progress-dashboard/pull/13))
  - Update page icon ([#15](https://github.com/git-mastery/progress-dashboard/pull/15))
  - Fix dashboard table is not using the full page width ([#16](https://github.com/git-mastery/progress-dashboard/pull/16))
- Test Drive Tour 6 ([#209](https://github.com/git-mastery/exercises/issues/209))
- Documentation:
  - [Onboarding Documentations](https://docs.google.com/document/d/1Exhw-FgQHSNw4E0X0iMFz5iqe2DqMTAT4bOeHAaPvek/edit?tab=t.0#heading=h.pckfygp0q8)

### Week 1

- Reviewed PRs: [#229](https://github.com/git-mastery/exercises/pull/229), [#236](https://github.com/git-mastery/exercises/pull/236), [#231](https://github.com/git-mastery/exercises/pull/231), [#232](https://github.com/git-mastery/exercises/pull/232), [#230](https://github.com/git-mastery/exercises/pull/230)
- Implemented PRs:
  - Remove cron job to update progress tracker ([#211](https://github.com/git-mastery/progress/pull/211))
  - Remove extra comma in contribution message ([#241](https://github.com/git-mastery/exercises/pull/241))
  - Fix issue with progress directory not found in progress sync ([#37](https://github.com/git-mastery/app/pull/37))
- Monitoring and address git-mastery issues by students

## Week 2

- Reviewed PRs: [#246](https://github.com/git-mastery/exercises/pull/246)
- Implemented PRs:
  - Modify progress reset to redownload base files ([#38](https://github.com/git-mastery/app/pull/38))
  - Adopt shadcn as core component library ([#17](https://github.com/git-mastery/progress-dashboard/pull/17))
  - Add minimum git version requirement check ([#39](https://github.com/git-mastery/app/pull/39))
  - Fix refetch behaviour of react query hooks ([#19](https://github.com/git-mastery/progress-dashboard/pull/19))
- Incident Reviews:
  - [I-1: OneDrive FileNotFound Error](https://docs.google.com/document/d/1UcKhHGxTwcA_XI6B6uzX3_HCJA2Qu4l_6c8GrTbmddw/edit?usp=drive_link)
- Reviewed RFC:
  - [Creating remote repositories in repo-smith](https://docs.google.com/document/d/1fZOgaR6G6SdbU20g16Q2DcgCuDfYsOZeYDGydbHMYa8/edit?tab=t.0#heading=h.x8t43doyrgeb)

### Week 3

- Reviewed PRs: [#249](https://github.com/git-mastery/exercises/pull/249),[#250](https://github.com/git-mastery/exercises/pull/250), [#251](https://github.com/git-mastery/exercises/pull/251), [#42](https://github.com/git-mastery/app/pull/42)
- Implemented PRs:
  - Remove workflow_run and add inherit secrets in publish workflow ([#22](https://github.com/git-mastery/repo-smith/pull/22))
  - Change bump version to pull_request_target trigger ([#41](https://github.com/git-mastery/app/pull/41))
  - Add AGENTS.md ([#20](https://github.com/git-mastery/git-autograder/pull/20))
  - Improve verify logic of T6L5/mix-messy-docs ([#255](https://github.com/git-mastery/exercises/pull/255))

### Week 4

- Reviewed PRs: [#243](https://github.com/git-mastery/exercises/pull/243), [#63](https://github.com/git-mastery/git-mastery/pull/63), [#257](https://github.com/git-mastery/exercises/pull/253), [#257](https://github.com/git-mastery/exercises/pull/257), [#44](https://github.com/git-mastery/app/pull/44), [#259](https://github.com/git-mastery/exercises/pull/259), [#264](https://github.com/git-mastery/exercises/pull/264)
- Implemeted PRs:
  - E2E App Testing Strategy Examples [#43](https://github.com/git-mastery/app/pull/43)
  - Implement hands-on T8L4/hp-remote-branch-rename [#258](https://github.com/git-mastery/exercises/pull/258)
  - Improve verify logic and update tests remote-branch-rename ([#260](https://github.com/git-mastery/exercises/pull/260))
- Issues created:
  - Unable to force delete local branch[#23](https://github.com/git-mastery/exercises/pull/253)
- RFCs created:
  - [E2E App Testing Strategy](https://docs.google.com/document/d/101Qh5SiW-MZGy3DH0lLvn2lqRutxkTKbx01A8dNyI6o/edit?tab=t.0)

### Week 5

- Implemented PRs:
  - Rename AGENTS.md file ([#51](https://github.com/git-mastery/app/pull/51))
  - Update starting branch for Tour 8 exercises ([#264](https://github.com/git-mastery/exercises/pull/264))
- RFCs created:
  - [Implementing Git hooks for linting and formatting RFC](https://docs.google.com/document/d/1LU8oDc19Lm_51v_g7iodC6a6Ze44k6lG5-gQ55AttBg/edit?tab=t.0#heading=h.x8t43doyrgeb)
  - [Publishing application to winget for Windows RFC](https://docs.google.com/document/d/1B81pyVML--aNEurCSobfrS61y_R0jL8rPmKwvkaHrDg/edit?tab=t.0#heading=h.x8t43doyrgeb)
  - Continue work on [E2E App Testing Strategy](https://docs.google.com/document/d/101Qh5SiW-MZGy3DH0lLvn2lqRutxkTKbx01A8dNyI6o/edit?tab=t.0)

### Week 6

- Implemented PRs:
  - [tooling] Add pre-commit hooks using LeftHook ([#265](https://github.com/git-mastery/exercises/pull/265))
  - Set up base infrastructure for app E2E tests ([#54](https://github.com/git-mastery/app/pull/54))

### Week 7

- Implemented PRs:
  - Add optimisations to E2E CI workflow ([#57](https://github.com/git-mastery/app/pull/57))
  - Make E2E tests more comprehensive and less flaky ([#58](https://github.com/git-mastery/app/pull/58))
- Lightning Talk: [Git Hooks Lightning Round Sharing](https://drive.google.com/file/d/1cMXc94juKlcMsiSyw3UJhH0O083Lf1WB/view?usp=sharing)
- Documentation:
  - Update developer documentation for precommit installation ([#4](https://github.com/git-mastery/developers/pull/4))

### Week 8

- Reviewed PRs: [#40](https://github.com/git-mastery/app/pull/40)
- Implemented PRs:
  - Split test workflow into PR and main branch push ([#59](https://github.com/git-mastery/app/pull/59))
  - Add winget-publish action in publish.yml ([#61](https://github.com/git-mastery/app/pull/61))
  - Update bump-version.yml to exit with status code 0 if no tag present ([#4](https://github.com/git-mastery/actions/pull/4))

### Week 9

- Perform release of Git-Mastery App v7.8.0
- Reviewed PRs: [#84](https://github.com/git-mastery/app/pull/84)
- Implemented PRs:
  - Cache pip dependencies using requirements.txt as cache key ([#69](https://github.com/git-mastery/app/pull/69))
  - Set up lefthook for app repository ([#76](https://github.com/git-mastery/app/pull/76))
  - Fix winget releaser action ([#80](https://github.com/git-mastery/app/pull/80))

### Week 10

- Reviewed PRs: [#90](https://github.com/git-mastery/app/pull/90),[#91](https://github.com/git-mastery/app/pull/91), [#93](https://github.com/git-mastery/app/pull/93), [#86](https://github.com/git-mastery/app/pull/86), [#87](https://github.com/git-mastery/app/pull/87), [#88](https://github.com/git-mastery/app/pull/88), [#89](https://github.com/git-mastery/app/pull/89), [#82](https://github.com/git-mastery/app/pull/82)
- Implemented PRs:
  - Migrate app to uv and set up dependabot ([#83](https://github.com/git-mastery/app/pull/83))
  - Update set up scripts in exercises repository ([#277](https://github.com/git-mastery/exercises/pull/277))

### Week 11

- Reviewed PRs: [#25](https://github.com/git-mastery/repo-smith/pull/25), [#24](https://github.com/git-mastery/git-autograder/pull/24), [#280](https://github.com/git-mastery/exercises/pull/280), [#281](https://github.com/git-mastery/exercises/pull/281)
- Implemented PRs:
  - Migrate exercises to uv ([#279](https://github.com/git-mastery/exercises/pull/279))
  - Update exercises contirbuting.md and README.md ([#283](https://github.com/git-mastery/exercises/pull/283))
  - Restructure and update developer documentation ([#6](https://github.com/git-mastery/developers/pull/6))
  - Update publish pypi library to use uv ([#6](https://github.com/git-mastery/actions/pull/6))

## Misc

- [Vibe Coding an App](https://docs.google.com/document/d/1lkt77dtJwEmgs9pRUB1wTd2rj8HiE-I5RNihyPNzDCc/edit?tab=t.0#heading=h.56d739jgyert)
- [Test Drive adding AI to iP](https://github.com/se-edu/guides/issues/190)
- [CSV Text Classifier](https://drive.google.com/drive/u/3/folders/14MJf8G1SOAYBnTzU7Z575gZ0tPuHiEGI)
