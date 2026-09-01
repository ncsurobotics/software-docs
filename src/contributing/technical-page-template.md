# Technical Page Template

This is the preferred structure for future SW9S subsystem pages. The purpose is to make a page useful to a new programmer, a returning team member, and someone with the source open beside them.

Do not apply these headings mechanically. A short page may combine sections; a deeply technical page may need additional sections. What matters is that the reader gets the mental model before the implementation detail, and can trace important claims back to source or team-confirmed operational knowledge.

## Suggested structure

### Why this exists

Start with the robot problem the subsystem solves. Explain what would be difficult or unsafe without it.

### Beginner mental model

Use plain language before introducing project terms. For example, explain a stability controller as a request to keep the vehicle behaving in a desired way, then introduce the particular SW9S command names.

### Underlying engineering or computer-science concept

Introduce the minimum theory needed to understand the implementation: a serial protocol, coordinate transform, asynchronous task, PID loop, image threshold, or message cache.

### How SW9S implements it

Name the real modules, structs, traits, functions, configuration types, and command names. Prefer stable references such as `src/comms/control_board/mod.rs`, `ControlBoard::new`, or `ActionExec<T>` over fragile line numbers.

### Inputs, processing, and outputs

State what enters the subsystem, the important transformations, and what leaves it. A compact flow diagram is often better than several paragraphs.

### Interactions with other systems

Describe the upstream producers, downstream consumers, configuration, hardware, tasks, or services that affect this component.

### Technical details

Put protocol bytes, units, constraints, concurrency behavior, data formats, timing, and failure handling here after the reader knows why they matter.

### How to debug or modify it

Explain observable outputs, relevant tests, logs, safe development steps, and the review boundaries. Be explicit if validation needs hardware.

### Known limitations or uncertainties

Separate source-derived facts from items that need team confirmation. Never convert a TODO, a stale configuration value, or an inferred deployment path into an operational guarantee.

### Relevant SW9S source

List the key repository paths and symbols a reader should open next.

### Last verified SW9S revision

Record the commit or release used to check implementation claims. If the page has not been runtime-verified, say so.

## Documentation status

Use the lightweight labels from [Documentation Status](../reference/documentation-status.md) where they clarify the confidence of a claim. A page should not become a wall of warnings; one concise status note near the relevant claim is usually enough.
