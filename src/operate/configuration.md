# Configuration

## Why configuration deserves care

Hardware paths, color thresholds, mission timings, and sensor settings should not be guessed at runtime. Configuration is the contract between source code and a particular vehicle/environment.

## SW9S implementation

`Config::new` in `src/config/mod.rs` reads exactly `config.toml` from the process working directory. Its fields include control-board/MEB/camera paths, color profiles, mission sections, sonar settings, and ZED settings. Individual mission schemas live in `src/config/`.

If loading or deserialization fails, `main.rs` logs the problem and uses `Config::default()`. This is a complete fallback, not a merge of valid partial settings with defaults.

## Important source-derived limitation

The only tracked sample is `night_config.toml`, not `config.toml`. Source inspection indicates it is incomplete for the current strict Serde schema, including some ZED, color-profile, gate/path, and spin fields. Defaults contain an empty color-profile map, so classical-vision missions that unwrap a selected profile can fail.

Do not solve this by copying a guessed configuration to a vehicle. The canonical config source, secrets policy, validation method, and deployment process are team-confirmation items.

## How to work with configuration

Trace a field through four places: the TOML key, its Rust config struct, the consumer, and a test or validated procedure. If a field is not consumed, document it as unused or investigate before relying on it.

## Last verified against SW9S

Source-derived from `fc780a1`.
