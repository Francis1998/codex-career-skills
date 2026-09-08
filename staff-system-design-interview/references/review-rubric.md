# Staff System Design Manuscript Review Rubric

Read this reference only after a complete draft exists. Classify every finding as blocking, major, or minor. A manuscript is ready only when no blocking or major findings remain. Reviewers return findings instead of editing the same file concurrently. After each revision, rerun applicable passes. Use at most two revision cycles unless the user explicitly requests more; if blocking or major findings remain after cycle two, report the manuscript as not ready with the unresolved findings and ask permission before another cycle. Report unresolved minor findings.

## Blocking checks

- The requested sequence, duration, format, output location, and explicit user constraints are followed.
- The complete interview question appears immediately after the title, before the assumptions and design sequence.
- A default ninety-minute time ledger assigns the entire final sixty minutes to deep dives, interviewer probes, closing synthesis, and the final workflow.
- Non-negotiable domain invariants appear before consistency, availability, and replication choices.
- Every prioritized functional requirement has a complete end-to-end workflow.
- The version-zero design is coherent and explicitly names the quantified targets it misses.
- The final integrated Mermaid diagram is literally the last content block.
- Physical order is timed transcript, then untimed follow-up bank, then final integrated diagram, with no substantive section between the bank and final diagram.

## Major checks

- Assumptions answer every material unanswered clarifying question.
- Functional requirements are prioritized and below-the-line scope is explicit.
- Non-functional targets are quantified and closed individually through a design modification, example, failure behavior, measurement, trade-off, rejected alternative, and reconsideration threshold.
- Every calculation changes or validates a design decision.
- Every introduced design element has a concrete example on first mention.
- Duplicate, delayed, reordered, conflicting, concurrent, and partial-failure semantics are addressed when applicable.
- Partitioning, hotspots, skew, rebalancing, tenfold growth, and hundredfold growth are addressed when applicable.
- Durability boundaries, replication, recovery, overload, backpressure, and graceful degradation are explicit.
- Security, isolation, cost, retention, migration, and independent health observation are handled when relevant.
- Follow-up answers do not contradict the main design.
- At least four progressive Mermaid diagrams exist and progress from version zero to the integrated design.
- Candidate speech consistently uses first-person plural voice, and no implementation code or pseudocode appears outside Mermaid diagrams.
- The final diagram's arrows reflect the prose: every required regional or asynchronous fan-out has a result path, every as-of or completeness constraint reaches the reader or evaluator, and no recovery or rejection edge bypasses authorization and admission.

## No-abbreviation inspection

Do not use shortened terms in candidate prose or visible diagram labels, even after expanding them. Inspect every all-capital token and common shortened form, including shortened names for programming interfaces, databases, request rates, service targets, distributed-systems theorems, expiration, processors, remote calls, web protocols, data encodings, identifiers, percentiles, version zero, scale multipliers, storage media, recovery targets, time standards, storage-tree designs, and transaction properties. The literal `TD` in a Mermaid `graph TD` header is the only blanket whitelist. Non-prose file extensions and official product names without an official expanded form may remain.

## Minor checks

- Interviewer turns feel natural and leave room to redirect.
- Prose is concise enough for the timed duration; reserve variants are clearly untimed.
- Progressive diagrams show only the design state reached at that point.
- Links resolve, headings are readable, and no unfinished placeholders remain.
- Performance claims are identified as requirements, estimates, benchmarks, or measurements rather than unsupported guarantees.
- A pre-existing output file is never overwritten without explicit permission; revisions may update the newly created draft.
- When delegation is available for this complex skill, an unseen-domain forward test and any explicit-duration or format-override test are run in an isolated temporary workspace, and their artifacts are inspected for domain-specific behavior.
