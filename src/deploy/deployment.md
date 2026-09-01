# Jetson, Docker, and Nix

## What deployment means here

Development, cross-platform builds, ZED services, and the software actually launched on a vehicle are related but different concerns. SW9S includes several artifacts for them, but source inspection indicates mixed maturity.

## Nix development shell

`flake.nix` defines Linux-focused shells with Rust tooling, LLVM/Clang, and an OpenCV-oriented non-FHS shell. It declares `x86_64-linux`, so it is not evidence of a supported macOS setup. Static inspection also found a package output referencing a shell name that is not defined.

## Docker/ZED

`docker/docker-compose.yml` currently has an active ZED service using `Dockerfile.ZED`, host networking, NVIDIA/Jetson assumptions, device access, and an upstream ZED ROS wrapper. Commented blocks include other services. The compose file does not visibly start the Rust SW9S binary, a YOLO service, an RTSP server, or a simulator.

The repository-root `Dockerfile` contains older SW8 naming and should be treated as historical/stale until a team owner confirms otherwise. The vendored YOLO material is not evidence that it is deployed.

## How to use this page

Use these files as a map for questions, not a field procedure. Confirm target Jetson/JetPack, ROS distribution, active service topology, environment variables, model availability, network policy, and what starts SW9S on boot before writing a deployment runbook.

## Last verified against SW9S

Source-derived from `fc780a1`; deployment status needs team confirmation.
