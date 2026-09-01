# Windows with WSL and VS Code

For Windows, the team's existing recommendation is to use VS Code through WSL (Windows Subsystem for Linux). VS Code is the editor; WSL provides a Linux environment, which is closer to the environment expected by SW9S tooling.

Start with the [VS Code WSL setup guide](https://code.visualstudio.com/docs/remote/wsl). Once WSL and VS Code are installed, open a terminal in the WSL environment and install Rust:

```sh
sudo apt update && sudo apt upgrade
sudo apt install build-essential rustup
rustup default stable
```

Then install the `rust-analyzer` extension in VS Code. It provides source navigation, type information, and compiler feedback while you read and edit Rust.

> Status: This is preserved team onboarding guidance. It is not yet a complete, verified SW9S build procedure; OpenCV, GStreamer, Nix, and other native requirements still need a team-verified setup page.
