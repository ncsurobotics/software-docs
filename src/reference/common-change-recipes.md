# Common Change Recipes

## Add a configuration field

Add the field to the appropriate type under `src/config/`, decide whether it has a safe default, add it to an example only after schema validation exists, and trace its consumer. A field that is parsed but unused is not a completed feature.

## Add a detector

Define the detector's input image, output type, coordinate convention, confidence/selection rule, and debug imagery. Implement against `VisualDetector` where appropriate, then connect it through `src/missions/vision.rs` and a mission transform. Confirm color/model calibration separately from movement response.

## Add an action or mission

Choose required capability traits, define typed inputs/outputs, compose existing actions where possible, then add a dispatcher alias in `run_mission`. Document cancellation and the physical consequence of every movement/payload side effect.

## Add a board command

Trace the high-level method, protocol payload, response/ACK handling, firmware expectation, units, timeout, and test fixture. This is a hardware-interface change, not just a Rust API change.

## Change vehicle mapping or PID

Do not use this handbook as authorization. These values are calibration and safety-critical. Require a confirmed vehicle model, a controlled procedure, review, observability, and recovery plan.

## Last verified against SW9S

Source-derived guidance from `fc780a1`; all hardware-changing recipes require team review.
