# Tests and Safe Change Workflow

## Current test reality

SW9S has a small number of inline Rust tests for frame parsing/logging, MEB arm debounce, camera integration, path vision, and octagon vision. One camera test is ignored. Some vision tests reference resource files that are not tracked, and several tests primarily produce output rather than assert behavior.

There is no project GitHub Actions workflow in the inspected checkout. Vendored Python tests are mainly lint/copyright checks rather than vision behavior tests.

## A safe workflow

1. Classify the change: pure code, configuration, communications, perception, movement, or operation.
2. Trace its source inputs and downstream hardware consequences.
3. Add or improve the narrowest test possible.
4. Run static/unit validation before hardware validation.
5. Obtain a team-approved procedure before touching a serial board, payload, thruster mapping, PID, or powered vehicle.
6. Record evidence and update the corresponding handbook page/status.

## What to test first

Pure protocol framing, parser behavior, configuration loading, data transforms, and detector geometry are good candidates for repeatable tests. Hardware integration should be explicit and isolated. Current test gaps include configuration samples, mission cancellation, command byte layouts, shutdown behavior, ROS topic decoding, simulation integration, and end-to-end flows.

## Last verified against SW9S

Source-derived from `fc780a1`; test commands themselves were not run in this handbook environment.
