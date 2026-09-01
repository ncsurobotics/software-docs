# Linux Status

SW9S is Linux-oriented: the repository includes an `x86_64-linux` Nix flake, V4L2/GStreamer camera code, serial-device paths, and Jetson-focused deployment material. That makes Linux the most plausible native development environment from source inspection.

This is not yet a verified setup recipe. Default Cargo features use native libraries such as OpenCV, and the repository's FHS/non-FHS Nix shells have different assumptions. Confirm the supported distribution, package versions, Nix workflow, and a successful build command with the team before treating Linux as an approved path.

## Last verified against SW9S

Source-derived from `fc780a1`; host setup needs team confirmation.
