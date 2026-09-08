---
name: manage-job-search
description: "Run a reusable job-search workflow from scratch or existing context: onboard preferences, discover and diligence roles, create a review queue, submit only explicitly approved applications, and track outcomes. Use when a user wants job research, application preparation/submission, or application tracking; do not use for general career advice without an active job-search workflow."
---

# Manage Job Search

Run job search as a stateful workflow, not a one-off list. The workflow works for any profession, geography, visa situation, seniority, or application system. User-specific facts belong in the user's workspace profile, not in this skill.

## First use: build from scratch

Before researching or applying, look for a user-provided resume/CV, profile, job queue, tracker, notes, and prior application context. If none exists, ask only the questions needed to start and create a small local profile:

- target roles, functions, industries, and acceptable adjacent roles;
- preferred locations, remote/hybrid/onsite limits, travel, and relocation;
- seniority or level range;
- compensation floor and whether it means base or total compensation;
- work authorization, sponsorship/transfer needs, and jurisdictions that matter;
- company preferences, company-size/stage threshold, risk tolerance, and protected/dream employers;
- search window and desired number of candidates;
- whether the user wants research only, application preparation, or submission after approval;
- resume and tracker locations, if the user already has them.

Do not ask for facts that are optional for the current step. Do not infer legal identity, immigration status, protected characteristics, compensation meaning, or willingness to relocate. Persist answers in a local profile only when the user wants a reusable profile.

## Existing context

When files or prior context exist:

1. Read the resume/CV for career claims.
2. Read the profile for application facts and user-approved defaults.
3. Read the queue and tracker for existing applications, holds, recruiter conversations, and deduplication.
4. Reconcile conflicts in favor of direct user statements, then the current profile, then the resume for work history. Preserve richer existing schemas and original files unless migration is requested.

Prefer a workspace structure such as:

- `job_search/JOB_QUEUE.md` — decision-ready role queue and rationale.
- `job_search/JOB_TRACKER.csv` — one row per exact requisition and pipeline state.
- `job_search/APPLICATION_PROFILE.private.md` — local PII and reusable answers.

Never upload a private profile, resume, address, government identifier, application tracker, or other PII to a public repository unless the user explicitly requests that exact action.

## Workflow modes

Choose the smallest mode that satisfies the request:

1. **Onboard:** create or update the local profile and identify missing constraints.
2. **Discover and review:** read [references/research-and-review.md](references/research-and-review.md).
3. **Prepare and apply:** read [references/application-and-tracking.md](references/application-and-tracking.md).
4. **Track:** reconcile reported applications, interviews, recruiter events, and confirmations without resubmitting.
5. **Mixed request:** research first, present the queue, wait for exact approval, then apply only approved roles.

## Non-negotiable invariants

- An approval authorizes only the exact role/requisition and canonical URL named by the user. It does not authorize sibling roles, referrals, recruiter messages, account creation, or future applications.
- Never submit before explicit per-role approval. A general request to automate job search is not application approval.
- Deduplicate against both the queue and tracker before every submission attempt.
- Distinguish an employer ATS first-published date from an update, repost, or job-board resurfacing. Never present a repost as a new requisition.
- Treat protected/dream employers as review-only until the user explicitly releases the hold. Withdrawing approval supersedes all earlier approval.
- Ground candidate claims in the resume/profile. Do not convert a keyword, adjacent skill, tutorial, or tool usage into unsupported ownership or production experience.
- Do not infer legal name, citizenship, country of birth, visa category, export-control/U.S.-person status, security clearance, non-compete obligations, disability, veteran status, or other legal attestations.
- Sponsorship is a hard filter only when the user says it is. Historical filings are evidence of past activity, not a promise for the current requisition; recommend confirmation for the exact role.
- Default to individual-contributor roles at the user's configured level. Exclude manager/director roles unless the user requests management track or the role is clearly hands-on technical leadership.
- Leave optional salary, cover-letter, demographic, marketing, and job-alert fields blank or declined unless the profile contains an approved preference.
- Stop for CAPTCHA, OTP, login, account creation, identity verification, unexpected legal questions, ambiguous required fields, or materially changed requisitions. Do not bypass controls or guess.
- After a confirmed submission, record observable evidence and update both queue and tracker immediately.
- For independent approved roles, batch preparation may run in parallel, but every page must be mapped to an exact job ID and unapproved roles must never be submitted.
- If a form needs user handoff or has a frontend failure, keep the page and safe entered values open. If the user submits it, mark `APPLIED_USER` and never retry.

## Status model

Use stable states:

`DISCOVERED`, `REVIEW`, `APPROVE_CODEX`, `HOLD_PROTECTED`, `CONTACT_FIRST`, `LOW_PRIORITY`, `SUBMISSION_BLOCKED`, `APPLIED_USER`, `APPLIED_CODEX`, `RECRUITER_SCREEN`, `INTERVIEWING`, `REJECTED`, `WITHDRAWN`, `OFFER`.

Do not use “applied” for a merely opened or partially filled form. Require a confirmation page, identifier, confirmation email, or a direct user report.

## Handoff

End every run with:

- changed files and statuses;
- submitted, blocked, held, skipped, and duplicate roles;
- exact user input needed for remaining blockers;
- clickable links to local artifacts;
- the next safe action.
