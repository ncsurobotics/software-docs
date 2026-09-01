# Logs, Rerun, and Debugging

## Why observability matters

When a robot misses a target or fails to move, you need evidence from each step of the chain—not just a final error. SW9S records several kinds of evidence.

## Source-visible outputs

| Output | What it can show |
|---|---|
| `console/<timestamp>.txt` | Messages written through the `logln!` macro. |
| `logging/control_board_in*.dat` and `logging/meb_in*.dat` | Raw received serial data when the logging feature is enabled. |
| `/tmp/cams_<timestamp>/` | Native camera recordings. |
| `/tmp/detect/` | Annotated vision images in logging-enabled paths. |
| `logging/sonar/` | Ping360 JSON scan records. |
| Rerun gRPC stream | ZED images, objects, and pose telemetry. |

`src/lib.rs` defines `logln!`, a timestamp, and the global Rerun accessor. Camera, serial, sonar, vision, and ZED modules add their own outputs.

## A useful debugging sequence

1. Identify the first unexpected boundary: configuration, device open, frame arrival, detection, action transform, command ACK, or physical response.
2. Inspect the nearest artifact for that boundary.
3. Reproduce in the least physical environment possible.
4. Add a narrow log/test around the suspected transformation rather than broad print statements everywhere.

## Limits

Not all `println!` output goes through `logln!`; logs have no universal schema; some runtime artifacts are committed in the repository without a confirmed fixture policy. Raw serial logging may not represent a perfect packet capture. Treat artifacts as debugging clues, not automatic proof of device behavior.

## Last verified against SW9S

Source-derived from `fc780a1`.
