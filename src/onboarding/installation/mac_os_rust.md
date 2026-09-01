# macOS Status

The inspected SW9S repository does not provide a confirmed macOS development path. Its Nix flake declares only `x86_64-linux`, and camera/deployment code assumes Linux and Jetson facilities such as V4L2, `/dev` devices, and NVIDIA tooling.

You can still use macOS for reading source, writing documentation, and some Rust-only work, but do not assume native camera, ROS 2, OpenCV, Docker, or full project builds will work without a team-verified environment. Windows with WSL or a supported Linux system is the safer starting point until the team establishes otherwise.

## Last verified against SW9S

Source-derived from `fc780a1`; macOS support needs team confirmation.
