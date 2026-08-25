## Windows Installation
- For windows the recommended approach is to use VSCode within WSL (Windows Subsystem for Linux). VSCode is a code editor, WSL is a virtualized Linux operating system.
- [Follow the VS Code WSL setup guide](https://code.visualstudio.com/docs/remote/wsl)
 
### After installing VS Code and WSL:
- open a new terminal from the top menu within VS Code and run these commands one by one to download Rust:
  - sudo apt update && sudo apt upgrade
  - sudo apt install build-essential rustup
  - rustup default stable

- Go to the VS Code 'Extensions' tab and install the rust-analyzer extension.