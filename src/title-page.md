# Welcome to SW9S

SeaWolf IX is AquaPack Robotics' autonomous underwater vehicle. **SW9S** is the Rust software repository that helps the vehicle turn a mission objective—such as moving through a gate or following a path—into observations, decisions, and commands for the robot's hardware.

> Handbook status: this is a generated, source-grounded first-pass handbook undergoing team review. It explains what the inspected SW9S source contains, while marking deployment, calibration, and safety facts that still need human confirmation.

## What is RoboSub?

RoboSub is an autonomous underwater robotics competition. The important word is *autonomous*: once a run begins, a person is not continuously steering the vehicle. The robot has to use its sensors, software, and embedded electronics to attempt the task on its own.

That changes what “writing code for a robot” means. It is not only an algorithm running on a laptop. A useful change has to fit into a real chain: sensors produce imperfect information, software interprets it, commands cross a hardware boundary, and the vehicle moves in water. Reliability and safe failure behavior matter as much as a clever detector or control rule.

## What SW9S is responsible for

At a high level, SW9S coordinates mission behavior and the interfaces around it:

- it starts named mission routines;
- it combines smaller actions such as observing, aligning, waiting, and moving;
- it communicates with the control board that drives the thrusters;
- it reads or routes information from cameras, the Main Electronics Board (MEB), sonar, and a ZED/ROS 2 path;
- it records useful observations and logs for debugging.

Some lower-level responsibilities appear to belong to external firmware or services rather than SW9S itself—for example, portions of thruster control, firmware watchdog behavior, and ZED container operation. This handbook distinguishes code that is visible in SW9S from details that require team confirmation.

## How to use this handbook

Read the book in order the first time. It moves from intuition to implementation:

1. Learn what the robot is trying to do and how the major pieces fit together.
2. Prepare a development environment and learn to navigate the source.
3. Learn the robotics and Rust ideas in the specific form SW9S uses them.
4. Follow a data flow from mission to hardware or from camera to movement.
5. Use source-linked subsystem pages when you are ready to make a change.

You do not need previous robotics experience. If a term such as *thruster allocation*, *PID*, *ROS 2*, or *async* is new, first focus on the plain-English explanation. Later pages will connect that explanation to the real Rust types, modules, and messages.

Begin with [SW9S in One Page](architecture/sw9s-in-one-page.md), then use [Reading the SW9S Codebase](architecture/reading-the-codebase.md) with the repository open beside you.
