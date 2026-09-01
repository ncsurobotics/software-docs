# Ping360 Sonar

## What sonar contributes

A camera sees light; a scanning sonar measures acoustic returns. The Ping360 can produce a sweep of nearby returns that may be useful where visual conditions are poor.

## SW9S implementation

`src/missions/sonar.rs` opens a configured serial port through the Blue Robotics Ping library, configures a Ping360, collects scan data, and writes a pretty JSON log under `logging/sonar/`. The configuration type is in `src/config/sonar.rs`.

The mission uses cancellation so an interrupted scan can stop its work. It currently accumulates a scan and records it rather than feeding it into a navigation, mapping, or obstacle-avoidance component.

## Debugging and modification

Start with serial path/baud configuration and generated JSON. If integrating sonar into a decision, first document the coordinate frame, scan format, timing, confidence assumptions, and safe fallback when data is missing.

## Last verified against SW9S

Source-derived from `fc780a1`; actual operational sonar use needs team confirmation.
