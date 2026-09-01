# Development Environment

This section is about preparing a personal development computer. It is not the same thing as deploying software to the vehicle: robot deployment, Jetson dependencies, and powered-hardware procedures will be documented separately after they are confirmed with the team.

## Current starting point

- [Windows with WSL and VS Code](installation/windows_rust.md) is the existing team-recommended path.
- Linux and macOS pages exist in the repository but have not yet been verified as SW9S development procedures, so they are intentionally not presented as supported instructions here.

The SW9S repository contains a Linux-focused Nix development shell and native dependencies such as OpenCV/GStreamer. Before relying on any setup guide for robot work, verify it against the current target hardware and the team's approved workflow.
