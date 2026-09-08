# Object-Oriented Design Manuscript Standard

## Output contract

The manuscript is both a rehearsal script and a study reference. A sixty-minute interview is the default, but an explicit user duration overrides it. The main transcript must remain speakable; detailed variants belong in the untimed follow-up bank. When the selected low-level design source expects implementation, the manuscript includes a real Python 3 implementation by default.

Use these rules:

- Candidate speech uses first-person plural voice.
- Put the complete interview question immediately after the title so the reader can follow every later requirement and code decision.
- Do not use shortened terms in candidate prose or visible diagram labels, even after expansion. Mermaid syntax headers and official product names are the only narrow exceptions.
- Include real source code in the selected language, defaulting to Python 3 when the user does not specify one. Embed it directly in the Markdown by default; create external files only when explicitly requested. Do not disguise pseudocode as implementation; identify complete code blocks, dependencies, and omitted production adapters.
- Include focused tests or executable examples for the main happy path, invalid input, exceptional state, repeated request, boundary transition, concurrency or locking behavior when relevant, and dependency failure.
- Define typed, domain-specific exceptions before implementation. Cover invalid input, missing resource, capacity exhaustion, illegal state transition, conflict or duplicate, retryable dependency failure, and invariant violation when applicable. Explain state change, retry behavior, and why `None`, magic values, or undifferentiated booleans are not sufficient.
- Evolve the code with the interview clock: first show exception and class/interface skeletons, then the core happy-path method, then edge cases and state transitions, then concurrency or persistence adaptations, and finally focused tests. Do not reveal a complete implementation before the design decisions that justify it.
- Generate one running example from the current question and reuse it consistently.
- Give every class, interface, value object, collection, policy, state, exception outcome, storage record, and diagram node a concrete example at first mention.
- Explain domain behavior before naming a design pattern. Never add a pattern merely to display vocabulary.
- Every consequential choice includes the chosen option, benefit, cost, rejected alternative, failure behavior, and a threshold that would trigger reconsideration.
- When a resource moves between owners, separate its lifecycle label from route ownership. A source may remain the owner of an older published snapshot while a successor is prepared; say which state accepts new work and which state only serves pinned readers.
- For online movement, spell out the final handoff: advance an ownership epoch, stop new admissions, wait for already admitted work with a bounded barrier, capture one final sequence per source, replay through each fence, conditionally publish the replacement, drain any durable post-fence queue with destination admission checks, and release the source fence. A single scalar fence is insufficient for a multi-source merge.
- If a post-fence queue is accepted before publication, freeze a reservation epoch and queue high-water mark before the replacement proof. Account for that reserved headroom in every direct and queued destination admission; a reservation is capacity, not a second logical size increment.
- Treat logical conservation and temporary physical duplication separately. Verify unique identities and weights for the logical view, and track extra physical copies only for capacity and cleanup.
- For copied records, keep global accepted-record identity separate from per-destination membership and size accounting. A retry across epochs must have zero logical-write delta, while the first copy into each successor must count once toward that successor's proof.
- In a multi-process design, distinguish source admission epochs from worker ownership epochs. A takeover may adopt a sealed source fence without reusing an admission token; shared permits and destination-capacity reservations need a durable compare-and-set or reconciliation rule.
- If old data is retained for readers, make snapshot acquisition and lease registration atomic and give cleanup an explicit lease check. If accepted work waits behind a handoff, define its durable queue owner, capacity bound, idempotency key, and crash-recovery drain path.
- End with the final complete Mermaid diagram.

## Recommended sixty-minute shape

These timings are defaults and should be rescaled for another requested duration.

| Elapsed time | Interview outcome |
|---|---|
| Zero to five minutes | Clarifying questions, assumptions, actors, and scope |
| Five to ten minutes | Functional scenarios, exclusions, and domain invariants |
| Ten to fifteen minutes | Core entities, value objects, and contracts |
| Fifteen to twenty-three minutes | Version-zero class responsibilities and primary interaction |
| Twenty-three to fifty-seven minutes | Deep dives, interviewer probes, and design evolution |
| Fifty-seven to sixty minutes | Requirement audit, trade-off recap, and final diagram |

The final thirty-seven minutes are deep dives or selected follow-ups, including the closing audit. If the user requests at least one hour of depth, extend the duration or place additional branches in the untimed bank rather than making the spoken script impossible.

All rules below are defaults unless the user explicitly changes them. Honor explicit requests for another length, location, inline delivery, plain text, no diagrams, a different diagram count, or a different depth.

## Required sequence

### Clarifying questions and assumptions

Ask questions that can change the object model: actors, ownership, lifecycle, identity, valid and invalid states, concurrency, persistence, external dependencies, timing, extensibility, and scope. State the assumed answer and its design consequence immediately when the interviewer does not answer.

Use the implementation-aware order from the supplied low-level design guidance: clarify before coding, summarize final requirements and exclusions, derive entities from nouns and behavior, define class state and public methods, implement the most interesting methods, walk one concrete scenario through the code, then discuss extensions. Keep exception outcomes specific and tied to the requirements.

### Functional scenarios and invariants

Prioritize three to five user or system scenarios. Write each as an observable outcome and include one concrete example. Put secondary features below the line. Then state non-negotiable invariants and the harm caused by violating them. Examples of domain-neutral form are “one resource cannot be owned by two active operations” or “a completed operation cannot be undone by a retry.”

When workload, timing, or capacity changes object responsibilities, include at least one quantified target, such as a maximum command latency or operation backlog. For a purely local domain model, state that scale is out of scope instead of inventing a distributed design.

### Core model and contracts

Distinguish entities, value objects, aggregate roots, policies, repositories, gateways, and domain services when they have different responsibilities. For example, compartment `C-17` has identity and mutable occupancy, while `PackageSize.SMALL` is an immutable value and an exact-size allocator is a replaceable policy.

Define operation contracts with preconditions, postconditions, returned result, error semantics, idempotency, and atomic state changes. Do not put every method on one manager class; explain the owner of each rule.

For each public method, pair the happy path with edge cases and the exception raised for each one. For example, a locker deposit raises a capacity exception when no matching compartment exists, while a pickup raises an invalid-token exception or an expired-token exception; the caller can distinguish whether retrying makes sense.

### Version-zero model

Build the smallest complete class collaboration before adding persistence, event buses, dependency injection frameworks, or distributed coordination. For each scenario, walk through:

1. initiating actor and request;
2. entry-point validation;
3. selected object and behavior owner;
4. collaborator calls and state changes;
5. response, error, and retry behavior;
6. one concrete example.

Include a responsibility or class diagram and a primary interaction diagram. Explicitly list which requirements version zero does not yet address.

When a write can race a structural change, version zero must still name the linearization point. It may use an in-process admission gate and journal, but it cannot rely on “catch up and then publish” without a final fence and a stated behavior for writes that arrive after that fence. If readers need repeatable data, snapshot acquisition must return an immutable storage read token together with the route and lease; a directory version alone is only routing consistency.

After the conceptual walkthrough, include the smallest complete implementation slice in staged code blocks. Show the logical file names, class and interface definitions, state transitions, exception paths, and a test or executable example. Do not attempt to implement an external database or hardware dependency when a replaceable protocol or fake is the clearer interview boundary.

### Deep dives

For each applicable quality or interviewer probe:

1. restate the invariant or target and version-zero gap;
2. show the smallest responsibility or collaboration change;
3. walk through the running example;
4. explain state, atomicity, concurrency, failure, and recovery;
5. state the trade-off and rejected alternative;
6. name a test or operational measurement;
7. give a reconsideration threshold;
8. update a diagram when the object topology changes.

Choose domain-specific deep dives. Common categories include allocation and contention, state-machine correctness, persistence and recovery, extension without modification, external adapters, testability, performance and memory, authorization, audit, and migration.

For online structural movement or routing ownership handoff, include explicit probes for a write after the high-water mark, an in-flight writer at the drain barrier, a catalog publication whose result is uncertain, a crash before queue drain, an orphan target, and a reader that opens during cleanup. Ordinary resource allocation need not invent a structural fence unless it changes ownership or routing. Explain how each applicable result is idempotent and how the route remains unambiguous.

### Follow-up bank and physical order

Use this physical order:

1. timed transcript through its verbal close;
2. untimed follow-up bank, including any decision audit;
3. final integrated diagram as the final content block.

The bank should cover applicable variants such as invalid input, repeated calls, boundary states, concurrent calls, partial failure, exception mapping, code review, persistence loss, object replacement, testing, new business rules, and “build without a named pattern” questions. Do not claim to answer literally every conceivable question; cover every applicable risk family.

## Pattern and responsibility guidance

Prefer plain responsibilities over pattern names:

- Use composition when a station may swap allocation policy without changing compartment behavior.
- Use a strategy when allocation rules vary, such as exact-size versus future larger-size fallback.
- Use explicit state transitions or a state object when behavior depends on lifecycle, such as occupied, expired, and awaiting staff removal.
- Use a repository or gateway when hardware or persistence should be replaceable in tests.
- Use an adapter around an external code generator or door controller.
- Use an observer or event publication only when multiple independent listeners need a committed transition; do not hide required synchronous behavior behind events.

For every pattern, state the simpler alternative and why it is not preferred for this question. Avoid inheritance hierarchies when a small composition boundary is clearer.

## Progressive diagrams

Use readable names and concrete labels. At minimum show:

1. responsibilities and ownership;
2. the primary request collaboration;
3. lifecycle or invariant transitions;
4. extension, persistence, or failure behavior when relevant;
5. one final integrated workflow and object collaboration diagram.

Each Mermaid block begins with `graph TD` unless the user explicitly chooses another diagram type. The final diagram must include every accepted class boundary and external dependency and must be the last content in the file.

After drafting, read and apply [review-rubric.md](review-rubric.md). When delegation is available and the skill is complex enough to warrant it, run an independent forward test in an isolated temporary workspace using only this skill and a genuinely unseen request. After the final revision, perform one clean mechanical and semantic validation.
