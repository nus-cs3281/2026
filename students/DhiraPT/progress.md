## Summary

In this project, I contributed heavily to architectural migrations, test migrations, infrastructure improvements, and bug fixes. My key contributions include:

- **Test Migration**:
  - Migrated a massive suite of E2E and Unit tests to support the new SQL architecture instead of the previous Datastore model (e.g., [FeedbackConstSumRecipientQuestionE2ETest #13318](https://github.com/TEAMMATES/teammates/pull/13318), [SubmitFeedbackResponsesAction #13424](https://github.com/TEAMMATES/teammates/pull/13424)). 
  - Added SQL API DB unit tests and fixed Javadoc links ([#13431](https://github.com/TEAMMATES/teammates/pull/13431)) to ensure reliable test coverage during the database transition.

- **Architectural Migration & Infrastructure**:
  - Executed major backend upgrades, including completely removing Google Cloud Datastore, Objectify, and legacy storage modules to finalize the V9 clean slate ([#13608](https://github.com/TEAMMATES/teammates/pull/13608)).
  - Upgraded the project to use Java 21 for Datastore Emulator compatibility ([#13362](https://github.com/TEAMMATES/teammates/pull/13362)) and updated Liquibase schemas ([#13680](https://github.com/TEAMMATES/teammates/pull/13680)).

- **Bug Fixes**:
  - Fixed a `NullPointerException` that occurred while creating `FeedbackSessionData` ([#13335](https://github.com/TEAMMATES/teammates/pull/13335)).
  - Resolved a data truncation issue in the `FeedbackResponse` answer column by increasing its size and adding unique constraints ([#13421](https://github.com/TEAMMATES/teammates/pull/13421)). Previously, long answers could be cut off or cause errors.
  - Fixed an assertion error in `GetStudentsActionIT` by implementing proper sorting by name for students in a team ([#13419](https://github.com/TEAMMATES/teammates/pull/13419)).

- **Issue Reporting & Community Support**:
  - Proposed and outlined major infrastructure improvements, such as simplifying the task queue to two email queues ([#13643](https://github.com/TEAMMATES/teammates/issues/13643)) and implementing bearer token authentication for cron and worker endpoints ([#13644](https://github.com/TEAMMATES/teammates/issues/13644)).
  - Actively reviewed 29 pull requests across the project, assisting contributors with critical migrations like the dynamic email templates vertical slice, accessibility (Axe) tests, and various SQL page migrations.

| Week   | Achievements                                                                                                                                                                                                  |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Week 0 | Submitted Issue: [NullPointerException while creating FeedbackSessionData #13334](https://github.com/TEAMMATES/teammates/issues/13334)                                                                        |
| Week 0 | Merged PR: [[#13334] Fix NullPointerException while creating FeedbackSessionData #13335](https://github.com/TEAMMATES/teammates/pull/13335)                                                                   |
| Week 0 | Merged PR: [[#13324] Migrate to FeedbackSubmitPageSql #13336](https://github.com/TEAMMATES/teammates/pull/13336)                                                                                              |
| Week 0 | Submitted Issue: [Radio button selection syncs across Constant Sum questions #13338](https://github.com/TEAMMATES/teammates/issues/13338)                                                                     |
| Week 0 | Merged PR: [[#13324] Migrate to AdminSearchPageSql #13337](https://github.com/TEAMMATES/teammates/pull/13337)                                                                                                 |
| Week 0 | Merged PR: [[#12048] Migrate Tests for FeedbackConstSumRecipientQuestionE2ETest #13318](https://github.com/TEAMMATES/teammates/pull/13318)                                                                    |
| Week 0 | Merged PR: [[#12048] Migrate Tests for AdminAccountsPageE2ETest #13340](https://github.com/TEAMMATES/teammates/pull/13340)                                                                                    |
| Week 0 | Merged PR: [[#12048] Migrate Tests for AdminNotificationsPageE2ETest #13341](https://github.com/TEAMMATES/teammates/pull/13341)                                                                               |
| Week 0 | Merged PR: [[#12048] Migrate Tests for AdminSessionsPageE2ETest #13342](https://github.com/TEAMMATES/teammates/pull/13342)                                                                                    |
| Week 0 | Merged PR: [[#12048] Migrate Tests for AutomatedSessionRemindersE2ETest #13343](https://github.com/TEAMMATES/teammates/pull/13343)                                                                            |
| Week 0 | Merged PR: [[#12048] Migrate Tests for FeedbackConstSumOptionQuestionE2ETest #13344](https://github.com/TEAMMATES/teammates/pull/13344)                                                                       |
| Week 0 | Merged PR: [[#12048] Migrate Tests for FeedbackContributionQuestionE2ETest #13345](https://github.com/TEAMMATES/teammates/pull/13345)                                                                         |
| Week 0 | Merged PR: [[#12048] Migrate Tests for FeedbackRankRecipientQuestionE2ETest #13346](https://github.com/TEAMMATES/teammates/pull/13346)                                                                        |
| Week 0 | Merged PR: [[#13324] Migrate to InstructorCourseDetailsPageSql #13347](https://github.com/TEAMMATES/teammates/pull/13347)                                                                                     |
| Week 0 | Reviewed PR: [[#12048] Migrate tests for InstructorFeedbackSessionsPageE2ETest #13330](https://github.com/TEAMMATES/teammates/pull/13330#pullrequestreview-2952453076)                                        |
| Week 0 | Merged PR: [[#12048] Migrate Tests for InstructorCourseEditPageE2ETest #13349](https://github.com/TEAMMATES/teammates/pull/13349)                                                                             |
| Week 0 | Merged PR: [[#12048] Migrate Tests for InstructorCourseJoinConfirmationPageE2ETest #13350](https://github.com/TEAMMATES/teammates/pull/13350)                                                                 |
| Week 0 | Reviewed PR: [[#13338] Radio button selection syncs across Constant Sum questions #13352](https://github.com/TEAMMATES/teammates/pull/13352#pullrequestreview-2972407833)                                     |
| Week 0 | Submitted Issue: [Optimize GitHub Actions #13356](https://github.com/TEAMMATES/teammates/issues/13356)                                                                                                        |
| Week 0 | Submitted Issue: [Datastore Emulator requires Java 21+ #13363](https://github.com/TEAMMATES/teammates/issues/13363)                                                                                           |
| Week 0 | Merged PR: [[#13363] Upgrade to Java 21 for Datastore Emulator compatibility #13362](https://github.com/TEAMMATES/teammates/pull/13362)                                                                       |
| Week 0 | Reviewed PR: [[#13291] PostgreSQL port conflict when running dev server #13355](https://github.com/TEAMMATES/teammates/pull/13355#pullrequestreview-3048597931)                                               |
| Week 1 | Reviewed PR: [[#13324] Migrate to InstructorFeedbackResultsPageSql #13367](https://github.com/TEAMMATES/teammates/pull/13367#pullrequestreview-3588850694)                                                    |
| Week 1 | Reviewed PR: [[#13119] Admin: Unable to create an instructor account if the same email was used for a student account #13360](https://github.com/TEAMMATES/teammates/pull/13360#pullrequestreview-3592799646) |
| Week 1 | Submitted Issue: [GetStudentsActionIT test fails with assertion error #13415](https://github.com/TEAMMATES/teammates/issues/13415)                                                                            |
| Week 2 | Merged PR: [[#13415] Fix(sqllogic): Sort students by name in getStudentsForTeam #13419](https://github.com/TEAMMATES/teammates/pull/13419)                                                                    |
| Week 2 | Reviewed PR: [[#13324] Migrate InstructorCoursesPage to SQL-based version #13414](https://github.com/TEAMMATES/teammates/pull/13414#pullrequestreview-3667309556)                                             |
| Week 2 | Submitted Issue: [Data Truncation in FeedbackResponse answer Column #13420](https://github.com/TEAMMATES/teammates/issues/13420)                                                                              |
| Week 2 | Merged PR: [Refactor(db): Increase answer column size and add unique constraints #13421](https://github.com/TEAMMATES/teammates/pull/13421)                                                                   |
| Week 2 | Merged PR: [[#12048] Migrate Unit Tests for SubmitFeedbackResponsesAction](https://github.com/TEAMMATES/teammates/pull/13424)                                                                                 |
| Week 2 | Reviewed PR: [[#12048] Migrate E2E Tests for SystemErrorEmailReportE2ETest #13427](https://github.com/TEAMMATES/teammates/pull/13427#pullrequestreview-3681698548) |
| Week 3 | Merged PR: [[#12048] Add SQL API DB unit tests and fix Javadoc links #13431](https://github.com/TEAMMATES/teammates/pull/13431)                                                                                 |
| Week 3 | Reviewed PR: [[#13435] Remove unnecessary date calculation #13436](https://github.com/TEAMMATES/teammates/pull/13436#pullrequestreview-3693964313) |
| Week 3 | Reviewed PR: [[#11754] Instructor creating course: 'Institute' drop-down is empty if there are no active courses #13437](https://github.com/TEAMMATES/teammates/pull/13437#pullrequestreview-3697527371) |
| Week 3 | Reviewed PR: [[#13324] Migrate E2E Tests for InstructorSessionIndividualExtensionPage #13428](https://github.com/TEAMMATES/teammates/pull/13428#pullrequestreview-3714676596) |
| Week 3 | Reviewed PR: [[#13449] Stabilise CompileLogsActionTest #13448](https://github.com/TEAMMATES/teammates/pull/13448#pullrequestreview-3714727825) |
| Week 4 | Reviewed PR: [[#12048] Add SQL Search Unit Tests #13447](https://github.com/TEAMMATES/teammates/pull/13447#pullrequestreview-3726332984) |
| Week 4 | Reviewed PR: [[#12048] Add account manager unit tests #13451](https://github.com/TEAMMATES/teammates/pull/13451#pullrequestreview-3733131344) |
| Week 4 | Reviewed PR: [[#12725] Make Java 21 the default version #13475](https://github.com/TEAMMATES/teammates/pull/13475#pullrequestreview-3738727377) |
| Week 5 | Reviewed PR: [[#12048] Migrate axe tests #13499](https://github.com/TEAMMATES/teammates/pull/13499#pullrequestreview-3749194195) |
| Week 5 | Reviewed PR: [[#13503] Broken L&P and JDK 25 Component tests #13508](https://github.com/TEAMMATES/teammates/pull/13508#pullrequestreview-3761338498) |
| Week 6 | Reviewed PR: [[#12048] Migrate Axe Test #13501](https://github.com/TEAMMATES/teammates/pull/13501#pullrequestreview-3769027420) |
| Week 7 | Submitted Issue: [Enhance histogram of logs visualization #13582](https://github.com/TEAMMATES/teammates/issues/13582) |
| Week 7 | Reviewed PR: [[#12048] Migrate GetDeadlineExtensionActionTest #13601](https://github.com/TEAMMATES/teammates/pull/13601#pullrequestreview-3937604376) |
| Week 7 | Reviewed PR: [[#12048] Migrate FeedbackQuestionDetails test classes to SQL #13602](https://github.com/TEAMMATES/teammates/pull/13602#pullrequestreview-3941672426) |
| Week 7 | Reviewed PR: [[#13606] Fix flaky date-time spec test in session edit form component #13607](https://github.com/TEAMMATES/teammates/pull/13607#pullrequestreview-3941715653) |
| Week 7 | Reviewed PR: [[#12048] Migrate JsonUtilsTest.java #13600](https://github.com/TEAMMATES/teammates/pull/13600#pullrequestreview-3941960811) |
| Week 7 | Merged PR: [[V9-clean-slate] Remove Google Cloud Datastore, Objectify, and legacy storage modules #13608](https://github.com/TEAMMATES/teammates/pull/13608) |
| Week 7 | Reviewed PR: [[#13611] Remove lnp tests #13612](https://github.com/TEAMMATES/teammates/pull/13612#pullrequestreview-3948397268) |
| Week 7 | Reviewed PR: [[#13356] Optimize GitHub Actions #13616](https://github.com/TEAMMATES/teammates/pull/13616#pullrequestreview-3951468800) |
| Week 8 | Merged PR: [[#13675] Upgrade liquibase #13680](https://github.com/TEAMMATES/teammates/pull/13680) |
| Week 8 | Merged PR: [[#13591] Remove remaining solr references #13623](https://github.com/TEAMMATES/teammates/pull/13623#pullrequestreview-3952633049) |
| Week 8 | Reviewed PR: [[#13495] Migrate to new angular handsontable wrapper #13615](https://github.com/TEAMMATES/teammates/pull/13615#pullrequestreview-3968498849) |
| Week 8 | Reviewed PR: [[#13621] Add UserProvisionTest #13622](https://github.com/TEAMMATES/teammates/pull/13622#pullrequestreview-3970248450) |
| Week 9 | Submitted Issue: [Simplify Task Queue: consolidate to two email queues #13643](https://github.com/TEAMMATES/teammates/issues/13643) |
| Week 9 | Submitted Issue: [Implement bearer token authentication for cron and worker endpoints #13644](https://github.com/TEAMMATES/teammates/issues/13644) |
| Week 9 | Submitted Issue: [Decouple Admin/Maintainer and Error Logs from GCP #13634](https://github.com/TEAMMATES/teammates/issues/13634) |
| Week 9 | Submitted Issue: [Admin/Instructor Email Template Customization #13635](https://github.com/TEAMMATES/teammates/issues/13635) |
| Week 9 | Reviewed PR: [[#13643] Simplify task queue by consolidating to two queues #13664](https://github.com/TEAMMATES/teammates/pull/13664#pullrequestreview-4004660950) |
| Week 9 | Reviewed PR: [[#13635] Add email_templates schema and DAO #13639](https://github.com/TEAMMATES/teammates/pull/13639#pullrequestreview-4006931606) |
| Week 9 | Reviewed PR: [[#13663] Update id of FeedbackResponseComment to be UUID type #13671](https://github.com/TEAMMATES/teammates/pull/13671#pullrequestreview-4008786028) |
| Week 9 | Reviewed PR: [[#13644] Remove GAE Dependency for Cron Jobs #13658](https://github.com/TEAMMATES/teammates/pull/13658#pullrequestreview-4004751803) |
| Week 9 | Reviewed PR: [[#13635] Implement REST endpoints and logic for email templates #13672](https://github.com/TEAMMATES/teammates/pull/13672#pullrequestreview-4038569193) |
| Week 10 | Submitted Issue: [EmailGeneratorTestIT fails due to hardcoded date #13700](https://github.com/TEAMMATES/teammates/issues/13700) |
| Week 10 | Reviewed PR: [[#13634] Remove Admin/Maintainer Logs #13633](https://github.com/TEAMMATES/teammates/pull/13633#pullrequestreview-4042479283) |
| Week 10 | Reviewed PR: [[#13635] Complete dynamic email templates vertical slice (UI + generation) #13695](https://github.com/TEAMMATES/teammates/pull/13695#pullrequestreview-4042829340) |
| Week 10 | Reviewed PR: [[#13656] Preserve hyperlink in plaintext email #13676](https://github.com/TEAMMATES/teammates/pull/13676#pullrequestreview-4046569993) |
| Week 10 | Reviewed PR: [[#13700] Fix EmailGeneratorTestIT #13701](https://github.com/TEAMMATES/teammates/pull/13701#pullrequestreview-4051360858) |
| Week 10 | Reviewed PR: [[#13066] Merge result table with pending account requests table #13619](https://github.com/TEAMMATES/teammates/pull/13619#pullrequestreview-4046717270) |
| Week 11 | Reviewed PR: [[#13738] Add feedbackSessionId to all session-related links #13744](https://github.com/TEAMMATES/teammates/pull/13744#pullrequestreview-4079509774) |
| Week 11 | Reviewed PR: [[#13590] Refactor student activity logs to write directly to PostgreSQL instead of parsing logs #13692](https://github.com/TEAMMATES/teammates/pull/13692#pullrequestreview-4046075835) |
| Week 12 | Reviewed PR: [[#13640] Upgrade encryption stack #13674](https://github.com/TEAMMATES/teammates/pull/13674#pullrequestreview-4047011894) |
| Week 12 | Submitted Issue: [Improve Liquibase schema migration workflow #13714](https://github.com/TEAMMATES/teammates/issues/13714) |
| Week 13 | Reviewed PR: [[#13644] Remove GAE Dependence for Cron Jobs #13690](https://github.com/TEAMMATES/teammates/pull/13690#pullrequestreview-4038714428) |
