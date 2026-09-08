# Staff System Design Manuscript Standard

## Output contract

The manuscript must work both as a rehearsal script and as a study reference. Ninety minutes is the default; a user-specified duration overrides it and requires proportional rescaling. Extensive variants belong in a follow-up bank after the timed transcript.

All rules below are defaults unless the user explicitly changes them. Honor explicit requests for another length, location, inline delivery, plain text, no diagrams, a different diagram count, or a different depth. Preserve the user's priorities and sequence within the requested format.

Use these writing rules:

- Put the complete interview question immediately after the title so the reader can follow every later requirement, assumption, and design decision.
- Candidate speech uses first-person plural voice.
- Do not use shortened terms in candidate prose or visible diagram labels, even after spelling them out. The literal Mermaid header `graph TD` and non-prose file extensions are syntax exceptions. An official product name may remain only when it has no official expanded form, and its architectural role must still be explained in plain language.
- Design logic is explained in plain language before implementation names are introduced.
- There is no source code or pseudocode. Small sample records, requests, responses, formulas, state transitions, and Mermaid diagrams are allowed because they clarify behavior rather than prescribe implementation.
- Generate one domain-specific running example from the current question and carry it through the manuscript. Do not reuse a static example embedded in this standard.
- Every material design element receives a concrete instance of that running example near its introduction.
- Every trade-off names the chosen option, its benefit, its cost, a credible alternative, and the reason that alternative is not preferred under the stated requirements.
- Name and distinguish every externally meaningful lifecycle boundary in the current domain, such as accepted, durably committed, derived-view-visible, and externally completed when those states exist. Do not collapse distinct states into one vague meaning of “written” or “done.”
- End with the final complete Mermaid workflow diagram.

## Recommended ninety-minute shape

These timings are the default. When the user requests another duration, rescale them while preserving the requested priorities.

| Elapsed time | Interview outcome |
|---|---|
| Zero to six minutes | Clarifying questions and explicit assumptions |
| Six to ten minutes | Prioritized functional requirements and exclusions |
| Ten to fifteen minutes | Quantified non-functional requirements |
| Fifteen to eighteen minutes | Design-driving estimates |
| Eighteen to twenty-two minutes | Core entities and system interfaces |
| Twenty-two to thirty minutes | Complete version-zero design and end-to-end example |
| Thirty to eighty-seven minutes | Deep dives driven by invariants, non-functional requirements, failures, and interviewer variants |
| Eighty-seven to ninety minutes | Closing deep-dive synthesis, risks, decisions, and final workflow |

The default ninety-minute manuscript therefore assigns the entire final sixty minutes to deep dives, probes, and closing synthesis. Put additional questions in an untimed follow-up bank so the spoken transcript remains feasible.

## Required sequence

### Clarifying questions and assumptions

Ask only questions that can change the architecture. Cover actors, core workflows, scale, traffic shape, query shape, freshness, consistency, durability, retention, geography, tenancy, security, and exclusions as relevant. Pair every unanswered question with a visible assumption and its design consequence.

### Functional requirements

Prioritize roughly three to five requirements. Write them as actor outcomes. Put secondary features below the line and explicitly state that the version-zero design will not solve them unless the interviewer promotes them.

### Non-functional requirements

Quantify the most important qualities. Avoid empty statements such as “the system is scalable.” Prefer a target such as “the ninety-ninth percentile critical user operation completes within one second.” State per-workflow consistency requirements and targets here; defer choosing consistency, replication, availability, and storage mechanisms until after the domain-invariant gate.

### Capacity estimates

Calculate only quantities that choose a design: peak writes, active partitioning identities, hot working set, response size, partition count, fan-out, bandwidth, and retained bytes. State that estimates are directional and show how a twofold mistake would or would not change the architecture.

### Domain invariants, core entities, and contracts

Before selecting consistency, availability, storage, or replication mechanisms, state the non-negotiable domain invariants and the harm caused by violating them. For each mutation, define atomicity, idempotency, conflicts, and network-partition behavior. When acknowledging a write could violate an irreversible invariant, defer or reject it instead of claiming unsafe availability.

Separate identity, mutable state, immutable events, and derived views as applicable. Define ownership, idempotency identity, timestamps, ordering, validation, and response semantics. Carry one named example through every prioritized functional workflow and applicable failure path.

### Version-zero design

Build the minimum complete path before adding caches, queues, replicas, indexes, or regional complexity that are not yet required. For every functional requirement, explain:

1. the initiating actor and request;
2. routing and validation;
3. state read or changed;
4. response and its guarantee;
5. one concrete example.

Include a Mermaid diagram at this stage and name every quantified non-functional target this baseline still misses.

### Deep dives

Address non-functional requirements one by one and evolve the baseline. Staff-level behavior includes finding fragile boundaries before being prompted, distinguishing control and data paths, defining overload behavior, and explaining how the system itself is observed.

For each deep dive:

1. restate the target and current failure;
2. describe the design change in plain language;
3. walk through the running example;
4. explain correctness and failure behavior;
5. quantify why it should meet the target;
6. state trade-offs and rejected alternatives;
7. accept one realistic interviewer challenge;
8. state the measured threshold that would trigger reconsideration;
9. update the diagram when topology changes.

Choose only applicable, question-specific deep dives, usually including the hardest invariant or algorithm, scale and hotspots, latency, durability and recovery, consistency, cost and lifecycle, security and isolation, operations and graceful degradation, and geographic growth.

### Wrap-up, follow-up bank, and physical document order

The timed wrap-up names the largest remaining risks, the measurement that would validate each risky assumption, and the first evolution trigger. The follow-up bank should give short, direct answers rather than repeating the transcript.

Use this physical order:

1. the timed transcript through its verbal close;
2. the untimed follow-up bank;
3. the final integrated diagram representing the design reached at the end of the timed interview.

The final diagram is physically placed after the bank solely to satisfy the final-block contract. Cover applicable questions from these families:

- requirement changes and alternative product scope;
- duplicate, missing, late, reordered, corrupt, and conflicting input;
- concurrency, idempotency, ordering, and consistency boundaries;
- a single process, host, disk, zone, region, dependency, or network failure;
- retry storms, poison data, queue lag, compaction backlog, and partial results;
- hot keys, skewed tenants, flash crowds, tenfold scale, and hundredfold scale;
- query planning, indexing, caching, pagination, fan-out, and admission control;
- storage format, compression, retention, deletion, backup, and restore;
- authentication, authorization, tenant isolation, encryption, audit, and abuse;
- cost ceilings and quality degradation under budget pressure;
- schema or contract evolution, backfill, migration, and rollout;
- observing the service through an independent external health path;
- active-active versus active-passive geography;
- replacing an off-the-shelf database, queue, or search engine with a custom design;
- testing, capacity validation, disaster exercises, and launch plan.

## Progressive diagram standard

Use readable component names rather than unexplained shortened labels. Keep arrows directional and label important guarantees such as “durably acknowledged,” “eventually visible,” or “retry-safe notification.” Progressive diagrams should normally show:

1. the version-zero functional workflow;
2. the hardened write and storage workflow;
3. the query or decision workflow;
4. the failure, asynchronous-processing, or geographic workflow when relevant;
5. the final complete workflow at the very end.

The final diagram must include every component that remains in the recommended design and must distinguish authoritative state, derived state, metadata, external dependencies, and operational feedback as applicable.

## Domain adaptation

Derive the architecture from the pasted question rather than reusing a stock component list. Generate a fresh running example and state the domain's own invariants before choosing consistency or availability. Apply probe categories only when relevant: a reservation problem emphasizes contention and expiration, a collaborative editor emphasizes ordering and conflict resolution, and a file service emphasizes metadata, content, and large-object transfer. Do not import time-series, label-cardinality, alert, or dashboard concepts into another domain unless the question explicitly asks for them.

After drafting, read and apply [review-rubric.md](review-rubric.md). When delegation is available and the skill is complex enough to warrant it, run an independent forward test in an isolated temporary workspace using only this skill and a genuinely unseen request; do not place test artifacts in the user's workspace.

After the final revision, perform one clean mechanical and semantic validation: check headings and timing, count and header-check diagrams, inspect abbreviation and first-person-voice violations, verify the final-block order, and review every major arrow in the integrated diagram against the prose.
