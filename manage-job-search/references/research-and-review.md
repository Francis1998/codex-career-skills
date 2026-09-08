# Research and Review Runbook

Read this reference for discovery, recommendation, company diligence, or queue generation.

## Candidate rubric

Use the user's profile, resume, context, and tracker to extract target and adjacent functions, demonstrated strengths and gaps, seniority, geography/work mode, sponsorship requirements, compensation handling, company-stage preferences, risk tolerance, protected employers, and already-submitted roles.

Do not hard-code a profession or technology. Include adjacent roles when the resume shows a credible path. If the user gives no search window or candidate count, ask or choose a modest default and state it.

## Discovery

Prefer employer career pages and ATS data, primary company announcements/filings, reputable reporting, job boards for discovery/repost timing, and labor/immigration data for sponsorship signals.

For each candidate record separately: ATS first-published date, last update, repost/resurfacing age, current listing status, and application URL. If only repost evidence is available, label it `RECENT_REPOST`.

## Role evaluation

Evaluate evidence rather than title or keyword overlap. Explain which responsibilities are demonstrated, which are adjacent and learnable, the likely screen risks, whether the work advances the user's direction, and whether the level and work mode are plausible.

Every reviewable row must include `Why this role`, tied to concrete resume evidence, and a candid gap/risk.

## Company evaluation

Every reviewable row must include `Why this company / why change`. When relevant, research founding year, headcount, funding round/date/amount/lead investors, total funding/valuation, public/private status, revenue/customer signals, stage, layoffs/acquisition/reorganization, regulatory or runway risks, and why an offer may justify leaving the user's current role.

Use company press releases, SEC filings, official investor materials, and reputable reporting. If facts conflict or cannot be verified, say `not verified`; never infer a funding round from marketing copy.

## Sponsorship and compliance

Record explicit sponsorship language, recent sponsorship/transfer evidence, citizenship/export-control/clearance restrictions, and confidence (`STRONG`, `MODERATE`, `WEAK`, `UNKNOWN`). Historical filings are directional evidence only.

## Required review row

Each `REVIEW`, `CONTACT_FIRST`, or `HOLD_PROTECTED` row should include:

| Field | Required content |
|---|---|
| Job ID | Stable local identifier |
| Company / role / exact link | Canonical employer URL |
| Freshness | First published versus updated/reposted |
| Location / work mode | Include onsite/travel expectations |
| Compensation | Base/equity/bonus; clarify missing meaning |
| Fit and evidence | Resume-to-JD mapping |
| Why this role | How the work advances the user's goal |
| Why this company / why change | Stage, scale/funding, traction, risks, and value relative to current role |
| Main gaps | Honest screen risks |
| Sponsorship | Explicit language and historical signal with caveat |
| Apply capability | Standard ATS, likely handoff, or contact-first |
| Decision | Current status |

Keep the rationale in the row or immediately adjacent to it; do not create a detached duplicate rationale section.

## Review boundary

Present the queue and wait for exact approval by job ID, exact role, or canonical URL. Do not submit while merely presenting recommendations.
