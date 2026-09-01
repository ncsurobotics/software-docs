# AquaPack Robotics Software Handbook

# Start Here

- [Welcome to SW9S](title-page.md)
- [Software Team Orientation](onboarding/introduction.md)
- [SW9S in One Page](architecture/sw9s-in-one-page.md)
- [Documentation Status](reference/documentation-status.md)

# Your First Week

- [Development Environment](onboarding/installation.md)
  - [Windows with WSL and VS Code](onboarding/installation/windows_rust.md)
  - [Linux Status](onboarding/installation/linux_rust.md)
  - [macOS Status](onboarding/installation/mac_os_rust.md)
- [Your First Repository Tour](first-week/repository-tour.md)

# How SW9S Fits Together

- [Reading the SW9S Codebase](architecture/reading-the-codebase.md)
- [Startup, Runtime, and Shutdown](architecture/runtime-lifecycle.md)

# Core Concepts in SW9S Context

- [Robot Motion, Frames, and Stability](core/motion-and-control.md)
- [Async Rust, Traits, and Actions](core/rust-and-actions.md)
- [Serial Messages, CRCs, and Acknowledgements](core/serial-protocols.md)

# Hardware Interfaces

- [Control Board and Thrusters](hardware/control-board.md)
- [Main Electronics Board (MEB)](hardware/meb.md)
- [Native Cameras](hardware/cameras.md)
- [ZED and ROS 2](hardware/zed-ros.md)
- [Ping360 Sonar](hardware/sonar.md)

# Configure and Operate

- [Configuration](operate/configuration.md)
- [Mission Commands and Safe Operation](operate/missions-and-safety.md)

# Mission and Action Architecture

- [The Action System](missions/action-system.md)
- [Mission Catalogue and Data Flows](missions/mission-catalogue.md)

# Vision

- [Vision Pipeline](vision/vision-pipeline.md)
- [Detectors, Models, and Active Learning](vision/detectors-and-models.md)
- [Active Learning Pipeline](vision/active_learning_pipeline.md)

# Observe, Test, Debug, Deploy

- [Logs, Rerun, and Debugging](observe/observability.md)
- [Tests and Safe Change Workflow](observe/testing.md)
- [Jetson, Docker, and Nix](deploy/deployment.md)

# Reference

- [Common Change Recipes](reference/common-change-recipes.md)
- [Source Map](reference/source-map.md)
- [Technical Page Template](contributing/technical-page-template.md)
- [Team-Confirmation Register](reference/team-confirmation-register.md)
