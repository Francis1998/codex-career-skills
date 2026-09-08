---
name: staff-object-oriented-design-interview
description: Turn a pasted object-oriented or low-level design interview question into an interview-ready Python 3 implementation manuscript with scoped assumptions, domain invariants, responsibility-driven classes, explicit interfaces, state transitions, exception contracts, tests, trade-offs, progressive diagrams, and realistic interviewer follow-ups. Use for interview preparation; do not use for production implementation plans or generic architecture essays.
---

# Staff Object-Oriented Design Interview

Create a manuscript that a senior staff software development engineer candidate can deliver in an object-oriented or low-level design interview. The design should be concrete enough to implement and explain: begin with the exact question, then requirements, entities, class interfaces, implementation, tests, extensibility, and interviewer follow-ups. Default to Python 3 code unless the user specifies another language or explicitly requests a no-code answer.

## Required reference

Read [references/manuscript-standard.md](references/manuscript-standard.md) completely before drafting. After a complete draft exists, read [references/review-rubric.md](references/review-rubric.md) completely and use it for an independent review loop.

## Inputs and source handling

- Treat the pasted question, explicit user constraints, and supplied artifacts as authoritative.
- Inspect local documents and cited pages when supplied. Use popularity signals only to explain a question-selection decision; never copy a reference answer without reconciling its contract.
- Inspect supplied OOD or low-level design guidance for its delivery sequence, code expectations, class-diagram conventions, and exception guidance. When a source includes an implementation, use its structure as a style signal, not as text to copy.
- Generate a fresh running example from the current question. Do not reuse an example embedded in this skill or its references.
- If the prompt omits scale, actors, lifecycle, error semantics, or extension points, ask targeted clarifying questions and then state assumptions with their design consequences.

## Deliverable

- Create a new Markdown manuscript in the requested location, or choose a descriptive non-existing filename in the current workspace. Never overwrite a file that existed before this run without explicit permission; revisions may update the draft created during this run. Honor an explicit inline-output request.
- Put an explicit `## Interview question` section immediately after the title. Quote the complete prompt in plain language, state the selected language, and list the assumptions that delimit the implementation. Never make the reader infer the question from a title or example.
- Use first-person plural candidate speech: “we,” “our,” and “us.” Do not use first-person singular.
- Do not use shortened terms in candidate prose or visible diagram labels, even after spelling them out. The literal Mermaid headers required by the user are syntax exceptions; official product names may remain only when they have no official expanded form.
- Include real source code for the selected language unless the user explicitly disables code. For the default Python 3 path, prefer type annotations, dataclasses where they clarify state, enumerations for finite states, protocols or abstract base classes for replaceable collaborators, and standard-library-only dependencies unless the prompt asks otherwise. Embed the code directly in the Markdown by default; create separate code files only when the user explicitly asks for them.
- Do not present pseudocode as if it were implementation. Separate conceptual explanations from code, identify which files are complete, and include the core methods that carry the behavior rather than only empty class shells.
- Include a code-block manifest with checkpoint times, a runnable example or test command, and focused tests for happy paths, invalid input, exceptional states, repeated requests, boundary transitions, concurrency or locking when relevant, and dependency failures.
- Evolve code with the interview clock. Start with exception and class/interface skeletons after requirements and class design; add the core happy-path method after version zero; add edge cases and state transitions in the relevant deep dive; add concurrency, persistence, and tests only when those probes occur. Do not present a complete implementation before the interviewer has reached its design decisions.
- Define domain-specific exceptions before implementation. Distinguish invalid input, missing resource, capacity exhaustion, illegal state transition, conflict or duplicate, retryable dependency failure, and invariant violation when those outcomes exist. Explain which exception is raised, what state changed, whether the caller may retry, and why returning `None`, a magic value, or an undifferentiated boolean is not preferred.
- Give each introduced class, interface, value object, collection, policy, exception outcome, persistence record, diagram element, or external dependency a nearby concrete example.
- Include realistic interviewer turns, objections, and candidate alignment checkpoints.
- Use at least five progressive Mermaid diagrams when diagrams are allowed: responsibility/class view, primary interaction, state or invariant view, implementation or exception view, and one final integrated diagram. Each diagram starts with `graph TD` unless the user explicitly requests another Mermaid diagram type.
- For any move, split, merge, allocation, or ownership handoff, distinguish lifecycle state from route ownership. State which version remains authoritative while a source is moving, and which state may accept new writes.
- For an online structural movement or routing ownership handoff, require a bounded cutover protocol: stop new admissions with an epoch, await already admitted work, capture a final per-source fence, replay through that fence, publish one conditional replacement, and drain post-fence work idempotently. Ordinary resource allocation does not need this protocol unless it changes ownership or routing. For multiple sources, use a complete fence vector and deterministic lock order.
- If old physical data is retained for readers, require an atomic snapshot-plus-lease acquisition and an explicit lease registry or equivalent deletion guard. If post-fence work is queued, require a durable queue owner, capacity bound, target admission check, and post-commit recovery path.
- When records are copied, distinguish global logical-record deduplication from per-destination membership accounting. A copy must not add a second logical record, but it must still contribute once to the successor's size proof.
- For multi-process movement, separate the source admission epoch from the worker ownership epoch. A worker takeover may adopt an existing sealed fence without reusing an admission token; all shared permits, destination-capacity reservations, and uncertain appends need a durable compare-and-set or reconciliation contract.
- End with one complete final workflow and object-collaboration diagram. Nothing substantive follows it.

## Method

1. Build a time budget matching the requested duration, with a sixty-minute OOD interview as the default. Preserve user overrides for duration, length, format, diagram count, depth, and delivery mode. If the user asks for at least one hour of deep dives, keep the timed path speakable and make the untimed bank explicitly long enough to supply that hour.
2. Start with the exact interview question, then targeted clarifying questions and explicit assumptions. Follow the source-guidance sequence: final requirements, exclusions, entities, class design, implementation, concrete verification, extensibility, and follow-ups.
3. State prioritized functional scenarios and explicit exclusions. Include the happy path, invalid input, boundary time, repeated request, and failure scenarios that can change the object model. When the object design has meaningful workload, timing, or capacity behavior, ask for or state at least one quantified target and explain which responsibility or data structure it changes; do not force distributed scale analysis onto a purely local domain exercise.
4. Identify actors, nouns, value objects, aggregate roots, policies, stateful entities, and external boundaries. Separate identity from mutable state and domain behavior from orchestration.
5. Define contracts in plain language: operation intent, inputs, outputs, preconditions, postconditions, idempotency, exceptions, ownership, and transaction boundaries. Give a concrete example for every contract. Map each exceptional outcome to a typed exception or explicit result and a retry rule.
6. Assign responsibilities using high cohesion and low coupling. Explain why behavior belongs on a class rather than in a service or caller, and call out where composition, strategy, state, adapter, repository, or observer patterns genuinely remove complexity.
7. Build a deliberately small version-zero object model and walk through each prioritized scenario step by step, including state changes and collaborator calls. Then evolve embedded Python 3 code or code in the requested language checkpoint by checkpoint: skeletons, core behavior, edge cases, deep-dive changes, and focused tests. Name the design qualities the code intentionally leaves to adapters or production infrastructure.
8. Spend the remaining interview time on focused deep dives: invariants and concurrency, lifecycle/state transitions, exception taxonomy, implementation quality, extensibility, persistence and recovery, testability, performance, security, and operational boundaries as applicable. For each choice, state benefit, cost, rejected alternative, failure behavior, measurement, and a reconsideration threshold. Explicitly cover the race between the last replay and publication, uncertain publication, post-commit queue drain, reader-lease cleanup, and orphan-target recovery whenever movement is online.
9. Add a compact but broad follow-up bank. Select only domain-relevant probes, including requirement changes, new variants, concurrency races, retries, invalid states, exception mapping, persistence failure, scale, migration, and “what if we cannot use a given pattern” variants.
10. Run independent architecture, interviewer, code-quality, and clarity reviews when delegation is available. Reviewers return blocking, major, and minor findings without concurrent edits. Rerun applicable passes after each revision, stop with no blocking or major findings, and after two cycles report not ready and ask permission before another cycle if major findings remain. Finish with mechanical validation plus a language-level syntax or test check for the included code.

## Handoff

Report the manuscript path, skill path, question-selection rationale when relevant, selected language, code-block manifest, review result, and validation performed. Do not paste the full manuscript unless requested.
