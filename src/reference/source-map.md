# Source Map

Use this page as an index when a handbook page names a subsystem.

| Concern | Primary SW9S source |
|---|---|
| Package/features | `Cargo.toml`, `src/lib.rs` |
| Startup and mission aliases | `src/main.rs`, especially `run_mission` |
| Configuration | `src/config/mod.rs` and `src/config/` |
| Framing/protocol | `src/comms/auv_control_board/` |
| Control board/vehicle | `src/comms/control_board/`, `vehicle_definition.rs` |
| MEB | `src/comms/meb/` |
| ZED | `src/comms/zed_ros2.rs` |
| Cameras | `src/video_source/` |
| Vision core/models | `src/vision/mod.rs`, `nn_cv2.rs`, `yolo_model.rs` |
| Task detectors | `src/vision/gate_cv.rs`, `path_cv.rs`, `slalom.rs`, `octagon.rs`, `gate_poles.rs` |
| Action/movement | `src/missions/action.rs`, `action_context.rs`, `movement.rs`, `vision.rs` |
| Missions | `src/missions/` |
| Sonar | `src/missions/sonar.rs`, `src/config/sonar.rs` |
| Deployment | `flake.nix`, `docker/`, root `Dockerfile` |

The handbook's initial source baseline is SW9S commit `fc780a1`. Paths and symbols are preferred over line numbers because line numbers change frequently.
