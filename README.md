# Reusable Codex Career Skills

Public, reusable Codex skills for job search and technical interview preparation.

## Included skills

- `manage-job-search` — stateful search, review, explicit approval, application, and tracking.
- `staff-system-design-interview` — staff-level system-design interview manuscripts and practice.
- `staff-object-oriented-design-interview` — Python-oriented object/low-level-design interview preparation.

## `manage-job-search`

The skill supports:

1. building a candidate profile from scratch or reconciling existing resume/context;
2. discovering roles and separating first publication from reposts;
3. evaluating both role fit and company quality/stage;
4. generating a review queue with “why this role” and “why this company / why change” in each row;
5. waiting for explicit approval of exact roles;
6. preparing multiple approved applications in parallel while preserving browser handoff;
7. submitting only approved roles and recording observable confirmation;
8. maintaining a deduplicated tracker.

The repository intentionally contains no candidate-specific data. Keep resumes, profiles, addresses, immigration details, and trackers in a private workspace.

## Install

Copy `manage-job-search/` into your Codex skills directory, or invoke it explicitly after installing it in your environment.

## Safety model

The skill never treats a general request to automate job search as permission to submit applications. Approval is per exact role/requisition and URL. CAPTCHA, verification, login, legal questions, and ambiguous required fields are handed back to the user.
