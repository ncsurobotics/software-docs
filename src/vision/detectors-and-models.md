# Detectors, Models, and Active Learning

## Two model-related paths

SW9S contains native OpenCV-DNN/ONNX code and a vendored Python ROS 2 `yolo_ros` workspace. They should not be conflated.

The native path uses `VisionModel`, `OnnxModel`, and `YoloProcessor` in `src/vision/nn_cv2.rs` and `yolo_model.rs`. Task adapters include `gate_poles.rs`; other model-oriented files include gate, slalom, and bin variants.

The vendored Python workspace under `docker/yolo-ros/` exposes separate ROS nodes and custom messages. Source inspection does not show it connected to the active Rust mission path or active Compose services.

## Important source-derived status

The `load_onnx!` macro embeds `src/vision/models/dummy_model.onnx` regardless of the macro model-name argument. That tracked file is zero bytes. Constructors using it should be treated as **experimental/unverified**, not as a deployed detector guarantee.

## Active learning

Active learning is the loop of collecting difficult examples, labeling/reviewing them, retraining, and validating whether a revised model improves task performance. The existing [Active Learning Pipeline](active_learning_pipeline.md) link is preserved as a team lead.

Before documenting training/deployment instructions, confirm model storage, class order, dataset policy, validation metrics, approvers, and how a model reaches the vehicle.

## Last verified against SW9S

Source-derived from `fc780a1`; model deployment requires team confirmation.
