# Object-Oriented Design Manuscript Review Rubric

Read this after a complete draft. Classify findings as blocking, major, or minor. Reviewers return findings without concurrent edits. Rerun applicable passes after each revision. Stop with no blocking or major findings; after two cycles, report not ready and request permission before a further cycle if either severity remains. Report unresolved minor findings.

## Blocking checks

- The requested sequence, duration, format, delivery mode, and explicit overrides are honored.
- The complete interview question appears immediately after the title, before assumptions or design discussion.
- The transcript is speakable for its stated duration and preserves the required deep-dive time.
- Domain invariants and the harm of violating them appear before class responsibilities and persistence choices.
- Every prioritized scenario has an end-to-end collaboration walk with state changes, result, and error behavior.
- The version-zero model is coherent, intentionally small, and explicitly names missed targets.
- The final integrated Mermaid diagram is literally the last content block, and the physical order is transcript, follow-up bank, final diagram.
- If the design has online movement, the transcript names a final admission fence and a bounded drain barrier; “copy then publish” without that handoff is blocking.

## Major checks

- Responsibilities are assigned to cohesive owners; orchestration does not become a god class.
- Entities, value objects, aggregate boundaries, policies, repositories, gateways, and external dependencies are distinguished where applicable.
- Preconditions, postconditions, atomicity, idempotency, conflict behavior, and retry semantics are explicit for each mutation.
- State transitions enumerate valid, invalid, terminal, and boundary-time behavior.
- Concurrent calls cannot violate the stated invariant; the chosen lock, conditional update, or ownership boundary is justified.
- Lifecycle state is distinct from route ownership, and every published version has one route owner per key or resource. Multiple source operations carry a complete per-source fence vector and deterministic acquisition order.
- Persistence and external effects have explicit failure and recovery behavior, including what is and is not transactional.
- A durable append has an explicit change-event or queue outcome; post-commit queue drain and source-fence release are idempotent recovery phases. Orphan targets are protected by an owner epoch or quarantine grace before deletion.
- Reader snapshot acquisition and lease registration are atomic when old physical data can be cleaned up. Queue reservations and destination admission cannot make a committed target exceed its threshold.
- Global record deduplication is not confused with successor membership accounting; copied records contribute once to each committed destination while retries contribute no second logical write.
- Source admission epochs, worker ownership epochs, shared permit leases, and destination-capacity reservations have explicit takeover, expiry, and reconciliation behavior.
- Extension points use composition or a justified pattern, and the design names the cost and rejected alternative.
- Tests cover happy path, invalid input, repeated request, boundary state, concurrency, dependency failure, and extension behavior when applicable.
- Security, authorization, audit, tenant or user isolation, and privacy appear when relevant.
- Every introduced design element has a nearby concrete example.
- Every consequential decision includes benefit, cost, rejected alternative, failure behavior, measurement, and reconsideration threshold.
- At least five progressive diagrams exist when diagrams are allowed, and they progress from responsibilities to final collaboration.
- Candidate speech uses first-person plural voice; no shortened terms appear in prose or visible diagram labels. Code fences are allowed when code is requested and are checked separately from Mermaid fences.
- Follow-up answers are domain-specific and do not contradict the main model.
- When code is requested or the source guidance expects it, the manuscript includes staged real implementation blocks in the selected language, a code-block manifest, and runnable tests or an executable example; code is not pseudocode or empty class shells.
- Code evolves in the same order as the interview: exception and class/interface skeletons first, then core behavior, then edge cases and deep-dive changes, then focused tests. A complete implementation appearing before its design decisions is a pacing and delivery defect.
- Typed domain-specific exceptions or explicit error results cover invalid input, missing resource, capacity exhaustion, illegal state, conflict or duplicate, retryable dependency failure, and invariant violation where applicable. Each exception states whether state changed and whether retry is safe.

## No-abbreviation inspection

Inspect all uppercase tokens and shortened forms. Candidate prose and visible diagram labels must use full terms rather than shortened names for interfaces, identifiers, databases, requests, synchronization, exceptions, and patterns. The literal Mermaid header `TD`, official product names without official expansions, and file extensions are narrow syntax exceptions.

## Minor checks

- Interviewer turns are natural and leave room for redirection.
- Every pattern name is backed by a responsibility and a rejected simpler alternative.
- Diagram labels fit and do not imply behavior absent from the prose.
- Links and local references resolve; no placeholders remain.
- A clean mechanical and semantic validation was run after the final revision.

## Forward tests

When delegation is available, test the skill in an isolated temporary workspace with genuinely unseen prompts, for example:

- “Design a cloud build scheduler with priorities and quotas.”
- “Design a multi-branch library lending model.”
- “Design a turn-based board game engine with undo.”

The output passes only if the invariants, object responsibilities, state machine, patterns, and follow-ups change with the domain. A generic manager class plus renamed methods is a failed test.
