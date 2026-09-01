# Team-Confirmation Register

This is an internal documentation-development register. It records facts that are important enough to document but cannot be safely established from the inspected SW9S source alone. Once a team owner confirms an item, move the result into the appropriate handbook page and retain a short decision record if it affects future work.

| Topic | Why it matters | Current source-based observation | Needed confirmation |
|---|---|---|---|
| Mission readiness | New members need to know what is safe and useful to run. | The dispatcher exposes many mission and test names, with placeholders and explicitly untested paths present. | Which missions are production-ready, experimental, diagnostic-only, or retired? |
| Configuration source | Wrong configuration can select bad device paths or make missions fail. | SW9S reads `config.toml`; the tracked `night_config.toml` appears incomplete for the current schema. | How is the actual vehicle `config.toml` created, stored, reviewed, and deployed? |
| Vehicle frames and signs | Motion code is meaningless without agreed axes and units. | Motor matrix, inversions, yaw sign, depth values, and movement transforms exist in source. | Body/world frames, positive directions, units, depth convention, camera offsets, and pool conventions. |
| Motor numbering and allocation | Incorrect mapping can cause unintended physical motion. | An eight-thruster definition is hard-coded in `src/main.rs`. | Physical motor numbering, geometry, inversion values, and current calibration. |
| Control-board indexing concern | Initialization may fail before a mission begins. | Source appears to use 0-based row enumeration where the matrix setter accepts 1 through 8. | Is this a known defect, an analysis error, or already handled by deployed firmware/branch differences? |
| Active vision path and models | Vision documentation must not describe a placeholder as a deployed detector. | Classical CV, native ONNX, ZED objects, and vendored Python YOLO all exist; the tracked default ONNX model is empty. | Which vision path runs on the vehicle, where models live, class mappings, and model promotion procedure. |
| ZED topics and role | ROS 2 names/types determine whether data is actually received. | Rust accepts ZED config but source currently uses hard-coded topics; mission use appears limited. | Deployed topics, message types, namespace, object-detection status, and whether ZED pose should affect missions. |
| Host-side safety behavior | Contributors must understand failure consequences. | SW9S watches MEB arm state and attempts shutdown/zeroing; board watchdog/firmware behavior is external. | Approved arm/disarm, leak/voltage response, panic behavior, watchdog guarantees, and emergency procedures. |
| Vehicle startup and deployment | A build guide needs the actual path from source to robot. | Compose primarily starts a ZED service; no visible service starts the Rust binary. | Who starts SW9S, on which device, with what environment, and through which approved procedure? |
| Deployment material | Historical files should not become misleading instructions. | Nix, root Dockerfile, Compose, and vendored YOLO material show mixed generations/status. | Supported development hosts, Jetson version, ROS distribution, active container topology, and simulator availability. |
| Logs and test assets | Examples should be intentional and reproducible. | Console/raw serial logs are committed; several vision tests reference missing resources. | Whether logs are fixtures and where required test assets belong. |

## How to resolve an item

1. Ask the person who owns the hardware, mission, or deployment boundary.
2. Record the answer with date, owner, and evidence such as a tested procedure, drawing, calibration artifact, or release revision.
3. Update the relevant handbook page with the confirmed information.
4. Change or remove this row only after the operational page has a durable home for the result.

## Status

**Needs team confirmation:** this register deliberately separates unverified operational questions from source-derived documentation.
