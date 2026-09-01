# Control Board and Thrusters

## Why this interface exists

SW9S runs on the Jetson, but the Jetson is not directly wired into a simple “forward” motor command. The control board is the interface between mission software and the vehicle's thrusters, IMU, depth sensor, watchdog, and lower-level control behavior.

## What SW9S sends

`ControlBoard` in `src/comms/control_board/mod.rs` exposes commands for motor matrix setup, inversions, degrees-of-freedom scales, raw thrusters, relative/global movement, two stability-assist modes, BNO055 settings, PID tuning, status, and reset.

During `ControlBoard::new`, source shows initialization of the motor matrix, inversions, movement scaling, BNO configuration, zero command, PID parameters, and watchdog handling. The vehicle definition types are in `vehicle_definition.rs`; the values used by the application are in `src/main.rs`.

## Sensor feedback

The response parser caches watchdog state, BNO055 orientation, and MS5837 bytes. `Angles::from_raw` turns an IMU quaternion into pitch/roll/yaw. Missions use yaw; source does not show a high-level decoded depth interface or a central host-side state estimator.

## What is external

The serial protocol and requests are visible in SW9S. Firmware motor allocation, real PID timing, electrical output, watchdog guarantees, sensor calibration, and physical wiring are not. Treat them as external system facts until confirmed.

## Important review item

**Needs team confirmation:** source inspection found a possible 0-based/1-based motor-matrix indexing mismatch during initialization. This handbook records it in the confirmation register; it does not claim the deployed robot is blocked or unsafe.

## Debugging and modification

Start with captured logs and parser/unit tests. For a command change, document byte format, ACK behavior, units, timeout, hardware owner, and an emergency stop procedure. Matrix, inversion, PID, and axis changes require hardware review.

## Last verified against SW9S

Source-derived from `fc780a1`.
