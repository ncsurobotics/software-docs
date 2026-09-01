# Robot Motion, Frames, and Stability

## Why the robot needs a control vocabulary

The vehicle cannot use a steering wheel. It has multiple thrusters, can move and rotate underwater, and must hold or change an orientation while sensors are noisy. Software therefore needs a shared vocabulary for requests such as “move forward,” “strafe,” “turn,” or “hold a depth.”

## Beginner mental model

A **degree of freedom** is one independent kind of motion. Underwater vehicles commonly describe three translations—forward/back, side-to-side, up/down—and three rotations—roll, pitch, yaw. A coordinate **frame** defines which directions and signs those words use. Without a confirmed frame, a number such as `+0.3` is not meaningful.

A **PID controller** is a feedback rule that compares a target with a measurement and continuously corrects the error. In SW9S, source inspection suggests important stability/PID work is performed by external control-board firmware after Rust sends a higher-level request. Confirm the deployed division of responsibility before tuning or operating it.

## SW9S implementation

`src/missions/movement.rs` contains movement actions and transforms. `src/comms/control_board/mod.rs` exposes raw, relative, global, and stability-assist commands. `VehicleDefinition` in `src/comms/control_board/vehicle_definition.rs` models a motor matrix, inversions, degrees-of-freedom scales, and PID axes; the active definition is hard-coded in `src/main.rs`.

The motor matrix is the mapping from desired vehicle motion to individual thruster contributions. Inverting a motor flips its physical direction. These values are vehicle calibration, not generic robotics constants.

## Inputs → processing → outputs

```text
target movement or visual offset
→ movement action / transform
→ board command (raw, relative, global, or stability assist)
→ serial protocol
→ external firmware and thrusters
```

IMU orientation arrives as a quaternion and is converted to pitch/roll/yaw by `Angles::from_raw` in `src/comms/control_board/util.rs`. A quaternion is a four-number rotation representation that avoids some problems with Euler angles; SW9S converts it into the more intuitive pitch/roll/yaw form for mission use.

## Limitations and safe modification

**Needs team confirmation:** body/world frame, signs, units, motor numbering, negative-depth convention, BNO axis mapping, matrix, inversions, PID values, and whether board firmware owns all closed-loop control. There is also a source-level motor-matrix indexing concern in the confirmation register. Do not change these values from a documentation-derived understanding.

## Last verified against SW9S

Source-derived from `fc780a1`.
