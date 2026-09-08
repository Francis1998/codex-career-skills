# Application and Tracking Runbook

Read this reference when the user approves applications, asks for form preparation/submission, or reports an application event.

## Authorization and deduplication

Before opening or submitting a form, map approval to one exact queue ID and URL, check the queue and tracker for prior/pending submission, verify the requisition is live and materially unchanged, and honor a direct user report as `APPLIED_USER` without resubmitting.

## Inspect and classify fields

Read all required fields and classify answers as `PROFILE_FACT`, `RESUME_FACT`, `TAILORED_TEXT`, `USER_REQUIRED`, or `OPTIONAL_SKIP`. Use the approved resume and profile. Do not infer legal/native name, immigration classification, protected characteristics, restrictive covenants, export-control status, clearance, or other legal answers.

## Safe defaults

Apply only defaults configured by the current user. These may include ordinary onsite/hybrid acceptance, routine privacy acknowledgement, application-status communication, and declining voluntary demographics. Do not universalize one user's defaults to another user.

For sponsorship, use the profile's jurisdiction-specific answer. For binary technical questions, answer `Yes` only when the profile/resume supports a truthful adjacent interpretation and explain the scope; never claim unsupported ownership. For required compensation, distinguish base from total compensation and ask if ambiguous.

## Batch preparation and browser handoff

- Prepare independent approved applications concurrently when safe, with an explicit page map such as `J014 -> Company Role`.
- Never rely on tab order and never submit an unapproved page.
- If a page reaches CAPTCHA, OTP, login, account creation, verification, or frontend failure, keep it open with safe entered values. Report the exact remaining action.
- If the user takes over and submits the open page, mark it `APPLIED_USER` and never retry.

## Submission

Submit only after exact approval and resolution of required fields. Wait for a confirmation page, identifier, or confirmation email. If a page times out, check for evidence before retrying; retry at most once when there is evidence the first attempt failed. Do not bypass access controls. If material job details changed, return it to `REVIEW` and request renewed approval.

## Record results

On success set `APPLIED_CODEX` or `APPLIED_USER`, record timestamp/timezone, exact URL, source, resume version, and confirmation evidence, then update exactly one tracker row. On a blocker set only that role to `SUBMISSION_BLOCKED`, record the barrier without unnecessary PII, and keep the page open for handoff.

Recommended tracker columns:

```text
Company,Role,Job URL,Location,Date Added,Date Applied,Status,Source,Next Event,Recruiter,Notes
```

Report each approved ID as submitted with confirmation, blocked and why, skipped as duplicate, returned to review, or closed/unavailable. Include links to updated local artifacts.
