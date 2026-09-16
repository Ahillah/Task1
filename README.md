#  Job Management — Close Job Feature (Jira & Agile Documentation)

##  Project Overview
This repository documents the Agile planning, user story mapping, and task breakdown for the **Job Applications & Job Closing** module, managed and configured in Jira.

---

##  Epics & Features
* **Epic:** Job Management
* **Feature:** Close Job & Application Control

---

##  User Stories & Tasks Breakdown

### 1. Recruiter Manually Closes an Active Job 
* **Role:** Recruiter
* **Story:** As a Recruiter, I want to manually close an active job posting, so that no more candidates can apply for it.
* **Acceptance Criteria (AC):** Job status updates to `Closed`, and new application submissions are blocked.
* **Priority:** High | **Story Points:** 3
* **Technical Tasks:**
  1. Update `Job` entity/enum to include `Closed` status + DB migration.
  2. Implement `PATCH /api/jobs/{id}/status` endpoint.
  3. Add authorization check (Recruiter / Job Owner only).
  4. Add validation to ensure job status is currently `Active`.

---

### 2. Automatically Reject Applications to Closed Jobs 
* **Role:** Candidate
* **Story:** As a Candidate, I want to be informed when attempting to apply to a closed job, so that I don't waste time on inactive listings.
* **Acceptance Criteria (AC):** System checks job status during application submission and returns `400 Bad Request` or `409 Conflict`.
* **Priority:** Highest | **Story Points:** 2
* **Technical Tasks:**
  1. Add job status validation in `POST /api/applications`.
  2. Return clear error response: `"Job is closed"`.

---

### 3. Auto-close Job on Expiry Date 
* **Role:** Recruiter
* **Story:** As a Recruiter, I want jobs to automatically close after their expiration date, so that I don't have to manage them manually.
* **Acceptance Criteria (AC):** Scheduled background worker updates expired jobs to `Closed`.
* **Priority:** Medium | **Story Points:** 5
* **Technical Tasks:**
  1. Add `ExpirationDate` field to `Job` entity + migration.
  3. Auto-update expired job statuses to `Closed`.

---

##  Sprint Planning (`Job Closing` Sprint)
* **Sprint Capacity:** 3 Story Points
* **Total Work Items:** 3 User Stories
* **Goal:** Ensure complete control over job lifecycles and prevent invalid candidate submissions.
