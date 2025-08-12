Project Understanding
A single-school web app that lets teachers file behavior incidents in 10–15 seconds, sends students to a supervised kiosk to complete a 4-question reflection (no student logins), and routes the reflection back to the teacher for near-instant review and closure. Must run reliably on campus, with kiosk-only student access, and the Clear Queue bug fixed before pilot.

Unknown Territory Map
Technical Unknowns
• Multi-kiosk queue integrity (locking, concurrency, device identity). Critical → Cheapest test: simulate with two kiosk tabs + mock device token; run 50 incident/reflection pairs.
• RLS/permissions for teacher vs. kiosk (write/read scopes, audit trails). Critical → Create minimal schema + RLS, attempt end-to-end flow with two roles.
• Offline/poor Wi-Fi behavior at kiosks (graceful retries, duplicate prevention). Important → Force network throttling, verify idempotent writes via request fingerprint.
• Real-time refresh for teacher review screen (listen/subscribe vs. polling). Important → Add a lightweight subscription/polling and compare latency vs. complexity.
• PII/FERPA-safe logging & exports (redaction, access logs). Important → Define fields + redaction policy; export a sample CSV and review.

User Assumptions
• Teachers can file in 10–15s during class. Evidence: none. Validate: stopwatch test with 3 teachers on a clickable prototype.
• Students complete the 4-Q reflection in ≤ 2 minutes under supervision. Evidence: anecdotal. Validate: 5 students, proctored dry run.
• Kiosk stations are reliably available and monitored. Evidence: assumption. Validate: map locations + brief staff survey.
• Same-day teacher approval is feasible. Evidence: assumption. Validate: pilot with daily reminder + measure closure time.
• Simple categories are sufficient for insights. Evidence: assumption. Validate: 2-week pilot, review ‘other/uncategorized’ rate.

Business Questions
• Will staff adopt this in real classrooms? Impact: without adoption, no value. Validate: pilot usage ≥ 70% of incidents captured for two weeks.
• Does it reduce repeat incidents? Impact: core outcome. Validate: track per-student repeat rate vs. prior 2 weeks (baseline).
• Is the workload net-positive? Impact: churn risk. Validate: teacher time saved vs. added steps via time-and-motion study.

Phase 1: Core Loop MVP (Single Kiosk)
• Goal: Prove the fastest viable Report → Reflection → Review → Close loop.
• Deliverable: Working flow with role-scoped RLS, one kiosk, event timing, and the Clear Queue bug fixed.
• Success criteria:
  ◦ Teacher report median ≤ 15s
  ◦ Reflection completion ≥ 90%
  ◦ Same-day approvals ≥ 80%
  ◦ No orphaned/duplicate queue entries
• Main risk: Queue corruption / role leakage.
• Go/No-go: All four criteria met in a 1-week hallway pilot.

Phase 2: Multi-Kiosk & Edge-Case Resilience
• Goal: Handle concurrency, device identity, and flaky network without breaking data integrity.
• Deliverable: Device tokening, idempotent submissions, retry/backoff, queue locks, and conflict resolution.
• Success criteria:
  ◦ 0 data dupes across 100 test runs
  ◦ ≤ 3s teacher screen update latency
  ◦ Recovery from network drop without staff intervention
• Main risk: Complexity causing regressions.
• Go/No-go: Pass automated concurrency suite + manual chaos tests.

Phase 3: Admin Insights & Compliance
• Goal: Turn captured data into useful, compliant insights.
• Deliverable: Basic dashboards (by category/time/student), CSV export with redaction, audit logs.
• Success criteria:
  ◦ Admin can answer 3 top questions without spreadsheets
  ◦ Exports pass a FERPA/PII checklist review
  ◦ <10% incidents labeled ‘other’
• Main risk: Insight quality limited by taxonomy.
• Go/No-go: Admin sign-off on insights + redaction policy.

Phase 4 (Optional): Schoolwide Pilot & Training
• Goal: Validate at scale with real classrooms.
• Deliverable: Teacher quick-start, kiosk setup guide, incident triage SOPs.
• Success criteria:
  ◦ ≥ 70% incident capture rate
  ◦ Staff satisfaction ≥ 4/5
  ◦ Repeat incidents down vs. baseline
• Main risk: Training gaps.
• Go/No-go: Meets targets over 2–4 weeks.

De-risking Strategy
Riskiest Assumption: Teachers can consistently file a report in ≤ 15 seconds during live instruction.
48-Hour Test Plan
1. Experiment: Build a no-code click-through (or thin web stub) for the teacher report + student reflection; run timed trials with 3 teachers and 5 students. Capture friction points.
2. Resources: 1 prototype, stopwatch logging, 30–45 minutes per participant, one proctor.
3. Success/Fail: Median teacher time ≤ 15s; reflection completion ≥ 90% under supervision. If not, identify top 3 slow steps.
4. Pivot Options: Reduce fields, add defaults/autofill, restructure UI (single screen), or defer taxonomy depth to post-submit edit.

Decision Framework
Kill Criteria (any 3):
• Median teacher report time >20s after 3 design iterations.
• Reflection completion <70% in supervised settings.
• Persistent queue corruption or PII risk not fixable without logins.

Pivot Triggers:
• Kiosk-only constraint blocks integrity → consider lightweight student codes/PINs.
• Real-time review proves unnecessary → swap to batched notifications.
• Insights unusable with current taxonomy → introduce 1-level deeper categories.

Success Indicators (early):
• Teacher report median trending to 12–15s within a week.
• Same-day closures ≥ 80% by week 2.
• Staff NPS ≥ +30 on first survey.

Recommended First Actions
• Run the 48-hour timing test with a clickable teacher+student flow and capture exact step timings.
• Isolate and fix the Clear Queue bug in a sandbox branch with a reproducible multi-tab test harness.
• Lock down minimal schema + RLS (teacher vs. kiosk) and wire basic event timing to prove the secure core loop.
