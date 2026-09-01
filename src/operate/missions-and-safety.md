# Mission Commands and Safe Operation

## What a mission command is

SW9S accepts positional command-line strings and dispatches them in `run_mission` in `src/main.rs`. They are executed sequentially, not through a polished subcommand CLI. A mission can be a competition behavior, a diagnostic, or a prototype; its presence in the dispatcher does not establish that it is approved for a vehicle run.

## Source-visible mission groups

- Basic/control: `arm`, `empty`, `depth_test`, `travel_test`, `descend`, `forward`, `pid_test`.
- Gate/path/slalom: `gate_run_coinflip`, `gate_run_yolo`, `gate_run_reckon`, `path_align`, `slalom_left`, `slalom_right`.
- Other tasks: `octagon`, `coinflip`, `spin`, `torpedo_only`, `sonar`, `bin`, `zed_test`.
- Utilities/experiments: `start_cam`, `open_cam_test`, `forever`/`infinite`, `example`.

Some aliases are surprising or stale-looking; for example, source accepts `surface_` and `surface-test`, not an obvious `surface_test`. Treat this page as a code-reading guide, not a command-to-run list.

## Safety boundary

Never infer a real arming/run procedure from source alone. Before a powered test, team confirmation is needed for vehicle state, physical restraint, kill/abort process, observer roles, configuration, expected motion, and recovery. The MEB arm watcher and control-board watchdog are code/firmware mechanisms, not substitutes for a human-approved procedure.

## Last verified against SW9S

Source-derived from `fc780a1`; all operational procedures need team confirmation.
