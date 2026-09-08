---
name: staff-system-design-interview
description: Turn a pasted system-design interview question into a staff-level, interview-ready manuscript with scoped requirements, a complete version-zero design, timed deep dives, explicit trade-offs, concrete examples, progressive workflow diagrams, and a broad follow-up bank. Use for senior staff interview practice or answer preparation; do not use for implementation plans, low-level coding designs, or production changes.
---

# Staff System Design Interview

Create a manuscript that a senior staff software development engineer candidate can actually deliver and adapt in a ninety-minute interview. Lead the design, expose assumptions, close gaps proactively, and preserve room for the interviewer to redirect the discussion.

## Required reference

For every manuscript request, read [references/manuscript-standard.md](references/manuscript-standard.md) completely before drafting. It contains the output contract, timing model, design sequence, and follow-up coverage standard. After a complete draft exists, read [references/review-rubric.md](references/review-rubric.md) completely and use it for the review loop.

## Inputs and sources

- Treat the pasted interview question and the user's explicit constraints as authoritative.
- Treat every timing, length, output-location, format, diagram-count, and depth rule in this skill as a default. When the user explicitly changes one, honor the request; for another duration, proportionally rescale the foundation and deep-dive blocks while preserving the requested priorities. An explicit inline-output request overrides the default file handoff.
- Inspect supplied local documents and cited pages when available. Extract only facts that materially affect the design; do not copy a reference answer blindly.
- If scale, latency, retention, consistency, or scope is missing, make reasonable interview assumptions and label them as assumptions. Ask the user only when guessing would materially change the requested deliverable.
- Perform calculations only when they change a partitioning, storage, latency, or cost decision.

## Deliverable

- Write a new Markdown manuscript in the location the user requests, or in the current workspace with a descriptive question-based filename. Resolve a filename that does not already exist, adding a numeric or date suffix when necessary. Never overwrite a manuscript that existed before this run unless the user explicitly requests it; revisions to the newly created draft may update that draft. If file creation is unavailable, or the user explicitly requests inline output, return the manuscript inline.
- Put an explicit `## Interview question` section immediately after the title. Quote the complete prompt in plain language, identify the actors and scope, and state the assumptions that delimit the design. Never make the reader infer the question from a title, running example, or source link.
- Write candidate speech in first-person plural voice, using “we,” “our,” and “us.”
- Do not use shortened terms in candidate prose or visible diagram labels, even after spelling them out. The literal Mermaid header `graph TD` and non-prose file extensions are syntax exceptions. An official product name may remain only when it has no official expanded form, and its architectural role must still be explained in plain language.
- Do not provide source code or pseudocode. Describe interfaces, records, state transitions, and algorithms in plain language with small concrete examples.
- Give every introduced record, file, service, queue, store, index, cache, job, policy, and diagram element a simple example near its first mention.
- Include realistic interviewer interruptions and concise candidate answers throughout, not just a detached architecture essay.
- Add at least four progressive Mermaid diagrams whose first line is `graph TD`: a version-zero workflow, two question-specific refinement workflows, and the final integrated workflow. Each diagram must match the design state reached at that point in the interview.
- End the manuscript with one complete final workflow diagram. Nothing substantive should follow that diagram.

## Method

Explicit user requests override the defaults above, including duration, length, output location, inline versus file delivery, diagram count, and depth. We honor a request for no diagrams or plain text even though the ordinary default includes progressive Mermaid diagrams; we still preserve the requested reasoning sequence in the permitted format.

1. Put the exact interview question first, then convert it into a prioritized interview scope and a visible time budget matching the requested duration, with ninety minutes as the default.
2. Start the transcript with targeted clarifying questions, then state the assumptions used for unanswered questions.
3. State prioritized functional requirements, explicit exclusions, quantified non-functional requirements, and only design-driving capacity estimates.
4. Before selecting consistency, replication, or availability behavior, state the non-negotiable domain invariants and the consequence of violating each one. For every mutation, define its atomicity boundary, idempotency behavior, conflict handling, and network-partition behavior. Defer or reject a write when acknowledging it could violate an irreversible invariant.
5. Define the core entities, system contracts, and one concrete example generated from the current question that will be carried through the entire interview.
6. Build the smallest end-to-end version-zero design one functional requirement at a time. Walk through requests, state changes, and responses, then name the quantified non-functional targets it still misses.
7. For a default ninety-minute manuscript, use the entire final sixty minutes for staff-level deep dives, interviewer probes, closing synthesis, and the final workflow. Address each non-functional requirement explicitly, identify bottlenecks before the interviewer does, and evolve the diagrams as the design changes.
8. For every material choice, state what we optimize, what we give up, at least one plausible alternative, why that alternative is not preferred for this question, and the measured threshold that would make us revisit the decision.
9. Add a compact but comprehensive follow-up bank covering, as applicable to the current question, correctness, failure, overload, security, privacy, cost, operations, migration, tenfold and hundredfold scale, geographic expansion, and a build-from-scratch constraint.
10. Run an independent review loop when delegation is available. Reviewers return findings without editing concurrently. Use one architecture and correctness pass, one skeptical interviewer pass, and one clarity and format pass; consolidate roles when fewer reviewers are available. Classify findings as blocking, major, or minor. After each revision, rerun all applicable passes. Stop when no blocking or major findings remain. Limit the loop to two revision cycles unless the user explicitly authorizes more; if blocking or major findings remain after cycle two, report the manuscript as not ready with those findings and ask permission before another cycle. Report unresolved minor findings. If delegation is unavailable, apply the same rubric as a self-review. Finish with one clean mechanical and semantic validation.

## Handoff

Report the manuscript path and, when relevant, the reusable skill path. Summarize the design's central decision and verification performed; do not paste the manuscript into the final response unless the user asks.
