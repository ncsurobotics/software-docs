# Reading the SW9S Codebase

## Start with the shape of the project

SW9S is one Cargo package, not a large Rust workspace. `Cargo.toml` defines two targets:

- the `sw9s` binary, whose entry point is `src/main.rs`;
- the `sw9s_lib` library, whose top-level module file is `src/lib.rs`.

This matters because the binary is where the robot application is assembled, while the library holds the reusable building blocks. When you want to understand what happens when the program starts, begin with `src/main.rs`. When you want to understand a subsystem, follow the module exports in `src/lib.rs` into the corresponding directory.

## A useful first-reading route

1. Read `Cargo.toml` to see the package, default features, and important dependencies such as Tokio, OpenCV, ROS 2, Rerun, and serial support.
2. Read `src/main.rs` from top to bottom. It shows how configuration, the control board, MEB, cameras, ZED, cancellation, and mission dispatch are connected.
3. Find `run_mission` in `src/main.rs`. It is the practical map from a command-line mission name to a mission implementation.
4. Read `src/missions/action.rs` and `src/missions/action_context.rs` before trying to understand a large mission. They explain the vocabulary used to compose behavior and acquire hardware access.
5. Follow one small mission into the subsystems it calls. A camera-based mission will lead to `src/missions/vision.rs`, `src/vision/`, `src/missions/movement.rs`, and then the control-board modules.

## The directories and why they matter

| Area | Why a contributor should care |
|---|---|
| `src/main.rs` | The composition root. It reveals startup order, global resources, mission names, and shutdown behavior. |
| `src/lib.rs` | Process-wide logging and the top-level map of library modules. |
| `src/config/` | The shape of configuration the program expects: device paths, mission settings, color profiles, sonar, and ZED fields. |
| `src/comms/` | The boundary between Jetson-side Rust and serial/ROS-facing devices. Start here for control board, MEB, protocol, and ZED work. |
| `src/missions/` | The robot's behavior layer. It contains action composition, movement primitives, vision adapters, and named mission routines. |
| `src/video_source/` | How native front/bottom camera frames arrive from V4L2/GStreamer. |
| `src/vision/` | Shared image/detection types plus task-specific classical and ONNX/YOLO-style detectors. |
| `docker/` and `flake.nix` | Development/deployment context, especially Jetson/ZED integration. Treat active versus historical material carefully. |

## How mission code relates to the architecture

A mission file is rarely self-contained. Its job is usually to express a behavior using actions. The action system supplies the control-flow vocabulary—sequence, conditional branch, race, loop, or concurrent work. The action context supplies only the resources an action says it needs, such as a front camera or control board.

That means an effective code-reading question is not “what does this directory contain?” but “what does this action consume, what does it produce, and where does the result go?” For a visual alignment action, the answer may be:

```text
front camera → image frame → detector → normalized offset → movement transform → stability command
```

Following that chain is more useful than reading every generic implementation in one pass.

## First changes: choose a narrow boundary

For a first contribution, prefer one of these bounded paths:

- improve a source-grounded documentation page;
- add a test around a pure parser or transform;
- trace a configuration field from TOML to its consumer;
- inspect one detector's input/output contract;
- improve a development-only diagnostic without changing vehicle behavior.

Avoid changing motor matrices, PID values, axis signs, arming/shutdown behavior, serial command layouts, or deployed camera/ROS configuration without a confirmed hardware procedure and review from the relevant team owners.

## Relevant SW9S source

`Cargo.toml`, `src/main.rs`, `src/lib.rs`, `src/config/`, `src/comms/`, `src/missions/`, `src/video_source/`, and `src/vision/` form the recommended first-reading set.

## Status

**Source-derived:** this describes the repository organization, not a promise that every module or deployment path is current production software.
