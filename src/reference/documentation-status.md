# Documentation Status

Robot software has two kinds of truth: what the source code says at a particular revision, and what the team has confirmed works on the current vehicle. They overlap, but they are not the same thing.

Use these labels sparingly when the distinction matters:

| Label | Meaning |
|---|---|
| **Verified** | Confirmed through a stated test, team-approved procedure, or current hardware/deployment validation. Say what was verified and when. |
| **Source-derived** | Directly supported by a named SW9S path or symbol at a stated revision. It may not have been executed on the vehicle. |
| **Needs team confirmation** | Important operational detail not established by source alone: wiring, calibration, mission readiness, active deployment, sign conventions, or approved safety practice. |
| **Experimental** | Present for exploration or development, but not approved as a reliable operational path. |
| **Historical/stale** | Kept for context but not assumed current. Explain why it is marked this way when known. |

Examples:

- “`run_mission` recognizes `sonar`” is **Source-derived**.
- “The `sonar` mission is approved for competition operation” needs a **Verified** or **Needs team confirmation** note.
- A container definition that names an older vehicle generation may be **Historical/stale**.

The goal is clarity, not decoration. Use normal prose by default and add one of these labels only where a reader could otherwise mistake an inference for a field-tested fact.
