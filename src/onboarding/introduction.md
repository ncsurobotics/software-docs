# Software Team Orientation

The AquaPack software team helps SeaWolf IX make decisions during an autonomous RoboSub run. RoboSub is an underwater robotics competition: after the run begins, the vehicle must perceive its surroundings, decide what to do next, and carry out mission tasks without a person steering it in real time.

That is why software matters so much. A camera detection is only useful if it can become a safe, well-timed movement. A mission idea is only useful if the robot can execute it reliably with the real vehicle, sensors, and electronics.

In practical terms, the code makes the robot do things. It connects the Jetson computer, the control board, sensors, cameras, and mission logic into one system.

## Tools you will encounter

SW9S is primarily written in Rust. Rust is the language used for the robot application because it can express complex, concurrent systems while making many memory and ownership mistakes harder to write.

The project also uses OpenCV for image processing, YOLO-style models for some object-detection experiments, ROS 2 and Docker around the ZED camera environment, and lower-level serial protocols for the electronics boards. You do not need to understand all of these on day one. The handbook introduces them in the order that makes their role on the robot clear.

## How to begin

Start with [Welcome to SW9S](../title-page.md), then read [SW9S in One Page](../architecture/sw9s-in-one-page.md). If you are setting up a development computer, use the [Development Environment](installation.md) page; the team's existing recommended Windows path is [Windows with WSL and VS Code](installation/windows_rust.md).

When you read technical pages, keep the source code open beside the book. The goal is not to memorize every module. It is to build a mental map: what information enters the system, where SW9S makes a decision, what hardware receives the result, and which details still need confirmation from the team.
