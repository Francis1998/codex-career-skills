---
name: staff-system-design-interview
description: Turn a pasted system-design interview question into a staff-level, interview-ready manuscript with scoped requirements, a complete version-zero design, timed deep dives, explicit trade-offs, concrete examples, progressive workflow diagrams, and a broad follow-up bank. Use for senior staff interview practice or answer preparation; do not use for implementation plans, low-level coding designs, or production changes.
---

# Staff System Design Interview

Create a manuscript that a senior staff software development engineer candidate can actually deliver in a sixty-minute interview, then extend safely when the interviewer gives another thirty minutes. Lead the design, expose assumptions, close gaps proactively, and preserve room for the interviewer to redirect the discussion.

## Required reference

For every manuscript request, read [references/manuscript-standard.md](references/manuscript-standard.md) completely before drafting. It contains the output contract, the sixty-minute core, the optional thirty-minute extension, and the design sequence. After a complete draft exists, read [references/review-rubric.md](references/review-rubric.md) completely and use it for the review loop.

## Inputs and sources

- Treat the pasted interview question and the user's explicit constraints as authoritative.
- Treat timing, length, output location, format, diagram count, and depth rules as defaults. The default has a complete Core-60 plus an optional Extension-30; an explicit user request overrides it.
- Inspect supplied local documents and cited pages when available. Extract only facts that materially affect the design; do not copy a reference answer blindly.
- If scale, latency, retention, consistency, or scope is missing, make reasonable interview assumptions and label them. Ask only when guessing would materially change the deliverable.
- Perform calculations only when they change a partitioning, storage, latency, or cost decision.

## Deliverable

- Write one final Markdown manuscript in the requested location, or choose a descriptive non-existing filename. Do not create a separate manifest or companion file unless requested.
- Put an explicit `## Interview question` section immediately after the title. State actors, scope, and assumptions.
- Write candidate speech in first-person plural voice, using “we,” “our,” and “us.”
- Do not use shortened terms in candidate prose or visible diagram labels, except the Mermaid syntax header `graph TD` and official names without an expansion.
- Do not provide source code or pseudocode. Describe interfaces, records, state transitions, and algorithms with small concrete examples.
- Include realistic interviewer interruptions and concise candidate answers throughout.
- Add at least four progressive Mermaid diagrams whose first line is `graph TD`. Start with a compact service-and-data topology, then add data/stream and question-specific deep-dive views. End with one readable integrated service architecture and critical workflow diagram; nothing substantive follows it.
- For study-oriented manuscripts, include optional data-model and technology-selection notes with fields, keys, indexes, retention, access patterns, and trade-offs. Mark what is “must draw” live versus “study detail.”

## Method

1. Put the exact interview question first, then create two visible time budgets: a sixty-minute core and an optional thirty-minute extension. If another duration is requested, rescale these layers instead of spreading equal detail across every topic.
2. Start with targeted clarifying questions and visible assumptions.
3. State prioritized functional requirements, exclusions, quantified non-functional requirements, and only design-driving estimates.
4. State invariants before choosing consistency, replication, or availability. Define atomicity, idempotency, conflicts, and network-partition behavior for mutations.
5. Define core entities, system interfaces, contracts, and one domain-specific running example. Include a small set of customer-facing and internal interface examples before the architecture.
6. For complex workflows, give a short numbered data flow before assigning component ownership.
7. Build the smallest complete version-zero design and name the targets it still misses. Mark one primary deep dive for Core-60 and the rest as Extension-30 candidates.
8. Make Core-60 land requirements, invariants, version zero, one highest-risk deep dive, failure/recovery, observability, and a concise close. Use Extension-30 only for the next highest-value deep dive, scale/cost/security or operations, migration, and interviewer probes.
9. For every material choice, state the optimization, cost, rejected alternative, failure behavior, measurement, and reconsideration threshold.
10. Add a compact follow-up bank covering applicable correctness, failure, overload, security, privacy, cost, operations, migration, scale, geography, and build-from-scratch probes.
11. Run architecture, skeptical-interviewer, and clarity reviews when delegation is available; otherwise apply the same rubric as a self-review. Finish with clean mechanical and semantic validation.

## Handoff

Report the single manuscript path and reusable skill path. Summarize the central design decision and verification performed; do not paste the full manuscript unless requested.
