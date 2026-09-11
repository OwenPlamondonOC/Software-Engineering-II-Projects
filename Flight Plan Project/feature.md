# Flight Plan — System Features

## Epic

**As a student**, when I want to do some activities to prepare me to get a job when I graduate, **I want** a checklist of tasks and events that I can do each semester I am in school **so that** I am prepared to successfully apply for a job.

## Product decisions

These rules come from the scoping answers and apply across all features.

| Topic | Decision |
| --- | --- |
| Roles | Three separate roles: **student**, **advisor**, and **administrator**. |
| Completion | **Mix:** most items are self-check; selected high-stakes items need **advisor confirmation**. |
| Plan assignment | Plan is chosen from the student’s **major**, with a **college-level fallback** if that major has no template. Advisors do not assign plans. |
| Semesters | **Fixed 8-term map only:** Freshman Fall through Senior Spring. No summers. No custom transfer calendars. Student sets current class standing. All eight terms stay visible. |
| Events | **Dated offerings.** An administrator enters date, time, and location (or link). Not generic “sometime this semester” activities. |

### Roles

| Role | Primary job |
| --- | --- |
| **Student** | Follow the 8-term checklist for their major, track completion, and see whether they are ready to apply for jobs. |
| **Advisor** | View assigned students’ progress, confirm or send back high-stakes items, and follow up with students who are behind. |
| **Administrator** | Create templates, map them to majors or colleges, enter and update dated events, mark required vs optional and self-check vs confirmation, and link advisors to students. |

Students cannot perform advisor or admin actions. Advisors cannot publish or edit school-wide templates unless they also have an admin account.

### Completion statuses

| Status | Meaning |
| --- | --- |
| Incomplete | Not done. |
| Pending advisor review | Student submitted a high-stakes item; it does not count as complete yet. |
| Complete | Self-check marked done, or a high-stakes item **confirmed by an advisor**. |
| Sent back | Advisor rejected a high-stakes item; the student must fix and resubmit. |

Pending and sent-back items do **not** count toward semester progress or “ready to apply.”

### Plan assignment

Administrators publish templates and map each major—or a college fallback—to a plan. The student does not pick a template. If the student changes major, they receive the new major’s plan. Overlapping completions are kept.

### Semester model

Terms are exactly:

1. Freshman Fall  
2. Freshman Spring  
3. Sophomore Fall  
4. Sophomore Spring  
5. Junior Fall  
6. Junior Spring  
7. Senior Fall  
8. Senior Spring  

The student selects which of these is current (for example Sophomore Fall). The matching term is highlighted. Students can still open other terms to work ahead or catch up.

### Events vs tasks

- **Task:** undated (or suggested timing only); description and optional resource links.  
- **Event:** always has date, time, and location or virtual link, entered by an administrator and placed on a term of a major/college template. Students see events that are on **their** plan, not a separate school-wide calendar. Administrators update dates when a new year’s offering is announced.

---

## Feature 1: Student account and academic profile

Students need an identity, major, and class standing on the 8-term map so the system can load the right plan and highlight the current semester.

### User stories

- **US-1.1** As a student, I want to create an account with my school email so that my flight plan is saved and available only to me.
- **US-1.2** As a student, I want to sign in and sign out securely so that I can return to my checklist across sessions.
- **US-1.3** As a student, I want to enter my major and current class standing (one of the eight terms, for example Sophomore Fall) so that the system can load my major’s plan and highlight this semester.
- **US-1.4** As a student, I want to update my major if I change programs so that I am switched to that major’s flight plan.
- **US-1.5** As a student, I want to update my class standing when a new fall or spring term starts so that the highlighted semester stays correct.
- **US-1.6** As a student, I want to recover access to my account if I forget my password so that I do not lose my progress.
- **US-1.7** As an advisor or administrator, I want to sign in with a role-specific account so that I see admin or caseload tools instead of a student checklist.

---

## Feature 2: Semester-based flight plan checklist

A checklist of career-prep tasks and dated events, grouped into the eight standard terms, using the template mapped to the student’s major (or college fallback).

### User stories

- **US-2.1** As a student, I want to see the flight plan for my major grouped into the eight standard terms (Freshman Fall through Senior Spring) so that I know what to work on now versus later.
- **US-2.2** As a student, I want each of those eight semesters to list that term’s tasks and dated events so that I have concrete activities that prepare me for a job.
- **US-2.3** As a student, I want the semester that matches my class standing highlighted so that I can focus on what I should do this term.
- **US-2.4** As a student, I want to expand or collapse past and future semesters so that I can review what I have already done and what is coming next.
- **US-2.5** As a student, I want tasks to show a description and events to show date, time, and location (or link) so that I know what to do and when to show up.
- **US-2.6** As a student, I want all eight terms of my plan visible even if I am a senior so that I can catch up on items I skipped earlier.
- **US-2.7** As a student, I want required items and optional items labeled so that I know what is essential versus recommended.

---

## Feature 3: Task and event completion tracking

Students check off ordinary items themselves. High-stakes items stay pending until an advisor confirms them.

### User stories

- **US-3.1** As a student, I want to mark a self-check task or event as complete so that I can keep a running record of what I have already done.
- **US-3.2** As a student, I want to unmark a self-check item if I marked it complete by mistake so that my checklist stays accurate.
- **US-3.3** As a student, I want items that need confirmation to show as “pending advisor review” after I submit them so that I know the box is not fully done yet.
- **US-3.4** As a student, I want incomplete, pending, complete, and sent-back items to look visually distinct so that I can scan my progress quickly.
- **US-3.5** As a student, I want to see how many items I have completed versus remaining for my current standing, counting only fully complete items, so that I know if I am on track this term.
- **US-3.6** As a student, I want to see why a high-stakes item was sent back so that I know what to fix.
- **US-3.7** As a student, I want my completion and pending status to persist after I log out so that I do not have to re-submit items every visit.

---

## Feature 4: Career-readiness progress overview

A summary view of whether the student is prepared to apply for jobs, using only fully complete required items.

### User stories

- **US-4.1** As a student, I want an overall progress indicator for my entire 8-term flight plan so that I can see how prepared I am as I approach Senior Spring.
- **US-4.2** As a student, I want to see which categories I still need (for example resume, internship, networking, interview practice) so that I can close gaps before I apply.
- **US-4.3** As a student, I want a simple “ready to apply” or “needs more prep” summary based on required items that are fully complete (self-check done; high-stakes items advisor-confirmed) so that I know if I am prepared to successfully apply for a job.
- **US-4.4** As a student, I want to see incomplete required items from terms before my current standing, plus dated events whose date has passed, so that I can catch up.

---

## Feature 5: Filtering and search

Students can narrow the checklist they already have. Personalization of *which* plan they get is handled by major mapping (Feature 8), not by this feature.

### User stories

- **US-5.1** As a student, I want to see which major or college plan I am on so that I understand why my checklist looks the way it does.
- **US-5.2** As a student, I want to filter my list by type (tasks vs. events) so that I can separately plan work items and dated offerings.
- **US-5.3** As a student, I want to filter by status (incomplete, pending advisor review, complete, sent back) so that I can focus on unfinished items.
- **US-5.4** As a student, I want to search tasks and events by keyword so that I can find a specific activity (for example “career fair” or “resume”).

---

## Feature 6: Dated events

Events are specific offerings with a schedule entered by an administrator and placed on a term of a template. Students only see events on their major (or college fallback) plan.

### User stories

- **US-6.1** As a student, I want to view an event’s description and why it helps job prep so that I can decide whether to attend.
- **US-6.2** As a student, I want to see each event’s date, time, and location (or link) so that I can put it on my calendar and show up.
- **US-6.3** As a student, I want a list of upcoming dated events from my flight plan (soonest first) so that I do not miss time-sensitive offerings.
- **US-6.4** As a student, I want past events I have not completed to stay visible as missed so that I know I still need to catch up or wait for a new date from an administrator.
- **US-6.5** As a student, I want to mark that I attended a self-check event so that my checklist reflects participation.
- **US-6.6** As an administrator, I want to create an event with name, description, date, time, and location or link, and place it on a term of a template, so that only students on that plan see it.
- **US-6.7** As an administrator, I want to update an event’s date, time, and location (or replace it with this year’s offering) so that students are not sent to last year’s schedule.

---

## Feature 7: Task guidance and resources

Checklist tasks should be actionable, with enough help that a student can complete them and, when needed, submit evidence for advisor review.

### User stories

- **US-7.1** As a student, I want each task to include a short “how to get started” description so that I am not left guessing what “update resume” means.
- **US-7.2** As a student, I want links to campus resources (career center, resume templates, mock interview sign-up) so that I can complete tasks using official support.
- **US-7.3** As a student, I want to add optional notes to a task (for example where I saved my resume) so that I can remember my own next steps.
- **US-7.4** As a student, I want to attach or record a related artifact (resume file, LinkedIn URL) when a high-stakes task requires it so that my advisor can review evidence before confirming.

---

## Feature 8: Flight plan templates (administrator)

Administrators own templates, major/college mapping, required vs optional flags, and which items need confirmation. Students receive a plan automatically from their profile.

### User stories

- **US-8.1** As an administrator, I want to create a flight plan template with tasks and events in each of the eight terms (Freshman Fall through Senior Spring) so that I can publish a plan per major or college.
- **US-8.2** As an administrator, I want to map each major to a template so that students in that major automatically receive the matching checklist.
- **US-8.3** As an administrator, I want to set a college-level fallback template for majors that do not have their own plan so that every student still gets a checklist.
- **US-8.4** As an administrator, I want to mark items as required or optional so that students and advisors know what must be completed before applying for jobs.
- **US-8.5** As an administrator, I want to mark selected items as requiring advisor confirmation so that high-stakes activities (resume review, mock interview) are not treated as done on an honor system.
- **US-8.6** As an administrator, I want to add, edit, or retire tasks over time so that the checklist stays current.
- **US-8.7** As an administrator, I want to assign advisor accounts and link advisors to students so that advisors only see the students they support.
- **US-8.8** As a student, I want my completions kept when I change majors or when an administrator updates a template, with new items appearing clearly, so that overlapping work is not lost.

---

## Feature 9: Advisor visibility and confirmation

Advisors coach students and confirm high-stakes items. They do not publish templates; they work with plans administrators already defined.

### User stories

- **US-9.1** As an advisor, I want to sign in with an advisor account so that I see my caseload instead of a personal student checklist.
- **US-9.2** As an advisor, I want to view an assigned student’s 8-term flight plan and status (incomplete, pending, complete, sent back) so that I can coach them on remaining job-prep gaps.
- **US-9.3** As an advisor, I want a queue of pending high-stakes items so that I can confirm or send back work that students submitted.
- **US-9.4** As an advisor, I want to confirm or reject a pending item with an optional comment so that the student’s checklist and readiness status stay accurate.
- **US-9.5** As an advisor, I want a list of my students who are behind on required items for their standing so that I can reach out before they graduate unprepared.
- **US-9.6** As an advisor, I want to leave a short note or suggested next step on a student’s plan so that the student knows what to do after a meeting.
- **US-9.7** As a student, I want to see which advisor is assigned to me so that I know who can help with my flight plan.

---

## Feature 10: Notifications and communication

Students should be prompted at useful times without having to remember to open the app.

### User stories

- **US-10.1** As a student, I want a notification at the start of a fall or spring term with that standing’s checklist so that I begin job-prep activities on time.
- **US-10.2** As a student, I want a notification when I have incomplete required items late in my current standing so that I can finish before the term ends.
- **US-10.3** As a student, I want a reminder before an upcoming dated event on my plan so that I do not miss the offering.
- **US-10.4** As a student, I want to manage notification preferences (email, in-app, or off) so that reminders stay helpful rather than noisy.

---

## Traceability to the epic

| Epic need | Features that address it |
| --- | --- |
| Activities that prepare me for a job after graduation | 2, 6, 7, 8 |
| Checklist of tasks and events | 2, 3, 6 |
| Organized by each semester I am in school | 1, 2, 8 |
| Prepared to successfully apply for a job | 3, 4, 7, 9 |

---

## Suggested priority (MVP first)

Decisions that are core to the product belong in MVP, not only the original student check-off.

1. **Must have (MVP):** Features 1, 2, 3, 6, 8, and 9 (three roles, 8-term major plan, mix completion with advisor confirm, dated events on the template).
2. **Should have:** Features 4 and 7 (readiness summary, task guidance and evidence for high-stakes items).
3. **Could have:** Features 5 and 10 (filtering/search, notifications).

## Out of scope (from decisions)

- Advisor-assigned or student-picked templates  
- Summer terms or custom calendars for transfers  
- Generic undated “do this sometime this term” events  
- Honor-system-only completion for every item, or confirmation required for every item  
- A school-wide event calendar separate from the student’s major plan (events live on the template)
