# Your First Repository Tour

## The goal of your first week

Do not start by trying to understand every mission. Your first goal is to build a map of the system: where execution starts, what talks to hardware, where behavior is composed, and which parts are safe to change without a vehicle.

The primary repository is `SW9S`. It is a Rust project with a little deployment material beside the source. `software-docs` is this handbook.

## A safe reading order

1. Read `SW9S/Cargo.toml` for package features and dependencies.
2. Read `SW9S/src/main.rs` for startup and mission dispatch.
3. Read `SW9S/src/missions/action.rs` and `action_context.rs` for the behavior vocabulary.
4. Pick one flow—camera to movement, MEB to shutdown, or sonar to log—and trace it through the source.

Avoid first changes to motor mapping, PID tuning, signs/axes, payloads, board protocols, or startup/shutdown. Those changes cross the boundary from software review into physical vehicle behavior.

## What you can explore without hardware

Source navigation, documentation, pure data transforms, parser tests, configuration tracing, and static code review are useful off-robot work. Camera, serial-board, ROS 2, and vehicle motion validation require environment or hardware that is not bundled by the repository.

## Last verified against SW9S

Source-derived from commit `fc780a1` (the inspected `main` revision). Development setup and hardware access remain team-confirmed topics.
